---
title: セキュリティで保護されたソフトウェア サプライ チェーンのベスト プラクティス
description: NuGet と GitHub を使用してソフトウェア サプライ チェーンをセキュリティで保護するためのベスト プラクティス。
author: JonDouglas
ms.author: jodou
ms.date: 02/08/2021
ms.topic: conceptual
ms.openlocfilehash: 4575d4779ed90150cec667489c85875b7fb87a8d
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726978"
---
# <a name="best-practices-for-a-secure-software-supply-chain"></a>セキュリティで保護されたソフトウェア サプライ チェーンのベスト プラクティス

オープンソースはあらゆる場所にあります。 多くの独自のコードベースやコミュニティ プロジェクトに含まれています。 現在、組織や個人が確認しなければならないのは、オープンソース コードを使用しているかどうかではなく、どのようなオープンソース コードをどれくらい使用しているかということです。

ソフトウェア サプライ チェーンの内容を把握していないと、上流の依存関係のいずれかに致命的な脆弱性があった場合、企業やその顧客が潜在的な侵害に対して脆弱になる可能性があります。 このドキュメントでは、"ソフトウェア サプライ チェーン" という用語の意味、その重要性、プロジェクトのサプライ チェーンをベスト プラクティスで保護する方法について詳しく説明します。

![The State of the Octoverse 2020 - オープンソース](media/opensource-percent.png)

## <a name="dependencies"></a>依存関係 

ソフトウェア サプライ チェーンとは、ご利用のソフトウェアに組み込まれるすべてのものと、それがどこから来たのかを示すために使用される用語です。 それは、ソフトウェア サプライ チェーンが依存している依存関係と、依存関係のプロパティです。 依存関係とは、ソフトウェアが実行する必要があるものです。 コード、バイナリ、またはその他のコンポーネントと、その取得元の場所 (リポジトリやパッケージ マネージャーなど) である場合があります。

それには、誰がコードを作成したか、いつ投稿されたか、セキュリティの問題がどのように確認されたか、既知の脆弱性、サポートされているバージョン、ライセンス情報、およびプロセスの任意の時点でそれに関係するすべてのものが含まれます。

また、サプライ チェーンには、ビルドとパッケージ化のスクリプトや、アプリケーションが依存するインフラストラクチャを実行しているソフトウェアなど、1 つのアプリケーションの範囲を超えるスタックの他の部分も含まれています。

## <a name="vulnerabilities"></a>脆弱性

現在、ソフトウェアの依存関係は広く利用されています。 プロジェクトの機能に多数のオープンソースの依存関係を使用したので、自分で作成する必要がなかった、というのは非常によくあることです。 これは、アプリケーションのほとんどの部分が、自分で作成したものではないコードで構成されていることを意味する可能性があります。 

![The State of the Octoverse 2020 - 依存関係](media/dependencies.png)

サードパーティやオープンソースの依存関係に含まれる可能性のある脆弱性は、おそらく、自分で作成したコードほど厳しく制御することができない依存関係であり、これによりサプライ チェーンに潜在的なセキュリティ リスクが生じる可能性があります。

このような依存関係のいずれかに脆弱性がある場合、それを使う側にも脆弱性がある可能性があります。 使う側が知ることなく依存関係のいずれかが変更される可能性があるということは、恐ろしいことです。 依存関係に脆弱性が存在していて、今は悪用できない場合でも、将来悪用される可能性があります。 

多数のオープンソース開発者やライブラリ作成者が作ったものを利用できるということは、何千もの知らない人が自分の運用コードに直接、効果的に寄与できることを意味します。 自分の製品が、ソフトウェア サプライ チェーンを通じて、修正プログラムが適用されていない脆弱性、悪意のない誤り、さらには依存関係に対する悪意のある攻撃からの影響を受けます。

## <a name="supply-chain-compromises"></a>サプライ チェーンの侵害

