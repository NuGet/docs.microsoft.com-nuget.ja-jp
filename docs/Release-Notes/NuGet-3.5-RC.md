---
title: "3.5 RC のリリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 3.5 RC のリリース ノートします。"
keywords: "NuGet 3.5 RC のリリース ノート、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fdb84da5f1648ce4508afe6ddcf04bddd41284d3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-35-rc-release-notes"></a>NuGet 3.5 RC のリリース ノートには

[NuGet 3.5 Beta2 リリース ノート](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM リリース ノート](../release-notes/nuget-3.5-RTM.md)

3.5 インチのリリースは NuGet クライアントの品質および性能を向上させることに重点を置きます。 さらにのサポートなど、いくつかの機能が出荷された[フォールバック フォルダー](https://github.com/NuGet/Home/issues/2899)、 [PackageType](https://github.com/NuGet/Home/issues/2476)でサポート`.nuspec`などです。

[懸案事項リスト](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5 RC")

## <a name="bug-fixes"></a>バグ修正

* パッケージのインストール/復元が失敗"パッケージが複数含まれている`.nuspec`ファイルです"。 - [#3231](https://github.com/NuGet/Home/issues/3231)

* nuget パックを強制的に追加`.tt`ファイルをコンテンツ フォルダーの内容に関係なく[#3203](https://github.com/NuGet/Home/issues/3203)

* nuget パック csproj (で`project.json`) packOptions と JSON ファイルの所有者が存在しない場合のクラッシュ[#3180](https://github.com/NuGet/Home/issues/3180)

* 用の nuget パック`project.json`概要、作成者、所有者などのような packOptions タグは無視[#3161](https://github.com/NuGet/Home/issues/3161)

* 出力内の依存関係が nuget パックには無視されます`.nuspec`の`project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* ロールバックを含む複数のパッケージの更新結果が、プロジェクト、破損状態 - [#3139](https://github.com/NuGet/Home/issues/3139)

* Netstandard プロジェクトのいずれかの下にあるコンテンツ ファイルは追加されません[#3118](https://github.com/NuGet/Home/issues/3118)

* ターゲットを .Net ライブラリをパッケージすることはできません標準正しく - [#3108](https://github.com/NuGet/Home/issues/3108)

* ファイルに新しいプロジェクト]-> [クラス ライブラリ (ポータブル) プロジェクトが失敗する VS2015 と Dev15 - -> [#3094](https://github.com/NuGet/Home/issues/3094)

* NuGet エラー - 1.0.0-* は有効なバージョン文字列ではありません[#3070。](https://github.com/NuGet/Home/issues/3070)

* 表示、パッケージのインストールの動作の失敗した Find-package [#3068](https://github.com/NuGet/Home/issues/3068)

* エラー時"Install-package jquery.validation"dev15 -  [#3061](https://github.com/NuGet/Home/issues/3061)

* VS 2015 がインストールされているバージョン 3.5.0 エラーが発生した、NuGet を使用すると上の 3 を更新するときに[#3053](https://github.com/NuGet/Home/issues/3053)

* パッケージ マネージャーの UI: パッケージを更新した後に新しいバージョンが表示されない- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey delete コマンド ラインでは、読み取り/に送信されない 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* 不適切な文字列: 安定したパッケージのリリースのプレリリースの依存関係のないです。 - [#3030](https://github.com/NuGet/Home/issues/3030)

* PCL (net46 および windows 10) プロジェクト get NullRef 例外を作成します。 - [#3014](https://github.com/NuGet/Home/issues/3014)

* AllowedVersions 制約 - によってより新しいバージョンが制限されているときに、Nuget の更新プログラムは情報メッセージを提供する必要があります[#3013](https://github.com/NuGet/Home/issues/3013)

* 資格情報のプラグインは、エラー-1 で終了しましたエラーをダウンロードする、複数のソースの資格情報プロバイダーを使用する場合にパッケージ化/ [#2885。](https://github.com/NuGet/Home/issues/2885)

* nuget パック パッケージ依存関係がありません Newtonsoft.Json - [#2876](https://github.com/NuGet/Home/issues/2876)

* Linux/MacOS + モノラル - ExecuteSynchronizedCore でバグ[#2860](https://github.com/NuGet/Home/issues/2860)

* VS が repositoryPath 内の環境変数をサポートしていません (nuget.exe は) - [#2763](https://github.com/NuGet/Home/issues/2763)

* ユーザー補助の問題を修正[#2745](https://github.com/NuGet/Home/issues/2745)

* ハイフンでつながれたプロファイルでポータブル フレームワークは拒否されます。 - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet パッケージ マネージャーで、詳細には適用されませんパッケージでそのオプションの一覧を明確にするため必要があります`project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* NuGet 3.3.0 更新で失敗 ' 追加の制約 で定義されている packages.config には、この動作ができなくなります '。 - [#1816](https://github.com/NuGet/Home/issues/1816)

* 無効なメッセージのスローを存在しないローカル ソースからパッケージをインストールする[#1674](https://github.com/NuGet/Home/issues/1674)

* 「アップグレード」使用できるフィルターは、表示のバージョンの制約に違反するアップグレード[#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>パフォーマンスの向上

* パフォーマンス: 向上 ContentModel ターゲット フレームワークの解析中に[#3162](https://github.com/NuGet/Home/issues/3162)

* パフォーマンス: 読み取りを回避する`runtime.json`の Rid がない復元ファイル[#3150](https://github.com/NuGet/Home/issues/3150)です。 CI のマシンでは、ASP.NET Web アプリケーションが 3 秒を 15 秒以上削減サンプルの復元します。

* パフォーマンス: パッケージ マネージャー コンソール init.ps1 読み込み時[#2956](https://github.com/NuGet/Home/issues/2956)です。 場合によっては 132s から 10 件に PackageManagerConsole を開くに時間が向上しました。

* NuGet の更新プログラム - ReSharper パフォーマンスの問題を解決[#3044](https://github.com/NuGet/Home/issues/3044): サンプルのプロジェクトはパッケージをインストールするのにかかる時間が 140s から 68s に短縮します。

## <a name="dcrs"></a>DCR

* NuGet は、ユーザーがいるベース dotnet tfm でアップグレード/インストール PCL に問題が発生の通知する必要があります[#3138](https://github.com/NuGet/Home/issues/3138)

* Tfm を使用したプロジェクトの不適切なインストールまたはアップグレードに警告する ="dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* Netcoreapp11 と netstandard17 サポート - 追加[#2998](https://github.com/NuGet/Home/issues/2998)

* Nuget.exe - でコンソールに NuGet 警告ヘッダーの内容を印刷[#2934](https://github.com/NuGet/Home/issues/2934)

* 活用 AssemblyMetadata 属性`.nuspec`トークンの置換 - [#2851](https://github.com/NuGet/Home/issues/2851)

* ロックされているプロパティ ファイルから削除、ロックの[#2379](https://github.com/NuGet/Home/issues/2379)

* シンボル パッケージのインストールでこれまで使用しないでまたは #2807 の更新

## <a name="features"></a>フィーチャー

* -フォールバック パッケージ フォルダーへのサポート[#2899](https://github.com/NuGet/Home/issues/2899)

* 設計およびツール パッケージをサポートするには、パッケージの種類の概念を実装[#2476](https://github.com/NuGet/Home/issues/2476)

* グローバル パッケージ フォルダーへのパスを取得する API [#2403](https://github.com/NuGet/Home/issues/2403)

* ネイティブなパッケージ更新のサポート - [#1291](https://github.com/NuGet/Home/issues/1291)
