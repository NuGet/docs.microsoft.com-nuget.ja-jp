---
title: NuGet パッケージの復元
description: プロジェクトが依存しているパッケージを NuGet が復元する方法について概要を説明します。復元を無効にする方法や、バージョンを制約する方法についても触れます。
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: da69181aebe3bebcea6acd6e15fde6b77dd33452
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580299"
---
# <a name="package-restore"></a>パッケージの復元

開発環境をいっそうクリーンにしてリポジトリのサイズを減らすため、NuGet の**パッケージの復元**では、プロジェクト ファイルまたは `packages.config`のいずれかに一覧表示されたすべてのプロジェクトの依存関係をインストールします。 Visual Studio では、プロジェクトがビルドされるときに、パッケージを自動的に復元できます。 `dotnet build` および `dotnet run` コマンド (.NET Core 2.0 以降) でも、自動復元を実行します。 また、Visual Studio、`nuget restore`、`dotnet restore`、および Mono の xbuild を利用すると、パッケージをいつでも復元できます。

パッケージの復元によって、ソース コントロール内にそれらのパッケージを格納しなくても、確実にすべてのプロジェクトの依存関係が使用できるようになります。 パッケージ バイナリを除外するようにリポジトリを構成する方法については、[パッケージとソースの管理](../consume-packages/packages-and-source-control.md)に関するページをご覧ください。

## <a name="package-restore-overview"></a>パッケージの復元の概要

パッケージの復元では、最初に、必要に応じて、プロジェクトの直接的な依存関係がインストールされます。この後、依存関係グラフ全体にパッケージの依存関係がインストールされます。

パッケージがまだインストールされていない場合、NuGet は最初に、パッケージを[キャッシュ](../consume-packages/managing-the-global-packages-and-cache-folders.md)からのパッケージの取得を試みます。 パッケージがキャッシュにない場合、NuGet は有効なすべてのソースからパッケージをダウンロードしようとします (「[Configuring NuGet behavior](Configuring-NuGet-Behavior.md)」(NuGet の動作を構成する) を参照してください。ソースは Visual Studio の **[ツール] > [オプション] > [NuGet パッケージ マネージャー] > [パッケージ ソース]** リストにも表示されます)。 復元時には、NuGet は、要求に最初に応答するソースのパッケージを使用して、パッケージ ソースの順序を無視します。

> [!Note]
> NuGet では、すべてのソースがチェックされるまで、パッケージの復元の失敗が表示されません。 このとき、NuGet では一覧の最後のソースについてのみ障害が報告されます。 このエラーは、ソースごとに個別にエラーが表示されていなくても、パッケージが他のソースの*いずれ*にも存在しないことを意味します。

パッケージの復元は、次の方法でトリガーされます。

- **dotnet CLI**: [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) コマンドを使用します。このコマンドは、プロジェクト ファイルに列記されたパッケージを復元します (「[PackageReference](../consume-packages/package-references-in-project-files.md)」 を参照してください)。 .NET Core 2.0 以降では、復元は、`dotnet build` と `dotnet run` で自動的に実行されます。

