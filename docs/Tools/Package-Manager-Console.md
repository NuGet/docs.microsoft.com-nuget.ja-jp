---
title: "NuGet パッケージ マネージャー コンソール ガイド |Microsoft ドキュメント"
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2b92b119-6861-406c-82af-9d739af230e4
description: "Visual Studio で NuGet パッケージ マネージャー コンソールを使用してパッケージを操作するための手順です。"
keywords: "NuGet パッケージ マネージャー コンソールで、NuGet powershell、NuGet パッケージを管理します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cc11963a9b9bfe9aa456d8cd4c8397e1084f660b
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2018
---
# <a name="package-manager-console"></a>パッケージ マネージャー コンソール

NuGet パッケージ マネージャー コンソールは、Windows 2012 以降のバージョンの Visual Studio に組み込まれています。 (にない Mac または Visual Studio のコード用の Visual Studio に含まれています。)

コンソールでは、使用できます。 [NuGet PowerShell コマンド](../tools/powershell-reference.md)見つけるには、インストール、アンインストール、および NuGet パッケージを更新します。 コンソールを使用する場合は必要、パッケージ マネージャーの UI が操作を実行する方法を提供できません。

たとえば、検索し、パッケージをインストールするは 3 つの簡単な手順で行います。

1. Visual Studio でプロジェクト/ソリューションを開きを使用してコンソールを開き、**ツール > NuGet Package Manager > パッケージ マネージャー コンソール**コマンド。

1. インストールするパッケージを検索します。 この既にわかっている場合は、手順 3. に進みます。

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. インストール コマンドを実行します。

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

このトピックの内容:

