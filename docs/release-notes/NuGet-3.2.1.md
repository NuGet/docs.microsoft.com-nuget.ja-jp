---
title: NuGet 3.2.1 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.2.1 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776516"
---
# <a name="nuget-321-release-notes"></a>NuGet 3.2.1 のリリースノート

[NuGet 3.2 リリースノート](../release-notes/nuget-3.2.md)  | [NuGet 3.3 リリースノート](../release-notes/nuget-3.3.md)

コマンドラインの NuGet 3.2.1 は2015年10月12日にリリースされ、3.2 リリースのいくつかの最適化と修正が行われており、 [dist.nuget.org](http://dist.nuget.org/index.html)から入手できます。

## <a name="improvements"></a>改善

* NuGet では、の元の大文字と小文字の区別に構成ファイルが使用されるようになりました `NuGet.Config` 。  これは、大文字と小文字を区別するオペレーティングシステム[1427](https://github.com/NuGet/Home/issues/1427)で重要です。
* NuGet の復元では、 `*.xproj` 1227 で処理する必要がある dnx プロジェクト () が無視されるようになりました `dnu` [](https://github.com/NuGet/Home/issues/1227)
* `index.json`およびパッケージ登録データ[1426](https://github.com/NuGet/Home/issues/1426)を使用する場合のネットワーク使用率の最適化
* V2 サービス[1448](https://github.com/NuGet/Home/issues/1448)でのより堅牢なリソースダウンロード処理の向上

## <a name="fixes"></a>修正

* NuGet 更新プログラムによる参照の更新 `.csproj` / `.vcxproj` [1483](https://github.com/NuGet/Home/issues/1483)
* 次に、特別なフォルダーが見つからない場合に、ローカルの nuget フォルダーが作成され[1531](https://github.com/NuGet/Home/issues/1531)ないようにします。
* ダウンロード中に破損したローカルキャッシュ内のパッケージの処理の改善 [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

コマンドラインと Visual Studio 拡張機能で解決される問題の完全な一覧については、「NuGet GitHub [3.2.1 マイルストーン](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)」を参照してください。

## <a name="known-issues"></a>既知の問題

GitHub の問題の一覧に関する問題は、引き続き次の場所にあります。 [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)