---
title: "NuGet の Uninstall-package PowerShell リファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: f4f5dc79-8e8e-4012-8986-873a5d9283d9
description: "Visual Studio で NuGet パッケージ マネージャー コンソールでアンインストール パッケージの PowerShell コマンドのリファレンスです。"
keywords: "NuGet パッケージ マネージャー コンソールで、NuGet Powershell コマンドでは、NuGet Powershell リファレンス、アンインストール パッケージ"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0899198a354a56615a48a1f7f428674a205f386b
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-package (Visual Studio でパッケージ マネージャー コンソール)

*このトピック内のコマンドをについて説明、 [NuGet Package Manager Console](Package-Manager-Console.md) Windows 上の Visual Studio でします。汎用の PowerShell アンインストール パッケージ コマンドでは、次を参照してください。、 [PowerShell PackageManagement 参照](/powershell/module/packagemanagement/?view=powershell-6)です。*

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

`Uninstall-Package`次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。

## <a name="examples"></a>使用例

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