サプライ チェーンの従来の定義は、製造業が基になっています。それは、何かを製造して供給するために必要なプロセスのチェーンです。 それには、計画、材料の供給、製造、小売が含まれます。 ソフトウェア サプライ チェーンも似ていますが、材料ではなくコードである点が異なります。 製造ではなく開発です。 鉱石を地中から掘り出す代わりに、コードはサプライヤー、市販品、オープンソースから供給され、通常、オープンソースのコードはリポジトリから取得されます。 リポジトリからコードを追加するということは、製品でそのコードの依存関係を取得することを意味します。

ソフトウェア サプライ チェーン攻撃の一例として、悪意のあるコードが依存関係に意図的に追加され、その依存関係のサプライ チェーンを使用して犠牲者にコードが配布される場合があります。 サプライ チェーン攻撃は現実のものです。 サプライ チェーンを攻撃する方法は多数あります。新しい共同作成者として悪意のあるコードを直接挿入したり、他の人が気付かないうちに共同作成者のアカウントを乗っ取ったり、さらには署名キーを侵害して依存関係の正式な一部ではないソフトウェアを配布することさえあります。

ソフトウェア サプライ チェーン攻撃は、それ自体が最終的な目標であることはあまりなく、攻撃者がマルウェアを挿入したり、後でアクセスできるようにバックドアを用意したりするための機会の始まりです。

![The State of the Octoverse 2020 - 脆弱性のライフサイクル](media/vulnerability-lifecycle.png)

## <a name="unpatched-software"></a>修正プログラムが適用されていないソフトウェア

現在、オープンソースの使用は広く行われており、近いうちに下火になるとは思われません。 オープンソース ソフトウェアの使用が止まることがないとすると、修正プログラムが適用されていないソフトウェアがサプライ チェーンのセキュリティに対する脅威になります。 では、プロジェクトの依存関係に脆弱性があるというリスクに対処するには、どうすればよいでしょうか。

- **環境内にあるものを把握する。** これには、依存関係とすべての推移的な依存関係を検出して、脆弱性やライセンスの制限など、それらの依存関係のリスクを理解する必要があります。
- **依存関係を管理する。** 新しいセキュリティ脆弱性が発見されたら、影響を受けるかどうかを判断し、受ける場合は、利用可能な最新バージョンとセキュリティ修正プログラムに更新する必要があります。 これは、新しい依存関係が導入される変更を確認したり、古い依存関係を定期的に監査したりする場合に特に重要です。
- **サプライ チェーンを監視する。** そのためには、依存関係を管理するために設けられている制御を監査します。 これは、依存関係に対してより制限の厳しい条件を適用するのに役立ちます。

![The State of the Octoverse 2020 - 勧告](media/advisories.png)

以降では、NuGet と GitHub に用意されているさまざまなツールと手法について説明します。それらを使用して、プロジェクト内の潜在的なリスクに対処できます。 

## <a name="knowing-what-is-in-your-environment"></a>環境内にあるものを把握する

### <a name="nuget-dependency-graph"></a>NuGet の依存関係グラフ

**📦 パッケージ利用者**

プロジェクトでの NuGet の依存関係は、該当するプロジェクト ファイルを直接見ることで確認できます。

通常、これは次の 2 つの場所のいずれかにあります。

-   [`packages.config`](../reference/packages-config.md) – プロジェクトのルートにあります。
-   [`<PackageReference>`](../consume-packages/package-references-in-project-files.md) – プロジェクト ファイルにあります。 

