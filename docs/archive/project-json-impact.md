---
title: "project.json の NuGet パッケージの作成者に与える影響 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 3.x での project.json の実装が、サポートされていない機能、コンテンツ、パッケージ形式などのパッケージの作成者にどのように影響するかの詳細です。"
keywords: "NuGet と project.json、project.json の影響、パッケージの作成に関する考慮事項、project.json の機能"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6104b4dac330869bc5724ffcf15cc0ac9ee26c1f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="impact-of-projectjson-when-creating-packages"></a><span data-ttu-id="8e56f-104">パッケージを作成するときの project.json の影響</span><span class="sxs-lookup"><span data-stu-id="8e56f-104">Impact of project.json when creating packages</span></span>

> [!Important]
> <span data-ttu-id="8e56f-105">このコンテンツは使用されていません。</span><span class="sxs-lookup"><span data-stu-id="8e56f-105">This content is deprecated.</span></span> <span data-ttu-id="8e56f-106">プロジェクトは、`packages.config` または PackageReference 形式のいずれかを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8e56f-106">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="8e56f-107">NuGet 3 以降で使用される `project.json` システムは、次のセクションで示されるように、いくつかの方法でパッケージの作成者に影響します。</span><span class="sxs-lookup"><span data-stu-id="8e56f-107">The `project.json` system used in NuGet 3+ affects package authors in several ways as described in the following sections.</span></span>

## <a name="changes-affecting-existing-packages-usage"></a><span data-ttu-id="8e56f-108">既存のパッケージの使用方法に影響する変更</span><span class="sxs-lookup"><span data-stu-id="8e56f-108">Changes affecting existing packages usage</span></span>

<span data-ttu-id="8e56f-109">従来の NuGet パッケージでは、推移的な世界に引き継がれていない一連の機能がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="8e56f-109">Traditional NuGet packages support a set of features that are not carried over to the transitive world.</span></span>

### <a name="install-and-uninstall-scripts-are-ignored"></a><span data-ttu-id="8e56f-110">スクリプトのインストールとアンインストールが無視される</span><span class="sxs-lookup"><span data-stu-id="8e56f-110">Install and uninstall scripts are ignored</span></span>

<span data-ttu-id="8e56f-111">[依存関係の解決](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference)に関するページで説明されている推移的な復元モデルには、"パッケージのインストール時刻" の概念はありません。</span><span class="sxs-lookup"><span data-stu-id="8e56f-111">The transitive restore model, described in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), does not have a concept of "package install time".</span></span> <span data-ttu-id="8e56f-112">パッケージは存在するか、存在しないかのいずれかですが、パッケージのインストール時に発生する一貫性のあるプロセスはありません。</span><span class="sxs-lookup"><span data-stu-id="8e56f-112">A package is either present or not present, but there is no consistent process that occurs when a package is installed.</span></span>

<span data-ttu-id="8e56f-113">また、インストール スクリプトは、Visual Studio でのみサポートされていました。</span><span class="sxs-lookup"><span data-stu-id="8e56f-113">Also, install scripts were supported only in Visual Studio.</span></span> <span data-ttu-id="8e56f-114">他の IDE では、このようなスクリプトをサポートするには、Visual Studio 拡張 API を模擬表示する必要があり、一般的なエディターやコマンドライン ツールではサポートされていませんでした。</span><span class="sxs-lookup"><span data-stu-id="8e56f-114">Other IDEs had to mock the Visual Studio extensibility API to attempt to support such scripts, and no support was available in common editors and command-line tools.</span></span>

### <a name="content-transforms-are-not-supported"></a><span data-ttu-id="8e56f-115">コンテンツの変換がサポートされない</span><span class="sxs-lookup"><span data-stu-id="8e56f-115">Content transforms are not supported</span></span>

<span data-ttu-id="8e56f-116">インストール スクリプトと同様に、変換はパッケージのインストールで実行され、通常はべき等ではありません。</span><span class="sxs-lookup"><span data-stu-id="8e56f-116">Similar to install scripts, transforms run on package install and are typically not idempotent.</span></span> <span data-ttu-id="8e56f-117">インストール時刻は存在しなくなったため、XDT 変換と同様の機能はサポートされません。また、このようなパッケージが推移的なシナリオで使用される場合は無視されます。</span><span class="sxs-lookup"><span data-stu-id="8e56f-117">Since there is no install time anymore, XDT Transform and similar features are not supported, and are ignored if such a package is used in a transitive scenario.</span></span>

### <a name="content"></a><span data-ttu-id="8e56f-118">Content</span><span class="sxs-lookup"><span data-stu-id="8e56f-118">Content</span></span>

