---
title: NuGet 2.8.6 リリース ノート
description: NuGet 2.8.6 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ee801a0edfe22888d65506cea557fd9c79dcf7bd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819719"
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