NuGet の依存関係の管理に使用する方法に応じて、Visual Studio の[ソリューション エクスプローラー](/visualstudio/ide/solutions-and-projects-in-visual-studio#solution-explorer)または [NuGet パッケージ マネージャー](../consume-packages/install-use-packages-visual-studio.md)を使用して依存関係を直接見ることもできます。

CLI 環境の場合は、[`dotnet list package`](/dotnet/core/tools/dotnet-list-package) コマンドを使用して、プロジェクトまたはソリューションの依存関係の一覧を表示できます。 

NuGet の依存関係の管理に関する詳細については、[こちらのドキュメントを参照してください](../consume-packages/overview-and-workflow.md)。

### <a name="github-dependency-graph"></a>GitHub の依存関係グラフ 

**📦 パッケージ利用者 | 📦🖊 パッケージ作成者**

GitHub の依存関係グラフを使用して、プロジェクトが依存しているパッケージと、それに依存するリポジトリを確認できます。 これは、その依存関係で検出された脆弱性を確認するのに役立ちます。

GitHub リポジトリの依存関係の詳細については、[こちらのドキュメントを参照してください](https://github.co/dependency-graph)。

### <a name="dependency-versions"></a>依存関係のバージョン

**📦 パッケージ利用者 | 📦🖊 パッケージ作成者**

依存関係のサプライ チェーンをセキュリティで保護するには、すべての依存関係とツールが最新の安定したバージョンに定期的に更新される必要があります。それらには、最新の機能と、既知の脆弱性に対するセキュリティ修正プログラムが含まれることが多いためです。 依存関係には、依存しているコード、利用するバイナリ、使用するツール、その他のコンポーネントが含まれる場合があります。 次のような場合が含まれます。

-   [Visual Studio](https://visualstudio.microsoft.com/downloads/)
-   [.NET SDK とランタイム](https://dotnet.microsoft.com/download)
-   [NuGet](https://www.nuget.org/downloads)
-   [NuGet パッケージ](../consume-packages/reinstalling-and-updating-packages.md)

## <a name="manage-your-dependencies"></a>依存関係を管理する

### <a name="nuget-deprecated-and-vulnerable-dependencies"></a>NuGet の非推奨および脆弱な依存関係

**📦 パッケージ利用者 | 📦🖊 パッケージ作成者**

[dotnet CLI](/dotnet/core/tools/dotnet-list-package) を使用して、プロジェクトまたはソリューションに存在する可能性がある、既知の非推奨、または脆弱な依存関係の一覧を表示できます。 `dotnet list package --deprecated` または `dotnet list package --vulnerable` コマンドを使用すると、既知の非推奨、または脆弱性の一覧が提供されます。

### <a name="github-vulnerable-dependencies"></a>GitHub の脆弱な依存関係

**📦 パッケージ利用者 | 📦🖊 パッケージ作成者**

プロジェクトが GitHub でホストされている場合、[GitHub Security](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors) を利用して、プロジェクト内のセキュリティ脆弱性とエラーを見つけることができます。また、コードベースに対する pull request をオープンすることで、Dependabot によってこれらが修正されます。 

持ち込まれる前に脆弱な依存関係を検出することは、["シフト レフト"](https://en.wikipedia.org/wiki/Shift-left_testing) 活動の 1 つの目標です。 ライセンス、推移的な依存関係、依存関係の経過期間など、依存関係に関する情報を取得できるようにすることは、そのために役立ちます。

Dependabot のアラートとセキュリティ更新プログラムの詳細については、[こちらのドキュメントを参照してください](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies)。

### <a name="nuget-feeds"></a>NuGet フィード

**📦 パッケージ利用者**

パブリックとプライベートの複数の NuGet ソース フィードを使用している場合は、任意のフィードからパッケージをダウンロードできます。 [依存関係かく乱](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610)などの既知の攻撃をビルドで予測してセキュリティ保護できるようにするには、パッケージの取得元である特定のフィードを把握するのがベスト プラクティスです。 保護のためには上流の機能で単一のフィードまたはプライベート フィードを使用できます。

パッケージ フィードのセキュリティ保護の詳細については、「[プライベート パッケージ フィードを使用するときにリスクを軽減する 3 つの方法](https://azure.microsoft.com/resources/3-ways-to-mitigate-risk-using-private-package-feeds/)」を参照してください。

### <a name="client-trust-policies"></a>クライアント信頼ポリシー

**📦 パッケージ利用者**

使用するパッケージで署名が必要なポリシーをオプトインすることができます。 これにより、作成者によって署名されている場合に限りパッケージの作成者を信頼したり、NuGet.org によって署名されたリポジトリである特定のユーザーまたはアカウントによって所有されている場合にパッケージを信頼したりすることができます。

クライアント信頼ポリシーを構成するには、[こちらのドキュメントを参照してください](../consume-packages/installing-signed-packages.md)。

### <a name="lock-files"></a>ロック ファイル

**📦 パッケージ利用者**

ロック ファイルには、パッケージのコンテンツ ハッシュが格納されます。 インストールしようとするパッケージのコンテンツ ハッシュがロック ファイルと一致する場合は、パッケージの再現性が保証されます。

ロック ファイルを有効にするには、[こちらのドキュメントを参照してください](../consume-packages/package-references-in-project-files.md#locking-dependencies)。

## <a name="monitor-your-supply-chain"></a>サプライ チェーンを監視する

### <a name="github-secret-scanning"></a>GitHub シークレット スキャン

**📦🖊 パッケージ作成者**

誤ってコミットされたシークレットが不正に使用されるのを防ぐため、GitHub によりリポジトリで NuGet API キーがスキャンされます。 

シークレット スキャンの詳細については、「[シークレット スキャンニングについて](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning)」を参照してください。

### <a name="author-package-signing"></a>作成者によるパッケージへの署名

**📦🖊 パッケージ作成者**

[作成者署名](../reference/signed-packages-reference.md)を使用すると、パッケージの作成者はパッケージに自分の ID をスタンプでき、利用者は身元を確認することができます。 これにより、内容の改ざんから保護され、パッケージの提供元とパッケージの信頼性に関する単一の正しい情報源として機能します。 クライアント信頼ポリシーと組み合わせると、パッケージが特定の作成者からのものであることを確認できます。

作成者によるパッケージへの署名については、[パッケージへの署名](../create-packages/sign-a-package.md)に関するページを参照してください。

### <a name="two-factor-authentication-2fa"></a>2 要素認証 (2FA)

**📦🖊 パッケージ作成者**

2 要素認証 (2FA) を有効にすると、[GitHub アカウントへのログイン](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa)または [NuGet.org パブリック パッケージ リポジトリへのログイン](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa)のときに、セキュリティ レイヤーを追加できます。 アカウントを保護するため、2 要素認証を有効にすることをお勧めします。

### <a name="package-id-prefix-reservation"></a>パッケージ ID プレフィックスの予約 

**📦🖊 パッケージ作成者**

パッケージの ID を保護するため、対応する名前空間でパッケージ ID プレフィックスを予約し、パッケージ ID プレフィックスが[指定した条件](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria)を満たしている場合、一致する所有者を関連付けることができます。 

ID プレフィックスの予約の詳細については、「[パッケージ ID プレフィックスの予約](../nuget-org/id-prefix-reservation.md)」を参照してください。

### <a name="deprecating-and-unlisting-a-vulnerable-package"></a>脆弱なパッケージの非推奨化と一覧からの削除

**📦🖊 パッケージ作成者**

作成したパッケージに脆弱性があることがわかっている場合に .NET パッケージ エコシステムを保護するには、パッケージを非推奨にして一覧から削除し、パッケージを検索するユーザーに表示されないようにすることをお勧めします。 非推奨で一覧にないパッケージを使用している場合は、パッケージの使用を避ける必要があります。

パッケージを非推奨にして一覧から削除する方法については、パッケージの[非推奨](../nuget-org/deprecate-packages.md)と[一覧からの削除](../nuget-org/policies/deleting-packages.md#unlisting-a-package)に関するドキュメントを参照してください。

## <a name="summary"></a>まとめ

ソフトウェア サプライ チェーンは、コードに組み込まれたり影響したりするすべてのものです。 サプライ チェーンの侵害は現実であり、一般に広がりつつありますが、それでもまだまれです。そのため、実施できる最も重要なことは、**依存関係を把握し、依存関係を管理し、** **サプライ チェーンを監視する** ことにより、サプライ チェーンを保護することです。

ここでは、サプライ チェーンをより効果的に表示、管理、監視するために NuGet と [GitHub](/learn/modules/maintain-secure-repository-github/) で現在使用できるさまざまな方法について学習しました。

世界中のソフトウェアのセキュリティ保護の詳細については、[The State of the Octoverse 2020 のセキュリティ レポート](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf)に関するページを参照してください。
