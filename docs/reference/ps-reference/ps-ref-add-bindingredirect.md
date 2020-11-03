---
title: NuGet Add-BindingRedirect PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールで Add-BindingRedirect PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 382ba9b179428c70e3eb16db86a363e095207d61
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237258"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (Visual Studio のパッケージマネージャーコンソール)

*Windows の Visual Studio の [パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md) 内でのみ使用できます。*

プロジェクトの出力パス内のすべてのアセンブリを調べ、必要に応じて、アプリケーションまたは web 構成ファイルにバインドリダイレクトを追加します。 このコマンドは、パッケージのインストール時に自動的に実行されます。

> [!NOTE]
> これは、packages.config ファイルを使用するシナリオにのみ適用されます。 詳細については、「 [NuGet packages.config ファイルリファレンス](~/reference/packages-config.md)」を参照してください。

バインディングリダイレクトとその使用理由の詳細については、.NET ドキュメントの「 [アセンブリバージョンのリダイレクト](/dotnet/framework/configure-apps/redirect-assembly-versions) 」を参照してください。

## <a name="syntax"></a>構文

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| ProjectName | 必要バインドリダイレクトを追加するプロジェクト。 -ProjectName スイッチ自体は省略可能です。 |

これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。

## <a name="common-parameters"></a>共通パラメーター

`Add-BindingRedirect` は、Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数の [一般的な PowerShell パラメーター](/powershell/module/microsoft.powershell.core/about/about_commonparameters)をサポートしています。

## <a name="examples"></a>使用例

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```