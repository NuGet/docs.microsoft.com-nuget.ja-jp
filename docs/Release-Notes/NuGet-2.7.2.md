---
title: "NuGet 2.7.2 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: c775d1d7-de26-476c-bf9e-0cf95986a22f
description: "NuGet 2.7.2 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。"
keywords: "NuGet 2.7.2 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5bb1eb346666c5d5ee790fcdcd7d844bfd37b22e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-272-release-notes"></a><span data-ttu-id="a8c82-104">NuGet 2.7.2 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="a8c82-104">NuGet 2.7.2 Release Notes</span></span>

<span data-ttu-id="a8c82-105">[NuGet 2.7.1 リリース ノート](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 リリース ノート](../release-notes/nuget-2.8.md)</span><span class="sxs-lookup"><span data-stu-id="a8c82-105">[NuGet 2.7.1 Release Notes](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md)</span></span>

<span data-ttu-id="a8c82-106">NuGet 2.7.2 は、2013 年 11 月 11 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="a8c82-106">NuGet 2.7.2 was released on November 11, 2013.</span></span>

## <a name="noteworthy-bug-fixes-and-features"></a><span data-ttu-id="a8c82-107">注目すべきことのバグ修正と機能</span><span class="sxs-lookup"><span data-stu-id="a8c82-107">Noteworthy Bug Fixes and Features</span></span>

### <a name="license-text"></a><span data-ttu-id="a8c82-108">ライセンスのテキスト</span><span class="sxs-lookup"><span data-stu-id="a8c82-108">License Text</span></span>
<span data-ttu-id="a8c82-109">はかなりの時間は、Visual Studio で Web アプリケーション プロジェクトの既定のテンプレートの一部としていくつかの一般的なオープン ソース ライブラリ用の NuGet パッケージが Microsoft に含まれているがします。</span><span class="sxs-lookup"><span data-stu-id="a8c82-109">For quite some time, Microsoft has included the NuGet packages for several popular open-source libraries as a part of the default templates for Web application projects in Visual Studio.</span></span> <span data-ttu-id="a8c82-110">jQuery は、ライブラリのこの型の最も一般的な例を示します可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a8c82-110">jQuery is probably the most well-known example of this type of library.</span></span> <span data-ttu-id="a8c82-111">サポート契約を製品と共に配信されるコンポーネントに関連付けられているため、パッケージのスクリプト ファイルには、パブリック nuget.org ギャラリーで同じパッケージで見つかったスクリプト ファイルよりも別のライセンスのテキストが含まれています。</span><span class="sxs-lookup"><span data-stu-id="a8c82-111">Because of the support agreement associated with components that are delivered along with a product, the package's script file contains different license text than the script file found in the same package on the public nuget.org gallery.</span></span> <span data-ttu-id="a8c82-112">テキストの違いは、パッケージの更新を防ぐためさまざまなコンテンツのハッシュ値を含むスクリプト ファイルを原因別のライセンスのテキスト ブロックの結果として処理 (およびためとして扱われる、プロジェクト内で変更)。</span><span class="sxs-lookup"><span data-stu-id="a8c82-112">This difference in text can prevent package updates from proceeding as a result of the different license text blocks causing the script files to have different content hash values (and therefore to be treated as modified within the project).</span></span>

<span data-ttu-id="a8c82-113">この問題を軽減するのには、NuGet 2.7.2 は、スクリプトの作成者には、次のように特別にマークされたセクション内にあるライセンスのテキスト ブロックを含めるを許可します。</span><span class="sxs-lookup"><span data-stu-id="a8c82-113">To mitigate this issue, NuGet 2.7.2 allows the script author to include the license text block within a specially marked section which looks as follows.</span></span>

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

<span data-ttu-id="a8c82-114">コンテンツを含むパッケージを更新するときにこのブロックを含むファイル NuGet はいない NuGet ギャラリーのバージョンと比較した結果に、ブロックの内容を考慮できます削除され元のコピーと一致する場合と同様に、コンテンツ ファイルを更新します。</span><span class="sxs-lookup"><span data-stu-id="a8c82-114">When updating packages with content files containing this block, NuGet does not factor the contents of the block into the comparison with the version on the NuGet gallery, and can therefore delete and update the content file as though it matches the original copy.</span></span>

<span data-ttu-id="a8c82-115">このブロックは、テキスト"NUGET:: 開始ライセンス TEXT"と"NUGET:: 終了ライセンス TEXT"の先頭で任意の場所に発生した行と最終行で識別されます。</span><span class="sxs-lookup"><span data-stu-id="a8c82-115">This block is identified by the text "NUGET: BEGIN LICENSE TEXT" and "NUGET: END LICENSE TEXT" occurring anywhere on the beginning and ending lines.</span></span>  <span data-ttu-id="a8c82-116">その他の書式設定の要件が存在していない言語に関係なく、テキスト ファイルの種類で使用するには、この機能を許可します。</span><span class="sxs-lookup"><span data-stu-id="a8c82-116">No other formatting requirements exist, allowing this feature to be used in any type of text file regardless of language.</span></span>

