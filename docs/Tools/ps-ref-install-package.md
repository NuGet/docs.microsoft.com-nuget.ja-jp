---
title: "NuGet のインストール パッケージの PowerShell リファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 879db0ef-6b72-4a4a-bb68-f9e3a00f64b8
description: "Visual Studio で NuGet パッケージ マネージャー コンソールのインストール パッケージの PowerShell コマンドのリファレンスです。"
keywords: "NuGet パッケージ マネージャー コンソールで、NuGet Powershell コマンドでは、NuGet Powershell リファレンス、インストール パッケージ"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d6b0c20545ecb82b0c2fa5214508381c0279c7cd
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>インストール パッケージ (Visual Studio でパッケージ マネージャー コンソール)

*このトピック内のコマンドをについて説明、 [NuGet Package Manager Console](Package-Manager-Console.md) Windows 上の Visual Studio でします。汎用の PowerShell のインストール パッケージ コマンドでは、次を参照してください。、 [PowerShell PackageManagement 参照](/powershell/module/packagemanagement/?view=powershell-6)です。*

プロジェクトにパッケージとその依存関係をインストールします。

## <a name="syntax"></a>構文

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

NuGet 2.8 + で`Install-Package`プロジェクトで既存のパッケージをダウン グレードできます。 たとえば、Microsoft.AspNet.MVC 5.1.0-rc1 がインストールされている場合は、次のコマンドはへのダウン グレードに 5.0.0 以降。

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

NuGet 2.7 およびそれ以前では、新しいバージョンが既にインストールされていることを示すエラーを説明します。
  
## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| ID | (必須)インストールするパッケージの識別子。 (*3.0 +*) パスまたは URL 識別子を指定できます、`packages.config`ファイルまたは`.nupkg`ファイル。 -Id スイッチ自体は省略可能です。 |
| IgnoreDependencies | このパッケージのみを依存関係は含めずをインストールします。 |
| ProjectName | 既定で、既定のプロジェクト、パッケージのインストール先のプロジェクトです。 |
| ソース | 検索するパッケージ ソースの URL またはフォルダーのパス。 ローカル フォルダー パスには、絶対パス、または現在のフォルダーの相対パスを指定できます。 省略した場合、`Install-Package`現在選択されているパッケージ ソースを検索します。 |
| Version | バージョンをインストールするパッケージの最新バージョンを既定とします。 |
| IncludePrerelease | プレリリースのパッケージのインストールを検討します。 省略した場合は、安定版パッケージのみが考慮されます。 |
| FileConflictAction | 上書きするか、プロジェクトによって参照されている既存のファイルを無視するように求められたらを実行するアクション。 指定できる値は*上書き、Ignore、None、OverwriteAll*、および*(3.0 以降)* *ignoreall です*です。 |
| DependencyVersion | 次のいずれかを使用する依存関係パッケージ バージョン:<br/><ul><li>*最小*(既定値): 最小バージョン</li><li>*HighestPatch*: 最小メジャー、マイナー最小、最高の修正プログラムのバージョン</li><li>*HighestMinor*: 主要な最小のバージョン、最高のマイナー、最上位の修正プログラム</li><li>*最も高い*(パラメーターなしで更新プログラム パッケージの既定): 最上位バージョン</li></ul>使用して、既定値を設定することができます、 [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section)での設定、`Nuget.Config`ファイル。 |
| WhatIf | 実際には、インストールを実行せず、コマンドを実行している場合にどうなるかを示します。 |

これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。

## <a name="common-parameters"></a>共通パラメーター

`Install-Package`次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。

## <a name="examples"></a>使用例

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