- **パッケージ マネージャー UI (Windows 上の Visual Studio)**: プロジェクトは、テンプレートから作成されとき、およびビルドされたときに自動的に復元されます (ただし、「[パッケージの復元の有効化と無効化](#enabling-and-disabling-package-restore)」で説明するオプションに基づきます)。 NuGet 4.0 以降では、NET Core SDK ベースのプロジェクトを変更した場合も復元が自動的に発生します。

    手動で復元するには、ソリューション エクスプローラーでソリューションを右クリックして、**[NuGet パッケージの復元]** を選択します。 1 つ以上の個別のパッケージが、まだ適切にインストールされない場合 (ソリューション エクスプローラーにエラー アイコンが表示されます)、パッケージ マネージャー UI を使用して、影響を受けるパッケージをアンインストールし、再インストールします。 「[パッケージの再インストールと更新](../consume-packages/reinstalling-and-updating-packages.md)」を参照してください。

    "このプロジェクトは、このコンピューター上にない NuGet パッケージを参照しています" または "1 つ以上の NuGet パッケージを復元する必要がありますが、同意が与えられていないため、復元できませんでした" というエラーが表示される場合は、「[パッケージの復元の有効化と無効化](#enabling-and-disabling-package-restore)」の手順に従って、自動復元を有効にしてください。 [パッケージの復元のトラブルシューティング](Package-restore-troubleshooting.md)に関するページもご覧ください。

- **NuGet CLI**: [nuget restore](../tools/cli-ref-restore.md) コマンドを使用します。このコマンドは、プロジェクト ファイルまたは `packages.config`に列記されたパッケージを復元します。 ソリューション ファイルを指定することもできます。

- **MSBuild**: [msbuild /t:restore](../reference/msbuild-targets.md#restore-target)コマンドを使用します。このコマンドは、プロジェクト ファイル (PackageReference のみ) に列記されたパッケージを復元します。 NuGet 4.x 以降および MSBuild 15.1 以降でのみ使用できます。これらは、Visual Studio 2017 に含まれています。 `nuget restore` と `dotnet restore` はどちらも、このコマンドを該当するプロジェクトに使います。

- **Visual Studio Team Services**: Team Services でビルド定義を作成する場合、ビルド タスクの前に、[NuGet の復元](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) タスクまたは [.NET Core の復元](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages)タスクが定義に追加されます。 このタスクは、多くのビルド テンプレートに既定で含まれます。

- **Team Foundation Server**: TFS 2013 以降では、TFS 2013 以降用のチーム ビルド テンプレートを使用していれば、ビルド時にパッケージが自動的に復元されます。 以前のバージョンの TFS では、前に説明したように、ビルド ステップを含めるだけでコマンド ラインの復元オプションのいずれかを呼び出すことができます。 必要に応じて、ビルド テンプレートを TFS 2013 に移行できます。 詳細については、[Team Foundation ビルドでのパッケージの復元](../consume-packages/team-foundation-build.md)に関するチュートリアルをご覧ください。

## <a name="enabling-and-disabling-package-restore"></a>パッケージの復元の有効化と無効化

パッケージの復元を有効にするには、主に Visual Studio の **[ツール] > [オプション] > [NuGet パッケージ マネージャー]** を使います。

![NuGet パッケージ マネージャーのオプションによるパッケージ復元動作の制御](media/Restore-01-AutoRestoreOptions.png)

- **見つからないパッケージのダウンロードを NuGet に許可**: 次に示すように、`NuGet.Config` ファイル (Windows では `%AppData%\NuGet\NuGet.Config`、Mac/Linux では `~/.nuget/NuGet/NuGet.Config`) の `packageRestore/enabled` の設定を変更することによって、パッケージ復元のすべての形式を制御します。 Visual Studio では、この設定を使用して、ソリューションのコンテキスト メニューの **[NuGet パッケージの復元]** コマンドを実行できるようになります。

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```

> [!Note]
>  `packageRestore/enabled` の設定は、Visual Studio の起動前またはビルドの開始前に環境変数 **EnableNuGetPackageRestore** の値を TRUE または FALSE に設定することにより、グローバルにオーバーライドできます。

- **Visual Studio でのビルド中に見つからないパッケージを自動的に確認**: 次に示すように、`NuGet.Config` ファイル (Windows では `%AppData%\NuGet\NuGet.Config`、Mac/Linux では `~/.nuget/NuGet/NuGet.Config`) の `packageRestore/automatic` 設定を変更することにより、自動復元を制御します。 このオプションをオンにして Visual Studio からビルドを実行すると、欠落しているパッケージが自動的に復元されます。 このオプションは、MSBuild を使用してコマンド ラインから実行されるビルドには影響しません。

    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

詳しくは、「NuGet config file」(NuGet config ファイル) の「[packageRestore section](../reference/nuget-config-file.md#packagerestore-section)」(packageRestore セクション) をご覧ください。

開発者や会社が、すべてのユーザーに対して、コンピューターでのパッケージの復元を有効または無効にすることが必要になる場合があります。 これを行うには、`%ProgramData%\NuGet\Config` (Windows、潜在的に Visual Studio 用の特定の `\{IDE}\{Version}\{SKU}\` フォルダー下にある) または `~/.local/share` (Mac/Linux) に配置されているグローバル NuGet 構成ファイルに上記の同じ設定を追加します。 その場合、個々のユーザーは、必要に応じてプロジェクト レベルで選択的に復元を有効にできます。 NuGet が複数の構成ファイルの優先順位を決定する方法の詳細については、「[NuGet の動作を構成する](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)」をご覧ください。

> [!Important]
> `nuget.config` の `packageRestore` 設定を直接編集する場合は、オプションのダイアログ ボックスに現在の値が表示されるように Visual Studio を再起動します。

## <a name="constraining-package-versions-with-restore"></a>復元でのパッケージのバージョンの制約

NuGet は、いずれかの方法でパッケージを復元する際、`packages.config`またはプロジェクト ファイルで指定されている制約に従います。

- `packages.config`: 依存関係の `allowedVersion` プロパティでバージョンの範囲を指定します。 「[パッケージの再インストールと更新](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)」をご覧ください。 例:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- プロジェクト ファイル (PackageReference): 依存関係のバージョン番号でバージョンの範囲を直接指定します。 例:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

いずれの場合も、「[Package versioning](../reference/package-versioning.md)」(パッケージのバージョン管理) で説明されている表記を使います。

## <a name="forcing-restore-from-package-sources"></a>パッケージ ソースから強制的に復元する

[グローバル パッケージとキャッシュ フォルダーの管理](managing-the-global-packages-and-cache-folders.md)に関するページで説明されているように、既定では、NuGet の復元操作では、"*グローバル パッケージ*" および "*HTTP キャッシュ*" フォルダーのパッケージを使用します。

"*グローバル パッケージ*" フォルダーの使用を回避するには、次のいずれかの操作を行います。

- `nuget locals global-packages -clear` または `dotnet nuget locals global-packages --clear` を使用して、フォルダーをクリアする
- 次のいずれかの方法を使った復元操作の前に、"*グローバル パッケージ*" フォルダーの場所を一時的に変更する
  - NUGET_PACKAGES 環境変数を別のフォルダーに設定する。
  - `globalPackagesFolder` (PackageReference を使用している場合) または `repositoryPath` (`packages.config` を使用している場合) を別のフォルダーに設定した `NuGet.Config` ファイルを作成する ([構成設定](../reference/nuget-config-file.md#config-section)に関するページを参照してください)。
  - MSBuild のみ: `RestorePackagesPath` プロパティで別のフォルダーを指定する。

HTTP ソースのキャッシュの使用を回避するには、次のいずれかの操作を行います。

- `nuget restore` で `-NoCache` オプションを使用するか、または `dotnet restore` で `--no-cache` オプションを使用する。 これらのオプションは、Visual Studio パッケージ マネージャーの UI またはコンソールを経由した復元操作には影響しません。
- `nuget locals http-cache -clear` または `dotnet nuget locals http-cache --clear` を使用してキャッシュをクリアする。
- 一時的に、NUGET_HTTP_CACHE_PATH 環境変数を別のフォルダーに設定する。

## <a name="troubleshooting"></a>トラブルシューティング

[パッケージの復元のトラブルシューティング](package-restore-troubleshooting.md)に関するページを参照してください。
