---
title: NuGet 3.4.2 リリース ノート
description: NuGet 3.4.2 などのリリース ノートには、問題、バグの修正、追加機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549152"
---
# <a name="nuget-342-release-notes"></a>NuGet 3.4.2 リリース ノート

[NuGet 3.4.1 リリース ノート](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 リリース ノート](../release-notes/nuget-3.4.3.md)

2016 年 4 月 8 日、3.4 および 3.4.1 で識別されたいくつかの問題に対処するにリリースされた NuGet 3.4.2 を解放します。

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe 3.4.2 RC が利用できるようになりました

Nuget.exe 3.4.2 の release candidate をダウンロードする[ここ](https://dist.nuget.org/index.html)します。

## <a name="updates-and-improvements"></a>更新プログラムと機能強化

* 厳密な依存関係グラフを使用してパッケージの更新プログラムが非常に長い時間がかかったし、Visual Studio がハングしている特定のシナリオでの更新プログラムのパフォーマンスが大幅に向上しました。
* nuget 復元せずにネットワーク トラフィックは、2.5 x – Visual Studio 内で 3 倍です。
* この変更だけでなくが問題を修正しましたできるほか、VS UI 内の数、更新プログラムをフェッチするときに 2 回に、ネットワークに達するされています。 これで 3.4/3.4.1 経験豊富なタイムアウトの問題ユーザーによって部分的に担当していました。
* No_proxy 設定のサポートが追加されました

## <a name="fixes"></a>修正プログラム

* Nuget.org のソースが NuGet の設定または config で不足している 3.4.1 に更新した後、問題を修正しました。
* FindPackagesById 3.4.1 で大文字と小文字の変更が Artifactory を中断する問題を修正しました。
* Fips nuget.exe の NuGet 復元でエラーの原因となった問題を修正しました。
* 無効なアイコンの URL を使用してソースを参照するときに、クラッシュを修正しました。
* バージョンと 'すべてのソース' からのエントリを結合すると問題が修正されました。

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>既知の問題が 3.4.2 で Windows x86 Commandline (RC)

RTM に到達する前に早期の次の週に、これらの問題が修正されます。

*  ソリューション ファイルがプロジェクト ファイルよりも下のフォルダー階層内に配置されている場合、ソリューションを実行している nuget の復元は失敗します。
*  V2 フィードを使用してパッケージで nuget delete コマンドを実行は失敗します。 V3 フィードを使用してください。


修正し、このリリースの機能強化の完全な一覧で、問題の一覧をご覧ください[ここ](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)します。