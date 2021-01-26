---
title: NuGet 2.8.5 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.8.5 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780355"
---
# <a name="nuget-285-release-notes"></a>NuGet 2.8.5 のリリースノート

[NuGet 2.8.3 のリリースノート](../release-notes/nuget-2.8.3.md)  | [NuGet 2.8.6 のリリースノート](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 は2015年3月30日にリリースされました。 これは、一部の修正プログラムが適用された 2.8.3 VSIX のマイナー更新です。

このリリースでは、 [Dnx ターゲットフレームワークモニカー](https://github.com/aspnet/dnx)の [NuGet パッケージマネージャーのサポート] ダイアログが追加されました。  次のような新しいフレームワークモニカーがサポートされています。

* **core50** -コア CLR と互換性のある ' base ' ターゲットフレームワークモニカー (tfm) です。
* **dnx452** -完全な4.5.2 バージョンのフレームワークを使用する dnx ベースのアプリに固有の A tfm
* **dnx46** -完全な4.6 バージョンのフレームワークを使用する dnx ベースのアプリに固有の A tfm
* **dnxcore50** -Core 5.0 バージョンのフレームワークを使用する dnx ベースのアプリに固有の A tfm

1つのバグが修正されました。これにより、パッケージを Fsharp.core プロジェクトに適切にインストールできませんでした。

https://nuget.codeplex.com/workitem/4400