<span data-ttu-id="8e56f-119">従来の NuGet パッケージでは、ソース コードや構成ファイルなどのコンテンツ ファイルを配布しています。</span><span class="sxs-lookup"><span data-stu-id="8e56f-119">Traditional NuGet packages are shipping content files such as source code and configuration files.</span></span> <span data-ttu-id="8e56f-120">通常、次の 2 つのシナリオで使用されます。</span><span class="sxs-lookup"><span data-stu-id="8e56f-120">There are used typically in two scenarios:</span></span>

1. <span data-ttu-id="8e56f-121">初期ファイルはプロジェクトにドロップされるため、ユーザーは後で編集することができます。</span><span class="sxs-lookup"><span data-stu-id="8e56f-121">Initial files dropped into the project so the user can edit them at a later time.</span></span> <span data-ttu-id="8e56f-122">一般的な例は、既定の構成ファイルです。</span><span class="sxs-lookup"><span data-stu-id="8e56f-122">The common example is default configuration files.</span></span>

1. <span data-ttu-id="8e56f-123">コンテンツ ファイルはプロジェクトにインストールされているアセンブリの補完として使用されます。</span><span class="sxs-lookup"><span data-stu-id="8e56f-123">Content files used as companions to the assemblies installed in the project.</span></span> <span data-ttu-id="8e56f-124">こちらの例は、アセンブリによって使用されるロゴ イメージになります。</span><span class="sxs-lookup"><span data-stu-id="8e56f-124">The example here would be a logo image used by an assembly.</span></span>

<span data-ttu-id="8e56f-125">現在、コンテンツのサポートは、スクリプトや変換と同じような理由で無効にされていますが、Microsoft ではコンテンツのサポートの設計を進めています。</span><span class="sxs-lookup"><span data-stu-id="8e56f-125">Support for content is currently disabled for similar reasons for scripts and transforms, but we are in the process of designing support for content.</span></span>

<span data-ttu-id="8e56f-126">コンテンツ ファイルはパッケージ内で引き続き実行することができ、現在は無視されますが、エンド ユーザーは引き続き適切な位置にコピーできます。</span><span class="sxs-lookup"><span data-stu-id="8e56f-126">Content files can still be carried inside the packages, and are ignored currently, however the end user can still copy them into the right spot.</span></span>

<span data-ttu-id="8e56f-127">コンテンツ ファイルを戻す提案のいずれかを表示でき、その進行状況はこちらで見守ることができます: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)。</span><span class="sxs-lookup"><span data-stu-id="8e56f-127">You can see one of the proposals for bringing back content files, and follow its progress, here: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span></span>

## <a name="impact-for-package-authors"></a><span data-ttu-id="8e56f-128">パッケージの作成者への影響</span><span class="sxs-lookup"><span data-stu-id="8e56f-128">Impact for package authors</span></span>

<span data-ttu-id="8e56f-129">上記の機能を使用するパッケージでは、別のメカニズムを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8e56f-129">Packages using the above features would have to use a different mechanism.</span></span> <span data-ttu-id="8e56f-130">このために一般的に最も便利なメカニズムは、引き続き完全にサポートされる MSBuild ターゲット/プロパティになります。</span><span class="sxs-lookup"><span data-stu-id="8e56f-130">The most commonly useful mechanism for this would be the MSBuild targets/props that continues to get fully supported.</span></span> <span data-ttu-id="8e56f-131">ビルド システムでは、パッケージでその他の規則を選ぶことができます。</span><span class="sxs-lookup"><span data-stu-id="8e56f-131">The build system can choose to pick up other conventions in the package.</span></span> <span data-ttu-id="8e56f-132">このようにして、MSBuild ターゲットが Roslyn アナライザーと同様にサポートされます。</span><span class="sxs-lookup"><span data-stu-id="8e56f-132">This is how MSBuild targets are supported as well as Roslyn analyzers.</span></span> <span data-ttu-id="8e56f-133">`packages.config` と `project.json` シナリオ用にターゲットとアナライザーをサポートするパッケージをビルドできます。</span><span class="sxs-lookup"><span data-stu-id="8e56f-133">It is possible to build packages that supports targets and analyzers for `packages.config` and `project.json` scenarios.</span></span>

<span data-ttu-id="8e56f-134">スタートアップが簡単になるように、プロジェクトを変更しようとするパッケージは、通常、ごく限られたシナリオのセットで動作するため、代わりに readme、またはパッケージの使用方法に関するガイダンスを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8e56f-134">Packages that attempt to modify the project to ease startup typically work in a very limited set of scenarios, and should instead provide a readme, or guidance on how to use the package.</span></span>

