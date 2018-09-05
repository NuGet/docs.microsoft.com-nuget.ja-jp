---
title: NuGet パッケージ マネージャー コンソールのガイド
description: Visual Studio で NuGet パッケージ マネージャー コンソールを使用してパッケージを操作するための手順です。
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 88979c67ea7f073f2ea5a02c445186642f77f210
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546879"
---
# <a name="package-manager-console"></a>パッケージ マネージャー コンソール

NuGet パッケージ マネージャー コンソールは、Windows 2012 以降のバージョンの Visual Studio に組み込まれています。 (違います Visual Studio for Mac または Visual Studio のコードに含まれています。)

コンソールを使用できます。 [NuGet PowerShell コマンド](../tools/powershell-reference.md)見つけるには、インストール、アンインストール、および NuGet パッケージを更新します。 コンソールを使用することは、パッケージ マネージャー UI が操作を実行する方法を提供しない場合に必要があります。 使用する`nuget.exe`コマンド コンソールを参照してください[コンソールで nuget.exe CLI を使用して](#using-the-nugetexe-cli-in-the-console)します。

などの検索とインストール パッケージは、次の 3 つの簡単なステップで行われます。

1. Visual Studio で、プロジェクト/ソリューションを開き、コンソールを使用して、開く、**ツール > NuGet パッケージ マネージャー > パッケージ マネージャー コンソール**コマンド。

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

> [!Important]
> コンソールで利用できるすべての操作を実行することも、 [NuGet CLI](../tools/nuget-exe-cli-reference.md)します。 ただし、コンソールのコマンドは、Visual Studio と保存されているプロジェクト/ソリューションのコンテキスト内で動作し、多くの場合、その同等の CLI コマンドよりも多くの作業します。 たとえば、コンソールを使用してパッケージをインストールする追加しますプロジェクトへの参照を CLI コマンドは実行されません。 このため、通常 Visual Studio で作業する開発者は、CLI にコンソールを使用してを優先します。

> [!Tip]
> 多くのコンソール操作は、既知のパスの名前を Visual Studio で開いたソリューションに依存します。 エラーが発生したことができます、保存されていないソリューションまたはソリューションがない場合、"ソリューションが開かれていないか、保存されません。 確認してください、オープンと保存されているソリューションがある。" これは、コンソールがソリューション フォルダーを判断できないことを示します。 保存されていないソリューションでは、保存または作成し、お持ちでない場合は、ソリューションを保存、開き、エラーを修正する必要があります。

## <a name="opening-the-console-and-console-controls"></a>コンソールを開き、コンソールのコントロール

1. Visual Studio を使用して、コンソールを開き、**ツール > NuGet パッケージ マネージャー > パッケージ マネージャー コンソール**コマンド。 コンソールは、配置および自由に配置できる Visual Studio のウィンドウ (を参照してください[Visual Studio でのウィンドウ レイアウトをカスタマイズ](/visualstudio/ide/customizing-window-layouts-in-visual-studio))。

1. 既定では、コンソール コマンドは、特定のパッケージのソースとのプロジェクトに対して、ウィンドウの上部にあるコントロールで設定されている動作します。

    ![パッケージ ソース ファイルおよびプロジェクトのパッケージ マネージャー コンソール コントロール](media/PackageManagerConsoleControls1.png)

1. 後続のコマンドの既定の設定を変更する別のパッケージのソースまたはプロジェクトを選択します。 上書きを既定値を変更することがなくこれらの設定のほとんどのコマンドをサポートして`-Source`と`-ProjectName`オプション。

1. パッケージ ソースを管理するには、歯車アイコンを選択します。 これへのショートカット、**ツール > オプション > NuGet パッケージ マネージャー > パッケージ ソース** ダイアログ ボックスでの説明に従って、[パッケージ マネージャー UI](package-manager-ui.md#package-sources)ページ。 また、プロジェクト セレクターの右側に、コントロールは、コンソールの内容をクリアします。

    ![パッケージ マネージャー コンソールの設定およびコントロールのクリア](media/PackageManagerConsoleControls2.png)

1. 一番右のボタンは、実行時間の長いコマンドを中断します。 たとえば、実行している`Get-Package -ListAvailable -PageSize 500`上位 500 のパッケージを実行するのに数分かかる場合があります (など、nuget.org の場合) には、既定のソースを一覧表示されます。

    ![パッケージ マネージャー コンソール ストップ コントロール](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>パッケージをインストールします。

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

参照してください[Install-package](../tools/ps-ref-install-package.md)します。

説明に従って、同じ手順を実行、コンソールでパッケージをインストールする[パッケージがインストールされているときに起こる](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed)、次の項目を追加。

- コンソールには、暗黙的な契約書には、そのウィンドウで該当するライセンス条項が表示されます。 条項に同意しない場合は、すぐに、パッケージをアンインストールする必要があります。
- パッケージへの参照はプロジェクト ファイルに追加されに表示されます**ソリューション エクスプ ローラー**下、**参照**ノード、プロジェクト ファイル内の変更を直接表示するプロジェクトを保存する必要があります。

## <a name="uninstalling-a-package"></a>パッケージをアンインストールします。

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

参照してください[Uninstall-package](../tools/ps-ref-uninstall-package.md)します。 使用[Get-package](../tools/ps-ref-get-package.md)に識別子を検索する必要がある場合、既定のプロジェクトにインストールされているすべてのパッケージを参照してください。

パッケージをアンインストールするには、次の操作は実行します。

- プロジェクト (および使用されている管理形式) から、パッケージへの参照を削除します。 参照が表示されなく**ソリューション エクスプ ローラー**します。 (表示から削除するプロジェクトをリビルドする必要があります、 **Bin**フォルダー)。
- 加えられた変更を反転させます`app.config`または`web.config`パッケージがインストールされている場合。
- 以前にインストールされている削除残存するパッケージがこれらの依存関係を使用しない場合は、依存関係。

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

## <a name="finding-a-package"></a>パッケージの検索

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

参照してください[Find-package](../tools/ps-ref-find-package.md)します。 Visual Studio 2013 以降を使用して、 [Get-package](../tools/ps-ref-get-package.md)代わりにします。

## <a name="availability-of-the-console"></a>コンソールの可用性

Visual Studio 2017、NuGet、NuGet パッケージ マネージャーが自動的にインストールを選択します。NET に関連するワークロードです。チェックして個別にインストールもできる、**個々 のコンポーネント > コード ツール > NuGet パッケージ マネージャー** Visual Studio 2017 インストーラーでオプションです。

また、NuGet パッケージ マネージャー Visual Studio 2015 以前のバージョンでは不足しているが場合、確認**ツール > 拡張機能と更新しています.** して NuGet パッケージ マネージャー拡張機能を検索します。 直接、拡張機能をダウンロードするには Visual Studio の拡張機能インストーラーを使用する場合は、 [ https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)します。

パッケージ マネージャー コンソールを Visual Studio for mac で現在ご利用いただけません 同等のコマンドでは、ただしを利用、 [NuGet CLI](nuget-exe-CLI-reference.md)します。 Visual Studio for Mac は NuGet パッケージを管理するための UI が。 参照してください[を含む NuGet パッケージをプロジェクトに](/visualstudio/mac/nuget-walkthrough)します。

パッケージ マネージャー コンソールでは、Visual Studio のコードに含まれません。

## <a name="extending-the-package-manager-console"></a>パッケージ マネージャー コンソールを拡張します。

一部のパッケージは、コンソールの新しいコマンドをインストールします。 たとえば、`MvcScaffolding`などのコマンドを作成します。`Scaffold`下図のように生成する ASP.NET MVC コント ローラーとビュー。

![インストールと MvcScaffold の使用](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>NuGet PowerShell プロファイルの設定

PowerShell プロファイルには、PowerShell を使用する場合、一般的に使用されるコマンドを使用できるようにすることができます。 NuGet は、通常、次の場所にある特定の NuGet プロファイルをサポートしています。

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

プロファイルを検索するには、次のように入力します。`$profile`コンソール。

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

詳細についてを参照してください[Windows PowerShell プロファイル](https://technet.microsoft.com/library/bb613488.aspx)します。

## <a name="using-the-nugetexe-cli-in-the-console"></a>コンソールで nuget.exe CLI を使用してください。

させる、 [ `nuget.exe` CLI](nuget-exe-cli-reference.md) 、パッケージ マネージャー コンソールで使用可能なインストール、 [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/)コンソールからのパッケージ。

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
