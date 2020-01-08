---
title: NuGet アンインストール-パッケージ PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールでの Uninstall-Package PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 05b7bf0e8abad0904b9e851ea6b7a5317e74229d
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384416"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Visual Studio パッケージ マネージャー コンソール)

*このトピックでは、Windows 上の Visual Studio の[パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md)内のコマンドについて説明します。汎用 PowerShell Uninstall-Package コマンドについては、 [Powershell PackageManagement のリファレンス](/powershell/module/packagemanagement/?view=powershell-6)を参照してください。*

プロジェクトからパッケージを削除し、必要に応じて依存関係を削除します。 他のパッケージがこのパッケージに依存している場合、–Force オプションを指定しない限り、コマンドは失敗します。

## <a name="syntax"></a>構文

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

他のパッケージがこのパッケージに依存している場合、–Force オプションを指定しない限り、コマンドは失敗します。

## <a name="parameters"></a>パラメーター

| パラメータ | 説明 |
| --- | --- |
| ID | 必要アンインストールするパッケージの識別子。 -Id スイッチ自体は省略可能です。 |
| Version | アンインストールするパッケージのバージョン。既定では、現在インストールされているバージョンが対象となります。 |
| RemoveDependencies | パッケージとその未使用の依存関係をアンインストールします。 つまり、依存関係に依存する別のパッケージがある場合、その依存関係はスキップされます。 |
| ProjectName | パッケージのアンインストール元のプロジェクト。既定のプロジェクトが既定のプロジェクトになります。 |
| Force | 他のパッケージが依存している場合でも、パッケージを強制的にアンインストールします。 |
| Whatif | 実際にアンインストールを実行せずにコマンドを実行した場合の動作を示します。 |

これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。

## <a name="common-parameters"></a>共通パラメーター

`Uninstall-Package` 次のサポート[一般的な PowerShell パラメーター](https://go.microsoft.com/fwlink/?LinkID=113216): Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。

## <a name="examples"></a>使用例

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
