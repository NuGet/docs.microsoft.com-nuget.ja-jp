---
title: NuGet 1.0 および1.1 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 1.1 のリリースノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4f90888eae4d039c99d6f6879a06107ec5a31a82
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384698"
---
# <a name="nuget-10-and-11-release-notes"></a>NuGet 1.0 および1.1 のリリースノート

[NuGet 1.2 リリースノート](../release-notes/nuget-1.2.md)

NuGet 1.0 は、2011年1月13日にリリースされました。  NuGet 1.1 は、2011年2月12日にリリースされました。

## <a name="overview"></a>の概要

このドキュメントには、メジャープレビューリリースに従ってグループ化された NuGet 1.0 のさまざまなリリースのリリースノートが含まれています。

NuGet には、次のコンポーネントが含まれています。

* 次のもので構成される*nuget.exe* *。
  * パッケージの参照とインストールに使用する Visual Studio 内の [**ライブラリパッケージの追加]** ダイアログ * ダイアログ。
  * **パッケージマネージャーコンソール*** Visual Studio 内の Powershell ベースのコンソール。
* *NuGet コマンドラインツール** パッケージを作成 (および最終的に発行) するために使用されるツールです。

NuGet Tools Visual Studio 拡張機能 (*nuget. .vsix*) には次のものが必要です。

* Visual Studio 2010 または Visual Web Developer 2010 Express。

NuGet コマンドラインツールを実行するには、次のものが必要です。

* .NET Framework バージョン4

## <a name="installation"></a>のインストール

