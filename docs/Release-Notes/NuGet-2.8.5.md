---
title: "NuGet 2.8.5 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 60b96b2e-2a61-4f10-b5ad-3299f5a6d453
description: "NuGet 2.8.5 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。"
keywords: "NuGet 2.8.5 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3b297704968b8423f60e9de08e27860dc375c019
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-285-release-notes"></a>NuGet 2.8.5 リリース ノート

[NuGet 2.8.3 リリース ノート](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 リリース ノート](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 は、2015 年 3 月 30 日にリリースされました。 マイナー アップデートはいくつかで VSIX、2.8.3 に修正プログラムを対象とします。

このリリースでは、NuGet パッケージ マネージャー ダイアログ ボックスのサポートが追加されました[DNX ターゲット フレームワーク モニカー](https://github.com/aspnet/dnx)です。  サポートされているこれらの新しいフレームワーク モニカーは次のとおりです。

* **core50** - a 'base' のターゲット フレームワーク モニカー (TFM) Core CLR と互換性があります。
* **dnx452** - A TFM DNX ベースを特定のアプリをフル 4.5.2 を使用して framework のバージョン
* **dnx46** - framework の 4.6 完全バージョンを使用して A TFM DNX ベースを特定のアプリ
* **dnxcore50** - A TFM DNX ベースを特定のアプリを Core 5.0 のバージョンの framework を使用します。

1 つのバグが修正された FSharp プロジェクトに正しくインストールされないパッケージ化するされませんでした。

https://nuget.codeplex.com/workitem/4400