---
title: NuGet 2.7.2 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.7.2 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7643bf930bca39684eb626fe737001bc3e3ea769
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776784"
---
# <a name="nuget-272-release-notes"></a><span data-ttu-id="ee9f7-103">NuGet 2.7.2 のリリースノート</span><span class="sxs-lookup"><span data-stu-id="ee9f7-103">NuGet 2.7.2 Release Notes</span></span>

<span data-ttu-id="ee9f7-104">[NuGet 2.7.1 のリリースノート](../release-notes/nuget-2.7.1.md)  | [NuGet 2.8 リリースノート](../release-notes/nuget-2.8.md)</span><span class="sxs-lookup"><span data-stu-id="ee9f7-104">[NuGet 2.7.1 Release Notes](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md)</span></span>

<span data-ttu-id="ee9f7-105">NuGet 2.7.2 は、2013年11月11日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="ee9f7-105">NuGet 2.7.2 was released on November 11, 2013.</span></span>

## <a name="noteworthy-bug-fixes-and-features"></a><span data-ttu-id="ee9f7-106">注目すべきバグの修正と機能</span><span class="sxs-lookup"><span data-stu-id="ee9f7-106">Noteworthy Bug Fixes and Features</span></span>

### <a name="license-text"></a><span data-ttu-id="ee9f7-107">ライセンスのテキスト</span><span class="sxs-lookup"><span data-stu-id="ee9f7-107">License Text</span></span>
<span data-ttu-id="ee9f7-108">多くの場合、Microsoft では、Visual Studio の Web アプリケーションプロジェクトの既定のテンプレートの一部として、いくつかの一般的なオープンソースライブラリの NuGet パッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ee9f7-108">For quite some time, Microsoft has included the NuGet packages for several popular open-source libraries as a part of the default templates for Web application projects in Visual Studio.</span></span> <span data-ttu-id="ee9f7-109">jQuery は、このタイプのライブラリの最もよく知られている例です。</span><span class="sxs-lookup"><span data-stu-id="ee9f7-109">jQuery is probably the most well-known example of this type of library.</span></span> <span data-ttu-id="ee9f7-110">製品と共に配信されるコンポーネントに関連付けられたサポート契約により、パッケージのスクリプトファイルには、パブリック nuget.org ギャラリーの同じパッケージにあるスクリプトファイルとは異なるライセンステキストが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ee9f7-110">Because of the support agreement associated with components that are delivered along with a product, the package's script file contains different license text than the script file found in the same package on the public nuget.org gallery.</span></span> <span data-ttu-id="ee9f7-111">このテキストの違いにより、異なるライセンステキストブロックの結果としてパッケージの更新が続行されないようにして、スクリプトファイルのコンテンツハッシュ値が異なる (したがって、プロジェクト内で変更として扱われる) ようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="ee9f7-111">This difference in text can prevent package updates from proceeding as a result of the different license text blocks causing the script files to have different content hash values (and therefore to be treated as modified within the project).</span></span>

<span data-ttu-id="ee9f7-112">この問題を軽減するために、NuGet 2.7.2 は、スクリプト作成者が、次のような特別にマークされたセクション内にライセンステキストブロックを含めることを許可します。</span><span class="sxs-lookup"><span data-stu-id="ee9f7-112">To mitigate this issue, NuGet 2.7.2 allows the script author to include the license text block within a specially marked section which looks as follows.</span></span>

```
/************** NUGET: BEGIN LICENSE TEXT **************
    * The following code is licensed under the MIT license
    * Additional license information below is informational
    * only.
    ************** NUGET: END LICENSE TEXT ***************/
```

<span data-ttu-id="ee9f7-113">このブロックを含むコンテンツファイルを使用してパッケージを更新する場合、NuGet では、ブロックの内容が NuGet ギャラリーのバージョンと比較されることはありません。そのため、コンテンツファイルが元のコピーと一致しているかのように削除および更新できます。</span><span class="sxs-lookup"><span data-stu-id="ee9f7-113">When updating packages with content files containing this block, NuGet does not factor the contents of the block into the comparison with the version on the NuGet gallery, and can therefore delete and update the content file as though it matches the original copy.</span></span>

<span data-ttu-id="ee9f7-114">このブロックは、開始行と終了行の任意の場所で発生する "NUGET: BEGIN LICENSE TEXT" と "NUGET: END LICENSE TEXT" というテキストで識別されます。</span><span class="sxs-lookup"><span data-stu-id="ee9f7-114">This block is identified by the text "NUGET: BEGIN LICENSE TEXT" and "NUGET: END LICENSE TEXT" occurring anywhere on the beginning and ending lines.</span></span>  <span data-ttu-id="ee9f7-115">他の書式設定の要件は存在しないため、言語に関係なく、任意の種類のテキストファイルでこの機能を使用できます。</span><span class="sxs-lookup"><span data-stu-id="ee9f7-115">No other formatting requirements exist, allowing this feature to be used in any type of text file regardless of language.</span></span>

