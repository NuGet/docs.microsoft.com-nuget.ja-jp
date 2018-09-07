---
title: NuGet 4.6 RTM リリース ノート
description: NuGet 4.6.0 のリリース ノートであり、既知の問題、バグ修正、追加機能、および DCR が含まれています。
author: anangaur
ms.author: anangaur
ms.date: 3/7/2018
ms.topic: conceptual
ms.openlocfilehash: 3c71d05144aa2b92b916d4ebf319c5a4e321581f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549845"
---
# <a name="nuget-46-rtm-release-notes"></a>NuGet 4.6 RTM リリース ノート

[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) には、[NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe) が付属しています。

## <a name="summary-whats-new-in-this-release"></a>概要: このリリースの新機能

* [パッケージの署名](../create-packages/sign-a-package.md)のサポートが追加されました。
* Visual Studio 2017 と nuget.exe では、[署名済みパッケージ](../reference/signed-packages-reference.md)について、パッケージをインストール、復元する前にパッケージの整合性を検証できるようになりました。
* 連続する復元のパフォーマンスが向上しました。

## <a name="known-issues"></a>既知の問題

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>.NET Framework と NuGet での .NET Standard 2.0 の問題 

.NET Standard とそのツールは、.NET Framework 4.6.1 をターゲットとするプロジェクトが、.NET Standard 2.0 以前をターゲットとする NuGet パッケージおよびプロジェクトを使用できるように設計されています。 [このドキュメント](https://github.com/dotnet/standard/issues/481)では、そのシナリオに関連する問題の概要、それらの問題を解決する計画、そのツールの今日の状態で展開できる解決策について説明します。

## <a name="top-issues-fixed-in-this-release"></a>このリリースで修正された主な問題

**パフォーマンスの改善**

* 変更がない場合に資産ファイルを書き込まない - [#6491](https://github.com/NuGet/Home/issues/6491)
* 子プロジェクトの TFM が親プロジェクトの TFM と一致しない場合、復元によって追加の MSBuild 評価が発生する - [#6311](https://github.com/NuGet/Home/issues/6311)
* 依存関係グラフ仕様の作成を最適化することで NoOp 復元のパフォーマンスを向上する - [#6252](https://github.com/NuGet/Home/issues/6252)

**バグ**

* ローカル フォルダーにプッシュすると、nupkg がロックされたままになる - [#6325](https://github.com/NuGet/Home/issues/6325)
* NuGet プラグインの実装: 複数の問題 - [#6149](https://github.com/NuGet/Home/issues/6149)
* UIHang - VSSolutionManager の MEF の初期化からクエリ サービス呼び出しを削除する - [#6110](https://github.com/NuGet/Home/issues/6110)
* 取り消されたパッケージ ダウンロード タスクのエラー報告の例外 - [#6096](https://github.com/NuGet/Home/issues/6096)
* NuGet.exe がアセンブリ名の '+' を '%2B' に置換する - [#5956](https://github.com/NuGet/Home/issues/5956)
* F1 キーを押しても PM UI とコンソールの正しいヘルプ ページが表示されない - [#5912](https://github.com/NuGet/Home/issues/5912)
* 特定の状況下で VS NuGet が絶対パスをプロジェクト ファイルに書き込む - [#5888](https://github.com/NuGet/Home/issues/5888)
* 4.3 の回帰を修正 - 変換で contentfile 内のプレースホルダー $product$ と $AssemblyGuid$ が置換されない - [#5880](https://github.com/NuGet/Home/issues/5880)
* ソースが複数ある dotnet restore がクラッシュする - [#5817](https://github.com/NuGet/Home/issues/5817)
* git のバージョン管理を使用するにはパックでプロジェクトのバージョンを再評価する必要がある - [#4790](https://github.com/NuGet/Home/issues/4790)
* 互換性のないパッケージをインストールした場合のわかりづらいエラーを改善 - [#4555](https://github.com/NuGet/Home/issues/4555)
* TemplateWizard のオプションで、パッケージを PackageReferences としてインストールする必要がある - [#4549](https://github.com/NuGet/Home/issues/4549)
* MSBuild.exe が開発者コマンド プロンプト以外から実行された場合にパッケージ配信されたプロパティ ファイルが無視される - [#4530](https://github.com/NuGet/Home/issues/4530)
* プロジェクトに適用されない .NET Standard ライブラリを参照する場合のわかりづらいエラー メッセージを修正 - [#4423](https://github.com/NuGet/Home/issues/4423)
* ポータブル プロファイルをターゲットとするパッケージの dotnet add package が失敗し、ほとんどガイダンスが表示されない - [#4349](https://github.com/NuGet/Home/issues/4349)
* dotnet pack - ProjectReference にバージョンのサフィックスがない - [#4337](https://github.com/NuGet/Home/issues/4337)
* .NET Core テンプレートのビルド エラーと VS のクラッシュ - [#3973](https://github.com/NuGet/Home/issues/3973)
* ソースの https:* のサービス インデックスを読み込むことができない - [#3681](https://github.com/NuGet/Home/issues/3681)
* nuget.exe list -allversions が動作しない - [#3441](https://github.com/NuGet/Home/issues/3441)
* 誤解を招く依存関係解決のエラー メッセージ - [#2984](https://github.com/NuGet/Home/issues/2984)
* nuget.exe の復元で .msbuildproj の .props および .targets ファイルが生成されない (v3.3.0-3.4.4 アップグレードの回帰) - [#2921](https://github.com/NuGet/Home/issues/2921)
* XAML ファイルを開いた状態で NuGet パッケージを更新するときに UI に遅延が生じる - [#2878](https://github.com/NuGet/Home/issues/2878)
* パスに不適切な文字があると、IIS の WebSite プロジェクトが失敗する - [#2798](https://github.com/NuGet/Home/issues/2798)
* CentOS 上で nuget add がハングする - [#2708](https://github.com/NuGet/Home/issues/2708)
* json.net の場合、packagesavemode -nupkg を使用した復元が失敗する - [#2706](https://github.com/NuGet/Home/issues/2706)
* restore コマンドの vs 出力ウィンドウでパッケージ マネージャー フィルターを使用できない - [#2704](https://github.com/NuGet/Home/issues/2704)

[このリリースで修正されたすべての問題一覧](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
