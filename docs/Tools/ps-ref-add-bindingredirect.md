---
title: "NuGet 追加 BindingRedirect PowerShell リファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio で NuGet パッケージ マネージャー コンソールに追加 BindingRedirect PowerShell コマンドのリファレンスです。"
keywords: "NuGet パッケージ マネージャー コンソールで、NuGet Powershell コマンドでは、NuGet Powershell リファレンス、追加 BindingRedirect"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 41f27d7a1b6b363a562f26590b220d9e11e944f1
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>(Visual Studio でパッケージ マネージャー コンソール) の追加-BindingRedirect

*内でのみ使用可能な[NuGet Package Manager Console](package-manager-console.md) Windows 上の Visual Studio でします。*

プロジェクトの出力パス内のすべてのアセンブリを調べ、必要に応じて、アプリケーションまたは web 構成ファイルにバインド リダイレクトを追加します。 このコマンドは、パッケージをインストールするときに自動的に実行されます。

バインディング リダイレクト、および使用する理由の詳細については、「[アセンブリ バージョンのリダイレクト](/dotnet/framework/configure-apps/redirect-assembly-versions).NET のドキュメントにします。

## <a name="syntax"></a>構文

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| ProjectName | (必須)バインド リダイレクトを追加するプロジェクトです。 -ProjectName スイッチ自体はオプションです。 |

これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。

## <a name="common-parameters"></a>共通パラメーター

`Add-BindingRedirect` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。

## <a name="examples"></a>使用例

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```