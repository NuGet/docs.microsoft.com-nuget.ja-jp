---
title: NuGet の Uninstall-package PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールのアンインストール パッケージの PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: c95479103be2cba3b4eb6964ea761870477863bd
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842476"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Visual Studio パッケージ マネージャー コンソール)

*このトピックでは、内のコマンドを説明します、[パッケージ マネージャー コンソール](package-manager-console.md)Windows 上の Visual Studio でします。一般的な PowerShell のアンインストール パッケージ コマンドは、次を参照してください。、 [PowerShell PackageManagement 参照](/powershell/module/packagemanagement/?view=powershell-6)します。*

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

`Uninstall-Package` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216):デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、および WarningVariable します。

## <a name="examples"></a>使用例

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
