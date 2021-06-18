---
title: NuGet 5.10 リリース ノート
description: 新機能、バグ修正、DCRs など、NuGet 5.10 のリリース ノート。
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 666eda5803b540dc18a9310f61c92dc74ff2089e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112356499"
---
# <a name="nuget-510-release-notes"></a>NuGet 5.10 リリース ノート

NuGet 配布の種類:

| NuGet のバージョン | 利用可能な Visual Studio バージョン | 利用可能な .NET SDK |
|:---|:---|:---|
| [**5.10.0**](https://nuget.org/downloads) | [Visual Studio 2019 バージョン 16.10](https://visualstudio.microsoft.com/downloads/) | [5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> .NET Core ワークロードVisual Studio 2019 でインストール済み
  
> [!NOTE]
> Visual Studio 16.10、MSBuild 16.10、および .NET 5.0.300 以降では、NuGet.exe 5.10 以降が必要です。

## <a name="summary-whats-new-in-510"></a>概要: 5.10 の新機能

* 署名: dotnet trusted-signers コマンドを実装する - [#8053](https://github.com/NuGet/Home/issues/8053)

* Linux では既定の検証を無効にし、Windows では既定[で有効にする](https://github.com/NuGet/Home/issues/10713)- #10713

* .NET 5+ Linux/MAC でパッケージ署名検証用の ENV 変数を追加する - [#10742](https://github.com/NuGet/Home/issues/10742)

* 大規模なソリューションの新しいパッケージのインストールパフォーマンスを向上させる - [#10166](https://github.com/NuGet/Home/issues/10166)

* `nfproj`Nuget CLI でサポートされているProjectExtensions の一覧にプロジェクトの種類を追加します。 - [#10562](https://github.com/NuGet/Home/issues/10562)

### <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

* プロジェクトを <requireLicenseAcceptance> パッキングするときに 要素を抑制[](https://github.com/NuGet/Home/issues/5133)する - #5133

* [CPVM] dotnet cli にプレビューの警告が表示される必要があります - [#10226](https://github.com/NuGet/Home/issues/10226)

* PMUI の背景色トークンと前景色トークンを CommonDocumentColors [-](https://github.com/NuGet/Home/issues/10608) #10608

* [バグ Bash]PM UI でタブをすばやく切り替えるときにエラー "ユーザーによって取り消された操作" が [エラー一覧] ウィンドウに表示される - [#10671](https://github.com/NuGet/Home/issues/10671)

* PM UI: ソリューション レベルでのパッケージ インストールのパフォーマンスを向上させる - [#10210](https://github.com/NuGet/Home/issues/10210)

* GetService を NuGet.Clients のすべての場所で GetServiceAsync に置き換える - [#3784](https://github.com/NuGet/Home/issues/3784)

* NuGet.exeパスに関するパックパフォーマンス `..` の問題 - [#5016](https://github.com/NuGet/Home/issues/5016)

* "nuget pack" のパフォーマンスは、ソース パスのレベルが上がって低下 [します。#5706](https://github.com/NuGet/Home/issues/5706)

* 重複するファイルを含む nuspec をパッケージ化する場合、NuGet ではエラーが発生しない。 - [#6941](https://github.com/NuGet/Home/issues/6941)

* NuGet パック "指定された DateTimeOffset を Zip ファイルのタイムスタンプに変換できません" [-](https://github.com/NuGet/Home/issues/7001) #7001

* パックされたパッケージのファイルのタイムスタンプは、タイムゾーンによってシフトされます[-](https://github.com/NuGet/Home/issues/7395) #7395

* NU1004 には、より多くのアクション可能な情報が含まれている必要[があります](https://github.com/NuGet/Home/issues/7696)- #7696

* [バグ Bash][テスト エラー]'dotnet restore --use-lock-file --locked-mode' - #8640 を実行するときに、空または形式のロック ファイル[を更新することはできません](https://github.com/NuGet/Home/issues/8640)。

* NuGetVersionRange を使用すると、論理的に正しくない範囲[](https://github.com/NuGet/Home/issues/9145)を解析#9145

* PM UI では、選択したパッケージ ソースとホバーされたパッケージ ソースの間で識別可能な背景色[を](https://github.com/NuGet/Home/issues/9538)表示できません - #9538

* インストールするプロジェクトを選択する場合のチェック ボックスがスクリーン リーダーによって読[](https://github.com/NuGet/Home/issues/9578)み取#9578

* 詳細ペインのバージョン ドロップダウンの既定の選択は、[インストール済み]/[更新] タブで [インストール済み]/[LatestStable] である必要があります - [#9887](https://github.com/NuGet/Home/issues/9887)

* 一部の .NET 5 SDK レポート TargetPlatformMoniker の回避策アカウントを削除 ` ,Version= `  -  [#9913](https://github.com/NuGet/Home/issues/9913)

* dotnet nuget verify is too quiet - [#10316](https://github.com/NuGet/Home/issues/10316)

* VersionRange で 1 桁の範囲を解析できない - [#10342](https://github.com/NuGet/Home/issues/10342)

* VS Solution Manager がデバッグ中に に null 例外を[スローする](https://github.com/NuGet/Home/issues/10352)- #10352

* CLI 例外メッセージを文字列リソース ファイルに移動する - [#10392](https://github.com/NuGet/Home/issues/10392)

* 使用されなコードを削除する (TabItemButtonAutomationPeer) - [#10435](https://github.com/NuGet/Home/issues/10435)

* 更新コンテキスト メニューは、最初に選択した項目までスクロールする必要があります - [#10498](https://github.com/NuGet/Home/issues/10498)

* ソリューション PMUI の詳細の横棒が重なっている - [#10533](https://github.com/NuGet/Home/issues/10533)

* 署名: 証明書の有効期限が切れ、タイムスタンプが信頼されていない場合にプライマリ署名の詳細[が表示](https://github.com/NuGet/Home/issues/10535)されない - #10535

* 有効なソースがない場合、PM UI が表示#10541 [](https://github.com/NuGet/Home/issues/10541)

* パッケージ メタデータ (詳細、非推奨) は、CodeSpaces の nuget.org からプルされない場合があります - [#10549](https://github.com/NuGet/Home/issues/10549)

* デバッグ セッション中に PMUI の初期化が例外で失敗する - [#10559](https://github.com/NuGet/Home/issues/10559)

* nuget の復元により、ビッグ エンディアン システムでパッケージの整合性チェックエラーが発生する - [#10567](https://github.com/NuGet/Home/issues/10567)

* PackagingException の代わりに FormatException が[スローされる](https://github.com/NuGet/Home/issues/10595)- #10595

* CPVM - グラフ の実行アルゴリズムでのコンカレンシーの問題 - [#10598](https://github.com/NuGet/Home/issues/10598)

* PMC PowerShell バージョンのテレメトリを追加する - [#10609](https://github.com/NuGet/Home/issues/10609)

* NuGetVersion の並べ替えパフォーマンスの向上 - [#10611](https://github.com/NuGet/Home/issues/10611)

* 信頼できる署名者の追加に一貫性のない引数があります - [#10647](https://github.com/NuGet/Home/issues/10647)

* Vs2019 v16.9.0: NuGet パッケージ マネージャー のタブを "更新プログラム" から "インストール済み" に切り替えても、フレームは更新されません。 - [#10654](https://github.com/NuGet/Home/issues/10654)

* PMUI のバージョン番号から "v" を[削除する](https://github.com/NuGet/Home/issues/10677)- #10677

* INuGetProjectService.GetInstalledPackagesAsync は、CPS プロジェクト システムの指定を受け取る前に を[スローします](https://github.com/NuGet/Home/issues/10681)- #10681

* [参照] タブの [埋め込みアイコンMicrosoft Visual Studioソースからアクセスが拒否される - [#10687](https://github.com/NuGet/Home/issues/10687)

* MSBuildProjectExtensionsPath が設定されていない場合に INuGetProjectService.GetInstalledPackagesAsync が[スローされる](https://github.com/NuGet/Home/issues/10739)- #10739

* "dotnet nuget remove source nuget.org" が初めて動作しない[-](https://github.com/NuGet/Home/issues/10745) #10745

* Nuget は、UI スレッドへの同期呼び出しを行う非同期メソッドでスレッドプール スレッドをブロックします [#10775。](https://github.com/NuGet/Home/issues/10775)

* ツール -> オプション -> NuGet パッケージ マネージャー文字列が切り捨てられる - [#10779](https://github.com/NuGet/Home/issues/10779)

* `PackageLoadContext.GetInstalledAndTransitivePackagesAsync` が実行され、パフォーマンスが低下する - [#10790](https://github.com/NuGet/Home/issues/10790)

* NuGet SDK パッケージで埋め込みアイコンを使用する - [#10795](https://github.com/NuGet/Home/issues/10795)

* SPDX ライセンス の一覧を更新する - [#10806](https://github.com/NuGet/Home/issues/10806)

**[このリリースで修正された問題の一覧 - 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**
  
**[このリリースのコミットの一覧 - 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**
  
### <a name="community-contributions"></a>コミュニティからの投稿

この NuGet リリースをすばらしいものにするのに役立ったすべての共同作成者に感謝します。

|担当者|Prs|発行|
|----|----|----|
[は、次の値を使用します。](https://github.com/louis-z) | [3991](https://github.com/NuGet/NuGet.Client/pull/3991) | VersionRange で 1 桁の範囲を解析できない - [#10342](https://github.com/NuGet/Home/issues/10342)
[omajid](https://github.com/omajid) | [3860](https://github.com/NuGet/NuGet.Client/pull/3860) | NuGet.Client build.sh 破損しています - [#10139](https://github.com/NuGet/Home/issues/10139)
[Malmal4G](https://github.com/Nirmal4G) | [3623](https://github.com/NuGet/NuGet.Client/pull/3623) | NuGet.Client build.sh 破損しています - [#10139](https://github.com/NuGet/Home/issues/10139)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | "nuget pack" のパフォーマンスは、ソース パスのレベルが上がって低下 [します。#5706](https://github.com/NuGet/Home/issues/5706)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | NuGet.exeのパフォーマンスの問題を修正しました。 相対パス - [#5016](https://github.com/NuGet/Home/issues/5016)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3940](https://github.com/NuGet/NuGet.Client/pull/3940) | CPVM - グラフ の実行アルゴリズムでのコンカレンシーの問題 - [#10598](https://github.com/NuGet/Home/issues/10598)
[(1970 年 1 月 12 月](https://github.com/josesimoes) | [3943](https://github.com/NuGet/NuGet.Client/pull/3943) | プロジェクトの種類 nfproj を Nuget CLI でサポートされているProjectExtensions の一覧に追加します。 - [#10562](https://github.com/NuGet/Home/issues/10562)

## <a name="feedback-welcome"></a>フィードバックへようこそ

お客様のフィードバックは Microsoft にとって重要です。  このリリースで問題が発生した場合は [、GitHub](https://github.com/NuGet/Home/issues) の問題と既存の問題 [Visual Studio Developer Community確認してください](https://developercommunity.visualstudio.com/) 。  NuGet 内の新しい問題については [、GitHub の問題 を報告してください](https://github.com/NuGet/Home/issues/new)。
NuGet エクスペリエンスに関する一般的な問題については、[](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)お気に入りの IDE の [問題の報告] オプションの [ヘルプ] の [問題の報告] >**お知らせください**。
