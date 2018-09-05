---
title: NuGet 2.6 リリース ノート
description: NuGet 2.6.1 の既知の問題、バグの修正、追加機能、および Dcr を含む WebMatrix のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f011a8db7ac2067a2ed7db67849d63f7dd40d1ce
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551944"
---
# <a name="nuget-26-release-notes"></a>NuGet 2.6 リリース ノート

[NuGet 2.5 リリース ノート](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 for WebMatrix のリリース ノート](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 は、2013 年 6 月 26 日にリリースされました。

## <a name="notable-features-in-the-release"></a>リリースで注目すべき機能

### <a name="support-for-visual-studio-2013"></a>Visual Studio 2013 のサポート

NuGet 2.6 は、Visual Studio 2013 のサポートを提供する最初のリリースです。 Visual Studio のすべてのエディションの Visual Studio 2012 のように、NuGet パッケージ マネージャー拡張機能が含まれています。

まだ Visual Studio 2010 と Visual Studio 2012 の両方をサポートしていると、拡張サイズをできるだけ小さく維持する方法の中に Visual Studio 2013 の最高レベルのサポートを提供するためには、中に Visual Studio 2013 用の別個の拡張機能を作成する、Visual Studio 2010 と 2012 の両方をターゲットに元の拡張子が続行されます。

NuGet 2.6 以降では、次の 2 つの拡張機能を発行します。

1. [NuGet パッケージ マネージャー](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (Visual Studio 2010 および 2012 に適用されます)
1. [Visual Studio 2013 用の NuGet パッケージ マネージャー](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

この分割は、 [nuget.org](https://nuget.org)ホーム ページの"NuGet のインストール"ボタンに移動、 [NuGet をインストールする](../install-nuget-client-tools.md)ページで、詳細については、さまざまな NuGet クライアントをインストールする方法を見つけることができます。

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>XDT Web.config 変換のサポート

NuGet クライアントの高度から要求された機能の 1 つは、Visual Studio のビルド構成の変換で使用されている、XDT 変換エンジンを使用してより強力な XML の変換をサポートするようにしています。

2013 年 4 月には、XDT の NuGet サポートに関する 2 つの大規模なお知らせを行いました。 最初は、XDT ライブラリ自体はされていた自体[NuGet パッケージとしてリリース](https://nuget.org/packages/Microsoft.Web.Xdt)と[CodePlex でのオープン ソース](http://xdt.codeplex.com/)します。 この手順では、NuGet クライアントを含むその他のオープン ソース ソフトウェアで自由に使用される、XDT エンジンが有効になります。 2 番目のお知らせは、NuGet クライアントでの変換、XDT エンジンの使用をサポートするために、プランをしました。 NuGet 2.6 には、この統合が含まれています。

#### <a name="how-it-works"></a>しくみ

NuGet の XDT サポートを利用するしくみは検索のと同様、 [config 変換機能を現在](../create-packages/source-and-config-file-transformations.md)します。
変換ファイルは、パッケージのコンテンツのフォルダーに追加されます。 ただし、構成の変換では、1 つのファイルを使用してのインストールおよびアンインストールの両方、XDT 変換には、次のファイルを使用してこれらのプロセスの両方を詳細に制御が有効にします。

- Web.config.install.xdt
- Web.config.uninstall.xdt

さらに、NuGet はファイルのサフィックスを使用して既存 web.config.transforms を使用してパッケージは引き続き機能するための変換を実行するには、どのエンジンを確認します。 XDT 変換は、XML ファイル (だけでなく web.config) にも適用できますこのに他のアプリケーション プロジェクトで利用できるようにします。

#### <a name="what-you-can-do-with-xdt"></a>XDT を行うことができます。

XDT の最大の強みの 1 つはその[単純ながらも強力な構文](http://msdn.microsoft.com/library/dd465326.aspx)XML DOM の構造を操作します。 別の構造に 1 つの固定ドキュメントの構造を単純にオーバーレイではなく XDT はさまざまな方法は、完全な XPath をサポートする単純な属性名が一致するから内の要素を照合するコントロールを提供します。 一致する要素または要素のセットが見つかった後、XDT 関数の豊富な操作を提供します、要素の追加、更新、または属性の削除、特定の場所に新しい要素を配置することまたは交換または全体を削除することを意味するかどうか要素とその子。

### <a name="machine-wide-configuration"></a>コンピューター全体の構成

NuGet のすばらしい強みの 1 つは、それ以外の場合の大きな実行可能ファイルまたはライブラリできる統合と最も重要なは維持され、バージョン管理された独立してモジュラー コンポーネントのセットに分割します。 この、1 つの副作用は製品または製品ファミリの従来の考え方がより断片化可能性があります。
NuGet のカスタム パッケージのソースの機能は、パッケージを整理するための 1 つの方法を提供します。ただし、カスタム パッケージのソースは、自分で検出可能ではありません。

NuGet 2.6 では、パス %programdata%/nuget/config フォルダー階層を検索して NuGet を構成するためのロジックを拡張します。製品インストーラーには、自社製品のカスタム パッケージのソースを登録するには、このフォルダーの下にカスタムの NuGet 構成ファイルを追加できます。 さらに、フォルダー構造は、製品、バージョン、および IDE の偶数の SKU のセマンティクスをサポートします。 これらのディレクトリからの設定は、"wins"では最後の優先順位戦略では、次の順序で適用されます。

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{Version}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*.config

この一覧で、{IDE} プレース ホルダーは、Visual Studio の場合"VisualStudio"になるように、NuGet が実行されている IDE に固有です。 {バージョン} (例: {SKU} プレース ホルダーを IDE によって提供されると"11.0":"WDExpress"、"VWDExpress"と"Pro"でそれぞれ)。 フォルダーには、多くの異なる *.config ファイルし、含めることができます。
そのため、ACME コンポーネント会社、製品インストーラーの一部としてソースを追加できますカスタム パッケージ、次のファイル パスを作成して Visual Studio 2012 の Professional、および Ultimate バージョンでのみ表示されます。

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

パッケージ ソースとしての登録を許可する、NuGet の構成ダイアログ ボックスが更新されてもフォルダー構造を使用する NuGet の構成にコンピューター全体のパッケージ ソースを追加するソフトウェア インストーラーのようなプログラムの簡単です、(例: %appdata%/nuget/nuget.config で登録されている) かユーザー固有またはコンピューター全体に適用します。

この機能は、Visual Studio 2013 でのファイルがインストールされているによって使用されています。

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

このファイルでは、「.NET Framework パッケージ」と呼ばれる新しいパッケージ ソースが構成されます。

![NuGet 構成ファイルのマシン全体の設定](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>検索のコンテキスト化

NuGet ギャラリーで提供されるパッケージの数は、指数のペースで成長を続けるは検索を改善する NuGet の優先度リストの上部にあるこれまでに残ります。 コンテキスト検索、つまり、潜在的な検索の妥当性を判断するための条件として NuGet は、バージョンと SKU の Visual Studio を使用している、およびビルドするプロジェクトの種類について使用して NuGet の計画的な機能の 1 つです。結果。

NuGet 2.6 以降、パッケージをインストールするたびに、インストールのコンテキストとして記録されます、インストール操作のデータの一部。  検索では、コンテキストのインストールの傾向によって検索結果を向上させるため、NuGet ギャラリーで、同じコンテキスト情報も送信します。  今後の更新プログラム、NuGet ギャラリーでは、この状況依存の関連性の向上を有効になります。

### <a name="tracking-direct-installs-vs-dependency-installs"></a>追跡との直接インストールされます。依存関係のインストール

上のパッケージの作成者はより証明書利用者、[パッケージ統計](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html)NuGet ギャラリーで提供します。  重要な不足しているデータ ポイントの作成者が求めている 1 つは、直接パッケージをインストールし、依存関係のインストールとの違いです。  これまで、NuGet クライアントは、開発者が直接パッケージをインストールするかどうか、または依存関係を満たすためにインストールされているかどうか、インストール操作を任意のコンテキストを送信しませんでした。
NuGet 2.6 以降、データがインストール操作で送信されるようになりましたが。  NuGet ギャラリーにパッケージの統計情報はで、独立したインストール操作としてそのデータを公開するは、"-依存関係"サフィックス。

* インストール
* 依存関係のインストール
* 更新
* 依存関係の更新
* 再インストール
* 依存関係を再インストール

別の操作の名前だけでなく依存パッケージ id は、インストールも記録されます。  今後の更新プログラム、NuGet ギャラリーでは、パッケージ作成者を開発者がそれらのパッケージをインストールする方法を完全に理解できるように、レポート内でそのデータを公開します。

## <a name="bug-fixes"></a>バグ修正

NuGet 2.6 には、いくつかのバグ修正も含まれています。 作業の完全な一覧の項目で修正された NuGet 2.6 では、くださいビュー、[このリリースの NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)します。