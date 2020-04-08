---
title: Visual Studio のコンソールを使用して NuGet パッケージをインストールし、管理する
description: Visual Studio で NuGet パッケージ マネージャー コンソールを使用してパッケージを操作する方法について説明します。
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 42031f7b5fe4d3c1b4dbe5e1bfbf9197014e0e88
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428577"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a>Visual Studio でパッケージ マネージャー コンソールを使用してパッケージをインストールおよび管理する (PowerShell)

Nuget パッケージ マネージャー コンソールでは、[NuGet PowerShell コマンド](../reference/powershell-reference.md)を使用して、NuGet パッケージを検索、インストール、アンインストール、および更新することができます。 操作を実行するための手段がパッケージ マネージャー UI で提供されていない場合には、コンソールを使用する必要があります。 コンソールで `nuget.exe` CLI コマンドを使用するには、「[コンソールで nuget.exe CLI を使用する](#use-the-nugetexe-cli-in-the-console)」を参照してください。

コンソールは、Windows の Visual Studio に組み込まれています。 Visual Studio for Mac や Visual Studio Code には含まれていません。

## <a name="find-and-install-a-package"></a>パッケージを検索してインストールする

たとえば、パッケージの検索とインストールは、次の 3 つの簡単な手順で行われます。

1. Visual Studio でプロジェクト/ソリューションを開き、 **[ツール] > [NuGet パッケージ マネージャー] > [パッケージ マネージャー コンソール]** コマンドを使用してコンソールを開きます。

1. インストールするパッケージを検索します。 既にわかっている場合は、手順 3 に進みます。

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
> コンソールで使用できるすべての操作は、[NuGet CLI](../reference/nuget-exe-cli-reference.md) を使用して行うこともできます。 ただし、コンソール コマンドは、Visual Studio と保存済みのプロジェクト/ソリューションのコンテキスト内で動作し、多くの場合、同等の CLI コマンドよりも多くの操作を実行します。 たとえば、コンソールを使用してパッケージをインストールすると、プロジェクトへの参照が追加されますが、CLI コマンドでは参照は追加されません。 このため、Visual Studio で作業する開発者は、通常、CLI ではなくコンソールを優先的に使用します。

> [!Tip]
> 多くのコンソール操作は、ソリューションが既知のパス名を使用して Visual Studio で開かれていることを前提に動作します。 保存されていないソリューションがある場合や、ソリューションがない場合は、"ソリューションが開いていないか、または保存されていません。 ソリューションが開いており、保存されていることを確認してください " というエラーが表示されます。 これは、コンソールがソリューション フォルダーを特定できないことを示します。 保存されていないソリューションを保存するか、ソリューションを開いていない場合は作成して保存することで、エラーを解決できます。

## <a name="opening-the-console-and-console-controls"></a>コンソールとコンソール コントロールを開く

1. **[ツール] > [NuGet パッケージ マネージャー] > [パッケージ マネージャー コンソール]** コマンドを使用して、Visual Studio でコンソールを開きます。 コンソールは、好みに合わせて配置できる Visual Studio ウィンドウです (「[Visual Studio のウィンドウ レイアウトをカスタマイズする](/visualstudio/ide/customizing-window-layouts-in-visual-studio)」を参照してください)。

1. 既定では、コンソール コマンドは、ウィンドウの上部にあるコントロールで設定された特定のパッケージ ソースとプロジェクトに対して動作します。

    ![パッケージ ソースとプロジェクトのパッケージ マネージャー コンソール コントロール](media/PackageManagerConsoleControls1.png)

1. 別のパッケージ ソースやプロジェクトを選択すると、後続のコマンドの既定値が変更されます。 既定値を変更せずにこれらの設定をオーバーライドするために、ほとんどのコマンドで `-Source` および `-ProjectName` オプションがサポートされています。

1. パッケージ ソースを管理するには、歯車アイコンを選択します。 これは、 **[ツール] > [オプション] > [NuGet パッケージ マネージャー]** ダイアログ ボックスへのショートカットです ([パッケージ マネージャー UI](install-use-packages-visual-studio.md#package-sources) に関するページで説明されています)。 また、プロジェクト セレクターの右側にあるコントロールを使用すると、コンソールの内容をクリアできます。

    ![パッケージ マネージャー コンソールの設定とクリアのためのコントロール](media/PackageManagerConsoleControls2.png)

1. 右端のボタンをクリックすると、実行時間の長いコマンドが中断されます。 たとえば、`Get-Package -ListAvailable -PageSize 500` を実行すると、既定のソース上の上位 500 パッケージ (nuget.org など) が一覧表示されます (これには数分かかることがあります)。

    ![パッケージ マネージャー コンソールの停止コントロール](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a>パッケージをインストールします

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

「[Install-Package](../reference/ps-reference/ps-ref-install-package.md)」を参照してください。

コンソールでパッケージをインストールすると、「[NuGet パッケージのインストールのしくみ](../concepts/package-installation-process.md)」で説明されているのと同じ手順が実行されるのに加えて、次の操作が実行されます。

- コンソールのウィンドウに、適用されるライセンス条項と暗黙の契約が表示されます。 条項に同意しない場合は、パッケージをすぐにアンインストールする必要があります。
- また、パッケージへの参照がプロジェクト ファイルに追加され、 **[参照]** ノードの下の**ソリューション エクスプローラー**に表示されます。プロジェクト ファイルの変更内容を直接確認するには、プロジェクトを保存する必要があります。

## <a name="uninstall-a-package"></a>パッケージをアンインストールします

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

「[Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md)」を参照してください。 識別子を確認する必要がある場合は、[Get-Package](../reference/ps-reference/ps-ref-get-package.md) を使用して、既定のプロジェクトに現在インストールされているすべてのパッケージを表示します。

パッケージをアンインストールすると、次の操作が実行されます。

- パッケージへの参照をプロジェクトから削除します (使用中の管理形式にかかわらず)。 参照は**ソリューション エクスプローラー**に表示されなくなります。 (**Bin** フォルダーから削除されたことを確認するには、プロジェクトのリビルドが必要になる場合があります。)
- パッケージがインストールされたときに `app.config` または `web.config` に加えられた変更を元に戻します。
- 以前にインストールされた依存関係を削除します (残りのパッケージがそれらの依存関係を使用していない場合)。

## <a name="update-a-package"></a>パッケージを更新する

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

「[Get-Package](../reference/ps-reference/ps-ref-get-package.md)」と「[Update-Package](../reference/ps-reference/ps-ref-update-package.md)」を参照してください

## <a name="find-a-package"></a>パッケージを検索する

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

「[Find-Package](../reference/ps-reference/ps-ref-find-package.md)」を参照してください。 Visual Studio 2013 以前では、[Get-Package](../reference/ps-reference/ps-ref-get-package.md) を使用してください。

## <a name="availability-of-the-console"></a>コンソールの可用性

Visual Studio 2017 以降では、.NET 関連のワークロードを選択すると、NuGet と NuGet パッケージ マネージャーが自動的にインストールされます。また、Visual Studio インストーラーで **[個別のコンポーネント]** > [コードツール] > [NuGet パッケージ マネージャー] を選択して、個別にインストールすることもできます。

また、Visual Studio 2015 以前で NuGet パッケージ マネージャーが見当たらない場合は、 **[ツール] > [拡張機能と更新プログラム]** を選択して、NuGet パッケージ マネージャー拡張機能を検索してください。 Visual Studio 内で拡張機能のインストーラーを使用できない場合は、拡張機能を [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) から直接ダウンロードできます。

パッケージ マネージャー コンソールは、現在、Visual Studio for Mac では使用できません。 ただし、これと同等のコマンドは、[NuGet CLI](../reference/nuget-exe-CLI-reference.md) を介して使用できます。 Visual Studio for Mac には、NuGet パッケージを管理するための UI が用意されています。 「[プロジェクトに NuGet パッケージを含める](/visualstudio/mac/nuget-walkthrough)」を参照してください。

パッケージ マネージャー コンソールは、Visual Studio Code には含まれていません。

## <a name="extend-the-package-manager-console"></a>パッケージ マネージャー コンソールを拡張する

一部のパッケージでは、コンソール用の新しいコマンドがインストールされます。 たとえば、`MvcScaffolding` では、`Scaffold` コマンドが次のように作成され、これにより、ASP.NET MVC のコントローラーとビューが生成されます。

![MvcScaffold のインストールと使用](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a>NuGet PowerShell プロファイルを設定する

Powershell プロファイルを使用すると、PowerShell を使用するすべての場所で、一般的に使用されるコマンドを使用できるようになります。 NuGet では、NuGet 固有のプロファイルがサポートされます。これは通常、次の場所にあります。

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

プロファイルを検索するには、コンソールで「`$profile`」と入力します。

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

詳細については、「[Windows PowerShell プロファイル](https://technet.microsoft.com/library/bb613488.aspx)」を参照してください。

## <a name="use-the-nugetexe-cli-in-the-console"></a>コンソールで nuget.exe CLI を使用する

パッケージ マネージャー コンソールで [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) を使用できるようにするには、コンソールから [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) パッケージをインストールします。

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
