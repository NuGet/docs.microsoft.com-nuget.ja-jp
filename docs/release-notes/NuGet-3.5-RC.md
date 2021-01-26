---
title: 3.5 RC リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.5 RC のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780206"
---
# <a name="nuget-35-rc-release-notes"></a>NuGet 3.5 RC リリースノート

[NuGet 3.5-Beta2 リリースノート](../release-notes/nuget-3.5-Beta2.md)  | [NuGet 3.5-RTM リリースノート](../release-notes/nuget-3.5-RTM.md)

3.5 リリースは、NuGet クライアントの品質とパフォーマンスを向上させることに重点を置いています。 さらに、 [フォールバックフォルダー](https://github.com/NuGet/Home/issues/2899)のサポート、およびでの [packagetype](https://github.com/NuGet/Home/issues/2476) のサポートなど、いくつかの機能を提供してい `.nuspec` ます。

[懸案事項リスト](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>バグの修正

* パッケージのインストール/復元が失敗し、"パッケージに複数のファイルが含まれています。" というエラーが表示さ `.nuspec` れます。 - [#3231](https://github.com/NuGet/Home/issues/3231)

* nuget パック `.tt` は、 [#3203](https://github.com/NuGet/Home/issues/3203)に関係なく、ファイルをコンテンツフォルダーに強制的に追加します。

* `project.json`JSON ファイル内に packOptions と owner がない場合[#3180](https://github.com/NuGet/Home/issues/3180) 、nuget pack .csproj (を含む) がクラッシュする

* の nuget パックでは `project.json` 、summary、authors、owners などの packOptions タグが無視されます。 [#3161](https://github.com/NuGet/Home/issues/3161)

* nuget パック `.nuspec` は `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)の出力の依存関係を無視します

* ロールバックを使用して複数のパッケージを更新すると、プロジェクトが破損した状態のままになります- [#3139](https://github.com/NuGet/Home/issues/3139)

* Netstandard.library プロジェクトでは、ContentFiles は追加されません- [#3118](https://github.com/NuGet/Home/issues/3118)

* .Net Standard をターゲットとするライブラリをパッケージ化できません- [#3108](https://github.com/NuGet/Home/issues/3108)

* ファイル > 新しいプロジェクト-> クラスライブラリ (ポータブル) プロジェクトが VS2015 と[#3094](https://github.com/NuGet/Home/issues/3094) Dev15 で失敗する

* NuGet エラー-1.0.0-* は有効なバージョン文字列ではありません- [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package を表示できませんが、Install-Package 動作 [#3068](https://github.com/NuGet/Home/issues/3068)

* Dev15 で "パッケージのインストール-検証" を行うとエラー [#3061](https://github.com/NuGet/Home/issues/3061)が発生する

* NuGet バージョンを使用する VS で VS 2015 update 3 をインストールすると3.5.0 エラーが発生する- [#3053](https://github.com/NuGet/Home/issues/3053)

* パッケージマネージャー UI: パッケージを更新した後、新しいバージョンは表示されません- [#3041](https://github.com/NuGet/Home/issues/3041)

* -Delete コマンドラインの ApiKey は3.5.0 で読み取り/送信されません- [#3037](https://github.com/NuGet/Home/issues/3037)

* 文字列が正しくありません: パッケージの安定したリリースでは、プレリリースの依存関係を設定することはできません。 - [#3030](https://github.com/NuGet/Home/issues/3030)

* PCL (net46 および windows 10) プロジェクトを作成すると、NullRef 例外が生成されます。 - [#3014](https://github.com/NuGet/Home/issues/3014)

* 新しいバージョンが allowedVersions 制約によって制限されている場合、Nuget 更新プログラムは情報メッセージを提供する必要があり [#3013](https://github.com/NuGet/Home/issues/3013)

* 複数の[#2885](https://github.com/NuGet/Home/issues/2885)ソースで資格情報プロバイダーを使用しているときに、資格情報プラグインがエラーで終了しました-1/エラーが発生したパッケージのダウンロード中

* nuget pack-パッケージの依存関係に Newtonsoft.Jsがありません- [#2876](https://github.com/NuGet/Home/issues/2876)

* Linux/MacOS + Mono [#2860](https://github.com/NuGet/Home/issues/2860)での ExecuteSynchronizedCore のバグ

* VS は repositoryPath の環境変数をサポートしていません (nuget.exe)- [#2763](https://github.com/NuGet/Home/issues/2763)

* アクセシビリティの問題を修正する- [#2745](https://github.com/NuGet/Home/issues/2745)

* ハイフネーションされたプロファイルを含むポータブルフレームワークは拒否されます。 - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet パッケージマネージャーは、[パッケージの詳細] のオプション一覧が適用されないことを明確にする必要があり `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* NuGet 3.3.0 の更新が ' 追加の制約で失敗しました...packages.config で定義されているため、この操作を実行できません。 ' - [#1816](https://github.com/NuGet/Home/issues/1816)

* 存在しないローカルソースからパッケージをインストールすると、偽のメッセージ[#1674](https://github.com/NuGet/Home/issues/1674)がスローされる

* "Upgrade v)" フィルターに[#1094](https://github.com/NuGet/Home/issues/1094)より、バージョンの制約に違反するアップグレードが表示されます。

## <a name="performance-improvements"></a>パフォーマンスの強化

* パフォーマンス: ContentModel ターゲットフレームワークの解析の向上- [#3162](https://github.com/NuGet/Home/issues/3162)

* パフォーマンス: `runtime.json` rid [#3150](https://github.com/NuGet/Home/issues/3150)を持たない復元用のファイルを読み取らないようにします。 CI マシンでは、サンプル ASP.NET Web アプリケーションの復元が15秒から3秒に短縮されました。

* パフォーマンス: パッケージマネージャーコンソール init.ps1 読み込み時間 [#2956](https://github.com/NuGet/Home/issues/2956)です。 場合によっては、132s から 10 PackageManagerConsole までの時間が短縮されます。

* NuGet 更新プログラム [#3044](https://github.com/NuGet/Home/issues/3044)でのパフォーマンスに関する問題の解決: サンプルプロジェクトでは、パッケージのインストールに要した時間が14秒から1分に短縮されました。

## <a name="dcrs"></a>DCR

* NuGet では、dotnet tfm ベースの PCL でのアップグレードまたはインストールによって問題が発生する可能性があることをユーザーに知らせる必要があり [#3138](https://github.com/NuGet/Home/issues/3138)

* [プロジェクトに対して無効なインストール/アップグレードを警告する]: "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* Netcoreapp11 と netstandard17 のサポートを追加する- [#2998](https://github.com/NuGet/Home/issues/2998)

* nuget.exe [#2934](https://github.com/NuGet/Home/issues/2934)で NuGet-Warning ヘッダーの内容をコンソールに出力する

* トークンの置換に AssemblyMetadata 属性を利用する `.nuspec` - [#2851](https://github.com/NuGet/Home/issues/2851)

* ロックファイルからロックされたプロパティを削除し [#2379](https://github.com/NuGet/Home/issues/2379)

* シンボルパッケージは、インストールまたは更新では使用しないでください #2807

## <a name="features"></a>特徴

* フォールバックパッケージフォルダーのサポート- [#2899](https://github.com/NuGet/Home/issues/2899)

* ツールパッケージをサポートするためのパッケージの種類の概念を設計および実装する- [#2476](https://github.com/NuGet/Home/issues/2476)

* グローバルパッケージフォルダーへのパスを取得するための API- [#2403](https://github.com/NuGet/Home/issues/2403)

* ネイティブパッケージの更新サポート- [#1291](https://github.com/NuGet/Home/issues/1291)
