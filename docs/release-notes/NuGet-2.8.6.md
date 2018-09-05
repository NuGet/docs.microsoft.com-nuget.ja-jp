---
title: NuGet 2.8.6 リリース ノート
description: NuGet 2.8.6 などのリリース ノートには、問題、バグの修正、追加機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d57c658999ed3c79b962de84fd973276833ef3fd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546492"
---
# <a name="nuget-286-release-notes"></a>NuGet 2.8.6 リリース ノート

[NuGet 2.8.5 リリース ノート](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 リリース ノート](../release-notes/nuget-2.8.7.md)

NuGet 2.8.6 がリリースされた修正プログラムと機能強化、Windows 10 UWP 開発モデル対応の配信可能性がありますパッケージをサポートするために、2.8.5 のマイナー アップデートとして、2015 年 7 月 20日一部の VSIX を対象とします。

このバージョンの NuGet パッケージ マネージャー拡張機能は、Visual Studio 2013 のサポートのみを提供します。

このリリースでは、NuGet パッケージ マネージャー ダイアログのサポートが追加必要があります。

* Windows 10 のアプリケーションの開発をサポートするために UAP ターゲット フレームワーク モニカーが導入されました。
* NuGet プロトコル バージョン 3 のエンドポイント
* サポート[Nuget.Config](../consume-packages/configuring-nuget-behavior.md)リポジトリ ソース protocolVersion 属性。 既定値は「2」
* ローカル キャッシュ内で必要なパッケージ バージョンが使用できない場合、リモート リポジトリにフォールバック