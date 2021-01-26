---
title: NuGet 2.6 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む、NuGet 2.6.1 向けのリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 812a0e806e29c5a2141db4f2fbab4bf91b0983f9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776832"
---
# <a name="nuget-26-release-notes"></a>NuGet 2.6 リリースノート

[NuGet 2.5 リリースノート](../release-notes/nuget-2.5.md)  | [WebMatrix の NuGet 2.6.1 のリリースノート](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 は、2013年6月26日にリリースされました。

## <a name="notable-features-in-the-release"></a>リリースの注目すべき機能

### <a name="support-for-visual-studio-2013"></a>Visual Studio 2013 のサポート

NuGet 2.6 は Visual Studio 2013 のサポートを提供する最初のリリースです。 また、Visual Studio 2012 と同様に、NuGet パッケージマネージャー拡張機能は Visual Studio のすべてのエディションに含まれています。

Visual Studio 2010 と Visual Studio 2012 の両方を引き続きサポートし、拡張のサイズを可能な限り小さく保つために、Visual Studio 2013 用に個別の拡張機能を作成していますが、元の拡張機能は Visual Studio 2010 と2012の両方を対象としています。 Visual Studio 2013

NuGet 2.6 以降、次のように2つの拡張機能を公開します。

1. [NuGet パッケージマネージャー](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (Visual Studio 2010 および2012に適用されます)
1. [Visual Studio 2013 用の NuGet パッケージマネージャー](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

この分割では、 [nuget.org](https://nuget.org) ホームページの [Nuget のインストール] ボタンをクリックすると、[ [nuget](../install-nuget-client-tools.md) のインストール] ページが表示されます。このページでは、さまざまな nuget クライアントのインストールに関する詳細情報を確認できます。

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>XDT Web.config 変換のサポート

NuGet クライアントで最も要求の高い機能の1つは、Visual Studio ビルド構成の変換で使用される XDT 変換エンジンを使用して、より強力な XML 変換をサポートすることでした。

2013年4月に、XDT の NuGet サポートに関して2つの大きな発表を行いました。 1つ目は、XDT ライブラリ自体が [NuGet パッケージとしてリリース](https://nuget.org/packages/Microsoft.Web.Xdt) され、 [CodePlex でオープンソース](http://xdt.codeplex.com/)になっていることでした。 この手順では、他のオープンソースソフトウェア (NuGet クライアントを含む) で XDT エンジンを自由に使用できるようになりました。 2番目の発表は、NuGet クライアントでの変換のための XDT エンジンの使用をサポートする計画でした。 NuGet 2.6 には、この統合が含まれています。

#### <a name="how-it-works"></a>しくみ

NuGet の XDT サポートを活用するために、このしくみは、 [現在の構成変換機能](../create-packages/source-and-config-file-transformations.md)に似ています。
変換ファイルは、パッケージのコンテンツフォルダーに追加されます。 ただし、構成変換では、インストールとアンインストールの両方に1つのファイルが使用されますが、XDT 変換では、次のファイルを使用して、両方のプロセスをきめ細かく制御できます。

- Web.config. install. xdt
- Web.config。 xdt

また、NuGet はファイルサフィックスを使用して変換を実行するエンジンを決定するため、既存の web.config を使用するパッケージは引き続き機能します。 XDT 変換は、web.config だけでなく) 任意の XML ファイルにも適用できます。これにより、プロジェクト内の他のアプリケーションに対してこれを活用できます。

#### <a name="what-you-can-do-with-xdt"></a>XDT でできること

XDT の最大の強みの1つは、XML DOM の構造を操作するための [単純で強力な構文](/previous-versions/aspnet/dd465326(v=vs.110)) です。 XDT では、1つの固定ドキュメント構造を別の構造に単にオーバーレイするのではなく、単純な属性名の照合から完全な XPath サポートまで、さまざまな方法で要素を照合するためのコントロールを提供します。 一致する要素または要素のセットが見つかった場合、XDT は、要素を操作するための豊富な機能セットを提供します。これは、属性の追加、更新、または削除、特定の場所への新しい要素の配置、または要素全体とその子の置換または削除を意味します。

### <a name="machine-wide-configuration"></a>Machine-Wide 構成

NuGet の優れた利点の1つは、それ以外の大規模な実行可能ファイルまたはライブラリをモジュール式のセットに分割することです。これらのコンポーネントは統合可能で、ほとんどの場合、個別に管理およびバージョン管理できます。 ただし、このような副作用の1つは、製品または製品ファミリの従来の考え方がより複雑になる可能性があるということです。
NuGet のカスタムパッケージソース機能は、パッケージを整理するための1つの方法を提供します。ただし、カスタムパッケージソースは独自に検出できません。

NuGet 2.6 では、パス% ProgramData%/NuGet/Config. でフォルダー階層を検索して、NuGet を構成するためのロジックを拡張します。製品インストーラーでは、このフォルダーにカスタムの NuGet 構成ファイルを追加して、製品用のカスタムパッケージソースを登録できます。 さらに、フォルダー構造は、IDE の製品、バージョン、および SKU のセマンティクスをサポートしています。 これらのディレクトリからの設定は、"last in wins" 優先順位戦略に従って次の順序で適用されます。

1. % Programdata% \N ugetconfig \* .config
2. % Programdata% \N ugetconfig \{ IDE} \* .config
3. % Programdata% \N ugetconfig \{ IDE} \{ バージョン} \* .config
4. % Programdata% \N ugetconfig \{ IDE} \{ バージョン} \{ SKU} \* .config

この一覧では、{IDE} プレースホルダーは NuGet が実行されている IDE に固有であるため、Visual Studio の場合は "VisualStudio" になります。 {Version} と {SKU} プレースホルダーは、IDE によって提供されています (例: "11.0"、"WDExpress"、"VWDExpress"、"Pro" など)。 このフォルダーには、さまざまな * .config ファイルを含めることができます。
そのため、ACME コンポーネント会社は、製品インストーラーの一部として、次のファイルパスを作成することによって、Visual Studio 2012 の Professional および Ultimate バージョンでのみ表示されるカスタムパッケージソースを追加できます。

% ProgramData% \NuGet\Config\VisualStudio\11.0\Pro\acme.config

フォルダー構造は、コンピューター全体のパッケージソースを NuGet の構成に追加するソフトウェアインストーラーなどのプログラムにとっては簡単ですが、[NuGet の構成] ダイアログも更新され、ユーザー固有 (% AppData%/NuGet/NuGet.Config に登録されているなど) またはコンピューター全体にパッケージソースを登録できるようになりました。

この機能は Visual Studio 2013 によって使用されます。この場合、ファイルは次の場所にインストールされます。

% ProgramData% \NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

このファイル内には、".NET Framework Packages" という名前の新しいパッケージソースが構成されています。

![NuGet 構成ファイルコンピューター全体の設定](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>身検索

NuGet ギャラリーによって提供されるパッケージの数は指数関数的に増加し続けているため、NuGet の優先度リストの上部には、検索の向上が続きます。 NuGet の予定されている機能の1つはコンテキスト検索です。つまり、NuGet では、使用している Visual Studio のバージョンと SKU に関する情報と、候補となる検索結果の関連性を判断するための条件として構築するプロジェクトの種類に関する情報が使用されます。

NuGet 2.6 以降では、パッケージがインストールされるたびに、インストールのコンテキストがインストール操作データの一部として記録されます。  検索でも同じコンテキスト情報が送信されます。これにより、NuGet ギャラリーはコンテキストのインストール傾向によって検索結果を向上させることができます。  今後、NuGet ギャラリーを更新することで、この状況に応じた関連性が向上します。

### <a name="tracking-direct-installs-vs-dependency-installs"></a>直接インストールと依存関係のインストールの追跡

パッケージの作成者は、NuGet ギャラリーで提供されている [パッケージの統計情報](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) によって、より多くの情報を利用できます。  作成者が要求した重要なデータポイントの1つに、パッケージの直接インストールと依存関係のインストールの違いがあります。  これまでは、NuGet クライアントは、開発者がパッケージを直接インストールしたかどうか、または依存関係を満たすためにインストールされたかどうかについて、インストール操作に関するコンテキストを一切送信しませんでした。
NuGet 2.6 以降、このデータはインストール操作のために送信されるようになります。  NuGet ギャラリーのパッケージ統計は、"-Dependency" サフィックスを使用して、そのデータを個別のインストール操作として公開します。

* インストール
* Install-Dependency
* 更新
* Update-Dependency
* 再インストール
* Reinstall-Dependency

異なる操作名に加えて、依存パッケージ id もインストール用に記録されます。  NuGet ギャラリーの今後の更新では、レポート内でそのデータが公開されるため、パッケージの作成者はパッケージのインストール方法を完全に理解できます。

## <a name="bug-fixes"></a>バグの修正

NuGet 2.6 には、いくつかのバグ修正も含まれています。 NuGet 2.6 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)を参照してください。