---
title: NuGet 3.2.1 のリリース ノート
description: などの NuGet 3.2.1 のリリース ノートには、問題、バグの修正、追加機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5ddbb8aa52ef85c823404364a3aca79fd16f3b1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548191"
---
# <a name="nuget-321-release-notes"></a>NuGet 3.2.1 のリリース ノート

[NuGet 3.2 リリース ノート](../release-notes/nuget-3.2.md) | [NuGet 3.3 のリリース ノート](../release-notes/nuget-3.3.md)

コマンドラインの NuGet 3.2.1、いくつかの最適化と 3.2 のリリースの修正、2015 年 10 月 12 日にリリースされ、はから利用可能な[dist.nuget.org](http://dist.nuget.org/index.html)します。

## <a name="improvements"></a>機能強化

* NuGet は、元の大文字小文字の区別を構成ファイルを使用するようになりました`NuGet.Config`します。  これは大文字のオペレーティング システムで重要な[1427](https://github.com/NuGet/Home/issues/1427)
* NuGet の復元は dnx プロジェクトを無視するようになりました (`*.xproj`) で処理する必要があります`dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* 使用する場合は、ネットワーク使用率を最適化`index.json`登録データをパッケージ化と[1426](https://github.com/NuGet/Home/issues/1426)
* V2 サービスをより堅牢に処理の強化されたリソース ダウンロード[1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>修正プログラム

* NuGet の更新が正しく更新`.csproj` / `.vcxproj`参照[1483](https://github.com/NuGet/Home/issues/1483)
* ローカル .nuget フォルダーが見つかりません、SpecialFolders.UserProfile ときに作成されないようにようになりましたこと[1531](https://github.com/NuGet/Home/issues/1531)
* ダウンロード中に破損がローカル キャッシュ内でのパッケージの処理を改善[1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

NuGet GitHub で見つかるコマンドラインと Visual Studio の拡張機能に対処された問題の完全な一覧[3.2.1 マイルス トーン](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>既知の問題

GitHub の問題一覧上の問題を追跡するために引き続き。 [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)