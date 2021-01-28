---
title: NuGet クライアント ツールのインストール
description: Visual Studio 用にクライアント ツール、dotnet コマンド ライン インターフェイス (CLI)、nuget CLI、およびパッケージ マネージャーをインストールするためのガイダンス。
author: JonDouglas
ms.author: jodou
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: 0e3938fc1ac748285ba26541a7d4e907c9a64156
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775903"
---
# <a name="install-nuget-client-tools"></a>NuGet クライアント ツールのインストール

> **パッケージをインストールする場合は、[Nuget パッケージのインストール方法](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)に関するページをご覧ください。**

パッケージ コンシューマーまたは作成者は、NuGet を使用するために、Visual Studio の NuGet 機能だけでなく、コマンド ライン インターフェイス (CLI) ツールも使用できます。 この記事では、さまざまなツールの機能とそれらのインストール方法について簡単に説明します。また、各ツールの[機能の可用性](#feature-availability)の比較も示します。 NuGet でパッケージの利用を開始するには、パッケージをインストールして使用する方法に関するページを参照してください ([dotnet CLI](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) 向けページと [Visual Studio](quickstart/install-and-use-a-package-in-visual-studio.md) 向けページがあります)。 NuGet パッケージの作成を開始するには、NET Standard パッケージの作成と公開に関するページを参照してください ([dotnet CLI](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) 向けページと [Visual Studio](quickstart/create-and-publish-a-package-using-visual-studio.md) 向けページがあります)。

| ツール&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 説明 | ダウンロード&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | .NET Core と .NET Standard ライブラリ、および任意の [SDK スタイルのプロジェクト](resources/check-project-format.md) (.NET Framework を対象とするものなど) のための CLI ツール。 .NET Core SDK 含まれており、すべてのプラットフォームで NuGet のコア機能を提供します。 (Visual Studio 2017 以降、dotnet CLI は .NET Core に関連するすべてのワークロードで自動的にインストールされます。)| [.NET Core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | .NET Framework ライブラリ、および任意の[非 SDK スタイルのプロジェクト](resources/check-project-format.md) (.NET Standard ライブラリを対象とするものなど) のための CLI ツール。 Windows のすべての NuGet 機能と、Mono で実行される場合の Mac および Linux の ほとんどの機能を提供します。 | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | Windows では、**NuGet パッケージ マネージャー** は、Visual Studio 2012 以降に含まれています。 Visual Studio では、[パッケージ マネージャー UI](consume-packages/install-use-packages-visual-studio.md) と[パッケージ マネージャー コンソール](consume-packages/install-use-packages-powershell.md)を提供します。NuGet の操作のほとんどは、これらを使用して実行できます。 | [Visual Studio](https://www.visualstudio.com/downloads/) |
| [Visual Studio for Mac](/visualstudio/mac/nuget-walkthrough) | Mac では、NuGet の機能は直接組み込まれています。 パッケージ マネージャー コンソールは、現在、使用できません。 他の機能については、CLI ツールの `dotnet.exe` または `nuget.exe` を使用します。  | [Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/) |
| [Visual Studio Code](https://code.visualstudio.com/docs) | Windows、Mac、または Linux では、NuGet 機能は、Marketplace 拡張機能から入手できます。また、CLI ツールの `dotnet.exe` または `nuget.exe` を使用して入手することもできます。 | [Visual Studio Code](https://code.visualstudio.com/Download/)|

さらに、[MSBuild CLI](reference/msbuild-targets.md) は、パッケージを復元および作成する機能を提供します。これはおもにビルド サーバーで有用です。 MSBuild は、NuGet を使用するための汎用ツールではありません。

パッケージ マネージャー コンソール コマンドは、Windows 上の Visual Studio 内でのみ機能し、他の PowerShell 環境では機能しません。

## <a name="visual-studio"></a>Visual Studio
### <a name="install-on-visual-studio-2017-and-newer"></a>Visual Studio 2017 以降へのインストール
Visual Studio 2017 以降、インストーラーには、NuGet パッケージ マネージャーと .NET を使用するすべてのワークロードが含まれます。 個別にインストール、またはパッケージ マネージャーがインストールされていることを確認するには、Visual Studio インストーラーを実行し、 **[個別のコンポーネント] > [コード ツール] > [NuGet パッケージ マネージャー]** の下でオプションを確認します。

### <a name="install-on-visual-studio-2015-and-older"></a>Visual Studio 2015 以前へのインストール
Visual Studio 2013 および 2015 用の NuGet 拡張機能は、[https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) からダウンロードできます。

Visual Studio 2010 以前の場合、"Visual Studio 用 NuGet パッケージ マネージャー" 拡張機能をインストールします。 検索結果の最初のページに拡張機能が表示されない場合は、[並べ替え] ドロップダウンを [ダウンロード数順] またはアルファベット順に変更してみてください。

## <a name="cli-tools"></a>CLI ツール
IDE で NuGet 機能をサポートするには、`dotnet` CLI または `nuget.exe` CLI のいずれかが使用できます。 `dotnet` CLI は、一部の Visual Studio ワークロード (.NET Core など) と共にインストールされます。 `nuget.exe` CLI は、前述のように個別にインストールする必要があります。

`dotnet.exe` と `nuget.exe` の 2 つの NuGet CLI ツールがあります。 比較については、「[機能の可用性](#feature-availability)」をご覧ください。

* .NET Core または .NET Standard を対象とするには、dotnet CLI をご使用ください。 SDK スタイルのプロジェクト形式 ([SDK 属性](/dotnet/core/tools/csproj#additions)が使用されます) の場合、`dotnet` CLI が必要です。
* .NET Framework (非 SDK スタイルのプロジェクトのみ) を対象とするには、`nuget.exe` CLI を使用します。 プロジェクトを `packages.config` から PackageReference に移行する場合は、dotnet CLI を使用します。

### <a name="dotnetexe-cli"></a>dotnet.exe CLI

.NET Core 2.0 CLI (`dotnet.exe`) は、すべてのプラットフォーム (Windows、Mac、Linux) で機能し、パッケージのインストール、復元、および公開など、NuGet のコア機能を提供します。 `dotnet` は、.NET Core プロジェクト ファイル (`.csproj`など) に直接統合されます。これは、ほとんどのシナリオで役立ちます。 また、`dotnet` は、各プラットフォーム用に直接構築されているので、Mono をインストールする必要はありません。

インストール:

- 開発者用コンピューターに [.NET Core SDK](https://aka.ms/dotnetcoregs) をインストールします。 Visual Studio 2017 以降、dotnet CLI は .NET Core 関連のワークロードで自動的にインストールされます。
- ビルド サーバーの場合は、「[継続的インテグレーション (CI) で .NET Core SDK とツールを使用する](/dotnet/core/tools/using-ci-with-cli)」の手順に従ってください。

dotnet CLI で基本的なコマンドを使用する方法を学習するには、[dotnet CLI を使用したパッケージのインストールと使用](consume-packages/install-use-packages-dotnet-cli.md)に関するページを参照してください。

### <a name="nugetexe-cli"></a>nuget.exe CLI

`nuget.exe` CLI (`nuget.exe`) は、すべての NuGet 機能を提供する Windows 用のコマンド ライン ユーティリティです。[Mono](https://www.mono-project.com/docs/getting-started/install/) を使用して Mac OSX および Linux でも実行できますが、いくつかの制限があります。

`nuget.exe` CLI で基本的なコマンドを使用する方法を学習するには、[nuget.exe CLI を使用したパッケージのインストールと使用](consume-packages/install-use-packages-nuget-cli.md)に関するページを参照してください。

インストール:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Windows で既存の nuget.exe を最新バージョンに更新するには、`nuget update -self` を使用します。

> [!Note]
> 最新の推奨される NuGet CLI はいつでも、`https://dist.nuget.org/win-x86-commandline/latest/nuget.exe` で入手できます。 古い継続的インテグレーション システムとの互換性を維持するために、以前の URL (`https://nuget.org/nuget.exe`) では現在、[非推奨の 2.8.6 CLI ツール](https://github.com/NuGet/NuGetGallery/issues/5381)が提供されています。

## <a name="feature-availability"></a>機能の可用性

| 機能 | dotnet CLI | nuget CLI (Windows) | nuget CLI (Mono) | Visual Studio (Windows) | Visual Studio for Mac |
| --- | --- | --- | --- | --- | --- |
| パッケージの検索 |  | &#10004; | &#10004; | &#10004; | &#10004; |
| パッケージのインストール/アンインストール | &#10004; | &#10004;(1) | &#10004; | &#10004; | &#10004; |
| パッケージの更新 | &#10004; | &#10004; | | &#10004; | &#10004; |
| パッケージの復元 | &#10004; | &#10004; | &#10004;(2) | &#10004; | &#10004; |
| パッケージ フィードの管理 (ソース) | | &#10004; | &#10004; | &#10004; | &#10004; |
| フィード上でのパッケージの管理 | &#10004; | &#10004; | &#10004; | | |
| フィードの API キーの設定 | | &#10004; | &#10004; | | |
| パッケージの作成 (3) | &#10004; | &#10004; | &#10004;(4) | &#10004; | |
| パッケージの公開 | &#10004; | &#10004; | &#10004; | &#10004; |  |
| パッケージのレプリケート |  | &#10004; | &#10004; | | |
| "*グローバル パッケージ*" フォルダーおよびキャッシュ フォルダーの管理 | &#10004; | &#10004; | &#10004; | | |
| NuGet の構成の管理 | | &#10004; | &#10004; | | |

(1) プロジェクト ファイルには影響しません。代わりに `dotnet.exe` を使用します。

(2) `packages.config` ファイルでのみ機能し、ソリューション (`.sln`) ファイルでは機能しません。

(3) 各種の高度なパッケージ機能は、Visual Studio UI ツールで表示されない場合のみ、CLI を通じて使用できます。

(4) `.nuspec` ファイルでは機能しますが、プロジェクト ファイルでは機能しません。

## <a name="upcoming-features"></a>今後の機能
今後の NuGet の機能をプレビューしたい場合は、[Visual Studio Preview](https://www.visualstudio.com/vs/preview/) をインストールします。これは、Visual Studio の安定版リリースと同時に実行できます。 問題を報告したり、プレビューに関するアイデアを共有したりするには、[NuGet GitHub リポジトリ](https://github.com/Nuget/Home/issues)で懸案事項を開きます。

### <a name="related-topics"></a>関連トピック

- [Visual Studio を使用してパッケージをインストールして管理する](consume-packages/install-use-packages-visual-studio.md)
- [PowerShell を使用してパッケージをインストールして管理する](consume-packages/install-use-packages-powershell.md)
- [dotnet CLI を使用してパッケージをインストールして管理する](consume-packages/install-use-packages-dotnet-cli.md)
- [nuget.exe CLI を使用してパッケージをインストールして管理する](consume-packages/install-use-packages-nuget-cli.md)
- [パッケージ マネージャー コンソール PowerShell のリファレンス](reference/powershell-reference.md)
- [パッケージの作成](create-packages/creating-a-package.md)
- [パッケージの公開](nuget-org/publish-a-package.md)

さらに、Windows で作業する開発者は、[NuGet パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)を探索することもできます。これは、NuGet パッケージを視覚的に調査、作成、および編集する、オープン ソースのスタンドアロン ツールです。 たとえば、パッケージをリビルドせずにパッケージ構造に試験的な変更を加える際に非常に役立ちます。
