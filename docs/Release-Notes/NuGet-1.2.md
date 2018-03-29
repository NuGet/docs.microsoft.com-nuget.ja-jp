---
title: NuGet 1.2 リリース ノート |Microsoft ドキュメント
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet 1.2 の既知の問題、バグの修正、追加された機能は、Dcr などのリリース ノートです。
keywords: NuGet 1.2 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0d95f41c5bc5d490764c9f128ee621e1037cef66
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-12-release-notes"></a><span data-ttu-id="0b1ea-104">NuGet 1.2 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="0b1ea-104">NuGet 1.2 Release Notes</span></span>

<span data-ttu-id="0b1ea-105">[NuGet 1.0 および 1.1 のリリース ノート](../release-notes/nuget-1.1.md) | [NuGet 1.3 リリース ノート](../release-notes/nuget-1.3.md)</span><span class="sxs-lookup"><span data-stu-id="0b1ea-105">[NuGet 1.0 and 1.1 Release Notes](../release-notes/nuget-1.1.md) | [NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md)</span></span>

<span data-ttu-id="0b1ea-106">NuGet 1.2 は、2011 年 3 月 30 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-106">NuGet 1.2 was released on March 30, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="0b1ea-107">新機能</span><span class="sxs-lookup"><span data-stu-id="0b1ea-107">New Features</span></span>

### <a name="framework-profile-support"></a><span data-ttu-id="0b1ea-108">フレームワークのプロファイルのサポート</span><span class="sxs-lookup"><span data-stu-id="0b1ea-108">Framework Profile Support</span></span>

<span data-ttu-id="0b1ea-109">開始日から NuGet サポートされているを持つライブラリは、さまざまなフレームワークを対象します。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-109">From the start, NuGet supported having libraries target different frameworks.</span></span> <span data-ttu-id="0b1ea-110">今すぐパッケージが Windows Phone のプロファイルなどの特定のプロファイルを対象とするアセンブリを含む可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-110">But now packages may contain assemblies that target specific profiles such as the Windows Phone profile.</span></span> <span data-ttu-id="0b1ea-111">フレームワークの特定のプロファイルを対象とするには、プロファイルの省略形の後にダッシュを追加します。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-111">To target a specific profile of a framework, append a dash followed by the profile abbreviation.</span></span> <span data-ttu-id="0b1ea-112">たとえば、Windows Phone (Windows Phone 7 とも呼ばれます) で実行されている SilverLight を対象とするには、次のスクリーン ショットに示すよう sl3 wp フォルダーにアセンブリを配置ことができます。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-112">For example, to target SilverLight running on a Windows Phone (aka Windows Phone 7), you can put an assembly in the sl3-wp folder as demonstrated in the following screenshot.</span></span>

![フレームワークのプロファイル フォルダーのレイアウト](./media/framework-profile-support.png)

<span data-ttu-id="0b1ea-114">なぜおだけを選択しなかった、モニカーとして"wp7"を使用するを依頼する場合があります。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-114">You might ask why we didn’t just choose to use “wp7” as the moniker.</span></span> <span data-ttu-id="0b1ea-115">一部にする Windows Phone 7 では、Silverlight の新しいバージョンを後で実行可能性があります、対象としている場合、どのフレームワーク プロファイルをに関する詳細を指定する必要がありますを予測しています。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-115">In part, we’re anticipating that Windows Phone 7 might run a newer version of Silverlight in the future, in which case you may need to be more specific about which framework profile you’re targetting.</span></span>

### <a name="automatically-add-binding-redirects"></a><span data-ttu-id="0b1ea-116">バインド リダイレクトを自動的に追加します。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-116">Automatically Add Binding Redirects</span></span>

<span data-ttu-id="0b1ea-117">パッケージを厳密な名前付きアセンブリをインストールするとき NuGet では、プロジェクトが必要なバインド リダイレクトをコンパイルし、それらを自動的に追加するプロジェクトの順序で構成ファイルに追加する場合が検出されます。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-117">When installing a package with strong named assemblies, NuGet can now detect cases where the project requires binding redirects to be added to the configuration file in order for the project to compile and add them automatically.</span></span> <span data-ttu-id="0b1ea-118">NuGet のバージョン管理というタイトルで David Ebbo のブログの投稿シリーズの一部 3"[バインド リダイレクトを使用して統一](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)"の詳細については、この機能の目的について説明します。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-118">Part 3 of David Ebbo’s blog post series on NuGet Versioning entitled “[Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)” covers the purpose of this feature in more details.</span></span>

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a><span data-ttu-id="0b1ea-119">フレームワーク アセンブリ参照 (GAC) を指定します。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-119">Specifying Framework Assembly References (GAC)</span></span>