<span data-ttu-id="8e56f-135">以下に示すパッケージ形式を使用するには、既存のパッケージはほとんど必要ありません。</span><span class="sxs-lookup"><span data-stu-id="8e56f-135">Most existing packages should not need to use the package format described below.</span></span>

<span data-ttu-id="8e56f-136">この形式では、最も重要視されるシナリオとしてネイティブ コンテンツを有効にします。</span><span class="sxs-lookup"><span data-stu-id="8e56f-136">The format enables native content as a first class scenario.</span></span> <span data-ttu-id="8e56f-137">つまり、マネージ アセンブリは、ターゲット プラットフォームに基づいたマネージ アセンブリと一緒にバイナリの実装を配布する、ハードウェアの実装に近いかによって異なるということです。</span><span class="sxs-lookup"><span data-stu-id="8e56f-137">This means that managed assemblies depending on close to hardware implementations to ship binary implementations alongside the managed assemblies based on the target platform.</span></span> <span data-ttu-id="8e56f-138">たとえば、System.IO.Compression パッケージでは、このテクノロジを使用しています。</span><span class="sxs-lookup"><span data-stu-id="8e56f-138">For example System.IO.Compression package is utilizing this technology.</span></span> [<span data-ttu-id="8e56f-139">https://www.nuget.org/packages/System.IO.Compression</span><span class="sxs-lookup"><span data-stu-id="8e56f-139">https://www.nuget.org/packages/System.IO.Compression</span></span>](https://www.nuget.org/packages/System.IO.Compression)

<span data-ttu-id="8e56f-140">要約すると、上記の機能が絶対に必要というわけではない場合、ここで説明されている形式は NuGet 3.x 以降によってのみサポートされるので、既存のパッケージ形式と一緒にしておくことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="8e56f-140">In summary if the functionality above is not absolutely necessary, we recommend sticking with the existing package format, as the format described here is supported only by NuGet 3.x+.</span></span>

<span data-ttu-id="8e56f-141">shim を使用して `packages.config` と `project.json` の両方のシナリオに機能するように、パッケージをビルドすることはできますが、上述の使用されていない機能ではなく、従来の方法でパッケージを構築すると簡単なことが多いです。</span><span class="sxs-lookup"><span data-stu-id="8e56f-141">It would be possible to build packages to work for both `packages.config` and `project.json` scenarios through shimming, however it's often simpler to just structure the packages the traditional way, without the deprecated features mentioned above.</span></span>

## <a name="3x-package-format"></a><span data-ttu-id="8e56f-142">3.x のパッケージ形式</span><span class="sxs-lookup"><span data-stu-id="8e56f-142">3.x package format</span></span>

<span data-ttu-id="8e56f-143">3.x のパッケージ形式は、NuGet 2.x を超える次のいくつかの追加機能を許可します。</span><span class="sxs-lookup"><span data-stu-id="8e56f-143">The 3.x package format allows for several additional features beyond NuGet 2.x:</span></span>

1. <span data-ttu-id="8e56f-144">コンパイルに使用される参照アセンブリとさまざまなプラットフォーム/デバイス上のランタイムに使用される実装アセンブリのセットを定義する。</span><span class="sxs-lookup"><span data-stu-id="8e56f-144">Defining a reference assembly used for compilation and a set of implementation assemblies used for runtime on different platforms/devices.</span></span> <span data-ttu-id="8e56f-145">この機能では、コンシューマーに一般的なセキュリティを提供しながら、プラットフォーム固有の API を利用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="8e56f-145">Which allows you to take advantage of platform specific APIs while providing a common surface area for your consumers.</span></span> <span data-ttu-id="8e56f-146">特に、中間ポータブル ライブラリの記述が簡単になります。</span><span class="sxs-lookup"><span data-stu-id="8e56f-146">Specifically this makes writing intermediate portable libraries easier.</span></span>

1. <span data-ttu-id="8e56f-147">パッケージがプラットフォーム (例: オペレーティング システム、CPU アーキテクチャ) でピボットすることを許可する。</span><span class="sxs-lookup"><span data-stu-id="8e56f-147">Allows packages to pivot on platforms e.g. operating systems or CPU architecture.</span></span>

1. <span data-ttu-id="8e56f-148">コンパニオン パッケージに対してプラットフォーム固有の実装の分離を許可する。</span><span class="sxs-lookup"><span data-stu-id="8e56f-148">Allows for separation of platform specific implementations to companion packages.</span></span>

1. <span data-ttu-id="8e56f-149">最も重要視される依存関係として、ネイティブの依存関係をサポートする。</span><span class="sxs-lookup"><span data-stu-id="8e56f-149">Support Native dependencies as a first class citizen.</span></span>