- [コンソールを開く](#opening-the-console-and-console-controls)
- [パッケージをインストールします。](#installing-a-package)
- [パッケージをアンインストールします。](#uninstalling-a-package)
- [パッケージを検索します。](#finding-a-package)
- [パッケージの更新](#updating-a-package)
- [コンソールの可用性](#availability-of-the-console)
- [パッケージ マネージャー コンソールの拡張](#extending-the-package-manager-console)
- [NuGet PowerShell プロファイルを設定します。](#setting-up-a-nuget-powershell-profile)

> [!Important]
> コンソールで使用できるすべての操作を実行することも、 [NuGet CLI](../tools/nuget-exe-cli-reference.md)です。 ただし、コンソールのコマンドは、Visual Studio と保存されているプロジェクト/ソリューションのコンテキスト内で動作し、多くの場合、それと等価の CLI コマンドよりも多くの作業します。 たとえば、コンソールを使用してパッケージをインストールする参照を追加プロジェクトに、CLI コマンドは実行されません。 このため、通常 Visual Studio で作業する開発者は、CLI にコンソールを使用してを選びます。

> [!Tip]
> 多くのコンソール操作は、既知のパス名で Visual Studio で開くソリューションによって異なります。 エラーを確認できます、保存されていないソリューションまたはソリューションがない場合、"ソリューションが開かれていないか、保存されません。 確認してください、開く、保存されているソリューションがある。" これは、コンソールで、ソリューション フォルダーを特定できないことを示します。 保存されていないソリューションを保存または作成があるない場合は、ソリューションを保存する場合は、エラーを修正する必要があります。

## <a name="opening-the-console-and-console-controls"></a>コンソール ウィンドウとコンソールのコントロールを開く

1. Visual Studio を使用して、コンソールを開き、**ツール > NuGet Package Manager > パッケージ マネージャー コンソール**コマンド。 コンソールでは、Visual Studio のウィンドウを配置し、たいただし配置されていることができます (を参照してください[Visual Studio でのウィンドウ レイアウトをカスタマイズ](/visualstudio/ide/customizing-window-layouts-in-visual-studio))。

1. 既定では、ウィンドウの上部にあるコントロールで設定されているコンソール コマンドが特定のパッケージのソース ファイルおよびプロジェクトに対して操作します。

    ![パッケージ ソース ファイルおよびプロジェクトのパッケージ マネージャー コンソールのコントロール](media/PackageManagerConsoleControls1.png)

1. 別のパッケージのソースまたはプロジェクトを選択すると、後続のコマンドの既定の設定を変更します。 上書きをこれらの設定、既定値を変更することがなくほとんどのコマンド サポート`-Source`と`-ProjectName`オプション。

1. パッケージ ソースを管理するには、歯車アイコンを選択します。 これへのショートカットを**ツール > オプション > NuGet Package Manager > パッケージ ソース** ダイアログ ボックスの定義に従って、[パッケージ マネージャーの UI](Package-Manager-UI.md#package-sources)ページ。 また、コントロールをプロジェクトのセレクターの右側には、本体の内容をクリアします。

    ![パッケージ マネージャー コンソールの設定およびクリア コントロール](media/PackageManagerConsoleControls2.png)

1. 一番右のボタンは、実行時間の長いコマンドを中断します。 たとえば、実行している`Get-Package -ListAvailable -PageSize 500`上位 500 のパッケージを実行するのに数分かかる場合があります (など nuget.org)、既定のソースを一覧表示します。

    ![Package Manager Console ストップ コントロール](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>パッケージをインストールします。

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

参照してください[Install-package](../tools/ps-ref-install-package.md)です。

パッケージをインストールするには、次の操作を実行します。

- 暗黙的なアグリーメントをコンソール ウィンドウで該当するライセンス条項を表示します。 条項に同意しない場合は、パッケージをすぐにアンインストールしてください。
- 使用されている参照形式で、プロジェクトへの参照を追加します。 参照は、ソリューション エクスプ ローラーと、該当する参照のフォーマット ファイルで、後で表示されます。 ただし、PackageReference、使用する必要があるプロジェクト ファイル内の変更を直接表示するプロジェクトを保存します。
- パッケージによってキャッシュされます。
    - PackageReference: パッケージにキャッシュされた`%USERPROFILE%\.nuget\packages`つまりファイルのロックと`project.assets.json`が更新されます。
    - `packages.config`: 作成、`packages`フォルダー内にサブフォルダーへのパッケージ ファイル、ソリューションのルートとコピーにします。 `package.config`ファイルを更新します。
- 更新プログラム`app.config`や`web.config`パッケージで使用する場合[ソースと config ファイルの変換](../create-packages/source-and-config-file-transformations.md)です。
- プロジェクトに既に存在していない場合は、すべての依存関係をインストールします。 プロセスでは、パッケージのバージョンを更新この可能性があります」の説明に従って[依存関係の解決](../consume-packages/dependency-resolution.md)です。
- Visual Studio のウィンドウで、使用可能な場合、パッケージの readme ファイルを表示します。

> [!Tip]
> パッケージをインストールする主な利点の 1 つ、`Install-Package`コンソールのコマンドは、パッケージ マネージャーの UI を使用した場合と同様に、プロジェクトへの参照を追加します。 これに対し、 `nuget install` CLI コマンドは、のみパッケージをダウンロードし、参照を自動的に追加できません。

## <a name="uninstalling-a-package"></a>パッケージをアンインストールします。

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

参照してください[Uninstall-package](../tools/ps-ref-uninstall-package.md)です。 使用して[Get-package](../tools/ps-ref-get-package.md)する識別子を検索する必要がある場合の既定のプロジェクトに現在インストールされているすべてのパッケージが表示されます。

パッケージをアンインストールするには、次の操作を実行します。

- プロジェクト (および、使用されている参照形式) から、パッケージへの参照を削除します。 参照がソリューション エクスプ ローラーで表示されません。 (表示から削除するプロジェクトをリビルドする必要があります、 **Bin**フォルダーです)。
- 加えられた変更を反転させます`app.config`または`web.config`パッケージがインストールされている場合。
- 以前にインストールされている削除の依存関係残存するパッケージがそれらの依存関係を使用しない場合。

> [!Tip]
> 同様に`Install-Package`、`Uninstall-Package`コマンドとは異なり、プロジェクト内の参照を管理するための利点には、 `nuget uninstall` CLI コマンド。

## <a name="updating-a-package"></a>パッケージの更新

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

参照してください[Get-package](../tools/ps-ref-get-package.md)と[更新プログラム パッケージ](../tools/ps-ref-update-package.md)

## <a name="finding-a-package"></a>パッケージを検索します。

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

参照してください[Find-package](../tools/ps-ref-find-package.md)です。 Visual Studio 2013 以前のバージョンでを使用して[Get-package](../tools/ps-ref-get-package.md)代わりにします。

## <a name="availability-of-the-console"></a>コンソールの可用性

Visual Studio 2017 で NuGet と NuGet パッケージ マネージャーが自動的にインストールを選択するときにします。NET に関連するワークロードです。インストールすることも、個別にチェックして、**個々 のコンポーネント > コード ツール > の NuGet package manager** Visual Studio 2017 インストーラー オプション。

NuGet パッケージ マネージャー Visual Studio 2015 以前のバージョンで、欠落している場合は確認も、**ツール > 拡張機能と更新しています.** NuGet Package Manager 拡張機能を検索します。 直接、拡張機能をダウンロードするには Visual Studio での拡張機能インストーラーを使用することがない場合は、 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)です。

パッケージ マネージャー コンソールは Visual Studio for mac と共に現在使用できません。 同等のコマンドがを介して使用できる、 [NuGet CLI](nuget-exe-CLI-reference.md)です。 Visual Studio for Mac は、NuGet パッケージを管理するための UI を持つはできます。 参照してください[などの NuGet パッケージ、プロジェクトの](/visualstudio/mac/nuget-walkthrough)します。

パッケージ マネージャー コンソールは、Visual Studio のコードに含まれていません。

## <a name="extending-the-package-manager-console"></a>パッケージ マネージャー コンソールの拡張

一部のパッケージは、コンソールの新しいコマンドをインストールします。 たとえば、`MvcScaffolding`のようなコマンドを作成`Scaffold`次に示すを生成する ASP.NET MVC のコント ローラーとビュー。

![インストールと MvcScaffold の使用](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>NuGet PowerShell プロファイルを設定します。

PowerShell のプロファイルでは、PowerShell を使用する場合、一般的に使用されるコマンドを使用できるようにすることができます。 NuGet は、通常、次の場所で見つかった NuGet 固有のプロファイルをサポートします。

```
%UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1
```

プロファイルを検索するには、次のように入力します。`$profile`コンソール。

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

詳細についてを参照してください[Windows PowerShell プロファイル](https://technet.microsoft.com/library/bb613488.aspx)です。
