---
title: "NuGet クライアント ツールのインストール | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "Visual Studio 用にクライアント ツール、コマンド ライン インターフェイス (CLI)、およびパッケージ マネージャーをインストールするためのガイダンス。"
keywords: "nuget.exe CLI、NuGet クライアント ツール、NuGet パッケージ マネージャー、NuGet パッケージ マネージャー コンソール、Visual Studio 用 NuGet、NuGet ベータ チャネル"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1abb30458c9ebfb0ffb28be254efd9709a9627f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="installing-nuget-client-tools"></a>NuGet クライアント ツールのインストール

> [!Tip]
>  **パッケージをインストールする場合は、[クイック スタート: パッケージを使用する](../Quickstart/Use-a-Package.md)をご覧ください。**

NuGet パッケージの構築、公開、使用に使用できる次の 2 つの主要なツールがあります。

1. [**NuGet CLI**](#nuget-cli) は、すべての NuGet 機能を提供する Windows 用のコマンド ライン ユーティリティです。Mono を使用、または .NET Core CLI (`dotnet`) を通じて、Mac OSX および Linux でも実行できます。
1. [**Visual Studio での NuGet パッケージ マネージャー**](#nuget-package-manager-in-visual-studio) (Windows のみ) は、パッケージを管理するための GUI ツールで、PowerShell コンソールが含まれており、これを通じて Visual Studio 内で直接、特定の NuGet コマンドを使用できます。 パッケージ マネージャーの UI とコンソールはどちらも Visual Studio (Windows) 2012 以降に含まれており、それより前のバージョンには手動でインストールできます。

    Visual Studio for Mac には、NuGet の機能が直接、組み込まれています。 チュートリアルについては、「[プロジェクトに NuGet パッケージを含める](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough)」をご覧ください。

    現時点では Visual Studio Code には組み込みの NuGet のサポートはありません。 NuGet CLI または [dotnet CLI](../Tools/dotnet-Commands.md) を使用してください。

NuGet CLI とパッケージ マネージャーは、どちらも次の操作をサポートしています。

- パッケージの検索
- パッケージのインストール
- パッケージの更新
- パッケージのアンインストール
- パッケージの復元 (パッケージ マネージャーの UI のみ)
- NuGet ソースの管理

次の機能は、NuGet CLI でのみサポートされます。

- パッケージの管理 (nuget.org またはプライベート フィード)
- パッケージの作成 
- パッケージの公開
- Nuget.Config の管理
- NuGet のキャッシュの管理
- パッケージのレプリケート

> [!Note]
> もう 1 つの優れたツールは、[NuGet パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)です。NuGet パッケージを視覚的に調査、作成、および編集する、オープン ソースのスタンドアロン ツールです。 このツールを使用すると、たとえば、パッケージ構造に実験的な変更を加えるたびに、パッケージをリビルドする必要がないため、非常に便利です。
> .NET Core アプリケーションの開発に使用されるクロス プラットフォーム [.NET Core CLI](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation) ツールチェーンは、delete、locals、push、pack、および restore など、複数の NuGet コマンドをサポートしています。 

## <a name="nuget-cli"></a>NuGet CLI

NuGet コマンド ライン インターフェイスは、すべての NuGet 機能へのアクセスを提供し、以降のセクションで説明するように、Windows、Mac OSX および Linux で実行できます。

### <a name="windows"></a>Windows

**直接ダウンロード:**

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> NuGet 1.4 以降では、`nuget update -self` を使用して既存の nuget.exe を最新バージョンに更新できます。

**その他のメソッド:**

- **Chocolatey**: [Chocolatey](http://chocolatey.org) クライアントを使用して、[NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey パッケージをインストールします。 

    ```ps
    choco install nuget.commandline
    ```

- **Visual Studio**: Visual Studio のパッケージ マネージャー コンソールから [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) パッケージをインストールします。

    > [!Note]
    > **NuGet 2.x ユーザーの場合**: NuGet 3.2 で導入された互換性に影響する変更点により、継続的なインテグレーション システムが中断される可能性を防止するため、[https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) は最新の安定した NuGet 2.x リリースをポイントします。

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a>Mac OSX および Linux

Mac OSX および Linux では、次の 2 つの方法で NuGet CLI を実行できます。

- NuGet のコア機能を含む [.NET Core SDK](https://www.microsoft.com/net/download/core) をインストールします。 ダウンロードが [github.com/dotnet/cli](https://github.com/dotnet/cli) にも一覧表示されます。 より多くの機能が必要な場合は、次の 2 番目のオプションを使用して、Mono で `nuget.exe` を使用します。

- [Mono](http://www.mono-project.com/docs/getting-started/install/) をインストールし、[nuget.org/downloads](https://nuget.org/downloads) から、Windows の `nuget.exe` コマンドライン実行可能ファイル (バージョン 3.2 以降) を使用します。 Mono で NuGet を実行する場合、次の制限があります。

    - テスト済みのコマンド:
        - .config
        - 削除
        - help
        - install
        - リスト
        - push
        - setApiKey
        - sources
        - spec

    - 部分的に機能するコマンド:
        - pack: `.nuspec` ファイルでは機能しますが、プロジェクト ファイルでは機能しません。
        - restore: `packages.config` ファイルと `project.json` ファイルでは機能しますが、ソリューション (`.sln`) ファイルでは機能しません。

    - 機能しないコマンド:
        - 更新

### <a name="related-topics"></a>関連トピック

- [NuGet CLI リファレンス](../tools/nuget-exe-cli-reference.md)
- [パッケージの作成](../create-packages/creating-a-package.md)
- [パッケージの公開](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a>Visual Studio の NuGet パッケージ マネージャー

NuGet パッケージ マネージャーは、Windows の Visual Studio 2012 以降のすべてのエディションに含まれます。 これにはパッケージ マネージャー UI ([参照](../tools/package-manager-ui.md)) と、特定のパッケージに付属するツールにアクセスできるパッケージ マネージャー コンソール ([参照](../tools/package-manager-console.md)) が含まれています。

Visual Studio 2017 インストーラーには、NuGet パッケージ マネージャーと .NET を使用するすべてのワークロードが含まれます。 個別にインストール、またはパッケージ マネージャーがインストールされていることを確認するには、Visual Studio 2017 インストーラーを実行し、**[個別のコンポーネント] > [コード ツール] > [NuGet パッケージ マネージャー]** の下でオプションを確認します。

> [!Note]
> コンソールには [PowerShell 2.0](http://support.microsoft.com/kb/968929) が必要です。これは、Windows 7 以降と Windows Server 2008 R2 以降では既にインストールされています。
>
> パッケージ マネージャー コンソールのコマンドも、Windows の Visual Studio 内でのみ機能します。 Visual Studio for Mac および Visual Studio Code を含む、その環境の外部で NuGet CLI を使用します。

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a>Visual Studio 2010 以前のパッケージ マネージャーのインストール

*この手順は、パッケージ マネージャーが既に含まれている Visual Studio 2012 以降では必要ありません。*

1. Visual Studio 2010 以前では、**[ツール] > [拡張機能と更新プログラム]** の順にクリックします。
1. **[オンライン]** に移動し、"Visual Studio 用 NuGet パッケージ マネージャー" を検索し、**[ダウンロード]** をクリックします。
1. [インストーラー] ダイアログ ボックスで、**[インストール]** をクリックします。
1. インストールが完了したら、Visual Studio を再起動します。

> [!Tip]
> Visual Studio で **[拡張機能と更新プログラム]** ダイアログが使用できない (たとえばプロキシによってブロックされている) 場合は、[https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) で Visual Studio 2013 および 2015 の拡張機能を直接、ダウンロードすることができます。

### <a name="updating-the-package-manager"></a>パッケージ マネージャーの更新

Visual Studio 2015 Update 2 以降では、パッケージ マネージャーが最新の安定版リリースに自動的に更新されます。

Visual Studio 2015 Update 1 以前では、**[ツール] > [拡張機能と更新プログラム]** コマンドを選択し、**[更新]** タブをクリックして、パッケージ マネージャーの新しいバージョンが使用可能かどうかを確認してください。  

### <a name="nuget-previews"></a>NuGet のプレビュー

リリース予定の NuGet の機能をプレビューしたい場合は、[Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/) をインストールします。これは、Visual Studio の安定版リリースと同時に実行できます。

Visual Studio 2015 用の以前の NuGet のベータ チャネル (`https://dotnet.myget.org/F/nuget-beta/vsix/`) は、使用されていないことに注意してください。

NuGet の任意のリリースの問題を報告したり、アイデアを共有するには、[NuGet GitHub リポジトリ](https://github.com/Nuget/Home)で懸案事項を作成します。

### <a name="related-topics"></a>関連トピック

- [パッケージ マネージャー UI のリファレンス](../tools/package-manager-ui.md)
- [パッケージ マネージャー コンソールのリファレンス](../tools/package-manager-console.md)
- [パッケージ マネージャー コンソール PowerShell のリファレンス](../tools/powershell-reference.md)