<span data-ttu-id="0b1ea-120">場合によっては、パッケージは、.NET Framework に含まれるアセンブリに依存可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-120">In some cases, a package may depend on an assembly that’s in the .NET Framework.</span></span> <span data-ttu-id="0b1ea-121">厳密には、必要はありません常に、パッケージのコンシューマーが、framework アセンブリを参照します。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-121">Strictly speaking, it’s not always necessary that the consumer of your package reference the framework assembly.</span></span> <span data-ttu-id="0b1ea-122">場合によっては、ことが重要、開発者がそのアセンブリ内の型に対して、パッケージを使用するためにコードを記述する必要がある場合などです。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-122">But in some cases, it's important, such as when the developer needs to code against types in that assembly in order to use your package.</span></span> <span data-ttu-id="0b1ea-123">新しい`frameworkAssemblies`要素、メタデータ要素の子要素のセットを指定できます。 `frameworkAssembly` 、GAC 内の Framework アセンブリを指す要素。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-123">The new `frameworkAssemblies` element, a child element of the metadata element, allows you to specify a set of `frameworkAssembly` elements pointing to a Framework assembly in the GAC.</span></span> <span data-ttu-id="0b1ea-124">Framework アセンブリに重点を置いてに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-124">Note the emphasis on Framework assembly.</span></span>
<span data-ttu-id="0b1ea-125">これらのアセンブリは、.NET Framework の一部としてすべてのコンピューター上に存在したと見なされます、パッケージに含まれません。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-125">These assemblies are not included in your package as they are assumed to be on every machine  as part of the .NET Framework.</span></span> <span data-ttu-id="0b1ea-126">次の表の属性の一覧、`frameworkAssembly`要素。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-126">The following table lists attributes of the `frameworkAssembly` element.</span></span>


|<span data-ttu-id="0b1ea-127">属性</span><span class="sxs-lookup"><span data-stu-id="0b1ea-127">Attribute</span></span> |<span data-ttu-id="0b1ea-128">説明</span><span class="sxs-lookup"><span data-stu-id="0b1ea-128">Description</span></span>|
|----------------|-----------|
|<span data-ttu-id="0b1ea-129">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="0b1ea-129">**assemblyName**</span></span>|<span data-ttu-id="0b1ea-130">*必要な*します。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-130">*Required*.</span></span> <span data-ttu-id="0b1ea-131">など、アセンブリの名前`System.Net`です。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-131">Name of the assembly such as `System.Net`.</span></span>|
|<span data-ttu-id="0b1ea-132">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="0b1ea-132">**targetFramework**</span></span>|<span data-ttu-id="0b1ea-133">*省略可能な*します。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-133">*Optional*.</span></span> <span data-ttu-id="0b1ea-134">フレームワークとプロファイル名 (またはエイリアス) を指定することにより、このフレームワーク アセンブリが"net40"または"sl4"などに適用されます。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-134">Allows specifying a framework and profile name (or alias) that this framework assembly applies to such as "net40" or "sl4".</span></span> <span data-ttu-id="0b1ea-135">説明されている同じ形式を使用して[複数のターゲット フレームワークをサポートする](../create-packages/supporting-multiple-target-frameworks.md)です。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-135">Uses the same format described in [Supporting Multiple Target Frameworks](../create-packages/supporting-multiple-target-frameworks.md).</span></span>|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a><span data-ttu-id="0b1ea-136">nuget.exe は今すぐ API キー資格情報を格納することが</span><span class="sxs-lookup"><span data-stu-id="0b1ea-136">nuget.exe now is able to store API Key credentials</span></span>

<span data-ttu-id="0b1ea-137">Nuget.exe コマンドライン ツールを使用する場合は、API キーを格納するようになりました SetApiKey コマンドを使用できます。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-137">When using the nuget.exe command line tool, you can now use the SetApiKey command to store your API key.</span></span> <span data-ttu-id="0b1ea-138">このように、パッケージをプッシュするたびに指定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-138">That way, you won’t need to specify it every time you push a package.</span></span> <span data-ttu-id="0b1ea-139">Nuget.exe と API キーを保存する方法の詳細については[パッケージを公開する方法、ドキュメントを読んで](../create-packages/publish-a-package.md)です。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-139">For more details on saving your API key with nuget.exe, [read the documentation on publishing a package](../create-packages/publish-a-package.md).</span></span>

