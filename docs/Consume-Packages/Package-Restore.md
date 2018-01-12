---
title: "NuGet パッケージの復元 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "プロジェクトが依存しているパッケージを NuGet が復元する方法について説明します。復元を無効にする方法や、バージョンを制約する方法についても触れます。"
keywords: "NuGet パッケージの復元, NuGet パッケージのインストール, パッケージのインストール, パッケージの復元, 依存関係のバージョン, 自動復元の無効化, パッケージのバージョンの制約"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4e819a2bb34bbe70f0f11d5adeed82b976a8cb65
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2018
---
# <a name="package-restore"></a>パッケージの復元

開発環境をいっそうクリーンにしてリポジトリのサイズを減らすため、NuGet の**パッケージの復元**では、プロジェクトがビルドされる前に、参照されているすべてのパッケージがインストールされます。 この広く使われている機能により、これらのパッケージをソース管理に格納しなくても、すべての依存関係をプロジェクトで利用できます (パッケージのバイナリを除外するようにリポジトリを構成する方法については、「[パッケージとソース管理](../consume-packages/packages-and-source-control.md)」をご覧ください)。

このトピックの内容:
- [パッケージの復元の簡単なガイド](#quick-guide-to-package-restore)
- [パッケージの復元の概要](#package-restore-overview)
- [パッケージの復元の有効化と無効化](#enabling-and-disabling-package-restore)
- [復元でのパッケージのバージョンの制約](#constraining-package-versions-with-restore)
- [コマンド ラインでの復元](#command-line-restore) (NuGet のすべてのバージョン)
- [Visual Studio での自動復元](#automatic-restore-in-visual-studio) (or NuGet 2.7 以降)
- [Visual Studio での MSBuild に統合された復元](#msbuild-integrated-restore) (or NuGet 2.6 以降)
- [Team Foundation ビルドでのパッケージの復元](#package-restore-with-team-foundation-build)

復元の動作はバージョンによって異なります。お使いの NuGet のバージョンを確認するには、コマンド ラインで `nuget.exe` を実行して、出力の最初の行を調べます。

ビルド サーバーでのパッケージの復元について詳しくは、[TFBuild でのパッケージの復元](../consume-packages/team-foundation-build.md)に関するページをご覧ください。

> [!Note]
> パッケージ復元用に構成されたプロジェクトは、Mono の xbuild でも動作します。

## <a name="quick-guide-to-package-restore"></a>パッケージの復元の簡単なガイド

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> "このプロジェクトは、このコンピューター上にない NuGet パッケージを参照しています" または "1 つ以上の NuGet パッケージを復元する必要がありますが、同意が与えられていないため、復元できませんでした" というエラーが表示される場合は、「[パッケージの復元の有効化と無効化](#enabling-and-disabling-package-restore)」の手順に従って、自動復元を有効にしてください。

## <a name="package-restore-overview"></a>パッケージの復元の概要

最初に、パッケージの参照は、プロジェクトの種類と NuGet のバージョンに応じて、次のいずれかのパッケージ管理形式で保持されています  (NuGet 4 と MSBuild 15.1 は Visual Studio 2017 でインストールされることに注意してください)。

| メソッド | NuGet のバージョン | 説明 | 
| --- | --- | --- |
| `packages.config` | 2.x 以降 | 依存関係の完全なディープ セットが列記されています。 `packages.config` に追加されたパッケージはプロジェクト ファイルにも追加される必要があり、ターゲットとプロパティもプロジェクト ファイルに追加される必要があります。 これは NuGet のすべてのバージョンの基本となる方法ですが、パフォーマンスは他のオプションより低下します  ([packages.config のスキーマ](../schema/packages-config.md)に関するページを参照)。 | 
| `project.json` | 3.x 以降 | UWP プロジェクトでの既定としてのみ使われますが、プロジェクトを `packages.config` から変換できます。 `project.json` には、最上位の依存関係のみが列記されます。 参照、ターゲット、プロパティはビルドの間にプロジェクトに動的に追加され、パフォーマンスは `packages.config` よりよくなります  ([project.json のスキーマ](../schema/project-json.md)に関するページを参照)。|
| PackageReference | 4.x 以降 | 依存関係は、プロジェクト ファイルの `<PackageReference>` ノードに、`<Reference>` および `<ProjectReference>` と共に直接列記されます。 `project.json` と同じように動作します。[プロジェクト ファイルでのパッケージの参照](../Consume-Packages/Package-References-in-Project-Files.md)に関するページをご覧ください。 |

次に、さまざまな方法で参照リストを使って復元を開始します。

コマンド ラインからまたは[パッケージ マネージャー コンソール](../tools/Package-Manager-Console.md)から:

| コマンド | 該当シナリオ |
| --- | --- | 
| `nuget restore` | すべてのバージョンの NuGet およびすべての参照の種類。 後の「[コマンド ラインでの復元](#command-line-restore)」をご覧ください。 | 
| `dotnet restore` | .NET Core プロジェクトの場合の `nuget restore` と同じです。 「[dotnet restore](/dotnet/articles/core/tools/dotnet-restore)」をご覧ください。 |
| `msbuild /t:restore` | [プロジェクト ファイルでのパッケージ参照](../Consume-Packages/Package-References-in-Project-Files.md)のみを使う Nuget 4.x 以降および MSBuild 15.1 以降。 `nuget restore` と `dotnet restore` はどちらも、このコマンドを該当するプロジェクトに使います。 「NuGet pack and restore as MSBuild targets」(MSBuild ターゲットとしての NuGet のパックと復元) の「[restore target](../schema/msbuild-targets.md#restore-target)」(ターゲットの復元) をご覧ください。|

visual Studio 自体もさまざまなタイミングでパッケージを復元します。

| 型 | 復元が行われるタイミング |
| --- | --- |
| テンプレートの復元 | 新しいプロジェクトの作成時に、一部のテンプレートが外部パッケージに依存している場合。 |
| ビルドの復元 | ビルドの最初のステップとして。 |
| ソリューションの復元 | ユーザーがソリューションを右クリックして **[NuGet パッケージの復元]** を選んだとき。 |
| プロジェクト変更時の復元 | *(NuGet 4.x のみ)* .NET Core SDK ベースのプロジェクトが使われているとき (プロジェクトの状態変化を含む)。 |

## <a name="enabling-and-disabling-package-restore"></a>パッケージの復元の有効化と無効化

パッケージの復元を有効にするには、主に Visual Studio の **[ツール] > [オプション] > [NuGet パッケージ マネージャー]** を使います。

![NuGet パッケージ マネージャーのオプションによるパッケージ復元動作の制御](media/Restore-01-AutoRestoreOptions.png)

- **見つからないパッケージのダウンロードを NuGet に許可**: 次に示すように、`%AppData%\NuGet\NuGet.Config` ファイルの `packageRestore/enabled` の設定を変更することによって、パッケージ復元のすべての形式を制御します。

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
    

- **Visual Studio でのビルド中に見つからないパッケージを自動的に確認**: 次に示すように、`%AppData%\NuGet\NuGet.Config` ファイルの `packageRestore/automatic` の設定を変更することにより、NuGet 2.7 以降での自動復元を制御します。
            
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

詳しくは、「NuGet config file」(NuGet config ファイル) の「[packageRestore section](../Schema/nuget-config-file.md#packagerestore-section)」(packageRestore セクション) をご覧ください。

開発者や会社が、すべてのユーザーに対する既定値を使って、コンピューターでのパッケージの復元を有効または無効にすることを望む場合があります。 これは、上と同じ設定を `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]` にあるグローバルな NuGet 構成ファイルに追加することによって実現できます。 その場合、個々のユーザーは、必要に応じてプロジェクト レベルで選択的に復元を有効にできます。 NuGet が複数の構成ファイルの優先順位を決める方法について詳しくは、「[Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)」(NuGet の動作を構成する) をご覧ください。

## <a name="constraining-package-versions-with-restore"></a>復元でのパッケージのバージョンの制約

NuGet は、いずれかの方法でパッケージを復元するとき、`packages.config`、`project.json`、またはプロジェクト ファイルで指定されている制約に従います。

- `packages.config`: 依存関係の `allowedVersion` プロパティでバージョンの範囲を指定します。 「[Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)」(パッケージの再インストールと更新) をご覧ください。 例:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- `project.json`: 依存関係のバージョン番号でバージョンの範囲を直接指定します。 例:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- プロジェクト ファイルのパッケージ参照: 依存関係のバージョン番号でバージョン範囲を直接指定します。 例:
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

いずれの場合も、「[Package versioning](../reference/package-versioning.md)」(パッケージのバージョン管理) で説明されている表記を使います。

## <a name="command-line-restore"></a>コマンド ラインでの復元

NuGet 2.7 以降では、[restore](../tools/cli-ref-restore.md) コマンドを使ってソリューション内のすべてのパッケージを復元します (`packages.config`、`project.json`、プロジェクト ファイル内のパッケージ参照のどれを使っている場合でも)。 次のどのバリエーションも、`c:\proj\app` などの指定されたプロジェクト フォルダーのパッケージを復元します。

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

NuGet 4.0 以降および MSBuild 15.1 以降の場合は、「[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md)」(MSBuild ターゲットとしての NuGet のパックと復元) で説明されている `MSBuild /t:restore` を使うこともできます。

## <a name="build-time-restore-in-visual-studio"></a>Visual Studio でのビルド時の復元

Visual Studio は、既定で、ビルドの開始時に足りないパッケージを自動的に復元します。 この動作は、**[ツール] > [オプション] > [NuGet パッケージ マネージャー] > [全般] > [Visual Studio でのビルド中に見つからないパッケージを自動的に確認]** をオフにすることによって変更できます。

有効にした場合、自動復元は次のように機能します。

1. ビルドが開始すると、Visual Studio はパッケージを復元するよう NuGet に指示します。
1. NuGet は、ソリューション内のすべての `packages.config` ファイルを再帰的に調べるか、`project.json` を調べるか、またはプロジェクト ファイル内を調べます。
1. 参照ファイルに列記されている各パッケージについて、NuGet はソリューションに既に存在するかどうかを調べます (プロジェクトが `packages.config`、`project.json`、またはプロジェクト ファイル内のパッケージ参照のいずれを使っているかに応じて、`packages` フォルダー、`project.lock.json`、または `project.assets.json` を調べます)。
1. パッケージが見つからない場合、NuGet は最初にキャッシュからのパッケージの取得を試みます (「[NuGet のキャッシュを管理する](../consume-packages/managing-the-nuget-cache.md)」を参照)。 パッケージがキャッシュにない場合、NuGet は **[ツール] > [オプション] > [NuGet パッケージ マネージャー] > [パッケージ ソース]** に列記されている有効なソースから、列記されている順序で、パッケージのダウンロードを試みます。 この場合、NuGet は、すべてのソースの確認が済むまでパッケージが見つからなかったことを示しません。すべてのソースを確認した時点で、リストの最後のソースについてのみ、エラーを報告します。 このエラーが表示された場合は、他のソースについて個別にエラーが表示されなくても、パッケージがどのソースにも存在しなかったことを意味します。
1. ダウンロードが成功した場合、NuGet はパッケージをキャッシュに格納して、ソリューションにインストールします (やはり、`packages` フォルダー、`project.lock.json`、または `project.assets.json` に)。ダウンロードが成功しなかった場合、NuGet は失敗し、ビルドは行われません。

このプロセスの間、進行状況ダイアログが表示され、パッケージの復元をキャンセルできます。

## <a name="package-restore-with-team-foundation-build"></a>Team Foundation ビルドでのパッケージの復元

パッケージの復元は、一般に、Team Foundation Server (TFS) や Visual Studio Team Services (および、ここでは説明されていない他のビルド システム) と同様に、ビルド サーバーでプロジェクトをビルドするときに使われます。

### <a name="visual-studio-team-services"></a>Visual Studio Team Services

Team Services でビルド定義を作成するときは、定義の他のビルド タスクの前に NuGet パッケージの復元タスクを単に追加します。 このタスクは、多くのビルド テンプレートに既定で含まれます。

![Visual Studio Team Service のビルド定義での NuGet パッケージの復元タスク](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a>Team Foundation Server

Team Foundation Server 2013 以降では、TFS 2013 以降用のチーム ビルド テンプレートを使っていると、ビルドの間に既定でパッケージが自動的に復元されます。

以前のバージョンのビルド テンプレートを使っている場合は (以前のバージョンの TFS から移行したプロジェクトなど)、ビルド テンプレートも TFS 2013 に移行する必要があります。 これは基本的に、お使いのソース管理 (TFVC または Git) の適切なテンプレートを使って、ビルド テンプレートのカスタム部分を作成し直すことを意味します。

以前のバージョンの TFS では、前に説明したように、ビルド ステップを含めるだけで[コマンド ライン復元](#command-line-restore)を開始できます。

詳しくは、「[Walkthrough of Package Restore with Team Foundation Build](../consume-packages/team-foundation-build.md)」(Team Foundation ビルドでのパッケージの復元のチュートリアル) をご覧ください。    