### <a name="add-binding-redirects-for-non-framework-assemblies"></a><span data-ttu-id="ee9f7-116">非フレームワークアセンブリのバインドリダイレクトを追加する</span><span class="sxs-lookup"><span data-stu-id="ee9f7-116">Add Binding Redirects for non-Framework Assemblies</span></span>
<span data-ttu-id="ee9f7-117">.NET Framework の一部であるアセンブリの場合、NuGet は、パッケージの更新時に、アプリケーションの構成ファイルへのバインドリダイレクトの追加をスキップします。</span><span class="sxs-lookup"><span data-stu-id="ee9f7-117">For assemblies that are part of the .NET Framework, NuGet skips adding binding redirects into the application's configuration file when updating the package.</span></span> <span data-ttu-id="ee9f7-118">この修正は、アセンブリが .NET Framework の一部と見なされない場合でも、一部のアセンブリにバインドリダイレクトが追加されていない NuGet 2.7 の回帰に対処します。</span><span class="sxs-lookup"><span data-stu-id="ee9f7-118">This fix addresses a regression in NuGet 2.7 whereby binding redirects were not being added for some assemblies, even though those assemblies are not considered a part of the .NET Framework.</span></span> <span data-ttu-id="ee9f7-119">NuGet 2.7.2 は、以前の NuGet 2.5 と2.6 の動作を復元し、バインドリダイレクトを追加します。</span><span class="sxs-lookup"><span data-stu-id="ee9f7-119">NuGet 2.7.2 restores the previous NuGet 2.5 and 2.6 behavior and adds the binding redirects.</span></span>

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a><span data-ttu-id="ee9f7-120">Xamarin ツールがインストールされたポータブルライブラリのインストール</span><span class="sxs-lookup"><span data-stu-id="ee9f7-120">Installing portable libraries with Xamarin Tools installed</span></span>
<span data-ttu-id="ee9f7-121">Xamarin の開発ツールがコンピューターにインストールされている場合、サポートされているフレームワーク構成データを変更して、既存のターゲットフレームワークの組み合わせと Xamarin フレームワークとの互換性を指定します。</span><span class="sxs-lookup"><span data-stu-id="ee9f7-121">When Xamarin's development tools are installed on a machine, they modify the supported frameworks configuration data to specify compatibility between existing target framework combinations and Xamarin frameworks.</span></span> <span data-ttu-id="ee9f7-122">バージョン2.7.2 では、NuGet はこれらの暗黙的な互換性規則を認識するようになりました。そのため、Xamarin プラットフォームを対象とする開発者は、Xamarin と互換性のあるものの、パッケージメタデータ自体に明示的にマークされていないポータブルライブラリを簡単にインストールできます。</span><span class="sxs-lookup"><span data-stu-id="ee9f7-122">With version 2.7.2, NuGet is now aware of these implicit compatibility rules, and therefore makes it easy for developers targeting Xamarin platforms to install portable libraries that are Xamarin-compatible but not explicitly marked as such in the package metadata itself.</span></span>

### <a name="machine-wide-configuration-settings-honored"></a><span data-ttu-id="ee9f7-123">コンピューター全体の構成設定が受け入れられる</span><span class="sxs-lookup"><span data-stu-id="ee9f7-123">Machine-wide configuration settings honored</span></span>
<span data-ttu-id="ee9f7-124">階層 Nuget.Config ファイルを使用する場合、ソリューションルートに最も近い Nuget.Config ファイルに対して repositoryPath キーが受け入れられませんでした。</span><span class="sxs-lookup"><span data-stu-id="ee9f7-124">When using hierarchical Nuget.Config files, the repositoryPath key was not being honored for Nuget.Config files closest to the solution root.</span></span> <span data-ttu-id="ee9f7-125">Visual Studio 2013 では、NuGet によって、"Microsoft と .NET" パッケージソースを追加するために、カスタムの Nuget.Config ファイルが% ProgramData% \NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="ee9f7-125">In Visual Studio 2013, NuGet installs a custom Nuget.Config file at %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config in order to add the "Microsoft and .NET" package source.</span></span> <span data-ttu-id="ee9f7-126">そのため、ソリューションでカスタム repositoryPath を使用するための回避策は、マシンレベルの Nuget.Config を削除することでした。これは、"Microsoft と .NET" パッケージソースを削除することを意味します。</span><span class="sxs-lookup"><span data-stu-id="ee9f7-126">As a result, the work-around for using a custom repositoryPath in a solution was to delete the machine-level Nuget.Config - which also meant removing the "Microsoft and .NET" package source.</span></span> <span data-ttu-id="ee9f7-127">2.7.2 では、階層的な Nuget.Config ファイルを使用する場合、repositoryPath の優先順位規則が使用されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="ee9f7-127">NuGet 2.7.2 now honors the precedence rules for repositoryPath when using hierarchical Nuget.Config files.</span></span>

## <a name="all-changes"></a><span data-ttu-id="ee9f7-128">すべての変更</span><span class="sxs-lookup"><span data-stu-id="ee9f7-128">All Changes</span></span>
<span data-ttu-id="ee9f7-129">NuGet 2.7.2 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ee9f7-129">For a full list of work items fixed in NuGet 2.7.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).</span></span>
