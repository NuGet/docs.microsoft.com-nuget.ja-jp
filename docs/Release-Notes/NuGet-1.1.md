---
title: "NuGet 1.0 および 1.1 のリリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0e7688f7-09d2-4477-9fdf-0e27f572a4de
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 1.1 のリリース ノートします。"
keywords: "NuGet 1.1 のリリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 00b6a8c6095e12ea2f4ca3fb5129d6c999071e3a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-10-and-11-release-notes"></a>NuGet 1.0 および 1.1 のリリース ノートします。

[NuGet 1.2 リリース ノート](../release-notes/nuget-1.2.md)

NuGet 1.0 は、2011 年 1 月 13 日にリリースされました。  NuGet 1.1 は、2011 年 2 月 12 日にリリースされました。

## <a name="overview"></a>概要

このドキュメントには、主要なプレビュー リリースに合わせてグループ化されている NuGet 1.0 のさまざまなリリースのリリース ノートが含まれています。

NuGet には、次のコンポーネントが含まれます。

* *NuGet.Tools.vsix* * から構成されます。
  * **ライブラリのパッケージ ダイアログ ボックスを追加*** で参照し、パッケージをインストールするために使用する Visual Studio ダイアログ ボックス。
  * **パッケージ マネージャー コンソール*** Powershell ベースの Visual Studio 内でのコンソールです。
* *NuGet コマンド ライン ツール** ツール パッケージを作成する (および最終的に発行) を使用します。

NuGet ツール Visual Studio 拡張機能 (*NuGet.Tools.vsix*) が必要です。

* Visual Studio 2010 または Visual Web Developer 2010 Express です。

NuGet コマンド ライン ツールが必要です。

* .NET framework Version 4

## <a name="installation"></a>インストール