### <a name="package-explorer"></a><span data-ttu-id="0b1ea-140">パッケージ エクスプ ローラー</span><span class="sxs-lookup"><span data-stu-id="0b1ea-140">Package Explorer</span></span>
<span data-ttu-id="0b1ea-141">パッケージ エクスプ ローラーは、サポート NuGet 1.2 に更新されました。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-141">Package Explorer has been updated to support NuGet 1.2.</span></span> <span data-ttu-id="0b1ea-142">詳細については、チェック アウト、[パッケージ エクスプ ローラーのリリース ノート](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)です。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-142">For more information, check out the [Package Explorer release notes](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).</span></span>

## <a name="other-featuresfixes"></a><span data-ttu-id="0b1ea-143">その他の機能/修正</span><span class="sxs-lookup"><span data-stu-id="0b1ea-143">Other features/fixes</span></span>

<span data-ttu-id="0b1ea-144">上記の一覧は、多くの機能を実装しましたおよび修正は、バグの中で最も顕著でした。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-144">The previous list were the most noticeable of the many features we implemented and bugs we fixed.</span></span> <span data-ttu-id="0b1ea-145">すべては実装されている/修正[59 作業項目](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)今回のリリースでします。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-145">All in all, we implemented/fixed [59 work items](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) in this release.</span></span>

## <a name="known-issues"></a><span data-ttu-id="0b1ea-146">既知の問題</span><span class="sxs-lookup"><span data-stu-id="0b1ea-146">Known Issues</span></span>

* <span data-ttu-id="0b1ea-147">**1.2 の非互換性をパッケージ化**: コマンド ライン ツールの最新バージョンでビルドされたパッケージ、nuget.exe (> 1.2) は、NuGet VS アドイン (1.1) などの古いバージョンでは動作しません。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-147">**1.2 Package incompatibility**: Packages built with the latest version of the command line tool, nuget.exe (> 1.2) will not work with older versions of the NuGet VS Add-in (such as 1.1).</span></span> <span data-ttu-id="0b1ea-148">互換性のないスキーマについて何かを示すエラー メッセージに実行するを実行する場合にこのエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-148">If you run into an error message stating something about incompatible schema, you are running into this error.</span></span> <span data-ttu-id="0b1ea-149">NuGet を最新バージョンに更新してください。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-149">Please update NuGet to the latest version.</span></span>
* <span data-ttu-id="0b1ea-150">**NuGet.Server 非互換性**: フィード NuGet.Server プロジェクトを使用して内部の NuGet をホストしている場合は、NuGet.Server の最新バージョンでそのプロジェクトを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-150">**NuGet.Server incompatibility**: If you’re hosting an internal NuGet feed using the NuGet.Server project, you’ll need to update that project with the latest version of NuGet.Server.</span></span>
* <span data-ttu-id="0b1ea-151">**署名の不一致エラー**: 署名の不一致に関するメッセージがアップグレード中にエラーが発生発生した場合は NuGet をまずアンインストールしてからインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-151">**Signature Mismatch Error**: If you run into an error during an upgrade with a message about a Signature Mismatch, you need to uninstall NuGet first and then install it.</span></span> <span data-ttu-id="0b1ea-152">これに記載されて、[既知の問題のページ](../release-notes/known-issues.md)詳細を提供します。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-152">This is listed in our [Known Issues page](../release-notes/known-issues.md) which provides more details.</span></span> <span data-ttu-id="0b1ea-153">問題は Visual Studio 2010 SP1 を実行しているユーザーに影響を与えるおよびバージョンが適切に署名できません NuGet 1.0 がインストールされているのみです。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-153">The issue only affects those running Visual Studio 2010 SP1 and have a version of NuGet 1.0 installed that was incorrectly signed.</span></span> <span data-ttu-id="0b1ea-154">このバージョンのみ利用可能となった、CodePlex web サイトから、短時間のため、この問題はならないに影響を与えるユーザーが多すぎます。</span><span class="sxs-lookup"><span data-stu-id="0b1ea-154">This version was only made available from the CodePlex website for a brief period so this issue shouldn't affect too many people.</span></span>