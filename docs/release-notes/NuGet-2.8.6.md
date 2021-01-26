---
title: NuGet 2.8.6 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.8.6 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776703"
---
# <a name="nuget-286-release-notes"></a>NuGet 2.8.6 のリリースノート

[NuGet 2.8.5 のリリースノート](../release-notes/nuget-2.8.5.md)  | [NuGet 2.8.7 のリリースノート](../release-notes/nuget-2.8.7.md)

NuGet 2.8.6 は、2015年7月20日にリリースされました。また、Windows 10 UWP 開発モデルのサポートと共に提供される可能性のあるパッケージのサポートを対象とした修正プログラムと機能強化が含まれています。

このバージョンの NuGet パッケージマネージャー拡張機能では Visual Studio 2013 のみがサポートされます。

このリリースでは、NuGet パッケージマネージャーダイアログで次の機能が追加されました。

* Windows 10 アプリケーション開発をサポートする UAP ターゲットフレームワークモニカーが導入されました。
* NuGet プロトコルバージョン3エンドポイント
* リポジトリソースでの [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion 属性のサポート。 既定値は "2" です。
* 必要なパッケージバージョンがローカルキャッシュで利用できない場合に、リモートリポジトリにフォールバックする