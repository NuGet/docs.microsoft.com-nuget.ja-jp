---
title: "3.5 Beta2 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0b76064f-0607-438a-bbf8-dd862690f48e
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 3.5 Beta 2 をリリース ノートです。"
keywords: "NuGet 3.5 Beta 2 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6dd388e52308d2f3cd32d4d6c66c2868f0ae2a41
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="35-beta2-release-notes"></a>3.5 Beta2 リリース ノート

[NuGet 3.5 ベータ リリース ノート](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC のリリース ノート](../release-notes/nuget-3.5-RC.md)

Visual Studio 2013 と nuget.exe 用、2016 年 6 月 27 日にリリースされた NuGet 3.5 Beta 2 RTM

[すべての変更ログ](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[懸案事項の一覧](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

# <a name="notable-changes"></a>主な変更点

## <a name="bug-fixes"></a>バグ修正

* 最新のエラー メッセージの認証されたフィードは、.NET Core でのパスワード decrpytion のサポートの不足が[#2942](https://github.com/NuGet/Home/issues/2942)

* パッケージ マネージャー コンソール Get-パッケージが失敗する .NET Core プロジェクトを開く - [#2932](https://github.com/NuGet/Home/issues/2932)

* NuGet プッシュ コマンドで 403 が不適切に処理を修正[#2910](https://github.com/NuGet/Home/issues/2910)

* DisableSourceControlIntegration が設定されている場合は、TFS ソース管理にバインドされているソリューション内のパッケージのアンインストールで問題を修正 true - [#2739](https://github.com/NuGet/Home/issues/2739)

* アカウントのターゲットではないパッケージ - を考慮するパッケージの更新の修正[#2724](https://github.com/NuGet/Home/issues/2724)

* レベルを設定するロガー Nuget パッケージ マネージャーの UI アクションの MSBuild の詳細レベルを使用して[#2705](https://github.com/NuGet/Home/issues/2705)

* 修正プログラムの NuGet 構成が無効な web サイト プロジェクトの VS 2015 VSIX (v3.4.3) - エラー [#2667](https://github.com/NuGet/Home/issues/2667)

* パックに関する問題を修正`.csproj`コンテンツ ファイルが含まれています - とき[#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) は機能しません - [#2653](https://github.com/NuGet/Home/issues/2653)

* 値をパッケージの作成時に null にすることはできません - Nuget 3.4.3 リリースで問題を解決[#2648](https://github.com/NuGet/Home/issues/2648)

* 復元は Nuget.Config から保存された資格情報を使用して VSTS フィード - [#2647](https://github.com/NuGet/Home/issues/2647)

* パフォーマンス - バージョンの比較コード内の修正プログラムの過剰な割り当て - [#2632](https://github.com/NuGet/Home/issues/2632)

* Nuget.exe の複数のインスタンスが並列 - 同じパッケージをインストールしようとするときの問題を修正[#2628](https://github.com/NuGet/Home/issues/2628)

* パフォーマンス - 複数のプロジェクトの操作の依存関係情報をキャッシュ - [#2619](https://github.com/NuGet/Home/issues/2619)

* 問題を修正パッケージのソースは追加設定から基になるリストが空のときに、 [#2617](https://github.com/NuGet/Home/issues/2617)

* デザイン時のファサード - に依存しているパッケージをインストールしようとするときは、誤解を招きやすいエラーを修正する[#2594](https://github.com/NuGet/Home/issues/2594)

* だけ最初のソースの設定"All"PackageManager コンソールから、パッケージをインストールしようと[#2557](https://github.com/NuGet/Home/issues/2557)

* (モノラル) - 書き込みの際、将来にファイルがパッケージの問題が修正[#2518](https://github.com/NuGet/Home/issues/2518)

* 障害が発生、検索するプロジェクトの更新のコマンドでは、例外を表示[#2418](https://github.com/NuGet/Home/issues/2418)

* 引数でフィード nuget v3.3 + からパッケージをインストールするときにパッケージの内容は正しく復元されません - NoCache パッケージが含まれている`.nupkg`ファイル - [#2354](https://github.com/NuGet/Home/issues/2354)

* -1 つのソースからパッケージが見つからない場合に、パッケージに問題を修正プログラムが (すべてのソース) をインストール[#2322](https://github.com/NuGet/Home/issues/2322)

* 1 つのソースの承認に失敗した場合は、ブロックをインストール[#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec`バージョン範囲は-IncludeReferencedProjects バージョン - をオーバーライドする必要があります[#1983](https://github.com/NuGet/Home/issues/1983)

* NuGet 3.3.0 更新で失敗 ' 追加の制約 で定義されている packages.config には、この動作ができなくなります '。 - [#1816](https://github.com/NuGet/Home/issues/1816)

* nuget.exe の更新プログラムは、アセンブリの厳密な名前およびプライベートの属性を削除します。 - [#1778](https://github.com/NuGet/Home/issues/1778)

* "DefaultPushSource"- の相対ファイル パスの問題が修正[#1746](https://github.com/NuGet/Home/issues/1746)

* 更新の競合回避モジュール エラー メッセージを向上させる[#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>機能および動作変更

* nuget.exe プッシュ タイムアウト パラメーターは機能しません - [#2785](https://github.com/NuGet/Home/issues/2785)

* nuget.exe restore を生成しない`.props`と`.targets`ファイル`.nuproj`プロジェクト (v3.4.3.855 の回帰) - [#2711](https://github.com/NuGet/Home/issues/2711)

* 機能拡張 API フレームワークでのインポートとを比較する必要がある[#2633](https://github.com/NuGet/Home/issues/2633)

* 使用する場合は、依存関係のオプションを非表示に`project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* 詳細な出力に nuget.exe バージョン ヘッダーを印刷[#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet は、{rid}/runtimes//nativeassets/{txm} のサポートを追加する必要があります/- [#2782](https://github.com/NuGet/Home/issues/2782)