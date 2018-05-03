---
title: NuGet 2.6 リリース ノート
description: WebMatrix の既知の問題、バグの修正、追加された機能は、Dcr などの NuGet 2.6.1 のリリース ノートです。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39ce6ac3d36464d26966b0dabb0893f09ad4afdc
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-26-release-notes"></a>NuGet 2.6 リリース ノート

[NuGet 2.5 リリース ノート](../release-notes/nuget-2.5.md) | [WebMatrix のリリース ノートについては、NuGet 2.6.1](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 は、2013 年 6 月 26 日にリリースされました。

## <a name="notable-features-in-the-release"></a>リリースで注目に値する機能

### <a name="support-for-visual-studio-2013"></a>Visual Studio 2013 のサポート

NuGet 2.6 は、Visual Studio 2013 のサポートを提供する最初のリリースです。 および Visual Studio のすべてのエディションの Visual Studio 2012 と同様に、NuGet Package Manager 拡張機能が含まれます。

まだ Visual Studio 2010 と Visual Studio 2012 の両方をサポートをできるだけ小さく拡張サイズを保持する方法の中に Visual Studio 2013 の最大限のサポートを提供するのには、中に Visual Studio 2013 用の別個の拡張機能を作成する、元の拡張子は、Visual Studio 2010 および 2012 の両方を対象に続行します。

NuGet 2.6 以降では、次に示す 2 つの拡張機能が公開します。

1. [NuGet Package Manager](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (Visual Studio 2010 および 2012 に適用されます)
1. [Visual Studio 2013 用の NuGet パッケージ マネージャー](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

この分割と、 [nuget.org](https://nuget.org)ホーム ページの"NuGet のインストール"ボタンに移動、 [NuGet をインストールする](../install-nuget-client-tools.md) ページで、さまざまな NuGet クライアントのインストールに関する詳細についてを見つけることができます。

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>XDT Web.config 変換のサポート

Visual Studio のビルド構成の変換で使用されている XDT 変換エンジンを使用してより強力な XML 変換をサポートするために、NuGet クライアントの高から要求された機能の 1 つがされました。

2013 年 4 月、XDT 用の NuGet のサポートに関する 2 つの大規模なお知らせを行いました。 1 つでした XDT ライブラリ自体はされていた自体[NuGet パッケージとしてリリース](https://nuget.org/packages/Microsoft.Web.Xdt)と[CodePlex でのオープン ソース](http://xdt.codeplex.com/)です。 この手順は、NuGet クライアントを含む、他のオープン ソース ソフトウェアで自由に使用する XDT エンジンを有効になります。 次のお知らせは、NuGet クライアントでの変換に XDT エンジンの使用をサポートするために、プランをでした。 NuGet 2.6 には、この統合が含まれています。

#### <a name="how-it-works"></a>しくみ

NuGet の XDT サポートを利用するしくみについては、検索と同様、[現在の構成変換機能](../create-packages/source-and-config-file-transformations.md)します。
変換ファイルは、パッケージのコンテンツ フォルダーに追加されます。 ただし、構成の変換は、インストールとアンインストールの両方の 1 つのファイルを使用して、XDT 変換は、次のファイルを使用してこれらのプロセスの両方に対して、きめ細かい制御を有効にします。

- Web.config.install.xdt
- Web.config.uninstall.xdt

さらに、NuGet はファイルのサフィックスを使用して既存 web.config.transforms を使用してパッケージを正しく動作させるための変換を実行するには、どのエンジンを確認します。 XDT 変換は、任意の XML ファイル (だけでなく、web.config ファイル) にも適用できますこのに他のアプリケーション プロジェクトで利用できるようにします。

#### <a name="what-you-can-do-with-xdt"></a>XDT で行うことができます。

XDT の大きなメリットの 1 つは、その[簡易かつ強力な構文](http://msdn.microsoft.com/library/dd465326.aspx)XML DOM の構造を操作します。 別の構造に 1 つの固定のドキュメントの構造を単純にオーバーレイするではなく XDT は一致するさまざまな名前の一致条件を完全な XPath のサポートを単純な属性からの方法で要素のコントロールを提供します。 つまり、追加、更新、または属性の削除、特定の場所に新しい要素を配置することまたは交換または全体を削除するかどうか、XDT が、要素を操作する豊富な一連の関数を提供、一致する要素または要素のセットが見つかると、要素とその子要素です。

### <a name="machine-wide-configuration"></a>コンピューター全体の構成

NuGet の優れた長所の 1 つが、それ以外の場合の大きな実行可能ファイルまたはライブラリにできる、統合された最も重要なメンテナンスとバージョン管理された個別にモジュール型のコンポーネントのセットを中断します。 これには、副作用の 1 つがの製品または製品ファミリの従来のアイデアがより断片化可能性のあります。
NuGet のカスタム パッケージのソース機能は、パッケージを整理するための 1 つの方法を提供します。ただし、カスタムのパッケージ ソースは、単独で検出可能ではありません。

NuGet 2.6 では、パス %programdata%/nuget/config 下のフォルダー階層を検索して NuGet を構成するためのロジックを拡張します。製品インストーラーには、自社製品のカスタム パッケージ ソースを登録するには、このフォルダーの下のカスタムの NuGet 構成ファイルを追加できます。 さらに、フォルダー構造は、製品、バージョン、および IDE の偶数の SKU のセマンティクスをサポートします。 これらのディレクトリからの設定は、"wins"で最後の優先順位戦略は、次の順序で適用されます。

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{Version}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*.config

この一覧で、{IDE} プレース ホルダーは、"VisualStudio"の場合は、Visual Studio できるように、NuGet が実行されている IDE に固有です。 {バージョン} と {SKU} プレース ホルダーが (たとえば、IDE によって提供されます。「11.0」と"WDExpress"、"VWDExpress"、"Pro"それぞれ)。 フォルダーでは、多くの異なる *.config ファイルを含めることができますし、します。
したがって、ACME コンポーネント会社の一部として、製品インストーラー、カスタム パッケージ ソースの追加、次のファイル パスを作成して Visual Studio 2012 の Professional、および Ultimate バージョンでのみ表示されます。

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

フォルダー構造では、NuGet の構成にコンピューター全体のパッケージ ソースを追加するソフトウェア インストーラーなどのプログラムに簡単です、中に、NuGet の構成ダイアログ ボックスが更新されとしてパッケージ ソースの登録を許可するにはいずれかのユーザー固有 (例: %appdata%/nuget/nuget.config で登録されている) またはコンピューター全体です。

ファイルがインストールされている Visual Studio 2013 でこの機能を利用するとします。

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

このファイルでは「.NET Framework パッケージ」と呼ばれる新しいパッケージ ソースが構成されています。

![NuGet Config ファイル マシン全体の設定](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>検索を付けた

NuGet ギャラリーで処理されたパッケージの数が指数のペースで拡大するように NuGet の優先度リストの上部にあることは検索を向上します。 NuGet の計画的な機能の 1 つは、コンテキストにより検索、つまり、潜在的な検索の妥当性を決定するための条件として NuGet は、バージョンと SKU の Visual Studio を使用していること、およびビルドするプロジェクトの種類に関する情報を使用結果。

NuGet 2.6 以降では、パッケージをインストールするたびに、インストールのコンテキストとして記録されますインストール操作データの一部。  検索では、コンテキストのインストールの傾向で検索結果を向上させる NuGet ギャラリーで、同じコンテキスト情報も送信します。  NuGet ギャラリーへの今後の更新プログラムは、この状況に応じた関連性の向上を有効になります。

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Vs の直接インストールを追跡します。依存関係のインストール

パッケージ作成者は、証明書利用者のより多くの[パッケージ統計](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html)NuGet ギャラリーで提供します。  大量の不足しているデータ ポイントの作成者ご要望を 1 つは、直接パッケージをインストールし、依存関係のインストールとの違いです。  これまでは、NuGet クライアントは、開発者が直接パッケージをインストールするかどうか、または依存関係を満たすためにインストールされているかどうかのインストール操作を囲むすべてのコンテキストを送信しませんでした。
データがそのインストール操作の今すぐ送信されることを NuGet 2.6 で開始しています。  NuGet ギャラリー パッケージの統計情報がそのデータとして公開する、別のインストール操作で、"-依存関係"サフィックス。

* インストール
* 依存関係のインストール
* 更新
* 依存関係の更新
* 再インストール
* 依存関係の再インストール

異なる操作名に加えて、依存パッケージ id をインストールするためにも記録されます。  NuGet ギャラリーへの今後の更新では、パッケージ作成者は、開発者がそのパッケージをインストールする方法を十分に理解できるように、レポート内でそのデータを公開します。

## <a name="bug-fixes"></a>バグ修正

NuGet 2.6 には、いくつかのバグ修正も含まれています。 作業の完全な一覧アイテムを固定 NuGet 2.6 にしてください。 ビュー、[今回のリリースの NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)です。