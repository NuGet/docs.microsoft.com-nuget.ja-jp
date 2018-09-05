---
title: NuGet 1.0 および 1.1 のリリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 1.1 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6222a996f2fdcaaa81a1b16d1c6da2749936712a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547022"
---
# <a name="nuget-10-and-11-release-notes"></a>NuGet 1.0 および 1.1 のリリース ノート

[NuGet 1.2 リリース ノート](../release-notes/nuget-1.2.md)

NuGet 1.0 は、2011 年 1 月 13 日にリリースされました。  NuGet 1.1 は、2011 年 2 月 12 日にリリースされました。

## <a name="overview"></a>概要

このドキュメントには、NuGet 1.0 の主要なプレビュー リリース別にグループ化のさまざまなリリースのリリース ノートが含まれています。

NuGet には、次のコンポーネントが含まれています。

* *NuGet.Tools.vsix* * から構成されます。
  * **ライブラリのパッケージ ダイアログ ボックスを追加*** を参照してパッケージをインストールするために使用する Visual Studio 内のダイアログ。
  * **パッケージ マネージャー コンソール*** Powershell ベースの Visual Studio 内でのコンソールです。
* *NuGet コマンド ライン ツール** ツール パッケージを作成する (および最終的に発行) を使用します。

NuGet ツール Visual Studio 拡張機能 (*NuGet.Tools.vsix*) が必要です。

* Visual Studio 2010 または Visual Web Developer 2010 Express。

NuGet コマンド ライン ツールが必要です。

* .NET framework Version 4

## <a name="installation"></a>インストール

