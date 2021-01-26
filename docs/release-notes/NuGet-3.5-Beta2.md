---
title: 3.5 Beta2 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.5 Beta 2 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776387"
---
# <a name="nuget-35-beta2-release-notes"></a>NuGet 3.5 Beta2 のリリースノート

[NuGet 3.5-ベータリリースノート](../release-notes/nuget-3.5-Beta.md)  | [NuGet 3.5-RC リリースノート](../release-notes/nuget-3.5-RC.md)

NuGet 3.5 Beta 2 RTM は、Visual Studio 2013 と nuget.exe に2016年6月27日にリリースされました

[完全な Changelog](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[懸案事項リスト](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>バグの修正

* 認証されたフィード用の .NET Core でのパスワード decrpytion のサポート不足に関するエラーメッセージを更新しました- [#2942](https://github.com/NuGet/Home/issues/2942)

* .NET Core プロジェクトが開いている場合、パッケージマネージャーコンソール Get-Package が失敗する [#2932](https://github.com/NuGet/Home/issues/2932)

* NuGet push コマンドでの403の不適切な処理を修正し [#2910](https://github.com/NuGet/Home/issues/2910)

* DisableSourceControlIntegration が true に設定されている場合に TFS ソース管理にバインドされているソリューションでのパッケージのアンインストールに関する問題を修正しました- [#2739](https://github.com/NuGet/Home/issues/2739)

* 対象外のパッケージを考慮するようにパッケージの更新を修正する- [#2724](https://github.com/NuGet/Home/issues/2724)

* MSBuild の詳細レベルを使用して Nuget パッケージマネージャーの UI 操作のロガーレベルを設定する- [#2705](https://github.com/NuGet/Home/issues/2705)

* Web サイトプロジェクトの NuGet 構成が無効であることを修正するエラー-VS 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)

* コンテンツファイルが含まれている場合のパックの問題を修正 `.csproj` する- [#2658](https://github.com/NuGet/Home/issues/2658)

* () の DefaultPushSource `NuGetDefaults.Config` `ProgramData\NuGet` が動作しません [#2653](https://github.com/NuGet/Home/issues/2653)

* Nuget 3.4.3 のリリースで問題を修正する-パッケージの作成時に値を null にすることはできません- [#2648](https://github.com/NuGet/Home/issues/2648)

* 復元では、VSTS フィードの Nuget.Config から格納された資格情報を使用します。 [#2647](https://github.com/NuGet/Home/issues/2647)

* パフォーマンス-バージョン comparsion で過剰な割り当てを修正するコード- [#2632](https://github.com/NuGet/Home/issues/2632)

* nuget.exe の複数のインスタンスが並列[#2628](https://github.com/NuGet/Home/issues/2628)で同じパッケージをインストールしようとしたときに発生する問題を修正します。

* パフォーマンス-複数プロジェクトの操作の依存関係情報をキャッシュする- [#2619](https://github.com/NuGet/Home/issues/2619)

* ソースリストが空のときにパッケージソースを設定から追加できない問題を修正しました- [#2617](https://github.com/NuGet/Home/issues/2617)

* デザイン時のファサードに依存するパッケージをインストールしようとすると[#2594](https://github.com/NuGet/Home/issues/2594) 、誤解を招くエラーを修正する

* "All" に設定して、パッケージを "All" に設定してパッケージをインストールすると、最初のソース[#2557](https://github.com/NuGet/Home/issues/2557)のみが試行される

* 将来 (Mono) で書き込み時間があるファイルを含むパッケージに関する問題を修正しました- [#2518](https://github.com/NuGet/Home/issues/2518)

* Update コマンドでプロジェクトの検索エラーが発生したときに例外を表示する- [#2418](https://github.com/NuGet/Home/issues/2418)

* パッケージに `.nupkg` [#2354](https://github.com/NuGet/Home/issues/2354)ファイルが含まれている場合、NoCache という引数を使用して nuget v 3.3 + フィードからパッケージをインストールすると、パッケージコンテンツが正しく復元されない

* 1つのソースからパッケージが欠落している場合に、パッケージのインストール (すべてのソース) の問題を修正しました。 [#2322](https://github.com/NuGet/Home/issues/2322)

* 1つのソースが承認に失敗した場合のインストールブロック- [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec`バージョン範囲は IncludeReferencedProjects バージョン- [#1983](https://github.com/NuGet/Home/issues/1983)をオーバーライドする必要があります

* NuGet 3.3.0 の更新が ' 追加の制約で失敗しました...packages.config で定義されているため、この操作を実行できません。 ' - [#1816](https://github.com/NuGet/Home/issues/1816)

* nuget.exe の更新では、アセンブリの厳密な名前とプライベート属性が削除されます。 - [#1778](https://github.com/NuGet/Home/issues/1778)

* "DefaultPushSource" の相対ファイルパスの問題を修正します- [#1746](https://github.com/NuGet/Home/issues/1746)

* 更新リゾルバーのエラーメッセージの改善- [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>機能と動作の変更

* nuget.exe のプッシュタイムアウトパラメーターが機能しません- [#2785](https://github.com/NuGet/Home/issues/2785)

* nuget.exe の復元で `.props` は、プロジェクトのファイルとファイルが生成されません `.targets` `.nuproj` (3.4.3.855 での回帰)- [#2711](https://github.com/NuGet/Home/issues/2711)

* フレームワークとインポート[#2633](https://github.com/NuGet/Home/issues/2633)を比較するには、機能拡張 API が必要です

* #2486 の使用時に依存関係オプションを非表示にする `project.json`  -  [](https://github.com/NuGet/Home/issues/2486)

* 詳細な出力[#1887](https://github.com/NuGet/Home/issues/1887)に nuget.exe バージョンヘッダーを出力する

* NuGet は/runtimes/{rid}/nativeassets/{txm}/のサポートを追加する必要があり [#2782](https://github.com/NuGet/Home/issues/2782)