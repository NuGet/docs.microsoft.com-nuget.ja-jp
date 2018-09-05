---
title: 3.5 RC リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 3.5 RC のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548539"
---
# <a name="nuget-35-rc-release-notes"></a>NuGet 3.5 RC リリース ノートします。

[NuGet 3.5 beta 2 リリース ノート](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM リリース ノート](../release-notes/nuget-3.5-RTM.md)

3.5 のリリースは NuGet クライアントの品質およびパフォーマンスの向上に重点を置いています。 さらになどのサポートのいくつかの機能が出荷された[Fallback フォルダー](https://github.com/NuGet/Home/issues/2899)、 [PackageType](https://github.com/NuGet/Home/issues/2476)サポート`.nuspec`など。

[懸案事項リスト](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>バグ修正

* パッケージのインストール/復元が失敗した"パッケージが複数含まれている`.nuspec`ファイル"。 - [#3231](https://github.com/NuGet/Home/issues/3231)

* nuget パックを強制的に追加します`.tt`- 何であってもコンテンツのフォルダーにファイルを[#3203](https://github.com/NuGet/Home/issues/3203)

* nuget パック csproj (で`project.json`) packOptions と JSON ファイルの所有者がない場合のクラッシュ[#3180](https://github.com/NuGet/Home/issues/3180)

* 用の nuget パック`project.json`概要、作成者、所有者などのような packOptions タグは無視[#3161](https://github.com/NuGet/Home/issues/3161)

* 出力内の依存関係を無視する nuget の pack`.nuspec`の`project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* プロジェクトの破損した状態のままロールバックを含む複数のパッケージを更新[#3139](https://github.com/NuGet/Home/issues/3139)

* いずれかの ContentFiles は netstandard プロジェクトには追加されません[#3118](https://github.com/NuGet/Home/issues/3118)

* .Net をターゲットとするライブラリをパッケージ化できません標準- [#3108](https://github.com/NuGet/Home/issues/3108)

* ファイルに新しいプロジェクト]-> [VS2015 で Dev15 - クラス ライブラリ (ポータブル) プロジェクトの失敗]-> [ [#3094](https://github.com/NuGet/Home/issues/3094)

* NuGet エラー - 1.0.0-* が有効なバージョン文字列のではない[#3070](https://github.com/NuGet/Home/issues/3070)

* 表示が、インストール パッケージの機能の検索パッケージが失敗する[#3068](https://github.com/NuGet/Home/issues/3068)

* エラー時に - dev15 で"Install-package jquery.validation" [#3061](https://github.com/NuGet/Home/issues/3061)

* VS 2015 がインストールされている 3 バージョン 3.5.0 のエラーが発生した、NuGet を使用して VS を更新するときに[#3053](https://github.com/NuGet/Home/issues/3053)

* パッケージ マネージャー UI: パッケージの更新後に新しいバージョンが表示されません- [#3041](https://github.com/NuGet/Home/issues/3041)

* -Apikey コマンド行の削除が読み取り/で送信されない 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* 文字列が正しくありません。 プレリリースの依存関係のパッケージの安定したリリースはありません。 - [#3030](https://github.com/NuGet/Home/issues/3030)

* PCL (net46 および windows 10) プロジェクト get NullRef 例外を作成します。 - [#3014](https://github.com/NuGet/Home/issues/3014)

* AllowedVersions 制約 - によって新しいバージョンが制限されていると、Nuget の更新プログラムは情報メッセージを提供する必要があります[#3013](https://github.com/NuGet/Home/issues/3013)

* 資格情報プラグインが-1 のエラーで終了しました]、[複数のソースの資格情報プロバイダーを使用する場合にパッケージをダウンロード中にエラー [#2885](https://github.com/NuGet/Home/issues/2885)

* nuget パック - 不足している Newtonsoft.Json パッケージの依存関係 - [#2876](https://github.com/NuGet/Home/issues/2876)

* ExecuteSynchronizedCore Linux/macos + - Mono 上でバグ[#2860](https://github.com/NuGet/Home/issues/2860)

* VS が repositoryPath 内の環境変数をサポートしていません (nuget.exe が) - [#2763](https://github.com/NuGet/Home/issues/2763)

* アクセシビリティの問題を修正[#2745](https://github.com/NuGet/Home/issues/2745)

* ハイフンでつながれたプロファイルを使用した移植可能なフレームワークは拒否されます。 - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet パッケージ マネージャーで、そのオプションの一覧でパッケージの詳細には適用されませんを明確にするため必要があります`project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* NuGet 3.3.0 更新が失敗 '... 制約で定義されている packages.config には、この動作ができなくなります '。 - [#1816](https://github.com/NuGet/Home/issues/1816)

* 無効なメッセージがスローされますが存在しないローカル ソースからパッケージをインストールする[#1674](https://github.com/NuGet/Home/issues/1674)

* 「少ないアップグレード」フィルターはバージョン制約に違反するアップグレードでは、表示[#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>パフォーマンスの向上

* : パフォーマンス contentmodel はターゲット フレームワークの解析のを向上させる[#3162](https://github.com/NuGet/Home/issues/3162)

* パフォーマンス: 読み取りを回避する`runtime.json`の Rid がない復元ファイル[#3150](https://github.com/NuGet/Home/issues/3150)します。 CI マシンでの ASP.NET Web アプリケーションが 3 秒を 15 秒から短縮サンプルを復元します。

* パフォーマンス: パッケージ マネージャー コンソール init.ps1 読み込み時間[#2956](https://github.com/NuGet/Home/issues/2956)します。 よって 132s から 10 件に PackageManagerConsole を開こうとする時間が向上しました。

* NuGet の更新 - ReSharper パフォーマンスの問題を解決[#3044](https://github.com/NuGet/Home/issues/3044): サンプル プロジェクトはパッケージのインストールにかかる時間が 140s から 68s に縮小します。

## <a name="dcrs"></a>DCR

* NuGet は、ベース dotnet tfm でアップグレード/インストール PCL の問題が生じたり - ユーザーに通知する必要があります[#3138](https://github.com/NuGet/Home/issues/3138)

* Tfm を使用したプロジェクトの不適切なインストールまたはアップグレードを警告する ="dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* 追加 netcoreapp11 と netstandard17 サポート - [#2998](https://github.com/NuGet/Home/issues/2998)

* Nuget.exe - で、コンソールへの NuGet 警告ヘッダーの内容を印刷[#2934](https://github.com/NuGet/Home/issues/2934)

* 利用して AssemblyMetadata 属性`.nuspec`トークンの置換 - [#2851](https://github.com/NuGet/Home/issues/2851)

* ロックされているプロパティはロック ファイルから削除[#2379](https://github.com/NuGet/Home/issues/2379)

* シンボル パッケージはこれまで使用できませんのインストールまたは #2807 の更新

## <a name="features"></a>フィーチャー

* フォールバックのパッケージ フォルダー - サポート[#2899](https://github.com/NuGet/Home/issues/2899)

* 設計および実装ツール パッケージをサポートするには、パッケージの種類の概念[#2476](https://github.com/NuGet/Home/issues/2476)

* API へのグローバル パッケージ フォルダーのパスを取得する[#2403](https://github.com/NuGet/Home/issues/2403)

* ネイティブ パッケージの更新のサポート - [#1291](https://github.com/NuGet/Home/issues/1291)
