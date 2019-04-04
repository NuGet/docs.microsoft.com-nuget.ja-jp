---
title: NuGet の Uninstall-package PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールのアンインストール パッケージの PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ae60473fbb716b23f40b0605be8aaa8515802315
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551644"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Visual Studio パッケージ マネージャー コンソール)

*このトピックでは、内のコマンドを説明します、 [NuGet パッケージ マネージャー コンソール](package-manager-console.md)Windows 上の Visual Studio でします。一般的な PowerShell のアンインストール パッケージ コマンドは、、 [PowerShell PackageManagement 参照](/powershell/module/packagemanagement/?view=powershell-6)を参照してください。*

必要に応じてその依存関係を削除する、プロジェクトからパッケージを削除します。 コマンドが失敗しない限り、他のパッケージは、このパッケージに依存している場合、– Force オプションを指定します。

## <a name="syntax"></a>構文

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

コマンドが失敗しない限り、他のパッケージは、このパッケージに依存している場合、– Force オプションを指定します。

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| ID | (必須)アンインストールするパッケージの識別子。 -Id スイッチ自体は省略可能です。 |
| Version | をアンインストールするパッケージのバージョン、現在インストールされているバージョンを既定値します。 |
| RemoveDependencies | パッケージとその未使用の依存関係をアンインストールします。 すべての依存関係の別のパッケージに依存している場合は、これはスキップされます。 |
| ProjectName | 既定では、既定のプロジェクト、パッケージをアンインストールするプロジェクトです。 |
| Force | 場合でも、依存している他のパッケージは、アンインストールするパッケージを強制的にします。 |
| WhatIf | 実際には、アンインストールを実行せず、コマンドを実行するときに何が起こるかを示します。 |

これらのパラメーターには、パイプラインの入力またはワイルドカード文字がそのまま使用します。

## <a name="common-parameters"></a>共通パラメーター

`Uninstall-Package` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。

## <a name="examples"></a>使用例

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
