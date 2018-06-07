---
title: NuGet の Uninstall-package PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールでアンインストール パッケージの PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 860a58c359c9b723564a70f83aee4eee5cebf16d
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818868"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Visual Studio パッケージ マネージャー コンソール)

*このトピック内のコマンドをについて説明、 [NuGet Package Manager Console](package-manager-console.md) Windows 上の Visual Studio でします。汎用の PowerShell アンインストール パッケージ コマンドでは、次を参照してください。、 [PowerShell PackageManagement 参照](/powershell/module/packagemanagement/?view=powershell-6)です。*

必要に応じてその依存関係を削除する、プロジェクトからパッケージを削除します。 コマンドが失敗しない限り、その他のパッケージは、このパッケージに依存している場合、– Force オプションを指定します。

## <a name="syntax"></a>構文

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

コマンドが失敗しない限り、その他のパッケージは、このパッケージに依存している場合、– Force オプションを指定します。

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| ID | (必須)アンインストールするパッケージの識別子。 -Id スイッチ自体は省略可能です。 |
| Version | をアンインストールするパッケージのバージョン、現在インストールされているバージョンを既定とします。 |
| RemoveDependencies | パッケージとその未使用の依存関係をアンインストールします。 つまり、すべての依存関係に依存している別のパッケージがある場合は、これはスキップされます。 |
| ProjectName | 既定で、既定のプロジェクト、パッケージをアンインストールするプロジェクトです。 |
| Force | 場合でも、依存している他のパッケージをアンインストールするパッケージを強制します。 |
| WhatIf | 実際には、アンインストールを実行せず、コマンドを実行している場合にどうなるかを示します。 |

これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。

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
