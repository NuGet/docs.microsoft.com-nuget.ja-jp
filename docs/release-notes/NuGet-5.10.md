---
title: NuGet 5.10 リリースノート
description: 新機能、バグ修正、および dcrs を含む NuGet 5.10 のリリースノート。
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 80a372074604f5c0073f78927b84de00e78acc74
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726952"
---
# <a name="nuget-510-release-notes"></a>NuGet 5.10 リリースノート

NuGet 配布の種類:

| NuGet のバージョン | 利用可能な Visual Studio バージョン | 利用可能な .NET SDK |
|:---|:---|:---|
| [**5.10.0**](https://nuget.org/downloads) | [Visual Studio 2019 バージョン16.10](https://visualstudio.microsoft.com/downloads/) | [5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> Visual Studio 2019 と共に .net Core ワークロードと共にインストールされる
  
> [!NOTE]
> Visual Studio 16.10、MSBuild 16.10、および .net 5.0.300 + には NuGet.exe 5.10 以降が必要です。

## <a name="summary-whats-new-in-510"></a>概要: 5.10 の新機能

* 署名: dotnet 信頼署名者コマンド[#8053](https://github.com/NuGet/Home/issues/8053)を実装する

* Linux では既定の検証を無効にしますが、Windows- [#10713](https://github.com/NuGet/Home/issues/10713)では既定で有効になります。

* .NET 5 + Linux/MAC [#10742](https://github.com/NuGet/Home/issues/10742)でパッケージ署名検証用の ENV 変数を追加する

* 大規模なソリューションのインストールの新しいパッケージのパフォーマンスを向上させる- [#10166](https://github.com/NuGet/Home/issues/10166)

* `nfproj`NUGET CLI の supportedProjectExtensions の一覧にプロジェクトの種類を追加します。 - [#10562](https://github.com/NuGet/Home/issues/10562)

### <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

* `<requireLicenseAcceptance>`プロジェクトをパッキングするときに要素を非表示にする- [#5133](https://github.com/NuGet/Home/issues/5133)

* [CPVM] プレビューの警告を dotnet cli に表示する必要があり [#10226](https://github.com/NuGet/Home/issues/10226)

* PMUI の背景色と前景色のトークンを CommonDocumentColors に更新して [#10608](https://github.com/NuGet/Home/issues/10608)

* [バグ Bash]PM UI ですばやくタブを切り替えると、"ユーザーによって操作が取り消されました" というエラーがエラー一覧ウィンドウに表示される- [#10671](https://github.com/NuGet/Home/issues/10671)

* PM UI: ソリューションレベルでのパッケージインストールのパフォーマンスを向上させる- [#10210](https://github.com/NuGet/Home/issues/10210)

* NuGet 内のすべての場所で、GetService を GetServiceAsync に置き換えます。クライアント- [#3784](https://github.com/NuGet/Home/issues/3784)

* `..`相対パス[#5016](https://github.com/NuGet/Home/issues/5016)での NuGet.exe pack のパフォーマンスの問題

* ソースパスのレベルを上げると、"nuget pack" のパフォーマンスが低下します- [#5706](https://github.com/NuGet/Home/issues/5706)

* 重複するファイルで nuspec をパッケージ化するときに NuGet がエラーになることはありません。 - [#6941](https://github.com/NuGet/Home/issues/6941)

* NuGet パック "指定された DateTimeOffset は Zip ファイルのタイムスタンプに変換できません"- [#7001](https://github.com/NuGet/Home/issues/7001)

* パックされたパッケージのファイルのタイムスタンプは、タイムゾーンの[#7395](https://github.com/NuGet/Home/issues/7395)によってシフトされます

* NU1004 には、より実用的な情報が含まれている必要があり [#7696](https://github.com/NuGet/Home/issues/7696)

* [バグ Bash][テストの失敗]' Dotnet restore を実行しているときに、空または間違った形式のロックファイルを更新することはできません----lock-file--locked-- [#8640](https://github.com/NuGet/Home/issues/8640)

* NuGetVersionRange を使用すると、論理的に間違った範囲を解析することができ [#9145](https://github.com/NuGet/Home/issues/9145)

* PM UI では、選択したパッケージソースとホバーしたパッケージソースの間に識別された背景色を表示できません- [#9538](https://github.com/NuGet/Home/issues/9538)

* インストールするプロジェクトを選択するためのチェックボックスがスクリーンリーダーによって読み込まれていません- [#9578](https://github.com/NuGet/Home/issues/9578)

* [詳細] ウィンドウのバージョンドロップダウンの既定の選択項目がインストールされているか、更新された[#9887](https://github.com/NuGet/Home/issues/9887)タブに LatestStable

* 一部の .net 5 sdk レポート targetplatformmoniker レポートの回避策アカウントを削除 ` ,Version= `  -  [#9913](https://github.com/NuGet/Home/issues/9913)

* dotnet nuget 検証が小さすぎる- [#10316](https://github.com/NuGet/Home/issues/10316)

* VersionRange で1桁の範囲を解析できません- [#10342](https://github.com/NuGet/Home/issues/10342)

* VS ソリューションマネージャーがデバッグ時に null 例外をスローする- [#10352](https://github.com/NuGet/Home/issues/10352)

* CLI 例外メッセージを文字列リソースファイルに移動する- [#10392](https://github.com/NuGet/Home/issues/10392)

* 停止しているコードの削除 (TabItemButtonAutomationPeer)- [#10435](https://github.com/NuGet/Home/issues/10435)

* コンテキストメニューを最初に選択した項目までスクロールする必要があります- [#10498](https://github.com/NuGet/Home/issues/10498)

* Solution PMUI の詳細に水平バーが重なっています- [#10533](https://github.com/NuGet/Home/issues/10533)

* 署名: 証明書の有効期限が切れたときにプライマリ署名の詳細が表示されない- [#10535](https://github.com/NuGet/Home/issues/10535)

* 有効なソースがない場合、PM UI が- [#10541](https://github.com/NuGet/Home/issues/10541)表示されません

* パッケージメタデータ (詳細、廃止) は[#10549](https://github.com/NuGet/Home/issues/10549) 、CodeSpaces で nuget.org から引き出されないことがあります。

* デバッグセッション中に、PMUI の初期化が例外で失敗する- [#10559](https://github.com/NuGet/Home/issues/10559)

* ビッグエンディアンシステムでパッケージの整合性チェックに失敗した場合、nuget の復元結果が [#10567](https://github.com/NuGet/Home/issues/10567)

* FormatException は[#10595](https://github.com/NuGet/Home/issues/10595) 、の代わりにスローされます。

* CPVM-グラフウォークアルゴリズムでの同時実行の問題- [#10598](https://github.com/NuGet/Home/issues/10598)

* PMC powershell バージョンのテレメトリを追加する- [#10609](https://github.com/NuGet/Home/issues/10609)

* NuGetVersion 並べ替えのパフォーマンスを向上させる- [#10611](https://github.com/NuGet/Home/issues/10611)

* 信頼された署名者の追加の引数が一致しません- [#10647](https://github.com/NuGet/Home/issues/10647)

* Vs2019 v 16.9.0: NuGet パッケージマネージャーのタブを [更新] から [インストール済み] に切り替えると、フレームが更新されません。 - [#10654](https://github.com/NuGet/Home/issues/10654)

* PMUI- [#10677](https://github.com/NuGet/Home/issues/10677)のバージョン番号から "v" を削除します。

* INuGetProjectService は、CPS プロジェクトシステムの申請を受け取る前に、 [#10681](https://github.com/NuGet/Home/issues/10681)をスローします。

* 埋め込みアイコンを使用すると、[参照] タブの[#10687](https://github.com/NuGet/Home/issues/10687)で、ソース "Microsoft Visual Studio オフラインパッケージ" からアクセスが拒否される

* MSBuildProjectExtensionsPath が設定されていない場合[#10739](https://github.com/NuGet/Home/issues/10739) 、INuGetProjectService がスローされます。

* "dotnet nuget remove source nuget.org" は初回[#10745](https://github.com/NuGet/Home/issues/10745)は機能しません

* Nuget は、非同期メソッドで threadpool スレッドをブロックし、UI スレッドへの同期呼び出しを行い [#10775](https://github.com/NuGet/Home/issues/10775)

* `PackageLoadContext.GetInstalledAndTransitivePackagesAsync` 配信不能コードと低下パフォーマンス- [#10790](https://github.com/NuGet/Home/issues/10790)

* NuGet SDK パッケージで埋め込みアイコンを使用する- [#10795](https://github.com/NuGet/Home/issues/10795)

* SPDX ライセンスリストを更新する- [#10806](https://github.com/NuGet/Home/issues/10806)

**[このリリースで修正されるすべての問題の一覧-5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**
  
**[このリリースのコミットの一覧-5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**
  
### <a name="community-contributions"></a>コミュニティからの投稿

この NuGet リリースに役立った共同作成者全員に感謝します。

|担当者|Pr|発行|
|----|----|----|
[ルイス-z](https://github.com/louis-z) | [3991](https://github.com/NuGet/NuGet.Client/pull/3991) | VersionRange で1桁の範囲を解析できません- [#10342](https://github.com/NuGet/Home/issues/10342)
[omajid](https://github.com/omajid) | [3860](https://github.com/NuGet/NuGet.Client/pull/3860) | NuGet。クライアント build.sh が壊れています- [#10139](https://github.com/NuGet/Home/issues/10139)
[Nirmal4G](https://github.com/Nirmal4G) | [3623](https://github.com/NuGet/NuGet.Client/pull/3623) | NuGet。クライアント build.sh が壊れています- [#10139](https://github.com/NuGet/Home/issues/10139)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | ソースパスのレベルを上げると、"nuget pack" のパフォーマンスが低下します- [#5706](https://github.com/NuGet/Home/issues/5706)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | NuGet.exe pack のパフォーマンスに問題があります... 相対パス- [#5016](https://github.com/NuGet/Home/issues/5016)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3940](https://github.com/NuGet/NuGet.Client/pull/3940) | CPVM-グラフウォークアルゴリズムでの同時実行の問題- [#10598](https://github.com/NuGet/Home/issues/10598)
[このように](https://github.com/josesimoes) | [3943](https://github.com/NuGet/NuGet.Client/pull/3943) | Nuget CLI の supportedProjectExtensions の一覧に、プロジェクトの種類として「モジュール」を追加します。 - [#10562](https://github.com/NuGet/Home/issues/10562)

## <a name="feedback-welcome"></a>フィードバックの開始

お客様のフィードバックは Microsoft にとって重要です。  このリリースに問題がある場合は、GitHub の[問題](https://github.com/NuGet/Home/issues)を確認し、既存の問題について[開発者 Community を Visual Studio](https://developercommunity.visualstudio.com/)してください。  NuGet 内の新しい問題については、 [GitHub の問題](https://github.com/NuGet/Home/issues/new)を報告してください。
NuGet エクスペリエンスに関する一般的な問題については、[**ヘルプ] >**[問題の報告] の下にあるお気に入りの IDE にある [問題点の [報告](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)] オプションを使用してお知らせください。
