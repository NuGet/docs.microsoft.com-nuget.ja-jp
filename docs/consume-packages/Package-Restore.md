---
title: NuGet パッケージの復元
description: プロジェクトが依存しているパッケージを NuGet が復元する方法について概要を説明します。復元を無効にする方法や、バージョンを制約する方法についても触れます。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 0df2b0ebcf438fba99291558f1cf929dcb32618b
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68316987"
---
# <a name="package-restore-options"></a>パッケージの復元オプション

開発環境をいっそうクリーンにしてリポジトリのサイズを減らすため、NuGet の**パッケージの復元**では、プロジェクト ファイルか `packages.config` に記載されているすべてのプロジェクトの依存関係をインストールします。 .NET Core 2.0+ の `dotnet build` コマンドと `dotnet run` コマンドでは、パッケージが自動的に復元されます。 Visual Studio では、プロジェクトのビルド時、パッケージを自動的に復元できます。ユーザーは Visual Studio、`nuget restore`、`dotnet restore`、Mono の xbuild を利用し、いつでもパッケージを復元できます。

パッケージの復元によって、ソース コントロール内に格納しなくても、すべてのプロジェクトの依存関係が使用できるようになります。 パッケージ バイナリを除外するようにソース コントロール リポジトリを構成するには、[パッケージとソースの管理](../consume-packages/packages-and-source-control.md)に関するページをご覧ください。 

## <a name="package-restore-overview"></a>パッケージの復元の概要

パッケージの復元では、最初に、必要に応じて、プロジェクトの直接的な依存関係がインストールされます。この後、依存関係グラフ全体にパッケージの依存関係がインストールされます。

パッケージがまだインストールされていない場合、NuGet は最初に、パッケージを[キャッシュ](../consume-packages/managing-the-global-packages-and-cache-folders.md)からのパッケージの取得を試みます。 パッケージがキャッシュにない場合、NuGet は、Visual Studio で **[ツール]** 、 **[オプション]** 、 **[NuGet パッケージ マネージャー]** 、 **[パッケージ ソース]** の順に選択すると一覧表示される、すべての有効なソースからのパッケージのダウンロードを試みます。 復元時には、NuGet は、要求に最初に応答するソースのパッケージを使用し、パッケージ ソースの順序を無視します。 NuGet の動作については、[一般的な NuGet 構成](Configuring-NuGet-Behavior.md)に関するページを参照してください。 

> [!Note]
> NuGet では、すべてのソースがチェックされるまで、パッケージの復元の失敗が表示されません。 このとき、NuGet では一覧の最後のソースについてのみ障害が報告されます。 このエラーは、ソースごとに個別にエラーが表示されていなくても、パッケージが他のソースの*いずれ*にも存在しないことを意味します。

## <a name="restore-packages"></a>パッケージの復元

パッケージの復元は次のいずれかの方法で開始できます。

