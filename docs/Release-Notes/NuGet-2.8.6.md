---
title: "NuGet 2.8.6 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 920c551c-18a7-40f4-a32b-ce84de6ea766
description: "NuGet 2.8.6 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。"
keywords: "NuGet 2.8.6 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4dfd0a76967280cc6a16b37fe2b2a3362231fce5
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-286-release-notes"></a>NuGet 2.8.6 リリース ノート

[NuGet 2.8.5 リリース ノート](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 リリース ノート](../release-notes/nuget-2.8.7.md)

NuGet 2.8.6 がリリースされた修正と Windows 10 UWP 開発モデルのサポートされる可能性があるパッケージをサポートするために強化、2.8.5 のマイナー アップデートとして、2015 年 7 月 20日の VSIX を対象とします。

このバージョンの NuGet パッケージ マネージャー拡張機能は、Visual Studio 2013 のサポートのみを提供します。

このリリースでは、NuGet Package Manager ダイアログには、サポートの追加が必要があります。

* Windows 10 のアプリケーションの開発をサポートするために UAP ターゲット フレームワーク モニカーが導入されました。
* NuGet プロトコル バージョン 3 のエンドポイント
* サポート[Nuget.Config](../consume-packages/configuring-nuget-behavior.md)リポジトリ ソースに対する protocolVersion 属性。 既定値は「2」
* ローカル キャッシュ内では、必要なパッケージのバージョンが使用できない場合に、リモート リポジトリに戻る