これを使用する[最新リリース](http://nuget.codeplex.com/releases/view/52018):

* 古いビルドをまずアンインストールします。 これを行う管理者として VS を実行する必要があります。
* あるすべての既存のフィードを削除します。
* 指す新しいフィードを追加[http://go.microsoft.com/fwlink/?LinkId=206669](http://go.microsoft.com/fwlink/?LinkId=206669)です。

## <a name="nuget-11"></a>NuGet 1.1

このリリースで修正された問題の一覧[をご覧ください](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

RC 以降 RTM の 1 つの問題が修正されました。

* [ソリューション内のすべてのプロジェクトが影響を受ける 474: パッケージの削除](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>リリース候補

CTP 2 以降のこのリリース候補版で行った変更を次に示します。 バグの完全な一覧を表示する問題の追跡ツールを参照してください。

* [コンソールからのパッケージの更新、依存関係が更新されることはできません。](http://nuget.codeplex.com/workitem/443)
* [パッケージの参照 (CTP1) いない箱を追加するパッケージの取得](http://nuget.codeplex.com/workitem/442)
* [壊れた参照のまま、パッケージの更新](http://nuget.codeplex.com/workitem/440)
* [Get-package- ダイアログ ボックスで、または集計 'すべて' のソースは、コンソールで選択されると、更新プログラムが失敗しました。](http://nuget.codeplex.com/workitem/439)
* [パッケージの検証エラーを取得します。](http://nuget.codeplex.com/workitem/426)
* [パッケージの追加 ダイアログからパッケージをインストールできない場合は、ユーザーを警告する します。](http://nuget.codeplex.com/workitem/425)
* [Get-package-更新プログラムの多数のパッケージを更新するときにスローされます](http://nuget.codeplex.com/workitem/424)
* [Nuspec ファイルが正しく作成されていないときのエラーの処理を向上させる](http://nuget.codeplex.com/workitem/423)
* [Nuget パックには、指定したファイルが無視されます。](http://nuget.codeplex.com/workitem/422)
* [最後から 2 番目のパッケージ ソースを削除して、"下へ移動 をクリックし、VS がクラッシュします。](http://nuget.codeplex.com/workitem/418)
* [パッケージのインストール中にアセンブリ参照を削除します。](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException 設定 ダイアログ ボックスを開くときに](http://nuget.codeplex.com/workitem/411)
* [パッケージ マネージャー コンソールでパッケージ ソースのアクセス キーは機能しません](http://nuget.codeplex.com/workitem/410)
* [NuGet VS 設定 ダイアログのアクセス キーが不適切なフィールドにフォーカスを与える](http://nuget.codeplex.com/workitem/409)
* [パッケージ ID の intellisense は、項目が多すぎますを照会できません必要があります。](http://nuget.codeplex.com/workitem/404)
* [プロジェクト名にドット文字を含むプロジェクトにパッケージを追加できませんでした。](http://nuget.codeplex.com/workitem/403)
* [Nuspec で指定されたファイルに発行します。](http://nuget.codeplex.com/workitem/400)
* [新しいビルドを使用する場合、正しい公式フィードを登録を取得する必要があります。](http://nuget.codeplex.com/workitem/399)
* [タグが # ではなくスペースを使用する必要があります。](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata 有用な情報がないです。](http://nuget.codeplex.com/workitem/388)
* [ダイアログ ボックスに不正使用のリンクを追加します。](http://nuget.codeplex.com/workitem/386)
* [App_Data を使用して Visual Studio で改ページのパッケージを解凍するには](http://nuget.codeplex.com/workitem/380)
* [タグを実装します。](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder により、空のパッケージ作成に依存していません。](http://nuget.codeplex.com/workitem/373)
* [パッケージの所有者 フィールドを追加します。](http://nuget.codeplex.com/workitem/365)
* [言い換えれば、VSIX のツールではなく、NuGet Package Manager VSIX マニフェストを更新します。](http://nuget.codeplex.com/workitem/364)
* [パッケージの get コマンドでは、すべてのソースが選択されているときにエラーがスローされます。](http://nuget.codeplex.com/workitem/359)
* [[オプション] ダイアログでパッケージ ソースの順序付けを許可します。](http://nuget.codeplex.com/workitem/356)
* [更新プログラム パッケージは以前のバージョンを削除できません。](http://nuget.codeplex.com/workitem/352)
* [依存関係を実装するバージョン範囲の指定](http://nuget.codeplex.com/workitem/347)
* [[新しいパッケージを追加] をクリックすると、visual Studio がクラッシュします。](http://nuget.codeplex.com/workitem/346)
* [パッケージの追加のダイアログでのダウンロードと評価を表示します。](http://nuget.codeplex.com/workitem/345)
* [ダイアログ ボックスでパッケージ ソースの間で変更すると、アクティブなソースが更新されません。](http://nuget.codeplex.com/workitem/344)
* [パッケージ マネージャーのコンソール ウィンドウのキー バインドを削除します。](http://nuget.codeplex.com/workitem/339)
* [インストール パッケージは、コマンドレットの名前として認識されない.](http://nuget.codeplex.com/workitem/338)
* [ローカルの依存関係を正規のフィードのフィードからパッケージのインストールは解決されません。](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies でまだ使用されている依存関係をスキップする必要があります。](http://nuget.codeplex.com/workitem/331)
* [元のページ要求を返すときに、ユーザーが別のページに移動できないページ ナビゲーションをキャンセルする場合](http://nuget.codeplex.com/workitem/325)
* [多数のパッケージでフィードを提供しているため、NuPack.Server のパフォーマンスを調査します。](http://nuget.codeplex.com/workitem/324)
* [パッケージのフィルター処理をもう一度以前に選択したソースではなく"New で"パッケージ ソースを使用します。](http://nuget.codeplex.com/workitem/321)
* [ダイアログ ボックスで、"Online" タブを選択するときに、既定のパッケージ ソースを選択してください。](http://nuget.codeplex.com/workitem/320)
* [パッケージ一覧は、既定でインストールされているパッケージを表示する必要があります。](http://nuget.codeplex.com/workitem/309)
* [アセンブリ参照 HintPaths](http://nuget.codeplex.com/workitem/294)
* [パッケージ マネージャー コンソールを開くときに例外](http://nuget.codeplex.com/workitem/268)
* [コンソールの intellisense が全体のフィードをダウンロードします。](http://nuget.codeplex.com/workitem/259)
* ['Active' を 'default' のパッケージ ソースの名前を変更する必要があります。](http://nuget.codeplex.com/workitem/258)
* [パッケージ ソース UI: 名前/ソース フィールドが空でない場合、[ok] を押すと、新しいソースが追加する必要があります](http://nuget.codeplex.com/workitem/257)
* [インストールされているパッケージの数が多いときにダイアログがとても遅くなります。](http://nuget.codeplex.com/workitem/243)
* [厳密な名前付きのアセンブリ バインド リダイレクトをサポートします。](http://nuget.codeplex.com/workitem/238)
* [パッケージの参照を追加してください.パッケージ ソースの下へドロップを含めるための UI](http://nuget.codeplex.com/workitem/226)
* [NuPack が agnostically、構成ファイル名の構成の変換をサポートする必要があります。](http://nuget.codeplex.com/workitem/224)
* [BasePath NuPack.exe で無効にするのには、します。](http://nuget.codeplex.com/workitem/222)
* [パッケージ ソースのフォールバック動作](http://nuget.codeplex.com/workitem/204)
* [GUI でクラッシュします。](http://nuget.codeplex.com/workitem/201)
* [並べ替えの追加のパッケージ ダイアログ ボックスにオプションの追加](http://nuget.codeplex.com/workitem/179)
* [パッケージ マネージャー コンソールのクリアするショートカット キー](http://nuget.codeplex.com/workitem/174)
* [PowerConsole により NuPack コンソールが失敗するには](http://nuget.codeplex.com/workitem/166)
* [コンソールとパッケージの追加 ダイアログは、要求でユーザー エージェントを設定する必要があります。](http://nuget.codeplex.com/workitem/141)
* [ビルド内には、VSIX および NuPack.exe のバージョン番号を設定します。](http://nuget.codeplex.com/workitem/134)
* [-一般的な PowerShell パラメーターを非表示にしますか。](http://nuget.codeplex.com/workitem/118)
* [コンソール コマンドの詳細なヘルプを追加します。](http://nuget.codeplex.com/workitem/110)
* [パッケージのダイアログが現在のパッケージ ソースの選択を許可する必要がありますを追加します。](http://nuget.codeplex.com/workitem/88)
* [異なる名前空間に移動 NuPack.Core クラス](http://nuget.codeplex.com/workitem/50)
* [追加のコマンドレットに関するヘルプ](http://nuget.codeplex.com/workitem/23)
* [パッケージのダウンロード後にフィードからハッシュを確認してください。](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

CTP 2 での最も重要な変更を次に示します。

* パッケージを OData サービス エンドポイント ATOM からフィードを切り替えられます: CTP2 バージョンの NuGet をアップグレードする場合は、パッケージのソースとして、次の URL を追加することを確認する: [http://go.microsoft.com/fwlink/?LinkID=204820](http://go.microsoft.com/fwlink/?LinkID=204820)です。
* 追加パッケージ コマンドの名前を変更*Install-package*です。
* 更新、`.nuspec`形式です。 `.nuspec`形式が含まれています、 *iconUrl*をパッケージの追加 ダイアログに表示される 32 x 32 png アイコンを指定するフィールドです。 必ず、パッケージを区別するために設定します。 `.nuspec`形式も含まれています、新しい*projectUrl*フィールドの詳細については、パッケージを提供する web ページを指すように使用することができます。

このビルドは古い`.nupkg`ファイル。 Null 参照例外が発生した場合、古いを使用している`.nupkg`ファイルし、更新後にリビルドする必要があります[NuGet コマンド ライン ツール](http://nuget.codeplex.com/releases/52017/download/165468)です。

(は含まれませんバグのコードの軽微なクリーンアップなど)。 NuGet CTP 2 の修正されたバグと機能の一覧を次に示します。

* [エラー アンパック パッケージ アセンブリとアセンブリのターゲット フレームワークを指定します。](http://nuget.codeplex.com/workitem/10)
* [簡単に見つけられる NuPack コンソール ウィンドウ](http://nuget.codeplex.com/workitem/14)
* [ILMerge nupack.exe リリース](http://nuget.codeplex.com/workitem/19)
* [優れたエラーと例外処理](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core]: PackageManager がフィードに関連するエラーを適切に処理する必要があります](http://nuget.codeplex.com/workitem/28)
* [コンソールの [新規] アイコン必要があります。](http://nuget.codeplex.com/workitem/29)
* [ダイアログ ボックス内の文字列をローカライズします。](http://nuget.codeplex.com/workitem/38)
* [NuPack キャッシュにダウンロードしたメモリ内 .nupack ファイル](http://nuget.codeplex.com/workitem/40)
* [コンソールを表示するため、既定のショートカットを変更する NuPack コンソール。](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem が共通のプロパティの既定値をサポートする必要があります。](http://nuget.codeplex.com/workitem/49)
* [その nuspec を使用して 1 つだけの nuspec ファイルとフォルダーで nupack.exe を実行している必要があります。](http://nuget.codeplex.com/workitem/52)
* [[プロジェクト] メニューが表示もプロジェクト/ソリューションが読み込まれるときにありません。](http://nuget.codeplex.com/workitem/54)
* [build.cmd 場合、コードベースのクリーンな複製に失敗します。](http://nuget.codeplex.com/workitem/56)
* [更新プログラムの使用可能な機能](http://nuget.codeplex.com/workitem/57)
* [コンソールで、プロンプトを削除、ダイアログ ボックスを使用してパッケージを追加する ダイアログ ボックス。](http://nuget.codeplex.com/workitem/73)
* [[インストール] をクリックして、パッケージを追加する速度が遅くビジュアル フィードバックがないと、多くの場合](http://nuget.codeplex.com/workitem/80)
* [インストールされたパッケージのある更新プログラムを検出する方法はありません。](http://nuget.codeplex.com/workitem/82)
* [ダイアログ ボックスで、インストールされているパッケージを更新する方法はありません。](http://nuget.codeplex.com/workitem/83)
* [ダイアログ ボックスで、インストールされているパッケージをアンインストールする方法はありません。](http://nuget.codeplex.com/workitem/84)
* [&ldquo;パッケージ参照の追加&hellip;&rdquo;インストールされている参照のコンテキスト メニューに表示されます](http://nuget.codeplex.com/workitem/85)
* [コンソールからのパッケージを更新した後、インストールを示します、古いバージョンと新しいバージョンの両方](http://nuget.codeplex.com/workitem/86)
* [使用後に、ダイアログ ボックスを使用する場合は、コンソールで、アクティビティが表示されなくなります](http://nuget.codeplex.com/workitem/87)
* [クリーンアップ コマンドライン nupack.exe での解析](http://nuget.codeplex.com/workitem/89)
* [パッケージ ソースにフレンドリ名を追加します。](http://nuget.codeplex.com/workitem/98)
* [パッケージのアイコンを含むをサポートする更新プログラムの .nuspec](http://nuget.codeplex.com/workitem/103)
* [フィードの UI は、URL をコピーできません。](http://nuget.codeplex.com/workitem/105)
* [パッケージの削除エラーの処理が向上します。](http://nuget.codeplex.com/workitem/107)
* [カーソルのフォーカスに依存のコンソール ウィンドウに入力します。](http://nuget.codeplex.com/workitem/112)
* [エラー メッセージが非常になります](http://nuget.codeplex.com/workitem/116)
* [インストールされているパッケージのパッケージの削除のパフォーマンスが正しくありません。](http://nuget.codeplex.com/workitem/117)
* [パッケージ ソースがない場合に失敗したパッケージを削除します。](http://nuget.codeplex.com/workitem/119)
* [パッケージ ソースが利用できないときに、パッケージの削除が失敗しました。](http://nuget.codeplex.com/workitem/120)
* [パッケージのメタデータと、フィードのタイトルを追加します。](http://nuget.codeplex.com/workitem/125)
* [追加ソース パラメーターを指定する追加のパッケージに戻す](http://nuget.codeplex.com/workitem/127)
* [パッケージ リストが必要 - ソース パラメーター](http://nuget.codeplex.com/workitem/128)
* [更新 NuPack.Server NuPack ユーザー エージェントをダウンロード パッケージを必要とするには](http://nuget.codeplex.com/workitem/142)
* [ライセンスの同意 ダイアログは、承認を必要とするすべての依存関係のライセンスを一覧表示する必要があります。](http://nuget.codeplex.com/workitem/145)
* [フィード内でパッケージをスローするときにエラーを記録します。](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe は空に行わないように&lt;licenseurl&gt;要素](http://nuget.codeplex.com/workitem/152)
* [Get-package-パッケージの追加インストール パッケージ、および削除パッケージをアンインストール パッケージを一覧パッケージの名前を変更します。](http://nuget.codeplex.com/workitem/155)
* [Visual Studio がクラッシュしたソリューション ナビゲーターからパッケージ参照の追加のメニュー項目を使用します。](http://nuget.codeplex.com/workitem/158)
* [[利用可能なパッケージ ソース] ラベルにコロンがありません。](http://nuget.codeplex.com/workitem/160)
* [.Nuspec xml 要素の大文字と小文字一貫して camel 形式、大文字と小文字を行う](http://nuget.codeplex.com/workitem/161)
* ['Admin' ビットをオンにする必要がある NuPack VSIX のマニフェスト](http://nuget.codeplex.com/workitem/162)
* [Null 参照エラーが発生したありませんフィードとリスト パッケージを実行する場合](http://nuget.codeplex.com/workitem/164)
* [nuget.exe: 宛先パスを指定](http://nuget.codeplex.com/workitem/171)
* [Powershell エラー WinXP でパッケージの管理コンソールを開く](http://nuget.codeplex.com/workitem/175)
* [パッケージの一覧を読み込んでいるときに VS クラッシュ](http://nuget.codeplex.com/workitem/176)
* [メタ パッケージ (ファイルのみの依存関係) を許可します。](http://nuget.codeplex.com/workitem/180)
* [Powershell スクリプトを Powershell 2.0 モジュールに変換します。](http://nuget.codeplex.com/workitem/181)
* [ターゲットが指定されている場合、PathResolver はパス部分の先頭のワイルドカード文字を破棄する必要があります。](http://nuget.codeplex.com/workitem/183)
* [依存関係のないです。](http://nuget.codeplex.com/workitem/186)
* [Elmah のインストール中にエラー](http://nuget.codeplex.com/workitem/192)
* [構成の変換は正しく動作しない&lt;configsections&gt;](http://nuget.codeplex.com/workitem/194)
* [変数 ' $グローバル: projectCache' 設定されていないために、取得できません](http://nuget.codeplex.com/workitem/203)
* [NuPack パッケージ作成用の MSBuild タスクを追加します。](http://nuget.codeplex.com/workitem/205)
* [リスト パッケージは、検索フィルター処理をサポートする必要があります。](http://nuget.codeplex.com/workitem/206)
* [パッケージの作成者は、ライセンスの URL を提供する場合は、ライセンスにリンクを常に表示します。](http://nuget.codeplex.com/workitem/208)
* [パッケージの削除を使用して「アクセス拒否」不定期例外](http://nuget.codeplex.com/workitem/213)
* [単体テストが失敗して: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [ファイルのフォールバック/既定のセットの特定のフレームワークのバージョンが見つからない場合に許可します。](http://nuget.codeplex.com/workitem/223)
* [パッケージの参照を追加してください.UI は、パッケージを削除することはできません。](http://nuget.codeplex.com/workitem/225)
* [パッケージ参照のいずれかの studio がクラッシュまたは複数のプロジェクトをアンロードを追加します。](http://nuget.codeplex.com/workitem/228)
* [構成変換が web.debug.config となりますファイルを作業に表示されません。](http://nuget.codeplex.com/workitem/229)
* [カスタム パッケージで発生しない init.ps1](http://nuget.codeplex.com/workitem/237)
* [パスを feedlist に追加すると、ときに既定のボタンに設定されている [ok] を自動的に閉じる場合は ENTER を押して、](http://nuget.codeplex.com/workitem/240)
* [アンインストールしようとしています行の 2 倍しようとすると、依存関係の VS がクラッシュする。](http://nuget.codeplex.com/workitem/241)
* [パッケージの追加ダイアログ ボックスでプロジェクトの URL を表示します。](http://nuget.codeplex.com/workitem/253)
* [既定のインストールされているパッケージに追加パッケージ ダイアログ](http://nuget.codeplex.com/workitem/254)
* [パッケージの追加 ダイアログのメニュー項目を変更します。](http://nuget.codeplex.com/workitem/261)
* [名前空間とアセンブリの名前を変更します。](http://nuget.codeplex.com/workitem/274)
* [NuGet へ NuPack プロジェクトの名前変更します。](http://nuget.codeplex.com/workitem/282)
* [依存関係の一覧で、次のテキストを追加します。](http://nuget.codeplex.com/workitem/288)
* [ライセンスの同意 ダイアログでライセンスの同意テキストを変更します。](http://nuget.codeplex.com/workitem/291)
* [パッケージの一覧の上のライセンスの同意 ダイアログにテキストを変更します。](http://nuget.codeplex.com/workitem/292)
* [OData は、fwlink URL を使用しません。](http://nuget.codeplex.com/workitem/304)
* [ページングに使用されるパッケージ数のキャッシュの活用経由でパッケージ マネージャー UI:](http://nuget.codeplex.com/workitem/317)
* [NuPack/NuGet -&gt;パッケージ マネージャー コンソールのエラー](http://nuget.codeplex.com/workitem/335)
* [パッケージのダイアログは、ライセンスへの同意を既にインストールされているパッケージを示しています。 追加](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

機能と NuGet CTP 1 の修正されたバグの一覧を次に示します。

* [.Nupack にパッケージの拡張機能の名前を変更する必要があります。](http://nuget.codeplex.com/workitem/1)
* [パッケージ ファイルをフォルダーに移動します。](http://nuget.codeplex.com/workitem/2)
* [インストールをマージ&amp;追加 PS コマンド](http://nuget.codeplex.com/workitem/3)
* [動詞-名詞コマンドレットの別名を作成します。](http://nuget.codeplex.com/workitem/4)
* [VS でソリューションを切り替えるときに混乱 NuPack](http://nuget.codeplex.com/workitem/6)
* [既定では、'packages' ソリューションのフォルダーを非表示にする必要があります。](http://nuget.codeplex.com/workitem/11)
* [コンテンツ項目には、トークンの置換後のサポートを追加します。](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI は、PackageSource API を使用する必要があります。](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core]: PackageManager は、それらをインストールする前にインストールされているパッケージをマーク](http://nuget.codeplex.com/workitem/27)
* [ソリューションから削除する既定のプロジェクトをであっても、削除されたプロジェクトとして既定値](http://nuget.codeplex.com/workitem/30)
* [「パートを追加できません、指定された URI のパッケージされているためです」で新しいパッケージが失敗します。](http://nuget.codeplex.com/workitem/32)
* [Visual Studio の GUI から"NuPack"文字列を削除します。](http://nuget.codeplex.com/workitem/35)
* [COPYRIGHT.txt に Apache ヘッダー ファイルを追加します。](http://nuget.codeplex.com/workitem/36)
* [更新 PackageSource コマンドを削除します。](http://nuget.codeplex.com/workitem/37)
* [パッケージ マネージャーを使用できないのは、プロファイルの読み込み時に、例外をスローします。](http://nuget.codeplex.com/workitem/39)
* [init.ps1、install.ps1 および uninstall.ps1 追加の状態を受信する必要があります。](http://nuget.codeplex.com/workitem/41)
* [コンソールとフル インストール パッケージを 1 つのパッケージに結合します。](http://nuget.codeplex.com/workitem/42)
* [ルートにない場合は XML に適用されている場合、Xml 変換ロジックは動作しません。](http://nuget.codeplex.com/workitem/43)
* [パッケージ ソース設定 ダイアログ ボックスを更新しないように、NuPack コンソールの管理します。](http://nuget.codeplex.com/workitem/44)
* [NuPack コンソール UI: 'パッケージ ソース' に 'パッケージ フィード' ドロップダウン リストの名前を変更します。](http://nuget.codeplex.com/workitem/45)
* [NuPack コンソールのオプション: NuPack コンソールと一致するように ' リポジトリ UI' の名前を変更します。](http://nuget.codeplex.com/workitem/46)
* [IIS または URL が開かれた web サイトに対する失敗したパッケージの追加](http://nuget.codeplex.com/workitem/53)
* [パッケージ マネージャーのソースは、FwLink を使用しません。](http://nuget.codeplex.com/workitem/55)
* [既定のパッケージ ソースを設定します。](http://nuget.codeplex.com/workitem/59)
* [オプションでパッケージ ソースを追加する、1 つのソースが指定されると、ときに、既定値であると仮定します。](http://nuget.codeplex.com/workitem/60)
* [ダイアログの UI は、偽の「最新」パッケージを示しています。](http://nuget.codeplex.com/workitem/62)
* [オプション: [キャンセル] をクリックすると取り消されませんの変更](http://nuget.codeplex.com/workitem/63)
* [パッケージの参照ダイアログの検索は大文字小文字を区別する必要がありますを追加します。](http://nuget.codeplex.com/workitem/65)
* [AssemblyInfo.cs ファイルに会社のメタデータを修正します。](http://nuget.codeplex.com/workitem/67)
* [VSIX のバージョン番号](http://nuget.codeplex.com/workitem/71)
* [パッケージの削除: を使用するのですか。2 回ヘルプを表示](http://nuget.codeplex.com/workitem/72)
* [プロジェクト レベルのパッケージのインストール/アンインストール パッケージを実行します。](http://nuget.codeplex.com/workitem/74)
* [サーバーは 1 つ nupack 検証に失敗したときに、フィードを作成できません。](http://nuget.codeplex.com/workitem/90)
* [NuPack アイコンを置き換える必要があります。](http://nuget.codeplex.com/workitem/94)
* [NTLM http プロキシをパッケージ フィードを認証しません。](http://nuget.codeplex.com/workitem/96)
* [ダイアログしない常に中央揃え、VS のウィンドウで起動します。](http://nuget.codeplex.com/workitem/100)
* [パッケージの詳細のフィールドの多くはダイアログ ボックスで設定されていません。](http://nuget.codeplex.com/workitem/102)
* [ダイアログの UI は著作者の名前を表示しません。](http://nuget.codeplex.com/workitem/108)
* [なぜ - パッケージの削除用のバージョン](http://nuget.codeplex.com/workitem/113)
* [ダイアログの UI の最新のタブを削除します。](http://nuget.codeplex.com/workitem/115)
* [VS クラッシュ時に適切では、少なくとも 1 つにダイアログの UI を開いた後にソリューション フォルダーをクリックします。](http://nuget.codeplex.com/workitem/126)
* [変更リスト パッケージの場合は、ローカル パラメーター-インストール](http://nuget.codeplex.com/workitem/129)
* [Packages.xml NuPack.config に名前の変更します。](http://nuget.codeplex.com/workitem/132)
* [コンソールは、行の末尾にカーソルを強制的します。](http://nuget.codeplex.com/workitem/135)
* [パッケージの削除の intellisense が壊れています。](http://nuget.codeplex.com/workitem/136)
* [RequireLicenseAcceptance フラグ .nuspec とフィードを追加します。](http://nuget.codeplex.com/workitem/137)
* [フィードの .nuspec 形式およびパッケージの LicenseUrl を追加します。](http://nuget.codeplex.com/workitem/138)
* [Acceptance ダイアログ ボックスを表示する承認を必要とするパッケージのインストール をクリックする必要があります。](http://nuget.codeplex.com/workitem/139)
* [パッケージの追加のダイアログを免責事項のテキストを追加します。](http://nuget.codeplex.com/workitem/140)
* [追加の免責事項ときのパッケージ コンソールが実行されて初めて](http://nuget.codeplex.com/workitem/143)
* [コンソールでパッケージをインストールした後の免責事項を表示します。](http://nuget.codeplex.com/workitem/144)
* [これは .nupkg .nupack 拡張子を変更します。](http://nuget.codeplex.com/workitem/146)