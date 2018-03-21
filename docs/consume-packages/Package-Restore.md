---
title: "NuGet パッケージの復元 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "プロジェクトが依存しているパッケージを NuGet が復元する方法について概要を説明します。復元を無効にする方法や、バージョンを制約する方法についても触れます。"
keywords: "NuGet パッケージの復元, NuGet パッケージのインストール, パッケージのインストール, パッケージの復元, 依存関係のバージョン, 自動復元の無効化, パッケージのバージョンの制約"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 761ef86a70e0a681449dc9fe86d6a52ac2b19bb1
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2018
---
# <a name="package-restore"></a>パッケージの復元

開発環境をいっそうクリーンにしてリポジトリのサイズを減らすため、NuGet の**パッケージの復元**では、プロジェクトがビルドされる前に、参照されているすべてのパッケージがインストールされます。 &mdash;Visual Studio、.NET Core 2.0 以降、および Mono の xbuild で利用できる&mdash;、この広く使用されている機能により、これらのパッケージをソース管理に格納しなくても、すべての依存関係をプロジェクトで利用できます (パッケージのバイナリを除外するようにリポジトリを構成する方法については、「[パッケージとソース管理](../consume-packages/packages-and-source-control.md)」を参照してください)。 パッケージは、いつでも手動で復元できます。

ビルド サーバーでのパッケージの復元について詳しくは、[TFBuild でのパッケージの復元](../consume-packages/team-foundation-build.md)に関するページをご覧ください。

## <a name="package-restore-overview"></a>パッケージの復元の概要

パッケージの復元では、最初に、必要に応じて、プロジェクトの直接的な依存関係がインストールされます。この後、依存関係グラフ全体にパッケージの依存関係がインストールされます。

パッケージがまだインストールされていない場合、NuGet は最初に、パッケージを[キャッシュ](../consume-packages/managing-the-nuget-cache.md)からのパッケージの取得を試みます。 パッケージがキャッシュにない場合、NuGet は有効なすべてのソースからパッケージをダウンロード (およびキャッシュ) しようとします (「[Configuring NuGet behavior](Configuring-NuGet-Behavior.md)」(NuGet の動作を構成する) を参照してください。ソースは Visual Studio の **[ツール] > [オプション] > [NuGet パッケージ マネージャー] > [パッケージ ソース]** リストにも表示されます)。 NuGet は、要求に最初に応答するソースのパッケージを使用して、パッケージ ソースの順序を無視します。

> [!Note]
> NuGet では、すべてのソースがチェックされるまで、パッケージの復元の失敗が表示されません。 このとき、NuGet では一覧の最後のソースについてのみ障害が報告されます。 このエラーは、ソースごとに個別にエラーが表示されていなくても、パッケージが他のソースの*いずれ*にも存在しないことを意味します。

パッケージの復元は、次の方法でトリガーされます。

- **dotnet CLI**: [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) コマンドを使用します。このコマンドは、プロジェクト ファイルに列記されたパッケージを復元します (「[PackageReference](../consume-packages/package-references-in-project-files.md)」 を参照してください)。 .NET Core 2.0 以降では、復元は、`dotnet build` と `dotnet run` で自動的に実行されます。

- **パッケージ マネージャー UI (Windows 上の Visual Studio)**: プロジェクトは、テンプレートから作成されとき、およびビルドされたときに自動的に復元されます (ただし、「[パッケージの復元の有効化と無効化](#enabling-and-disabling-package-restore)」で説明するオプションに基づきます)。 NuGet 4.0 以降では、NET Core SDK ベースのプロジェクトを変更した場合も復元が自動的に発生します。

    手動で復元するには、ソリューション エクスプローラーでソリューションを右クリックして、**[NuGet パッケージの復元]** を選択します。 1 つ以上の個別のパッケージが、まだ適切にインストールされない場合 (ソリューション エクスプローラーにエラー アイコンが表示されます)、パッケージ マネージャー UI を使用して、影響を受けるパッケージをアンインストールし、再インストールします。 「[パッケージの再インストールと更新](../consume-packages/reinstalling-and-updating-packages.md)」を参照してください。

    "このプロジェクトは、このコンピューター上にない NuGet パッケージを参照しています" または "1 つ以上の NuGet パッケージを復元する必要がありますが、同意が与えられていないため、復元できませんでした" というエラーが表示される場合は、「[パッケージの復元の有効化と無効化](#enabling-and-disabling-package-restore)」の手順に従って、自動復元を有効にしてください。

- **NuGet CLI**: [nuget restore](../tools/cli-ref-restore.md) コマンドを使用します。このコマンドは、プロジェクト ファイル (「[PackageReference](../consume-packages/package-references-in-project-files.md)」 を参照) または [packages.config](../reference/packages-config.md) に列記されたパッケージを復元します。 ソリューション ファイルを指定することもできます。

- **MSBuild**: [msbuild /t:restore](../reference/msbuild-targets.md#restore-target)コマンドを使用します。このコマンドは、プロジェクト ファイルに列記されたパッケージを復元します (「[PackageReference](../consume-packages/package-references-in-project-files.md)」 を参照してください)。 NuGet 4.x 以降および MSBuild 15.1 以降でのみ使用できます。これらは、Visual Studio 2017 に含まれています。 `nuget restore` と `dotnet restore` はどちらも、このコマンドを該当するプロジェクトに使います。

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
    <br/>
    > [!Note]
    >  `packageRestore/enabled` の設定は、Visual Studio の起動前またはビルドの開始前に環境変数 **EnableNuGetPackageRestore** の値を TRUE または FALSE に設定することにより、グローバルに上書きできます。

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

開発者や会社が、すべてのユーザーに対して、コンピューターでのパッケージの復元を有効または無効にすることが必要になる場合があります。 これは、前述の設定と同じ設定を、`%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]` にあるグローバルな NuGet 構成ファイルに追加することによって実現できます。 その場合、個々のユーザーは、必要に応じてプロジェクト レベルで選択的に復元を有効にできます。 NuGet が複数の構成ファイルの優先順位を決定する方法の詳細については、「[NuGet の動作を構成する](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)」をご覧ください。

## <a name="constraining-package-versions-with-restore"></a>復元でのパッケージのバージョンの制約

NuGet は、いずれかの方法でパッケージを復元する際、`packages.config`またはプロジェクト ファイルで指定されている制約に従います。

- `packages.config`: 依存関係の `allowedVersion` プロパティでバージョンの範囲を指定します。 「[パッケージの再インストールと更新](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)」をご覧ください。 例:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- PackageReference: 依存関係のバージョン番号でバージョンの範囲を直接指定します。 例:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

いずれの場合も、「[Package versioning](../reference/package-versioning.md)」(パッケージのバージョン管理) で説明されている表記を使います。

## <a name="troubleshooting"></a>トラブルシューティング

[パッケージの復元のトラブルシューティング](package-restore-troubleshooting.md)に関するページを参照してください。