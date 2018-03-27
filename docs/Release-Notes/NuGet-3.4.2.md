---
title: "NuGet 3.4.2 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 3.4.2 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。"
keywords: "NuGet 3.4.2 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 892a965e67762af2ae42c2d6ee75d2838104d1c2
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-342-release-notes"></a>NuGet 3.4.2 リリース ノート

[NuGet 3.4.1 リリース ノート](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 リリース ノート](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2 は 2016 年 4 月 8 日、3.4 および 3.4.1 で識別されたいくつかの問題を解決するにリリースされたリリースします。

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe 3.4.2 RC が利用できるようになりました

Nuget.exe 3.4.2 のリリース候補版をダウンロードする[ここ](https://dist.nuget.org/index.html)です。

## <a name="updates-and-improvements"></a>更新プログラムと機能強化

* 特定のシナリオ、詳細な依存関係グラフを使用してパッケージで更新プログラムが非常に長い時間がかかりし、Visual Studio のハング状態にある更新プログラムのパフォーマンスを大幅に改善おが。
* ネットワーク トラフィックがない nuget の復元は 2.5 ~ x 3 Visual Studio 内で高速です。
* この変更だけでなくおが問題を修正できるほか、VS UI 内の数、更新プログラムをフェッチするときに 2 回に、ネットワークにヒットされたお。 これが部分的に 3.4/3.4.1 の経験豊富ないくつかのタイムアウトの問題顧客を担当します。
* No_proxy 設定のサポートが追加されました

## <a name="fixes"></a>修正プログラム

* Nuget.org のソースがある NuGet 設定または config で不足している 3.4.1 に更新した後、問題を修正しました。
* 問題を修正、FindPackagesById 3.4.1 で大文字と小文字の変更が Artifactory を中断します。
* FIPS nuget.exe と NuGet の復元に失敗の原因となった問題を修正しました。
* [無効] アイコンの URL を使用してソースを参照するときに、クラッシュを修正しました。
* バージョンと 'すべてのソース' からエントリを結合すると問題を修正しました。

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>3.4.2 で既知の問題 Windows x86 Commandline (RC)

RTM に達する前に初期の次の週に、これらの問題が修正されます。

*  ソリューション ファイルがプロジェクト ファイルよりも下のフォルダー階層内に配置されている場合、ソリューションを実行している nuget の復元は失敗します。
*  V2 のフィードを使用してパッケージで nuget delete コマンドを実行は失敗します。 V3 フィードを使用してください。


、修正し、このリリースの機能強化の完全な一覧を確認して問題の一覧[ここ](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)です。