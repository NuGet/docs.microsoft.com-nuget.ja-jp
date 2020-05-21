---
title: NuGet 5.6 リリースノート
description: 新機能、バグ修正、および DCRs を含む NuGet 5.6 のリリースノート。
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727807"
---
# <a name="nuget-56-release-notes"></a>NuGet 5.6 リリースノート

NuGet 配布の種類:

| NuGet のバージョン | 利用可能な Visual Studio バージョン| 利用可能な .NET SDK|
|:---|:---|:---|
| [**5.6.0**](https://nuget.org/downloads) | [Visual Studio 2019 バージョン 16.6](https://visualstudio.microsoft.com/downloads/) | [3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup>.NET Core ワークロードを含む Visual Studio 2019 と共にインストールされます。

## <a name="summary-whats-new-in-56"></a>概要: 5.6 の新機能

* フローティングバージョンでのプレリリースパッケージをサポートします。 `Version="*-*"`、 `Version="1.*-*"` 、およびは、指定された範囲内で、プレリリースバージョンを含む最新バージョンに類似してい[#912](https://github.com/NuGet/Home/issues/912)

### <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

**バグ**

* `nuget push *.nupkg`snupkg が存在しない場合に失敗します- [#8148](https://github.com/NuGet/Home/issues/8148)

* パックなど、いくつかのコードパスは、ロケールに依存しません。 RegexOptions を使用します。 Regexoptions.cultureinvariant- [#8246](https://github.com/NuGet/Home/issues/8246)

* パフォーマンス: アンロードされたプロジェクトシナリオの DG 仕様をプレビュー復元で記述することはできません- [#8793](https://github.com/NuGet/Home/issues/8793)

* 復元: ソリューションの依存関係グラフの仕様をキャッシュしてパフォーマンスを向上させる- [#9201](https://github.com/NuGet/Home/issues/9201)

* Pm コンソールを使用してパッケージをインストールした後、SDK スタイルプロジェクトで PM UI が機能しない- [#9203](https://github.com/NuGet/Home/issues/9203)

* 埋め込みアイコンは、ローカルパッケージフィードを含む PM UI では表示できません (/vs \- [#9225](https://github.com/NuGet/Home/issues/9225)によって異なります)

* NuGetVersion () は解析に失敗した場合に false を返します- [#9255](https://github.com/NuGet/Home/issues/9255)

* `nuget.exe push`のヘルプでは、ソース `-source` URL ではなくソース名の使用を提案する必要があり[#9265](https://github.com/NuGet/Home/issues/9265)

* `dotnet nuget add package SourceUri`無効な既定のパッケージソース名を作成します- [#9277](https://github.com/NuGet/Home/issues/9277)

* スクリーンリーダーが "検索中..." をアナウンスしないタブを切り替えるときのメッセージ- [#9307](https://github.com/NuGet/Home/issues/9307)

* アクセシビリティ: 暗いテーマでは、フォーカスを示す四角形の色は PM UI タブにはアクセスできません- [#9336](https://github.com/NuGet/Home/issues/9336)

* MSBuild 14 以下では、nuget.exe 5.5 を復元できません- [#9458](https://github.com/NuGet/Home/issues/9458)

* メッセージの復元中にミリ秒単位の時間をログに記録しない- [#8977](https://github.com/NuGet/Home/issues/8977)

* IOutputConsole を非同期[#9268](https://github.com/NuGet/Home/issues/9268)にする

* 一部の英語以外のカルチャでは、MSBuild バージョンの選択が正しく機能しません- [#9322](https://github.com/NuGet/Home/issues/9322)

* #9337 に既定の形式がありません `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)

* Perf: RestoreOperationLogger に不要なスレッドアフィニティがあります- [#9288](https://github.com/NuGet/Home/issues/9288)

* コマンドのドキュメントの自動作成 `dotnet nuget` - [#9146](https://github.com/NuGet/Home/issues/9146)

* 既定の詳細度では、各プロジェクトの noop 復元を報告することはできません- [#8792](https://github.com/NuGet/Home/issues/8792)

* `-DependencyVersion`のサポートパラメーター `NuGet.exe update` は、インストールコマンド[#7694](https://github.com/NuGet/Home/issues/7694)と似ています。


**Dcr**

* Net 5.0 ターゲットフレームワークの初期サポートを追加する- [#9584](https://github.com/NuGet/Home/issues/9584)

* PM UI [#9278](https://github.com/NuGet/Home/issues/9278)の [更新] タブで、ID でパッケージを並べ替えます。


**[このリリースで修正されるすべての問題の一覧-5.6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**
