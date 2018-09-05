---
title: 3.5 beta 2 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 3.5 Beta 2 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b47939e2fafc11823c41a849b3c58bbf0800ada
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551992"
---
# <a name="nuget-35-beta2-release-notes"></a>NuGet 3.5 beta 2 リリース ノートします。

[NuGet 3.5 のベータ リリース ノート](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC リリース ノート](../release-notes/nuget-3.5-RC.md)

用と nuget.exe の Visual Studio 2013、2016 年 6 月 27 日にリリースされた NuGet 3.5 Beta 2 の RTM

[完全な変更ログ](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[懸案事項リスト](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>バグ修正

* 更新されたエラー メッセージの認証されたフィード - .NET Core でのパスワード decrpytion のサポートの不足を[#2942](https://github.com/NuGet/Home/issues/2942)

* パッケージ マネージャー コンソール Get-パッケージが失敗する場合は、.NET Core プロジェクトを開く - [#2932](https://github.com/NuGet/Home/issues/2932)

* NuGet push コマンドで 403 が不適切に処理を修正[#2910](https://github.com/NuGet/Home/issues/2910)

* DisableSourceControlIntegration が設定されている場合は、TFS ソース管理にバインドされているソリューション内のパッケージのアンインストールで問題を修正する true - [#2739](https://github.com/NuGet/Home/issues/2739)

* アカウントのターゲット以外パッケージ - を考慮するパッケージの更新の修正[#2724](https://github.com/NuGet/Home/issues/2724)

* MSBuild の詳細レベルを使用して UI アクションの Nuget パッケージ マネージャーのログ レベルを設定する[#2705](https://github.com/NuGet/Home/issues/2705)

* NuGet の構成の修正プログラムは、web サイト プロジェクトの VS 2015 VSIX (v3.4.3) - で無効なエラー [#2667](https://github.com/NuGet/Home/issues/2667)

* パックに関する問題を修正`.csproj`コンテンツ ファイルが含まれています - とき[#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) が動作しない - [#2653](https://github.com/NuGet/Home/issues/2653)

* 値をパッケージの作成時に null にすることはできません - Nuget 3.4.3 リリースで問題を解決[#2648](https://github.com/NuGet/Home/issues/2648)

* 復元は Nuget.Config から保存された資格情報を使用して VSTS フィード - [#2647](https://github.com/NuGet/Home/issues/2647)

* パフォーマンス - 内のバージョンの比較コード修正の過剰な割り当て - [#2632](https://github.com/NuGet/Home/issues/2632)

* Nuget.exe の複数のインスタンスが、並列 - 同じパッケージをインストールしようとしています問題を修正[#2628。](https://github.com/NuGet/Home/issues/2628)

* パフォーマンスのマルチ プロジェクトの操作の依存関係情報をキャッシュ - [#2619](https://github.com/NuGet/Home/issues/2619)

* 問題を修正するソースのリストが空の場合に、パッケージ ソースというが設定から追加する場所[#2617](https://github.com/NuGet/Home/issues/2617)

* デザイン時のファサードに依存するパッケージをインストールするときに、誤解を招きやすいエラーを修正する[#2594](https://github.com/NuGet/Home/issues/2594)

* のみ最初のソース -"All"の設定で PackageManager コンソールからパッケージをインストールしようと[#2557](https://github.com/NuGet/Home/issues/2557)

* 書き込み時間が、将来の (Mono) - ファイルのパッケージに関する問題を解決[#2518](https://github.com/NuGet/Home/issues/2518)

* 障害が発生した検索のプロジェクトで update コマンドの場合に表示される例外[#2418](https://github.com/NuGet/Home/issues/2418)

* 引数でフィードから nuget v3.3 以降、パッケージをインストールするときにパッケージのコンテンツは正しく復元されません、パッケージが含まれている場合 - NoCache`.nupkg`ファイル - [#2354](https://github.com/NuGet/Home/issues/2354)

* パッケージに問題を修正プログラムが - 1 つのソースからパッケージが見つからない場合に、(すべてのソース) をインストール[#2322](https://github.com/NuGet/Home/issues/2322)

* 1 つのソース - 承認に失敗した場合は、ブロックをインストール[#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` バージョン範囲は-IncludeReferencedProjects バージョン - をオーバーライドする必要があります[#1983](https://github.com/NuGet/Home/issues/1983)

* NuGet 3.3.0 更新が失敗 '... 制約で定義されている packages.config には、この動作ができなくなります '。 - [#1816](https://github.com/NuGet/Home/issues/1816)

* nuget.exe の更新プログラムは、アセンブリの厳密な名前とプライベートの属性を削除します。 - [#1778](https://github.com/NuGet/Home/issues/1778)

* "DefaultPushSource"- の相対ファイル パスの問題が修正[#1746](https://github.com/NuGet/Home/issues/1746)

* 更新競合回避モジュールのエラー メッセージの改善[#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>機能および動作変更

* nuget.exe プッシュのタイムアウト パラメーターは機能しません - [#2785](https://github.com/NuGet/Home/issues/2785)

* nuget.exe の復元を生成しない`.props`と`.targets`ファイル`.nuproj`プロジェクト (v3.4.3.855 の回帰) - [#2711](https://github.com/NuGet/Home/issues/2711)

* 機能拡張 API フレームワークの imports とを比較する必要がある[#2633](https://github.com/NuGet/Home/issues/2633)

* 使用する場合は、依存関係のオプションを非表示に`project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* 詳細な出力 - で nuget.exe のバージョン ヘッダーを印刷[#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet は、{rid}/runtimes//nativeassets/{txm} のサポートを追加する必要があります、- [#2782](https://github.com/NuGet/Home/issues/2782)