- **Visual Studio**:Windows の Visual Studio で、次のいずれかの方法を使用します。

    - パッケージを自動的に復元する。 パッケージの復元は、テンプレートからプロジェクトを作成するとき、またはプロジェクトをビルドするときに、「[パッケージ復元の有効化と無効化](#enable-and-disable-package-restore-visual-studio)」に記載されているオプションに基づいて自動的に行われます。 NuGet 4.0+ では、SDK スタイルのプロジェクト (通常は .NET Core または .NET Standard プロジェクト) の変更時にも復元が行われます。

    - パッケージを手動で復元する。 手動で復元するには、**ソリューション エクスプローラー**でソリューションを右クリックして、 **[NuGet パッケージの復元]** を選択します。 1 つまたは複数の個別パッケージが正しくインストールされていない場合、 **[ソリューション エクスプローラー]** にエラー アイコンが表示されます。 右クリックして **[NuGet パッケージの管理]** を選択し、 **[パッケージ マネージャー]** を使用し、影響を受けるパッケージをアンインストールし、再インストールします。 詳細については、「[パッケージを再インストールして更新する](../consume-packages/reinstalling-and-updating-packages.md)」を参照してください。

    "このプロジェクトは、このコンピューター上にない NuGet パッケージを参照しています" または "1 つ以上の NuGet パッケージを復元する必要がありますが、同意が与えられていないため、復元できませんでした" というエラーが表示される場合は、[自動復元を有効にしてください](#enable-and-disable-package-restore-visual-studio)。 また、[パッケージの自動復元への移行](#migrate-to-automatic-package-restore-visual-studio)および[パッケージの復元のトラブルシューティング](Package-restore-troubleshooting.md)に関するページもご覧ください。

- **dotnet CLI**:コマンド ラインで、使用するプロジェクトが含まれているフォルダーに切り替えてから、[dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) コマンドを使用して、[PackageReference](../consume-packages/package-references-in-project-files.md) でプロジェクト ファイルに記載されているパッケージを復元します。 .NET Core 2.0 以降では、復元は `dotnet build` コマンドと `dotnet run` コマンドで自動的に行われます。  

- **nuget.exe CLI**:コマンド ラインで、使用するプロジェクトが含まれているフォルダーに切り替えてから、[nuget restore](../reference/cli-reference/cli-ref-restore.md) コマンドを使用して、プロジェクトやソリューション ファイル、または　`packages.config` に記載されているパッケージを復元します。 

- **MSBuild**:[msbuild -t:restore](../reference/msbuild-targets.md#restore-target) コマンドを使用して、PackageReference を使用するプロジェクト ファイルに一覧表示されているパッケージを復元します。 このコマンドは、Visual Studio 2017 以降のバージョン含まれる NuGet 4.x+ と MSBuild 15.1+ でのみ利用できます。 `nuget restore` と `dotnet restore` の両方で、該当するプロジェクトにこのコマンドが使用されます。

- **Azure Pipelines**:Azure Pipelines でビルド定義を作成するとき、定義の中でビルド タスクの前に NuGet [復元](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages)または .NET Core [復元](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops)タスクを含めます。 一部のビルド テンプレートには、既定で復元タスクが含まれています。

- **Azure DevOps Server**:Azure DevOps Server と TFS 2013 以降では、TFS 2013 以降のチーム ビルド テンプレートを使用している場合、ビルド時にパッケージが自動的に復元されます。 それより前の TFS バージョンの場合、コマンドラインで復元を実行するビルド ステップを含めたり、任意で、ビルド テンプレートを後続のバージョンに移行したりできます。 詳細については、[Team Foundation ビルドでパッケージ復元を設定する](../consume-packages/team-foundation-build.md)方法に関するページをご覧ください。

## <a name="enable-and-disable-package-restore-visual-studio"></a>パッケージ復元の有効化と無効化 (Visual Studio)

Visual Studio では、パッケージ復元の管理は主に、 **[ツール]** 、 **[オプション]** 、 **[NuGet パッケージ マネージャー]** の順に選択して行います。

![NuGet パッケージ マネージャーのオプションによるパッケージ復元の制御](media/Restore-01-AutoRestoreOptions.png)

- **見つからないパッケージのダウンロードを NuGet に許可**: `NuGet.Config` ファイル (Windows では `%AppData%\NuGet\`、Mac/Linux では `~/.nuget/NuGet/`) の [packageRestore セクション](../reference/nuget-config-file.md#packagerestore-section)の `packageRestore/enabled` 設定を変更することによって、パッケージ復元のすべての形式を制御します。 また、この設定により、Visual Studio でソリューションのコンテキスト メニューの **[NuGet パッケージの復元]** コマンドが有効になります。

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    
  > [!Note]
  > `packageRestore/enabled` 設定をグローバルにオーバーライドするには、Visual Studio の起動前またはビルドの開始前に環境変数 **EnableNuGetPackageRestore** の値を TRUE または FALSE に設定します。

- **Visual Studio でのビルド中に見つからないパッケージを自動的に確認**: `NuGet.Config` ファイルの [packageRestore セクション](../reference/nuget-config-file.md#packagerestore-section)の `packageRestore/automatic` 設定を変更することにより、自動復元を制御します。 このオプションを True に設定していると、Visual Studio からビルドを実行したとき、欠落しているパッケージが自動的に復元されます。 この設定が MSBuild コマンド ラインから実行されるビルドに影響を与えることはありません。

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

コンピューター上のすべてのユーザーに対してパッケージ復元を有効または無効にする目的で、開発者または会社は構成設定をグローバル `nuget.config` ファイルに追加できます。 グローバル `nuget.config` は Windows の `%ProgramData%\NuGet\Config` の特定の `\{IDE}\{Version}\{SKU}\` Visual Studio フォルダーにある場合があります。Mac/Linux の場合は `~/.local/share` です。 その場合、個々のユーザーは、必要に応じてプロジェクト レベルで選択的に復元を有効にできます。 NuGet で複数の構成ファイルに優先順位を付けるしくみについては、[共通 NuGet 構成](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)に関するページを参照してください。

> [!Important]
> `nuget.config` で直接、`packageRestore` 設定を編集する場合、 **[オプション]** ダイアログ ボックスに現在の値が表示されるように Visual Studio を再起動します。

## <a name="constrain-package-versions-with-restore"></a>復元でパッケージ バージョンを制約する

NuGet で何らかの方法でパッケージを復元するとき、`packages.config` またはプロジェクト ファイルに指定した制約が適用されます。

- `packages.config` では、依存関係の `allowedVersion` プロパティでバージョン範囲を指定できます。 詳細については、[アップグレード バージョンの制約](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)に関するページを参照してください。 次に例を示します。

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- プロジェクト ファイルでは、PackageReference を使用し、依存関係の範囲を直接指定できます。 次に例を示します。

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

いずれの場合も、「[Package versioning](../reference/package-versioning.md)」(パッケージのバージョン管理) で説明されている表記を使います。

## <a name="force-restore-from-package-sources"></a>パッケージ ソースから強制的に復元する

[グローバル パッケージとキャッシュ フォルダーの管理](managing-the-global-packages-and-cache-folders.md)に関するページで説明されているように、既定では、NuGet の復元操作では、"*グローバル パッケージ*" フォルダーと "*HTTP キャッシュ*" フォルダーのパッケージを使用します。

"*グローバル パッケージ*" フォルダーの使用を回避するには、次のいずれかの操作を行います。

- `nuget locals global-packages -clear` または `dotnet nuget locals global-packages --clear` を使用して、フォルダーをクリアします。
- 次のいずれかの方法で、復元操作の前に "*グローバル パッケージ*" フォルダーの場所を一時的に変更します。
  - NUGET_PACKAGES 環境変数を別のフォルダーに設定する。
  - `globalPackagesFolder` (PackageReference を使用している場合) または `repositoryPath` (`packages.config` を使用している場合) を別のフォルダーに設定した `NuGet.Config` ファイルを作成する。 [構成設定](../reference/nuget-config-file.md#config-section)に関するページを参照してください。
  - MSBuild のみ:`RestorePackagesPath` プロパティで別のフォルダーを指定する。

HTTP ソースのキャッシュの使用を回避するには、次のいずれかの操作を行います。

- `nuget restore` で `-NoCache` オプションを使用するか、`dotnet restore` で `--no-cache` オプションを使用する。 これらのオプションは、Visual Studio パッケージ マネージャーまたはコンソールを経由した復元操作には影響しません。
- `nuget locals http-cache -clear` または `dotnet nuget locals http-cache --clear` を使用してキャッシュをクリアする。
- 一時的に NUGET_HTTP_CACHE_PATH 環境変数を別のフォルダーに設定する。

## <a name="migrate-to-automatic-package-restore-visual-studio"></a>パッケージの自動復元への移行 (Visual Studio)

NuGet 2.6 およびそれ以前では、以前は MSBuild に統合されたパッケージの復元がサポートされていましたが、現在ではサポートされていません。 (これは通常、Visual Studio でソリューションを右クリックし、 **[NuGet パッケージの復元を有効にする]** を選択することで有効になりました)。 ご自身のプロジェクトで、非推奨の、MSBuild に統合されたパッケージの復元を使用する場合は、パッケージの自動復元に移行してください。

MSBuild に統合されたパッケージの復元が使用されるプロジェクトには、通常、次の 3 つのファイルを含む *.nuget* フォルダーが含まれています:*NuGet.config*、*nuget.exe*、*NuGet.targets*。 *NuGet.targets* ファイルの存在によって、NuGet で MSBuild に統合されたアプローチが引き続き使用されるかどうかが決まります。そのため、移行中にこのファイルを削除する必要があります。

パッケージの自動復元に移行するには:

1. Visual Studio を閉じます。
2. *.nuget/nuget.exe* と *.nuget/NuGet.targets* を削除します。
3. 各プロジェクト ファイルごとに、`<RestorePackages>` 要素を削除し、*NuGet.targets* への参照をすべて削除します。

パッケージの自動復元をテストするには:

1. ソリューションから *packages* フォルダーを削除します。
2. Visual Studio でソリューションを開き、ビルドを開始します。

   パッケージの自動復元によって、各依存関係パッケージがダウンロードおよびインストールされ、それらがソース管理に追加されることはありません。

## <a name="troubleshooting"></a>トラブルシューティング

[パッケージの復元のトラブルシューティング](package-restore-troubleshooting.md)に関するページを参照してください。
