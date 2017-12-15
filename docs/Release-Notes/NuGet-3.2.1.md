---
title: "NuGet 3.2.1 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: d27c3bb9-8db1-439a-a134-54e20b7a7766
description: "NuGet 3.2.1 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。"
keywords: "NuGet 3.2.1 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2001d9518a34bbd5f2879de6123ec13abf4ae08
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-321-release-notes"></a>NuGet 3.2.1 リリース ノート

[NuGet 3.2 リリース ノート](../release-notes/nuget-3.2.md) | [NuGet 3.3 リリース ノート](../release-notes/nuget-3.3.md)

コマンドラインの NuGet 3.2.1 リリースのほんの一部の最適化と 3.2 のリリースの修正された、2015 年 10 月 12日から[dist.nuget.org](http://dist.nuget.org/index.html)です。

## <a name="improvements"></a>機能強化

* NuGet は、元の大文字と小文字の構成ファイルを使用するようになりました`NuGet.Config`です。  これは、大文字小文字を区別のオペレーティング システムで重要[1427](https://github.com/NuGet/Home/issues/1427)
* NuGet の復元は dnx プロジェクトを無視するようになりました (`*.xproj`) で処理する必要があります`dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* 使用する場合は、ネットワーク使用率を最適化`index.json`登録データをパッケージ化と[1426](https://github.com/NuGet/Home/issues/1426)
* 処理 v2 サービスでより堅牢に強化されたリソースのダウンロード[1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>修正プログラム

* NuGet の更新プログラムが正しく更新`.csproj` / `.vcxproj`参照[1483](https://github.com/NuGet/Home/issues/1483)
* 今すぐローカル .nuget フォルダーを SpecialFolders.UserProfile が見つからないときに作成して妨げて[1531](https://github.com/NuGet/Home/issues/1531)
* 処理がダウンロード中に破損しているローカル キャッシュ内でのパッケージの強化[1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

コマンドラインと Visual Studio の拡張機能は含まれて NuGet GitHub の課題の完全な一覧[3.2.1 マイルス トーン](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>既知の問題

あることができます、GitHub の問題一覧上の問題を追跡するために続行: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)