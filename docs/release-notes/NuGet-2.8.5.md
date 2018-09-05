---
title: NuGet 2.8.5 リリース ノート
description: NuGet 2.8.5 などのリリース ノートには、問題、バグの修正、追加機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548626"
---
# <a name="nuget-285-release-notes"></a>NuGet 2.8.5 リリース ノート

[NuGet 2.8.3 リリース ノート](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 リリース ノート](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 は、2015 年 3 月 30 日にリリースされました。 マイナー更新は、2.8.3 に一部の VSIX に修正プログラムが対象とします。

このリリースで NuGet パッケージ マネージャー ダイアログのサポートが追加された[DNX ターゲット フレームワーク モニカー](https://github.com/aspnet/dnx)します。  サポートされているこれらの新しいフレームワーク モニカーは次のとおりです。

* **core50** - 'base' のターゲット フレームワーク モニカー (TFM)、Core CLR と互換性があります。
* **dnx452** - 完全 4.5.2 を使用して A TFM を DNX ベース特定のアプリ、フレームワークのバージョン
* **dnx46** - 4.6 を完全なバージョンの framework を使用して A TFM を DNX ベース特定のアプリ
* **dnxcore50** - Core 5.0 のバージョンの framework を使用して、TFM を DNX ベース特定のアプリ

1 つのバグには、FSharp プロジェクトに正しくインストールされませんでした、パッケージが修正済み。

https://nuget.codeplex.com/workitem/4400