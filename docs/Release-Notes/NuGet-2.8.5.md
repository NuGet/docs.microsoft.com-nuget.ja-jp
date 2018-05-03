---
title: NuGet 2.8.5 リリース ノート
description: NuGet 2.8.5 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 40557035e445d07e7acf301e34b750b329ba9990
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
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