---
title: NuGet のエコシステムの概要
description: NuGet エコシステムの包括的なリソースには、NuGet ソース、Microsoft 以外の NuGet プロジェクト、ユーティリティ、およびトレーニング資料が含まれます。
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 31243076f36f6ff274c4377c1773ea59dda8c834
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495502"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a>NuGet のエコシステムの概要

2010 年の登場以降、NuGet は、開発プロセスのさまざまな側面を改善および自動化するための多くの機会を提供しています。

NuGet は、[Apache v2 ライセンス](http://choosealicense.com/licenses/apache/)で許可されるオープン ソースであるため、他のプロジェクトが NuGet を利用し、企業は自社製品でのサポートを構築できます。 オープン ソース プロジェクトまたはエンタープライズ アプリケーションの開発では、NuGet と、NuGet 上およびその周囲に構築された他のアプリケーションが、ソフトウェア開発プロセスを向上させるため広範なツールのエコシステムを提供します。

これらのプロジェクトのすべては、開発者の貢献によって革新的に発展できます。 NuGet 自体に貢献するのと同様に、不具合の報告、新しい機能のアイデアの提供、フィードバックの提供、ドキュメントの記述、可能な場合はコードの提供によってもこれらのプロジェクトに貢献できます。

## <a name="net-foundation-projects"></a>.NET Foundation プロジェクト

NuGet は、Microsoft の開発プラットフォーム用の無料のオープン ソース パッケージ管理システムを提供します。 NuGet は、いくつかのクライアント ツール、および[公式 NuGet ギャラリー](http://www.nuget.org)を構成する一連のサービスで構成されます。 これらを組み合わせることで形成される NuGet プロジェクトは、[.NET Foundation](http://www.dotnetfoundation.org/) によって管理されます。

NuGet 組織には、GitHub 上のさまざまなリポジトリが含まれています。 [https://github.com/Nuget/Home](https://github.com/Nuget/Home) には、すべてのリポジトリの概要と、さまざまな NuGet コンポーネントが見つかる場所が記載されています。

## <a name="microsoft-projects"></a>Microsoft Project

Microsoft は、NuGet の開発に広範囲に貢献しました。 Microsoft の社員によって行われたすべての貢献もオープン ソースであり、.NET Foundation に寄付されています (著作権を含む)。

## <a name="non-microsoft-projects"></a>Microsoft 以外のプロジェクト

その他の多くの個人や企業が、NuGet エコシステムに大きな貢献を行っています。 ここに表示される各プロジェクトは、NuGet のコア コンポーネントとは別のライセンスがある可能性があります。そのため、使用前にライセンス条項に同意できることを確認してください。

- [AppVeyor CI](https://www.appveyor.com/)
- [Artifactory](https://www.jfrog.com/artifactory/)
- [BoxStarter](http://boxstarter.org/)
- [Chocolatey](https://chocolatey.org/)
- [CoApp](http://coapp.org/)
- [JetBrains ReSharper](https://resharper-plugins.jetbrains.com/)
- [JetBrains TeamCity](https://www.jetbrains.com/teamcity/)
- [Klondike](https://github.com/themotleyfool/Klondike)
- [MinimalNugetServer](https://github.com/TanukiSharp/MinimalNugetServer)
- [MyGet (または NuGet-as-a-service)](http://www.myget.org/)
- [NuGet パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [NuGet サーバー](http://nugetserver.net/)
- [OctopusDeploy](https://octopus.com/)
- [Paket](https://fsprojects.github.io/Paket/)
- [ProGet (Inedo)](http://inedo.com/proget)
- [scriptcs](http://scriptcs.net/)
- [SharpDevelop](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [Sonatype Nexus](http://www.sonatype.com/nexus-repository-sonatype)
- [SymbolSource](http://www.symbolsource.org/Public)
- [Xamarin と MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a>その他の NuGet ベース ユーティリティ

以下は、NuGet 上に構築されたツールとユーティリティです。

- [Glimpse の拡張機能](http://getglimpse.com/Packages) (プラグインはパッケージ)
- [NuGetMustHaves.com](http://nugetmusthaves.com/)
- [Orchard](http://www.orchardproject.net/) (CMS モジュールは、Orchard Gallery でホストされる v1 NuGet フィードから取得されます)
- [NuGet サーバーの Java 実装](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- [NuGetLatest](https://twitter.com/NuGetLatest) (新しいパッケージの公開をツイートする Twitter bot)
- [DefinitelyTyped](http://definitelytyped.org/) (NuGet に公開される[自動](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript Type [定義](http://www.nuget.org/packages?q=DefinitelyTyped))

## <a name="training-materials-and-references"></a>トレーニング資料と参照

通常、新しいツールまたはテクノロジの使用には、学習曲線が伴います。 幸運なことに、NuGet には急な学習曲線はまったくありません。 実際に、すべてのユーザーが[パッケージの使用を](../quickstart/use-a-package.md)すぐに開始できます。

ただし、パッケージを作成し (特に良いパッケージ)、さらに自動化されたビルドと配置プロセスに NuGet を対応させる場合、次のリソースに少し時間を費やす必要があります。

- [NuGet ブログ](http://blog.nuget.org/)
- [Twitter の NuGet チーム@nuget](http://twitter.com/nuget)
- ブック:
  - [Apress Pro NuGet](http://bit.ly/ProNuGet)
  - [NuGet 2 Essentials](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a>個々のパッケージのドキュメント

[NuDoq](http://nudoq.org) は、簡単にアクセスおよび更新できる NuGet パッケージのドキュメントを提供します。

NuDoq は、nuget.org ギャラリー サーバーを定期的にポーリングし、最新のパッケージの更新を取得し、ライブラリ ドキュメント ファイルをアンパックして処理し、状況に応じてサイトを更新します。

## <a name="adding-your-project"></a>プロジェクトを追加する

このページへの貴重な追加となる NuGet エコシステム プロジェクトがある場合は、編集して pull request をこのページに送信してください。
