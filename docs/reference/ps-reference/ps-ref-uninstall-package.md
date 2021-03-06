---
title: NuGet Uninstall-Package PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールで Uninstall-Package PowerShell コマンドのリファレンスです。
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 371e95c341efbce1c4a15facefc15cd51b266141
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901786"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Visual Studio のパッケージマネージャーコンソール)

*このトピックでは、Windows 上の Visual Studio の [パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md) 内のコマンドについて説明します。汎用 PowerShell Uninstall-Package コマンドについては、 [Powershell PackageManagement のリファレンス](/powershell/module/packagemanagement)を参照してください。*

プロジェクトからパッケージを削除し、必要に応じて依存関係を削除します。 他のパッケージがこのパッケージに依存している場合、–Force オプションを指定しない限り、コマンドは失敗します。

## <a name="syntax"></a>構文

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

他のパッケージがこのパッケージに依存している場合、–Force オプションを指定しない限り、コマンドは失敗します。

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| Id | 必要アンインストールするパッケージの識別子。 -Id スイッチ自体は省略可能です。 |
| Version | アンインストールするパッケージのバージョン。既定では、現在インストールされているバージョンが対象となります。 |
| RemoveDependencies | パッケージとその未使用の依存関係をアンインストールします。 つまり、依存関係に依存する別のパッケージがある場合、その依存関係はスキップされます。 |
| ProjectName | パッケージのアンインストール元のプロジェクト。既定のプロジェクトが既定のプロジェクトになります。 |
| Force | 他のパッケージが依存している場合でも、パッケージを強制的にアンインストールします。 |
| WhatIf | 実際にアンインストールを実行せずにコマンドを実行した場合の動作を示します。 |

これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。

## <a name="common-parameters"></a>共通パラメーター

`Uninstall-Package` は、Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数の [一般的な PowerShell パラメーター](/powershell/module/microsoft.powershell.core/about/about_commonparameters)をサポートしています。

## <a name="examples"></a>使用例

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```