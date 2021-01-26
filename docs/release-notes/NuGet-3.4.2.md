---
title: NuGet 3.4.2 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.4.2 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780248"
---
# <a name="nuget-342-release-notes"></a>NuGet 3.4.2 のリリースノート

[NuGet 3.4.1 のリリースノート](../release-notes/nuget-3.4.1.md)  | [NuGet 3.4.3 のリリースノート](../release-notes/nuget-3.4.3.md)

2016年4月8日にリリースされた NuGet 3.4.2 は、3.4 および3.4.1 リリースで特定されたいくつかの問題に対処しています。

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe 3.4.2 RC を使用できるようになりました

nuget.exe 3.4.2 のリリース候補は [こちら](https://dist.nuget.org/index.html)からダウンロードできます。

## <a name="updates-and-improvements"></a>更新プログラムと機能強化

* 特定のシナリオにおける更新のパフォーマンスが大幅に改善されました。深い依存関係グラフを含むパッケージの更新には、非常に長い時間がかかり、Visual Studio がハングしました。
* ネットワークトラフィックのない nuget の復元は、Visual Studio 内で 2.5 x ~ 3 倍高速になります。
* この変更に加えて、VS UI で更新数をフェッチするときに2回ネットワークに到達したという問題を修正しました。 これは、3.4/3.4.1 で発生したいくつかのタイムアウト問題を部分的に担当していました。
* No_proxy 設定のサポートを追加しました

## <a name="fixes"></a>修正

* 3.4.1 に更新した後、nuget.org source が NuGet の設定または config にない問題を修正しました。
* 3.4.1 で FindPackagesById の大文字と小文字の変更が発生した場合の問題を修正します。
* nuget.exe による NuGet の復元でエラーが発生した FIPS の問題を修正しました。
* 無効なアイコンの URL を使用してソースを参照するときのクラッシュを修正します。
* ' すべてのソース ' からのバージョンとエントリのマージに関する問題を修正しています。

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>3.4.2 Windows x86 コマンドライン (RC) の既知の問題

これらの問題は、RTM に達する前に、次の週の前に修正されます。

*  ソリューションファイルがプロジェクトファイルよりも下位のフォルダー階層に配置されている場合、ソリューションで nuget の復元を実行することはできません。
*  V2 フィードを使用してパッケージで nuget delete コマンドを実行すると、失敗します。 代わりに V3 フィードを使用します。


このリリースの修正プログラムと機能強化の完全な一覧については、 [ここ](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)で問題の一覧を確認してください。