### <a name="add-binding-redirects-for-non-framework-assemblies"></a><span data-ttu-id="a8c82-117">アセンブリ以外のフレームワークをバインド リダイレクトを追加します。</span><span class="sxs-lookup"><span data-stu-id="a8c82-117">Add Binding Redirects for non-Framework Assemblies</span></span>
<span data-ttu-id="a8c82-118">.NET Framework の一部であるアセンブリの場合は、NuGet はパッケージを更新するときにアプリケーションの構成ファイルに追加のバインド リダイレクトをスキップします。</span><span class="sxs-lookup"><span data-stu-id="a8c82-118">For assemblies that are part of the .NET Framework, NuGet skips adding binding redirects into the application's configuration file when updating the package.</span></span> <span data-ttu-id="a8c82-119">この修正プログラムのアドレス、バインド リダイレクト追加されませんでした中、一部のアセンブリでは、それらのアセンブリがない場合でも NuGet 2.7 の回帰には、.NET Framework の一部と見なされます。</span><span class="sxs-lookup"><span data-stu-id="a8c82-119">This fix addresses a regression in NuGet 2.7 whereby binding redirects were not being added for some assemblies, even though those assemblies are not considered a part of the .NET Framework.</span></span> <span data-ttu-id="a8c82-120">NuGet 2.7.2 は、以前の NuGet 2.5 および 2.6 の動作を復元し、バインド リダイレクトを追加します。</span><span class="sxs-lookup"><span data-stu-id="a8c82-120">NuGet 2.7.2 restores the previous NuGet 2.5 and 2.6 behavior and adds the binding redirects.</span></span>

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a><span data-ttu-id="a8c82-121">Xamarin ツールがインストールされているポータブル ライブラリをインストールします。</span><span class="sxs-lookup"><span data-stu-id="a8c82-121">Installing portable libraries with Xamarin Tools installed</span></span>
<span data-ttu-id="a8c82-122">マシンには、Xamarin の開発ツールがインストールされている、ときに、既存のターゲット フレームワークの組み合わせ、および Xamarin フレームワークの間の互換性を指定する、サポートされているフレームワークの構成データを変更します。</span><span class="sxs-lookup"><span data-stu-id="a8c82-122">When Xamarin's development tools are installed on a machine, they modify the supported frameworks configuration data to specify compatibility between existing target framework combinations and Xamarin frameworks.</span></span> <span data-ttu-id="a8c82-123">バージョン 2.7.2、NuGet は、これらの暗黙的な互換性規則の対応するようになりましたしたがって簡単で、パッケージのようなをする Xamarin と互換性のあるが、明示的にマークされているポータブル ライブラリをインストールする Xamarin プラットフォームを対象とする開発者向けメタデータ自体です。</span><span class="sxs-lookup"><span data-stu-id="a8c82-123">With version 2.7.2, NuGet is now aware of these implicit compatibility rules, and therefore makes it easy for developers targeting Xamarin platforms to install portable libraries that are Xamarin-compatible but not explicitly marked as such in the package metadata itself.</span></span>

### <a name="machine-wide-configuration-settings-honored"></a><span data-ttu-id="a8c82-124">コンピューター全体の構成設定の受け入れ</span><span class="sxs-lookup"><span data-stu-id="a8c82-124">Machine-wide configuration settings honored</span></span>
<span data-ttu-id="a8c82-125">Nuget.Config ファイルの階層を使用する場合、ソリューションのルートに最も近い Nuget.Config ファイルの repositoryPath キーが受け付けられませんでしたされています。</span><span class="sxs-lookup"><span data-stu-id="a8c82-125">When using hierarchical Nuget.Config files, the repositoryPath key was not being honored for Nuget.Config files closest to the solution root.</span></span> <span data-ttu-id="a8c82-126">Visual Studio 2013 では、NuGet は、"Microsoft および .NET"のパッケージ ソースを追加するために %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config でカスタム Nuget.Config ファイルをインストールします。</span><span class="sxs-lookup"><span data-stu-id="a8c82-126">In Visual Studio 2013, NuGet installs a custom Nuget.Config file at %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config in order to add the "Microsoft and .NET" package source.</span></span> <span data-ttu-id="a8c82-127">その結果、回避ソリューションでカスタム repositoryPath を使用するためも、"Microsoft および .NET"のパッケージ ソースを削除するためのもののコンピューター レベル。 Nuget.Config を削除することでした。</span><span class="sxs-lookup"><span data-stu-id="a8c82-127">As a result, the work-around for using a custom repositoryPath in a solution was to delete the machine-level Nuget.Config - which also meant removing the "Microsoft and .NET" package source.</span></span> <span data-ttu-id="a8c82-128">NuGet 2.7.2 では、repositoryPath の優先順位規則 Nuget.Config ファイルの階層を使用する場合。</span><span class="sxs-lookup"><span data-stu-id="a8c82-128">NuGet 2.7.2 now honors the precedence rules for repositoryPath when using hierarchical Nuget.Config files.</span></span>

## <a name="all-changes"></a><span data-ttu-id="a8c82-129">すべての変更</span><span class="sxs-lookup"><span data-stu-id="a8c82-129">All Changes</span></span>
<span data-ttu-id="a8c82-130">作業の完全な一覧の項目で修正 NuGet 2.7.2、くださいビュー、[今回のリリースの NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)です。</span><span class="sxs-lookup"><span data-stu-id="a8c82-130">For a full list of work items fixed in NuGet 2.7.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).</span></span>
