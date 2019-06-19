---
title: NuGet 追加 BindingRedirect PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールで追加 BindingRedirect の PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: dec7db04c5cf239863b9c00e9f5bc0dde42c7e47
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551658"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (Package Manager Console in Visual Studio)

*内でのみ使用可能な[NuGet パッケージ マネージャー コンソール](package-manager-console.md)Windows 上の Visual Studio でします。*

プロジェクトの出力パス内のすべてのアセンブリを調べ、必要に応じて、アプリケーションまたは web 構成ファイルにバインド リダイレクトを追加します。 このコマンドは、パッケージをインストールすると自動的に実行されます。

バインド リダイレクトと使用する理由の詳細については、「[アセンブリ バージョンのリダイレクト](/dotnet/framework/configure-apps/redirect-assembly-versions).NET ドキュメントにします。

## <a name="syntax"></a>構文

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| ProjectName | (必須)バインド リダイレクトを追加するプロジェクトです。 -ProjectName スイッチ自体は省略可能です。 |

これらのパラメーターには、パイプラインの入力またはワイルドカード文字がそのまま使用します。

## <a name="common-parameters"></a>共通パラメーター

`Add-BindingRedirect` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable

## <a name="examples"></a>使用例

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```