これを使用する[最新リリース](http://nuget.codeplex.com/releases/view/52018):

* まず、以前のビルドをアンインストールします。 これを行う管理者として VS を実行する必要があります。
* 必要のあるすべての既存フィードを削除します。
* 指す新しいフィードを追加する[ http://go.microsoft.com/fwlink/?LinkId=206669](http://go.microsoft.com/fwlink/?LinkId=206669)します。

## <a name="nuget-11"></a>NuGet 1.1

このリリースで修正された問題の一覧[はこちら](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

RC から RTM の 1 つの問題が修正されました。

* [ソリューション内のすべてのプロジェクトの影響を与えるパッケージを削除する 474 問題点。](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>リリース候補

CTP 2 以降では、このリリース候補の変更を次に示します。 バグの完全な一覧を表示する問題の追跡ツールを参照してください。

* [コンソールからパッケージを更新しても、依存関係は更新されません。](http://nuget.codeplex.com/workitem/443)
* [Bin 追加パッケージを取得しないパッケージ参照 (CTP1)](http://nuget.codeplex.com/workitem/442)
* [壊れた参照のままパッケージの更新](http://nuget.codeplex.com/workitem/440)
* [Get-package-ダイアログ ボックスで、または集計 'すべて' のソースが、コンソールで選択されているときに、更新プログラムが失敗します。](http://nuget.codeplex.com/workitem/439)
* [パッケージの検証エラーを取得します。](http://nuget.codeplex.com/workitem/426)
* [パッケージの追加 ダイアログからパッケージをインストールできない場合は、ユーザーを警告します。](http://nuget.codeplex.com/workitem/425)
* [Get-package-更新プログラムの多数のパッケージを更新するときにスローされます](http://nuget.codeplex.com/workitem/424)
* [Nuspec ファイルが正しく作成されていない場合はエラー処理を向上させる](http://nuget.codeplex.com/workitem/423)
* [Nuget の pack には、指定したファイルが無視されます。](http://nuget.codeplex.com/workitem/422)
* [最後から 2 番目のパッケージ ソースを削除して、"下へ移動 をクリックし、VS がクラッシュします。](http://nuget.codeplex.com/workitem/418)
* [パッケージのインストール中にアセンブリ参照を削除します。](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException 設定 ダイアログ ボックスを開くときに](http://nuget.codeplex.com/workitem/411)
* [パッケージ マネージャー コンソールでパッケージ ソースのアクセス キーが機能しません。](http://nuget.codeplex.com/workitem/410)
* [VS NuGet の設定ダイアログへのアクセス キーが不適切なフィールドにフォーカスを与える](http://nuget.codeplex.com/workitem/409)
* [パッケージ ID の intellisense は、項目が多すぎますを照会しないでください。](http://nuget.codeplex.com/workitem/404)
* [プロジェクト名にドット文字を含むプロジェクトにパッケージを追加できませんでした。](http://nuget.codeplex.com/workitem/403)
* [Nuspec での指定のファイルと発行します。](http://nuget.codeplex.com/workitem/400)
* [新しいビルドを使用する場合は、正しい公式フィードを登録する必要があります。](http://nuget.codeplex.com/workitem/399)
* [タグは、# ではなくスペースを使用する必要があります。](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata 有用な情報が不足しています](http://nuget.codeplex.com/workitem/388)
* [不正使用のリンクを追加 ダイアログ ボックス](http://nuget.codeplex.com/workitem/386)
* [App_Data を使用して Visual Studio でパッケージの区切りを解凍するには](http://nuget.codeplex.com/workitem/380)
* [タグを実装します。](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder により作成される依存関係のない空のパッケージ](http://nuget.codeplex.com/workitem/373)
* [パッケージの所有者 フィールドを追加します。](http://nuget.codeplex.com/workitem/365)
* [VSIX のツールではなく、NuGet パッケージ マネージャーと VSIX マニフェストを更新します。](http://nuget.codeplex.com/workitem/364)
* [Get-package コマンドでは、すべてのソースが選択されているときにエラーがスローされます。](http://nuget.codeplex.com/workitem/359)
* [[オプション] ダイアログでパッケージ ソースの順序付けを許可します。](http://nuget.codeplex.com/workitem/356)
* [更新プログラム パッケージでは、以前のバージョンは削除されません。](http://nuget.codeplex.com/workitem/352)
* [依存関係の実装バージョンの範囲の指定](http://nuget.codeplex.com/workitem/347)
* [[新しいパッケージを追加] をクリックすると、visual Studio がクラッシュします。](http://nuget.codeplex.com/workitem/346)
* [パッケージの追加 ダイアログでダウンロードおよび評価を表示します。](http://nuget.codeplex.com/workitem/345)
* [パッケージ ソース ダイアログ ボックスの間で変更すると、アクティブなソースが更新されません。](http://nuget.codeplex.com/workitem/344)
* [パッケージ マネージャー コンソール ウィンドウのキー バインドを削除します。](http://nuget.codeplex.com/workitem/339)
* [インストール パッケージは、コマンドレットの名前として認識されない.](http://nuget.codeplex.com/workitem/338)
* [ローカルの依存関係を定期的なフィードのフィードからパッケージのインストールは解決されません。](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies はまだ使用されている依存関係をスキップする必要があります。](http://nuget.codeplex.com/workitem/331)
* [元のページ要求が返されます場合、ページ ナビゲーションをキャンセルするには、ユーザーが別のページに移動ことはできません。](http://nuget.codeplex.com/workitem/325)
* [パッケージの数が多いフィードを提供するためには、NuPack.Server のパフォーマンスを調査します。](http://nuget.codeplex.com/workitem/324)
* [以前に選択したソースではなく、「新規」のパッケージ ソースを使用、パッケージの 2 番目の時間をフィルター処理します。](http://nuget.codeplex.com/workitem/321)
* [ダイアログ ボックスで [オンライン] タブを選択する際に、既定のパッケージ ソースを選択してください。](http://nuget.codeplex.com/workitem/320)
* [パッケージの一覧は、既定でインストールされているパッケージを表示する必要があります。](http://nuget.codeplex.com/workitem/309)
* [アセンブリ参照 HintPaths](http://nuget.codeplex.com/workitem/294)
* [パッケージ マネージャー コンソールを開いているときに例外](http://nuget.codeplex.com/workitem/268)
* [コンソールの intellisense は、全体のフィードをダウンロードします。](http://nuget.codeplex.com/workitem/259)
* ['Active' を 'default' のパッケージ ソースの名前を変更する必要があります。](http://nuget.codeplex.com/workitem/258)
* [パッケージ ソースの UI: 名前/ソース フィールドが空でない場合、新しいソースを追加する必要があります [ok] を押すと](http://nuget.codeplex.com/workitem/257)
* [インストールされているパッケージの数が多い場合、ダイアログが非常に低速になります](http://nuget.codeplex.com/workitem/243)
* [厳密な名前付きのアセンブリ バインド リダイレクトをサポートします。](http://nuget.codeplex.com/workitem/238)
* [パッケージ参照を追加してください.パッケージ ソースの下のドロップを含めるための UI](http://nuget.codeplex.com/workitem/226)
* [NuPack が agnostically config ファイル名の構成の変換をサポートする必要があります。](http://nuget.codeplex.com/workitem/224)
* [BasePath NuPack.exe で無効にするのには、します。](http://nuget.codeplex.com/workitem/222)
* [パッケージ ソースのフォールバック動作](http://nuget.codeplex.com/workitem/204)
* [GUI でクラッシュします。](http://nuget.codeplex.com/workitem/201)
* [並べ替えの追加のパッケージ ダイアログ ボックスにオプションの追加](http://nuget.codeplex.com/workitem/179)
* [パッケージ マネージャー コンソールをクリアするショートカット キー](http://nuget.codeplex.com/workitem/174)
* [PowerConsole により失敗する NuPack コンソール](http://nuget.codeplex.com/workitem/166)
* [コンソールとパッケージの追加 ダイアログは、要求でユーザー エージェントを設定する必要があります。](http://nuget.codeplex.com/workitem/141)
* [ビルドで、VSIX と NuPack.exe のバージョン番号を設定します。](http://nuget.codeplex.com/workitem/134)
* [-一般的な PowerShell パラメーターを非表示にします。](http://nuget.codeplex.com/workitem/118)
* [コンソール コマンドの詳細なヘルプを追加します。](http://nuget.codeplex.com/workitem/110)
* [追加パッケージのダイアログが現在のパッケージ ソースの選択を許可する必要があります。](http://nuget.codeplex.com/workitem/88)
* [異なる名前空間への移動 NuPack.Core クラス](http://nuget.codeplex.com/workitem/50)
* [コマンドレットのヘルプを追加します。](http://nuget.codeplex.com/workitem/23)
* [パッケージのダウンロード後フィードからハッシュを確認します。](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

以下は、CTP 2 での最も重要な変更です。

* パッケージの OData サービス エンドポイントに ATOM フィードを切り替える: CTP2 バージョンの NuGet にアップグレードする場合は、パッケージ ソースとして、次の URL を追加することを確認する:`https://feed.nuget.org/ctp2/odata/v1/`します。
* パッケージの追加コマンドの名前を変更*Install-package*します。
* 更新、`.nuspec`形式。 `.nuspec`形式が含まれています、 *iconUrl*パッケージの追加 ダイアログに表示される 32 x 32 の png アイコンを指定するフィールド。 これに、パッケージを区別するために設定を必ずします。 `.nuspec`形式も含まれています、新しい*projectUrl*フィールドが、パッケージに関する情報を提供する web ページを指すように使用することができます。

このビルドは、以前では動作しません`.nupkg`ファイル。 Null 参照例外が発生した場合、古いを使用している`.nupkg`ファイルを開き、更新と再構築する必要があります[NuGet コマンド ライン ツール](http://nuget.codeplex.com/releases/52017/download/165468)します。

次に示します (は含まれませんのバグをコードの軽微なクリーンアップなど。) NuGet CTP 2 の修正されたバグ、機能の一覧。

* [エラー アンパック パッケージ アセンブリとアセンブリの TargetFramework を指定します。](http://nuget.codeplex.com/workitem/10)
* [簡単に見つけられる NuPack コンソール ウィンドウ](http://nuget.codeplex.com/workitem/14)
* [ILMerge nupack.exe リリース](http://nuget.codeplex.com/workitem/19)
* [エラーと例外処理の強化](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core]: PackageManager がフィードに関連するエラーを適切に処理する必要があります](http://nuget.codeplex.com/workitem/28)
* [コンソールの新しいアイコンが必要](http://nuget.codeplex.com/workitem/29)
* [ダイアログ ボックスの文字列をローカライズします。](http://nuget.codeplex.com/workitem/38)
* [NuPack キャッシュがメモリ内 .nupack ファイルをダウンロード](http://nuget.codeplex.com/workitem/40)
* [NuPack コンソール: コンソールを表示するため、既定のショートカットを変更します。](http://nuget.codeplex.com/workitem/48)
* [プロジェクト システムは、共通プロパティの既定値をサポートする必要があります。](http://nuget.codeplex.com/workitem/49)
* [その nuspec を使用して 1 つだけの nuspec ファイル nupack.exe をフォルダーで実行されている必要があります。](http://nuget.codeplex.com/workitem/52)
* [[プロジェクト] メニュー表示もとプロジェクト/ソリューションが読み込まれていません。](http://nuget.codeplex.com/workitem/54)
* [build.cmd がコードベースのクリーンな複製で失敗します。](http://nuget.codeplex.com/workitem/56)
* [更新プログラムの使用可能な機能](http://nuget.codeplex.com/workitem/57)
* [コンソールで、プロンプトを削除、ダイアログ ボックスを使用してパッケージを追加 ダイアログ ボックス。](http://nuget.codeplex.com/workitem/73)
* [[インストール] をクリックして、パッケージを追加することがない視覚的なフィードバックに遅く、多くの場合、](http://nuget.codeplex.com/workitem/80)
* [更新プログラムがある、インストールされているパッケージのうちを検出する方法はありません。](http://nuget.codeplex.com/workitem/82)
* [ダイアログ ボックスで、インストールされているパッケージを更新する方法はありません。](http://nuget.codeplex.com/workitem/83)
* [ダイアログ ボックスで、インストールされているパッケージをアンインストールする方法はありません。](http://nuget.codeplex.com/workitem/84)
* [&ldquo;パッケージ参照の追加&hellip;&rdquo;がインストールされている参照のコンテキスト メニューに表示されます](http://nuget.codeplex.com/workitem/85)
* [コンソールからのパッケージを更新した後、古いバージョンと新しいバージョンの両方インストール示します](http://nuget.codeplex.com/workitem/86)
* [ダイアログ ボックスを使用する場合は、コンソールで、アクティビティは、使用後に表示されなくなります。](http://nuget.codeplex.com/workitem/87)
* [クリーンアップのコマンド ライン nupack.exe で解析します。](http://nuget.codeplex.com/workitem/89)
* [パッケージ ソースにフレンドリ名を追加します。](http://nuget.codeplex.com/workitem/98)
* [パッケージのアイコンなどをサポートする更新プログラムの .nuspec](http://nuget.codeplex.com/workitem/103)
* [フィードの UI は、URL のコピーを許可しません。](http://nuget.codeplex.com/workitem/105)
* [パッケージの削除エラーの処理が向上します。](http://nuget.codeplex.com/workitem/107)
* [コンソール ウィンドウに入力することによってカーソルのフォーカス異なります](http://nuget.codeplex.com/workitem/112)
* [エラー メッセージが非常になります](http://nuget.codeplex.com/workitem/116)
* [インストールされていないパッケージのパッケージの削除のパフォーマンスが正しくありません。](http://nuget.codeplex.com/workitem/117)
* [パッケージ ソースがない場合に失敗したパッケージの削除](http://nuget.codeplex.com/workitem/119)
* [パッケージ ソースが利用できない場合、パッケージの削除が失敗します。](http://nuget.codeplex.com/workitem/120)
* [パッケージのメタデータをフィードのタイトルを追加します。](http://nuget.codeplex.com/workitem/125)
* [追加パッケージの追加には、ソース パラメーター](http://nuget.codeplex.com/workitem/127)
* [パッケージの一覧が必要 - ソース パラメーター](http://nuget.codeplex.com/workitem/128)
* [Update NuPack.Server NuPack ユーザー エージェントにパッケージのダウンロードを要求するには](http://nuget.codeplex.com/workitem/142)
* [ライセンスの同意 ダイアログへの同意を必要とするすべての依存関係のライセンスを一覧表示する必要があります。](http://nuget.codeplex.com/workitem/145)
* [フィードにパッケージをスローした場合、エラーをログします。](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe は空にできないように&lt;licenseurl&gt;要素](http://nuget.codeplex.com/workitem/152)
* [Get パッケージのアンインストール パッケージの インストール パッケージをパッケージの削除の追加のパッケージをリスト パッケージの名前を変更します。](http://nuget.codeplex.com/workitem/155)
* [ソリューション ナビゲーターからパッケージ参照の追加 メニュー項目を使用して Visual Studio がクラッシュします。](http://nuget.codeplex.com/workitem/158)
* [[使用可能なパッケージ ソース] ラベルにコロンがありません。](http://nuget.codeplex.com/workitem/160)
* [.Nuspec xml 要素の文字種一貫して camel 規約に従った大文字と小文字を行う](http://nuget.codeplex.com/workitem/161)
* [NuPack VSIX のマニフェストは、'admin' ビットで有効にする必要があります。](http://nuget.codeplex.com/workitem/162)
* [Null 参照のエラーが発生しないフィードとリスト パッケージを実行する場合](http://nuget.codeplex.com/workitem/164)
* [nuget.exe: 宛先パスの指定](http://nuget.codeplex.com/workitem/171)
* [Powershell のエラー WinXP でパッケージの管理コンソールを開く](http://nuget.codeplex.com/workitem/175)
* [パッケージの一覧を読み込んでいるときに VS がクラッシュします。](http://nuget.codeplex.com/workitem/176)
* [メタ パッケージ (ファイルのみの依存関係) を許可します。](http://nuget.codeplex.com/workitem/180)
* [Powershell スクリプトを Powershell 2.0 モジュールに変換します。](http://nuget.codeplex.com/workitem/181)
* [ターゲットを指定すると、PathResolver はパス部分の先頭のワイルドカード文字を破棄する必要があります。](http://nuget.codeplex.com/workitem/183)
* [依存関係のないです。](http://nuget.codeplex.com/workitem/186)
* [Elmah をインストール中にエラー](http://nuget.codeplex.com/workitem/192)
* [構成変換は正しく動作しない&lt;configsections&gt;](http://nuget.codeplex.com/workitem/194)
* [変数 ' $グローバル: projectCache' 設定されていないために、取得できません](http://nuget.codeplex.com/workitem/203)
* [NuPack パッケージを作成するための MSBuild タスクを追加します。](http://nuget.codeplex.com/workitem/205)
* [リスト パッケージは、検索、フィルター処理をサポートする必要があります。](http://nuget.codeplex.com/workitem/206)
* [ライセンスに、パッケージの作成者は、ライセンス URL を提供する場合のリンクを常に表示します。](http://nuget.codeplex.com/workitem/208)
* [パッケージの削除「アクセス拒否」不定期の例外](http://nuget.codeplex.com/workitem/213)
* [単体テストの失敗: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [フォールバック/既定の一連のファイルの特定のバージョンのフレームワークが見つからない場合に許可します。](http://nuget.codeplex.com/workitem/223)
* [パッケージ参照を追加してください.UI は、パッケージを削除することはできません。](http://nuget.codeplex.com/workitem/225)
* [パッケージの参照時に 1 つの studio がクラッシュするまたは複数のプロジェクトをアンロードを追加します。](http://nuget.codeplex.com/workitem/228)
* [Web.debug.config ファイルを作業するのには構成変換が表示されません。](http://nuget.codeplex.com/workitem/229)
* [init.ps1 カスタム パッケージを起動できません。](http://nuget.codeplex.com/workitem/237)
* [自動的に閉じる場合は ENTER を押すために、既定のボタンが [ok] に設定されて、feedlist にパスを追加するときに](http://nuget.codeplex.com/workitem/240)
* [アンインストールしようとしています行の 2 倍を試行した場合は、依存関係の VS がクラッシュする。](http://nuget.codeplex.com/workitem/241)
* [パッケージの追加 ダイアログでプロジェクトの URL を表示します。](http://nuget.codeplex.com/workitem/253)
* [既定のインストールされているパッケージをパッケージの追加 ダイアログ](http://nuget.codeplex.com/workitem/254)
* [パッケージの追加 ダイアログのメニュー項目を変更します。](http://nuget.codeplex.com/workitem/261)
* [名前空間とアセンブリの名前を変更します。](http://nuget.codeplex.com/workitem/274)
* [NuGet に NuPack プロジェクトの名前変更します。](http://nuget.codeplex.com/workitem/282)
* [依存関係の一覧で、次のテキストを追加します。](http://nuget.codeplex.com/workitem/288)
* [ライセンスの同意 ダイアログでライセンスへの同意のテキストを変更します。](http://nuget.codeplex.com/workitem/291)
* [パッケージの一覧の上のライセンスの同意 ダイアログでテキストを変更します。](http://nuget.codeplex.com/workitem/292)
* [OData は、fwlink の URL を使用しません。](http://nuget.codeplex.com/workitem/304)
* [ページングに使用されるパッケージ数の積極的なキャッシュ経由でパッケージ マネージャー UI の場合。](http://nuget.codeplex.com/workitem/317)
* [NuPack/NuGet -&gt;パッケージ マネージャー コンソールのエラー](http://nuget.codeplex.com/workitem/335)
* [追加パッケージのダイアログでは、ライセンスへの同意を既にインストールされているパッケージが表示されます。](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

次に機能と NuGet CTP 1 の修正されたバグの一覧を示します。

* [.Nupack にパッケージの拡張機能の名前を変更する必要があります。](http://nuget.codeplex.com/workitem/1)
* [パッケージ ファイルをフォルダーに移動します。](http://nuget.codeplex.com/workitem/2)
* [インストールをマージ&amp;PS の追加コマンド](http://nuget.codeplex.com/workitem/3)
* [動詞-名詞コマンドレットのエイリアスを作成します。](http://nuget.codeplex.com/workitem/4)
* [VS でソリューションを切り替えるときに混乱して NuPack](http://nuget.codeplex.com/workitem/6)
* [既定では、'パッケージ' ソリューション フォルダーを非表示にする必要があります。](http://nuget.codeplex.com/workitem/11)
* [コンテンツ項目でトークンの置換後のサポートを追加します。](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI は、PackageSource API を使用する必要があります。](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core]: PackageManager は、それらをインストールする前にインストールされているパッケージをマーク](http://nuget.codeplex.com/workitem/27)
* [ソリューションからの削除の既定プロジェクトでは、既定値として削除されたプロジェクトもが表示されます。](http://nuget.codeplex.com/workitem/30)
* [新しいパッケージが「パートを追加できません、指定された URI のパッケージされているためです」で失敗します。](http://nuget.codeplex.com/workitem/32)
* [Visual Studio の GUI から"NuPack"文字列を削除します。](http://nuget.codeplex.com/workitem/35)
* [COPYRIGHT.txt に Apache ヘッダー ファイルを追加します。](http://nuget.codeplex.com/workitem/36)
* [Update PackageSource コマンドを削除します。](http://nuget.codeplex.com/workitem/37)
* [パッケージ マネージャーを使用できないのは、プロファイルの読み込み時に、例外をスローします。](http://nuget.codeplex.com/workitem/39)
* [init.ps1、install.ps1 および uninstall.ps1 追加の状態を受信する必要があります。](http://nuget.codeplex.com/workitem/41)
* [コンソールと GUI のパッケージを 1 つのパッケージに結合します。](http://nuget.codeplex.com/workitem/42)
* [ルートにない場合は XML に適用される場合は、Xml 変換ロジックは機能しません](http://nuget.codeplex.com/workitem/43)
* [ソースの設定 ダイアログの NuPack コンソールを更新しないパッケージの管理します。](http://nuget.codeplex.com/workitem/44)
* [NuPack コンソール UI: 'パッケージ ソース' を 'パッケージがフィード' ドロップダウン リストの名前を変更します。](http://nuget.codeplex.com/workitem/45)
* [NuPack コンソール オプション: NuPack コンソールと一致するように ' リポジトリ UI' の名前を変更します。](http://nuget.codeplex.com/workitem/46)
* [IIS または URL から開かれた web サイトに対する失敗したパッケージの追加](http://nuget.codeplex.com/workitem/53)
* [パッケージ マネージャーのソースは、FwLink を使用しません。](http://nuget.codeplex.com/workitem/55)
* [既定のパッケージ ソースを設定します。](http://nuget.codeplex.com/workitem/59)
* [1 つのソースが指定されている場合は、オプションでは、パッケージ ソースを追加、するときに、既定値は想定しています。](http://nuget.codeplex.com/workitem/60)
* [ダイアログの UI は、偽の「最新」のパッケージを示しています。](http://nuget.codeplex.com/workitem/62)
* [オプション: [キャンセル] をクリックするとは取り消されませんの変更](http://nuget.codeplex.com/workitem/63)
* [パッケージの参照 ダイアログの検索は大文字と小文字を区別しないはずを追加します。](http://nuget.codeplex.com/workitem/65)
* [AssemblyInfo.cs ファイルで会社のメタデータを修正します。](http://nuget.codeplex.com/workitem/67)
* [VSIX のバージョン番号](http://nuget.codeplex.com/workitem/71)
* [パッケージの削除: を使用して - ですか。2 回ヘルプを表示します](http://nuget.codeplex.com/workitem/72)
* [プロジェクト レベルのパッケージのインストール/アンインストール パッケージを実行します。](http://nuget.codeplex.com/workitem/74)
* [サーバーの 1 つ nupack 検証に失敗したときに、フィードを作成することができません。](http://nuget.codeplex.com/workitem/90)
* [NuPack アイコンを置き換える必要があります。](http://nuget.codeplex.com/workitem/94)
* [パッケージをフィードする NTLM http プロキシを認証しません。](http://nuget.codeplex.com/workitem/96)
* [ダイアログは常に中央揃え、VS のウィンドウで起動します。](http://nuget.codeplex.com/workitem/100)
* [パッケージの詳細のフィールドの多くは、ダイアログ ボックスで設定されていません。](http://nuget.codeplex.com/workitem/102)
* [ダイアログの UI は、著者の名を表示しません。](http://nuget.codeplex.com/workitem/108)
* [理由のバージョンのパッケージの削除](http://nuget.codeplex.com/workitem/113)
* [ダイアログの UI では、最近使用したタブを削除します。](http://nuget.codeplex.com/workitem/115)
* [適切なときに、VS のクラッシュは、少なくとも 1 つダイアログの UI を開いた後、ソリューション フォルダーをクリックします。](http://nuget.codeplex.com/workitem/126)
* [変更リスト パッケージのローカル、パラメーター-インストールされています。](http://nuget.codeplex.com/workitem/129)
* [Packages.xml NuPack.config に名前の変更します。](http://nuget.codeplex.com/workitem/132)
* [コンソールは、行の末尾にカーソルを強制的します。](http://nuget.codeplex.com/workitem/135)
* [パッケージの削除の intellisense が壊れています](http://nuget.codeplex.com/workitem/136)
* [.Nuspec とフィードを RequireLicenseAcceptance フラグを追加します。](http://nuget.codeplex.com/workitem/137)
* [.Nuspec 形式およびパッケージの LicenseUrl フィードを追加します。](http://nuget.codeplex.com/workitem/138)
* [同意 ダイアログを表示する同意を必要とするパッケージのインストール をクリックする必要があります。](http://nuget.codeplex.com/workitem/139)
* [パッケージの追加ダイアログに免責事項のテキストを追加します。](http://nuget.codeplex.com/workitem/140)
* [免責事項ときのパッケージ コンソールを実行して、初めての追加します。](http://nuget.codeplex.com/workitem/143)
* [コンソールでパッケージをインストールした後の免責事項を表示します。](http://nuget.codeplex.com/workitem/144)
* [.Nupack 拡張子を .nupkg に変更します。](http://nuget.codeplex.com/workitem/146)