この[最新リリース](http://nuget.codeplex.com/releases/view/52018)を使用するには:

* まず、古いビルドをアンインストールします。 これを行うには、管理者として VS を実行する必要があります。
* 既存のすべてのフィードを削除します。
* <https://go.microsoft.com/fwlink/?LinkId=206669>を指す新しいフィードを追加します。

## <a name="nuget-11"></a>NuGet 1.1

このリリースで修正された問題の一覧については、[こちらを参照](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)してください。

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

RC 以降、RTM に関して1つの問題が修正されました。

* [問題 474: パッケージの削除がソリューションのすべてのプロジェクトに影響する](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Release Candidate

次に、このリリース候補 (CTP 2 以降) で行われた変更を示します。 問題の追跡ツールにアクセスして、バグの完全な一覧を確認します。

* [コンソールからパッケージを更新しても、依存関係は更新されません。](http://nuget.codeplex.com/workitem/443)
* [パッケージを追加すると、パッケージ参照ではない bin が開始されます (CTP1)](http://nuget.codeplex.com/workitem/442)
* [パッケージを更新すると、壊れた参照が残る](http://nuget.codeplex.com/workitem/440)
* [パッケージの取得-ダイアログで更新が失敗するか、コンソールで [すべての集計ソース] が選択されています。](http://nuget.codeplex.com/workitem/439)
* [パッケージ検証エラーの取得](http://nuget.codeplex.com/workitem/426)
* [[パッケージの追加] ダイアログボックスからパッケージをインストールできない場合にユーザーに警告する](http://nuget.codeplex.com/workitem/425)
* [Get-Package-多数のパッケージを更新するときに更新がスローされる](http://nuget.codeplex.com/workitem/424)
* [Nuspec ファイルが正しく作成されない場合のエラー処理の向上](http://nuget.codeplex.com/workitem/423)
* [指定されたファイルを Nuget パックが無視します](http://nuget.codeplex.com/workitem/422)
* [最後から2番目のパッケージソースを削除し、[下へ移動] をクリックすると、クラッシュと](http://nuget.codeplex.com/workitem/418)
* [パッケージのインストール中にアセンブリ参照を削除する](http://nuget.codeplex.com/workitem/413)
* [設定ダイアログを開くときの InvalidOperationException](http://nuget.codeplex.com/workitem/411)
* [パッケージマネージャーコンソールでパッケージソースのアクセスキーが機能しない](http://nuget.codeplex.com/workitem/410)
* [NuGet VS の設定ダイアログのアクセスキーによって、誤ったフィールドにフォーカスが移動される](http://nuget.codeplex.com/workitem/409)
* [パッケージ ID の intellisense では、クエリの実行に必要な項目が多すぎます](http://nuget.codeplex.com/workitem/404)
* [プロジェクト名にドット文字を含むパッケージをプロジェクトに追加できませんでした](http://nuget.codeplex.com/workitem/403)
* [Nuspec で指定されたファイルに問題があります](http://nuget.codeplex.com/workitem/400)
* [新しいビルドを使用するときに、正しい公式フィードが登録される必要があります](http://nuget.codeplex.com/workitem/399)
* [タグは、ではなくスペースを使用する必要があります。#](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata に有用な情報がありません](http://nuget.codeplex.com/workitem/388)
* [ダイアログへの不正のレポートの追加リンク](http://nuget.codeplex.com/workitem/386)
* [App_Data を使用した Visual Studio でのパッケージの中断の解凍](http://nuget.codeplex.com/workitem/380)
* [タグを実装する](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder では、依存関係のない空のパッケージを作成できます](http://nuget.codeplex.com/workitem/373)
* [パッケージの [所有者の追加] フィールド](http://nuget.codeplex.com/workitem/365)
* [Vsix ツールではなく NuGet パッケージマネージャーとして VSIX マニフェストを更新する](http://nuget.codeplex.com/workitem/364)
* [Get-Package コマンドは、すべてのソースが選択されたときにエラーをスローします](http://nuget.codeplex.com/workitem/359)
* [[オプション] ダイアログボックスでパッケージソースの順序付けを許可する](http://nuget.codeplex.com/workitem/356)
* [更新プログラム-パッケージが古いバージョンを削除しない](http://nuget.codeplex.com/workitem/352)
* [依存関係のバージョン範囲指定を実装する](http://nuget.codeplex.com/workitem/347)
* [[新しいパッケージの追加] をクリックすると Visual Studio がクラッシュする](http://nuget.codeplex.com/workitem/346)
* [[パッケージの追加] ダイアログでダウンロードと評価を表示する](http://nuget.codeplex.com/workitem/345)
* [ダイアログでパッケージソース間を変更しても、アクティブなソースが更新されない](http://nuget.codeplex.com/workitem/344)
* [パッケージマネージャーコンソールウィンドウのキーバインドを削除します。](http://nuget.codeplex.com/workitem/339)
* [インストール-パッケージはコマンドレットの名前として認識されません...](http://nuget.codeplex.com/workitem/338)
* [ローカルフィードからのパッケージのインストール通常のフィードの依存関係が解決されない](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies は、まだ使用されている依存関係をスキップする必要があります](http://nuget.codeplex.com/workitem/331)
* [ページナビゲーションをキャンセルした場合、元のページ要求が返されても、ユーザーは別のページに移動できません。](http://nuget.codeplex.com/workitem/325)
* [多数のパッケージを含むフィードを提供するために、NuPack サーバーのパフォーマンスを調査します。](http://nuget.codeplex.com/workitem/324)
* [2回目にパッケージをフィルター処理すると、以前に選択したソースではなく、"新しい" パッケージソースが使用されます。](http://nuget.codeplex.com/workitem/321)
* [ダイアログの [オンライン] タブを選択する場合は、[既定のパッケージソース] を選択する必要があります。](http://nuget.codeplex.com/workitem/320)
* [リスト-既定では、パッケージにインストールされているパッケージが表示されます](http://nuget.codeplex.com/workitem/309)
* [アセンブリ参照 HintPaths](http://nuget.codeplex.com/workitem/294)
* [パッケージマネージャーコンソールを開いているときに例外が発生しました](http://nuget.codeplex.com/workitem/268)
* [コンソール intellisense によるフィード全体のダウンロード](http://nuget.codeplex.com/workitem/259)
* [' Default ' パッケージソースの名前を ' Active ' に変更する必要があります](http://nuget.codeplex.com/workitem/258)
* [パッケージソースの UI: [OK] を押すと、名前/ソースフィールドが空でない場合に新しいソースが追加されます](http://nuget.codeplex.com/workitem/257)
* [インストールされているパッケージの数が多い場合、ダイアログが非常に遅くなる](http://nuget.codeplex.com/workitem/243)
* [厳密な名前付きアセンブリのバインディングリダイレクトをサポートする](http://nuget.codeplex.com/workitem/238)
* [パッケージ参照の追加...パッケージソースのドロップダウンを含めるための UI](http://nuget.codeplex.com/workitem/226)
* [NuPack は、構成ファイル名の config transform agnostically をサポートする必要があります](http://nuget.codeplex.com/workitem/224)
* [NuPack で BasePath をオーバーライドできるようにします。](http://nuget.codeplex.com/workitem/222)
* [パッケージソースのフォールバック動作](http://nuget.codeplex.com/workitem/204)
* [GUI でのクラッシュ](http://nuget.codeplex.com/workitem/201)
* [[パッケージの追加] ダイアログに並べ替えオプションを追加する](http://nuget.codeplex.com/workitem/179)
* [パッケージマネージャーコンソールをクリアするショートカットキー](http://nuget.codeplex.com/workitem/174)
* [PowerConsole によって NuPack コンソールが失敗する](http://nuget.codeplex.com/workitem/166)
* [コンソールと [パッケージの追加] ダイアログボックスで、要求にユーザーエージェントを設定します。](http://nuget.codeplex.com/workitem/141)
* [ビルドで VSIX と NuPack のバージョン番号を設定します。](http://nuget.codeplex.com/workitem/134)
* [一般的な PowerShell パラメーターを非表示にする-?](http://nuget.codeplex.com/workitem/118)
* [コンソールコマンドの詳細なヘルプを追加する](http://nuget.codeplex.com/workitem/110)
* [[パッケージの追加] ダイアログで、現在のパッケージソースを選択できるようにする](http://nuget.codeplex.com/workitem/88)
* [NuPack のコアクラスを別の名前空間に移動する](http://nuget.codeplex.com/workitem/50)
* [コマンドレットにヘルプを追加する](http://nuget.codeplex.com/workitem/23)
* [パッケージのダウンロード後にフィードからハッシュを確認する](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

CTP 2 で行われる最も重要な変更は次のとおりです。

* パッケージフィードを ATOM から OData サービスエンドポイントに切り替えた場合: CTP2 バージョンの NuGet にアップグレードする場合は、次の URL をパッケージソースとして追加する必要があります: `https://feed.nuget.org/ctp2/odata/v1/`。
* パッケージの追加コマンドの名前を*Install パッケージ*に変更しました。
* `.nuspec` 形式が更新されました。 `.nuspec` 形式には、[パッケージの追加] ダイアログに表示される32x32 の png アイコンを指定するための*Iconurl*フィールドが含まれるようになりました。 そのため、パッケージを区別するように設定してください。 `.nuspec` 形式には、パッケージに関する詳細情報を提供する web ページをポイントするために使用*できる新しい [* ユーザー設定] フィールドも含まれています。

このビルドは、古い `.nupkg` ファイルでは機能しません。 Null 参照例外が発生した場合は、古い `.nupkg` ファイルを使用しているため、更新された[NuGet コマンドラインツール](http://nuget.codeplex.com/releases/52017/download/165468)を使用して再構築する必要があります。

次に、NuGet CTP 2 で修正された機能とバグの一覧を示します (マイナーコードクリーンアップのバグは含まれていません)。

* [アセンブリの TargetFramework を指定するするときに、パッケージアセンブリの展開エラーが発生します。](http://nuget.codeplex.com/workitem/10)
* [NuPack コンソールウィンドウをより見つけやすくする](http://nuget.codeplex.com/workitem/14)
* [Nupack のリリースを ILMerge](http://nuget.codeplex.com/workitem/19)
* [より優れたエラー/例外処理](http://nuget.codeplex.com/workitem/24)
* [[Nupack. Core]: パッケージがフィードに関連するエラーを適切に処理する必要があります](http://nuget.codeplex.com/workitem/28)
* [コンソールに新しいアイコンが必要](http://nuget.codeplex.com/workitem/29)
* [ダイアログ内の文字列のローカライズ](http://nuget.codeplex.com/workitem/38)
* [NuPack キャッシュがダウンロードされました。 nupack ファイルがメモリ内にあります](http://nuget.codeplex.com/workitem/40)
* [NuPack コンソール: コンソールを表示するための既定のショートカットを変更します。](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem は共通プロパティの既定値をサポートする必要があります](http://nuget.codeplex.com/workitem/49)
* [Nuspec ファイルが1つだけあるフォルダーで nupack を実行する場合は、nuspec を使用する必要があります。](http://nuget.codeplex.com/workitem/52)
* [プロジェクト/ソリューションが読み込まれていない場合でも、[プロジェクト] メニューが表示される](http://nuget.codeplex.com/workitem/54)
* [コードベースのクリーンクローンでビルド .cmd が失敗する](http://nuget.codeplex.com/workitem/56)
* [更新プログラムの利用可能な機能](http://nuget.codeplex.com/workitem/57)
* [ダイアログ: ダイアログボックスを使用してパッケージを追加すると、コンソールのプロンプトが削除されます。](http://nuget.codeplex.com/workitem/73)
* [[インストール] をクリックしてパッケージを追加すると、多くの場合、視覚的なフィードバックはありません。](http://nuget.codeplex.com/workitem/80)
* [インストールされているパッケージのどれに更新プログラムがあるかを検出する方法はありません。](http://nuget.codeplex.com/workitem/82)
* [ダイアログでインストールされているパッケージを更新する方法はありません。](http://nuget.codeplex.com/workitem/83)
* [ダイアログでインストールされているパッケージをアンインストールする方法はありません](http://nuget.codeplex.com/workitem/84)
* [インストールされている参照のコンテキストメニューに表示される [パッケージ参照の追加]&hellip;&rdquo; &ldquo;](http://nuget.codeplex.com/workitem/85)
* [コンソールからパッケージを更新すると、古いバージョンと新しいバージョンの両方がインストール済みとして表示されます。](http://nuget.codeplex.com/workitem/86)
* [コンソールのアクティビティは、ダイアログを使用すると、使用後に表示されなくなります。](http://nuget.codeplex.com/workitem/87)
* [Nupack のクリーンアップコマンドライン解析](http://nuget.codeplex.com/workitem/89)
* [パッケージソースにフレンドリ名を追加する](http://nuget.codeplex.com/workitem/98)
* [パッケージアイコンの追加をサポートするように nuspec を更新します。](http://nuget.codeplex.com/workitem/103)
* [フィード UI で URL のコピーが許可されない](http://nuget.codeplex.com/workitem/105)
* [パッケージの削除エラー処理が改善されます。](http://nuget.codeplex.com/workitem/107)
* [コンソールウィンドウでの入力はカーソルフォーカスに依存します](http://nuget.codeplex.com/workitem/112)
* [エラーメッセージが表示する](http://nuget.codeplex.com/workitem/116)
* [インストールされていないパッケージの削除パッケージのパフォーマンスに問題がある](http://nuget.codeplex.com/workitem/117)
* [パッケージソースが存在しない場合、パッケージの削除に失敗する](http://nuget.codeplex.com/workitem/119)
* [パッケージソースが使用できない場合、パッケージの削除に失敗する](http://nuget.codeplex.com/workitem/120)
* [パッケージメタデータとフィードにタイトルを追加します。](http://nuget.codeplex.com/workitem/125)
* [-Source パラメーターを追加してパッケージに戻します。](http://nuget.codeplex.com/workitem/127)
* [リスト-パッケージは-Source パラメーターを持つ必要があります](http://nuget.codeplex.com/workitem/128)
* [Nupack サーバーを更新して、パッケージをダウンロードするように NuPack ユーザーエージェントを要求する](http://nuget.codeplex.com/workitem/142)
* [同意が必要なすべての依存関係のライセンスの一覧を表示するライセンス同意ダイアログ](http://nuget.codeplex.com/workitem/145)
* [パッケージがフィードでスローされたときにエラーをログに記録する](http://nuget.codeplex.com/workitem/150)
* [NuPack では、空の &lt;licenseurl&gt; 要素を許可しないでください](http://nuget.codeplex.com/workitem/152)
* [リスト名の変更-パッケージにパッケージを追加し、パッケージをインストールパッケージに追加して、パッケージをアンインストールにパッケージ化します。](http://nuget.codeplex.com/workitem/155)
* [ソリューションナビゲーターの [パッケージ参照の追加] メニュー項目を使用すると、Visual Studio がクラッシュする](http://nuget.codeplex.com/workitem/158)
* ["利用可能なパッケージソース" ラベルにコロンがありません](http://nuget.codeplex.com/workitem/160)
* [Nuspec xml 要素の大文字と小文字の区別を一貫して camel 形式にする](http://nuget.codeplex.com/workitem/161)
* [NuPack VSIX のマニフェストで ' admin bit ' を有効にする必要があります](http://nuget.codeplex.com/workitem/162)
* [フィードを含まないリストパッケージを実行すると、null 参照エラーが発生します。](http://nuget.codeplex.com/workitem/164)
* [nuget.exe: 宛先パスを指定します](http://nuget.codeplex.com/workitem/171)
* [WinXP で Package Management コンソールを開くときの Powershell エラー](http://nuget.codeplex.com/workitem/175)
* [パッケージリストを読み込もうとしている間に VS がクラッシュする](http://nuget.codeplex.com/workitem/176)
* [メタパッケージを許可する (ファイルは使用せず、依存関係のみ)](http://nuget.codeplex.com/workitem/180)
* [Powershell スクリプトを Powershell 2.0 モジュールに変換する](http://nuget.codeplex.com/workitem/181)
* [ターゲットが指定されている場合、PathResolver は、ワイルドカード文字の前のパス部分を破棄する必要があります](http://nuget.codeplex.com/workitem/183)
* [依存関係なし](http://nuget.codeplex.com/workitem/186)
* [Elmah のインストールエラー](http://nuget.codeplex.com/workitem/192)
* [構成の変換は &lt;configsections では正しく機能しません&gt;](http://nuget.codeplex.com/workitem/194)
* [変数 ' $global:p rojectCache ' は設定されていないため取得できません](http://nuget.codeplex.com/workitem/203)
* [NuPack パッケージを作成するための MSBuild タスクを追加する](http://nuget.codeplex.com/workitem/205)
* [リスト-パッケージは検索/フィルター処理をサポートする必要があります](http://nuget.codeplex.com/workitem/206)
* [パッケージ作成者がライセンス URL を提供する場合は、常にライセンスへのリンクを表示する](http://nuget.codeplex.com/workitem/208)
* [削除パッケージを使用すると、時折 "アクセスが拒否されました" 例外が発生する](http://nuget.codeplex.com/workitem/213)
* [失敗した単体テスト: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [特定 framework バージョンが見つからない場合に、フォールバック/既定のファイルセットを許可する](http://nuget.codeplex.com/workitem/223)
* [パッケージ参照の追加...UI でパッケージを削除できません](http://nuget.codeplex.com/workitem/225)
* [1つ以上のプロジェクトがアンロードされると、パッケージ参照の追加がクラッシュする](http://nuget.codeplex.com/workitem/228)
* [構成の変換が、web.config ファイルで動作していないように見える](http://nuget.codeplex.com/workitem/229)
* [カスタムパッケージで初期化が起動しない](http://nuget.codeplex.com/workitem/237)
* [フィードの一覧にパスを追加すると、既定のボタンが [OK] に設定されます。そのため、ENTER キーを押すと自動的に閉じられます。](http://nuget.codeplex.com/workitem/240)
* [依存関係をアンインストールしようとすると、1つの行で2回試行された場合、VS がクラッシュします。](http://nuget.codeplex.com/workitem/241)
* [[パッケージの追加] ダイアログボックスでプロジェクトの URL を表示する](http://nuget.codeplex.com/workitem/253)
* [インストールされているパッケージへのパッケージの追加ダイアログの既定値](http://nuget.codeplex.com/workitem/254)
* [[パッケージの追加] ダイアログメニュー項目を変更します。](http://nuget.codeplex.com/workitem/261)
* [名前空間とアセンブリの名前を変更する](http://nuget.codeplex.com/workitem/274)
* [NuPack プロジェクトの名前を NuGet に変更する](http://nuget.codeplex.com/workitem/282)
* [依存関係の一覧の下に次のテキストを追加します。](http://nuget.codeplex.com/workitem/288)
* [[ライセンスの同意] ダイアログでライセンスの同意テキストを変更する](http://nuget.codeplex.com/workitem/291)
* [パッケージの一覧の上にある [ライセンスの同意] ダイアログのテキストを変更する](http://nuget.codeplex.com/workitem/292)
* [OData が fwlink URL で動作しない](http://nuget.codeplex.com/workitem/304)
* [パッケージマネージャー UI: ページングに使用されるパッケージ数の積極的なキャッシュ](http://nuget.codeplex.com/workitem/317)
* [NuPack/NuGet-&gt; パッケージマネージャーコンソールのエラー](http://nuget.codeplex.com/workitem/335)
* [[パッケージの追加] ダイアログは、既にインストールされているパッケージのライセンスの同意を示します](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

次に、NuGet CTP 1 で修正された機能とバグの一覧を示します。

* [パッケージの拡張子の名前をに変更する必要があります。 nupack](http://nuget.codeplex.com/workitem/1)
* [パッケージファイルをフォルダーに移動する](http://nuget.codeplex.com/workitem/2)
* [マージインストール &amp; PS コマンドの追加](http://nuget.codeplex.com/workitem/3)
* [動詞と名詞のコマンドレットのエイリアスを作成する](http://nuget.codeplex.com/workitem/4)
* [VS でソリューションを切り替えるときに NuPack が混乱する](http://nuget.codeplex.com/workitem/6)
* [既定では、' パッケージ ' ソリューションフォルダーを非表示にする必要があります](http://nuget.codeplex.com/workitem/11)
* [コンテンツ項目でのトークン置換のサポートを追加します。](http://nuget.codeplex.com/workitem/12)
* [NuPack。 UI は Register-packagesource API を使用する必要があります。](http://nuget.codeplex.com/workitem/26)
* [[Nupack. Core]: パッケージをインストールする前に、パッケージをインストール済みとしてマークします。](http://nuget.codeplex.com/workitem/27)
* [ソリューションから既定のプロジェクトを削除しても、削除されたプロジェクトが既定値として表示される](http://nuget.codeplex.com/workitem/30)
* ["パッケージに既に存在するため、指定された URI にパートを追加できません。" というエラーが発生し、パッケージが失敗します。](http://nuget.codeplex.com/workitem/32)
* [Visual Studio GUI から "NuPack" 文字列を削除する](http://nuget.codeplex.com/workitem/35)
* [Apache ヘッダーを著作権 .txt ファイルに追加する](http://nuget.codeplex.com/workitem/36)
* [Register-packagesource コマンドを削除します。](http://nuget.codeplex.com/workitem/37)
* [プロファイルの読み込みで例外がスローされたときにパッケージマネージャーを使用できない](http://nuget.codeplex.com/workitem/39)
* [ps1、install. ps1 および uninstall. ps1 は追加の状態を受け取る必要があります。](http://nuget.codeplex.com/workitem/41)
* [コンソールパッケージと GUI パッケージを1つのパッケージに結合する](http://nuget.codeplex.com/workitem/42)
* [Xml 変換ロジックがルートにない XML に適用されている場合は機能しない](http://nuget.codeplex.com/workitem/43)
* [[パッケージソース設定の管理] ダイアログボックスで NuPack コンソールが更新されない](http://nuget.codeplex.com/workitem/44)
* [NuPack コンソール UI: ' パッケージフィード ' ドロップダウンリストの名前を ' パッケージソース ' に変更します](http://nuget.codeplex.com/workitem/45)
* [NuPack コンソールオプション: ' Repository UI ' の名前を NuPack コンソールと一致するように変更します](http://nuget.codeplex.com/workitem/46)
* [IIS または URL から開かれた web サイトに対してパッケージを追加できない](http://nuget.codeplex.com/workitem/53)
* [パッケージマネージャーソースが FwLink で動作しない](http://nuget.codeplex.com/workitem/55)
* [既定のパッケージソースの設定](http://nuget.codeplex.com/workitem/59)
* [オプションでパッケージソースを追加するときに、ソースが1つしか指定されていない場合は、それが既定値であると仮定します。](http://nuget.codeplex.com/workitem/60)
* [ダイアログ UI に、偽の "最近" のパッケージが表示される](http://nuget.codeplex.com/workitem/62)
* [オプション: [キャンセル] をクリックしても変更はキャンセルされない](http://nuget.codeplex.com/workitem/63)
* [パッケージ参照の追加ダイアログ検索で大文字と小文字を区別しない](http://nuget.codeplex.com/workitem/65)
* [AssemblyInfo.cs files での会社のメタデータの修正](http://nuget.codeplex.com/workitem/67)
* [VSIX のバージョン番号](http://nuget.codeplex.com/workitem/71)
* [パッケージの削除:-? を使用します。ヘルプを2回表示します](http://nuget.codeplex.com/workitem/72)
* [プロジェクトレベルパッケージのインストール/アンインストールパッケージの実行](http://nuget.codeplex.com/workitem/74)
* [1つの nupack が検証に失敗したときに、サーバーがフィードを作成できません](http://nuget.codeplex.com/workitem/90)
* [NuPack アイコンを置き換える必要があります](http://nuget.codeplex.com/workitem/94)
* [NTLM http プロキシは、パッケージフィードに対して認証を行いません。](http://nuget.codeplex.com/workitem/96)
* [ダイアログが常に VS ウィンドウの中央に表示されない](http://nuget.codeplex.com/workitem/100)
* [パッケージの詳細のフィールドの多くがダイアログに設定されていません](http://nuget.codeplex.com/workitem/102)
* [ダイアログ UI に作成者の名前が表示されない](http://nuget.codeplex.com/workitem/108)
* [理由-パッケージを削除するためのバージョン](http://nuget.codeplex.com/workitem/113)
* [ダイアログ UI の [最近使ったもの] タブを削除する](http://nuget.codeplex.com/workitem/115)
* [少なくとも1つのダイアログ UI を開いた後にソリューションフォルダーを右クリックすると、VS がクラッシュします。](http://nuget.codeplex.com/workitem/126)
* [List-Package の-Local パラメーターを-Installed に変更します。](http://nuget.codeplex.com/workitem/129)
* [Packages を NuPack に変更します。](http://nuget.codeplex.com/workitem/132)
* [コンソールでカーソルを強制的に行末にする](http://nuget.codeplex.com/workitem/135)
* [削除-パッケージの intellisense が壊れています](http://nuget.codeplex.com/workitem/136)
* [RequireLicenseAcceptance フラグを nuspec と Feed に追加します。](http://nuget.codeplex.com/workitem/137)
* [LicenseUrl を nuspec 形式およびパッケージフィードに追加する](http://nuget.codeplex.com/workitem/138)
* [[同意が必要なパッケージのインストール] をクリックすると受け入れダイアログが表示される](http://nuget.codeplex.com/workitem/139)
* [[パッケージの追加] ダイアログに免責事項のテキストを追加する](http://nuget.codeplex.com/workitem/140)
* [パッケージコンソールを初めて実行するときに免責事項を追加する](http://nuget.codeplex.com/workitem/143)
* [コンソールでパッケージをインストールした後に免責事項を表示する](http://nuget.codeplex.com/workitem/144)
* [. Nupack 拡張機能の名前を. nupack に変更します。](http://nuget.codeplex.com/workitem/146)