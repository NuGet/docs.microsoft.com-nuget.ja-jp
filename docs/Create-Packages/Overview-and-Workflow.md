---
title: "NuGet パッケージの作成の概要とワークフロー | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet パッケージの作成と発行プロセスの概要と、プロセスの他の特定の部分へのリンク。"
keywords: "NuGet パッケージの作成, NuGet 作成の概要, NuGet 作成のワークフロー, パッケージ作成ワークフロー, パッケージ作成の概要。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 46d7737d57a91ee7b0434f4695c393423730c7bc
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2018
---
# <a name="package-creation-workflow"></a><span data-ttu-id="05c52-104">パッケージ作成ワークフロー</span><span class="sxs-lookup"><span data-stu-id="05c52-104">Package creation workflow</span></span>

<span data-ttu-id="05c52-105">パッケージの作成はコンパイル済みコード (通常は .NET アセンブリ) から始めます。このコードはパッケージ化して、パブリック nuget.org ギャラリーまたは組織内のプライベート ギャラリーを通じて他のユーザーと共有します。</span><span class="sxs-lookup"><span data-stu-id="05c52-105">Creating a package starts with the compiled code (typically .NET assemblies) that you want to package and share with others, either through the public nuget.org gallery or a private gallery within your organization.</span></span> <span data-ttu-id="05c52-106">パッケージには、パッケージのインストール時に表示される Readme などの追加ファイルを含めることができます。また、特定のプロジェクト ファイルへの変換を含めることもできます。</span><span class="sxs-lookup"><span data-stu-id="05c52-106">The package can also include additional files such as a readme that is displayed when the package is installed, and can include transformations to certain project files.</span></span>

<span data-ttu-id="05c52-107">パッケージは、独自のコードを含めずに、任意の数の他の依存関係にプルする場合にも対応できます。</span><span class="sxs-lookup"><span data-stu-id="05c52-107">A package can also serve to only pull in any number of other dependencies, without containing any code of its own.</span></span> <span data-ttu-id="05c52-108">このようなパッケージは、複数の独立したパッケージで構成される SDK を配信する便利な方法です。</span><span class="sxs-lookup"><span data-stu-id="05c52-108">Such a package is a convenient way to deliver an SDK that's composed of multiple independent packages.</span></span> <span data-ttu-id="05c52-109">その他の場合、パッケージにはデバッグを支援するシンボル (`.pdb`) ファイルのみを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="05c52-109">In other cases, a package may contain only symbol (`.pdb`) files to aid debugging.</span></span>

> [!Note]
> <span data-ttu-id="05c52-110">他の開発者が使用するパッケージを作成する場合は、他の開発者が自分の作業に依存していることを理解することが重要です。</span><span class="sxs-lookup"><span data-stu-id="05c52-110">When you create a package for use by other developers, it's important to understand that they are taking a dependency on your work.</span></span> <span data-ttu-id="05c52-111">したがって、パッケージの作成と発行は、バグの修正とその他の更新を行うことへのコミットメントも意味します。また、容易に保持できるように、少なくともパッケージをオープン ソースとして使用できるようにすることへのコミットメントも意味します。</span><span class="sxs-lookup"><span data-stu-id="05c52-111">As such, creating and publishing a package also implies a commitment to fixing bugs and making other updates, or at the very least making the package available as open source so others can help to maintain it.</span></span>

<span data-ttu-id="05c52-112">いずれにせよ、パッケージの作成は、パッケージ化するアセンブリと他のファイルを決定することから始まります。</span><span class="sxs-lookup"><span data-stu-id="05c52-112">Whatever the case, creating a package begins with deciding which assemblies and other files to package.</span></span> <span data-ttu-id="05c52-113">次に、マニフェスト ファイル (`.nuspec` ファイルと呼ばれる) を作成し、パッケージの ID、バージョン番号、著作権情報、MSBuild のプロパティとターゲットなどと共にパッケージの内容を記述します。</span><span class="sxs-lookup"><span data-stu-id="05c52-113">You then create a manifest file, referred to as a `.nuspec` file, to describe the package's contents along with its identifer, version number, copyright information, MSBuild props and targets, and much more.</span></span>

<span data-ttu-id="05c52-114">適切なフォルダーに必要なファイルをすべて準備し、適切な `.nuspec` ファイルを作成したら、次は、`nuget pack` コマンド (または [MSBuild パック ターゲット](../reference/msbuild-targets.md)) を使用して、`.nupkg` ファイルにすべてまとめます。</span><span class="sxs-lookup"><span data-stu-id="05c52-114">When you've prepared all the necessary files in the appropriate folders and have created the appropriate `.nuspec` file, you then use the `nuget pack` command (or the [MSBuild pack target](../reference/msbuild-targets.md)) to put everything together into a `.nupkg` file.</span></span> <span data-ttu-id="05c52-115">これで、ホストが他の開発者に使用できるようにするどのパッケージでも配置できます。</span><span class="sxs-lookup"><span data-stu-id="05c52-115">You're then ready to deploy the package to whatever host makes it available to other developers.</span></span>

> [!Tip]
> <span data-ttu-id="05c52-116">`.nupkg` 拡張子を持つ NuGet パッケージは単なる ZIP ファイルです。</span><span class="sxs-lookup"><span data-stu-id="05c52-116">A NuGet package with the `.nupkg` extension is simply a ZIP file.</span></span> <span data-ttu-id="05c52-117">パッケージの内容を簡単に確認するには、拡張子を `.zip` に変更し、その内容を通常どおり展開します。</span><span class="sxs-lookup"><span data-stu-id="05c52-117">To easily examine any package's contents, change the extension to `.zip` and expand its contents as usual.</span></span> <span data-ttu-id="05c52-118">念のため、ホストへのアップロードを試行する前に拡張子を `.nupkg` に戻してください。</span><span class="sxs-lookup"><span data-stu-id="05c52-118">Just be sure to change the extension back to `.nupkg` before attempting to upload it to a host.</span></span>

<span data-ttu-id="05c52-119">作成プロセスを学習して理解するために、まず、「[Creating a package](../create-packages/creating-a-package.md)」 (パッケージの作成) を参照してください。ここでは、すべてのパッケージに共通の中核となるプロセスについて説明されています。</span><span class="sxs-lookup"><span data-stu-id="05c52-119">To learn and understand the creation process, start with [Creating a package](../create-packages/creating-a-package.md) which guides you through the core processes common to all packages.</span></span>

<span data-ttu-id="05c52-120">そこから、パッケージの他の多くのオプションを検討することができます。</span><span class="sxs-lookup"><span data-stu-id="05c52-120">From there, you can consider a number of other options for your package:</span></span>

- <span data-ttu-id="05c52-121">「[Supporting Multiple Target Frameworks](../create-packages/supporting-multiple-target-frameworks.md)」 (複数のターゲット フレームワークのサポート) では、さまざまな .NET Framework の複数のバリアントを含むパッケージを作成する方法が説明されています。</span><span class="sxs-lookup"><span data-stu-id="05c52-121">[Supporting Multiple Target Frameworks](../create-packages/supporting-multiple-target-frameworks.md) describes how to create a package with multiple variants for different .NET Frameworks.</span></span>
- <span data-ttu-id="05c52-122">「[Creating Localized Packages](../create-packages/creating-localized-packages.md)」 (ローカライズされたパッケージの作成) では、複数の言語リソースを含むパッケージを構築する方法と、個別のローカライズされたサテライト パッケージを使用する方法が説明されています。</span><span class="sxs-lookup"><span data-stu-id="05c52-122">[Creating Localized Packages](../create-packages/creating-localized-packages.md) describes how to structure a package with multiple language resources and how to use separate localized satellite packages.</span></span>
- <span data-ttu-id="05c52-123">「[Pre-release Packages](../create-packages/prerelease-packages.md)」 (プレリリース パッケージ) では、アルファ、ベータ、rc パッケージをそれらに関心のあるユーザー向けにリリースする方法が示されています。</span><span class="sxs-lookup"><span data-stu-id="05c52-123">[Pre-release Packages](../create-packages/prerelease-packages.md) demonstrates how to release alpha, beta, and rc packages to those customers who are interested.</span></span>
- <span data-ttu-id="05c52-124">「[Source and Config File Transformations](../create-packages/source-and-config-file-transformations.md)」 (ソースと構成ファイルの変換) では、プロジェクトに追加されたファイルでの一方向のトークン置換を実行する方法と、パッケージのアンインストール時に取り消すこともできる設定を使用して `web.config` と `app.config` を変更する方法が説明されています。</span><span class="sxs-lookup"><span data-stu-id="05c52-124">[Source and Config File Transformations](../create-packages/source-and-config-file-transformations.md) describes how you can do both one-way token replacements in files that are added to a project, and modify `web.config` and `app.config` with settings that are also backed out when the package is uninstalled.</span></span>
- <span data-ttu-id="05c52-125">「[Symbol Packages](../create-packages/symbol-packages.md)」 (シンボル パッケージ) では、コンシューマーがデバッグ時にコードにステップ インできるように、ライブラリでシンボルを提供するためのガイダンスが提供されています。</span><span class="sxs-lookup"><span data-stu-id="05c52-125">[Symbol Packages](../create-packages/symbol-packages.md) offers guidance for supplying symbols for your library that allow consumers to step into your code while debugging.</span></span>
- <span data-ttu-id="05c52-126">「[Package versioning](../reference/package-versioning.md)」 (パッケージのバージョン管理) では、依存関係 (自分のパッケージから利用する他のパッケージ) がある場合に使用できる正確なバージョンを特定する方法が説明されています。</span><span class="sxs-lookup"><span data-stu-id="05c52-126">[Package versioning](../reference/package-versioning.md) discusses how to identify the exact versions that you allow for your dependencies (other packages that you consume from your package).</span></span>
- <span data-ttu-id="05c52-127">「[Native Packages](../create-packages/native-packages.md)」 (ネイティブ パッケージ) では、C++ コンシューマー用のパッケージの作成プロセスが説明されています。</span><span class="sxs-lookup"><span data-stu-id="05c52-127">[Native Packages](../create-packages/native-packages.md) describes the process for creating a package for C++ consumers.</span></span>

<span data-ttu-id="05c52-128">nuget.org にパッケージを発行する準備ができたら、「[Publish a package](../create-packages/publish-a-package.md)」 (パッケージの発行) の簡単なプロセスに従います。</span><span class="sxs-lookup"><span data-stu-id="05c52-128">When you're then ready to publish a package to nuget.org, follow the simple process in [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="05c52-129">nuget.org ではなくプライベート フィードを使用する場合は、[パッケージのホスティングの概要](../hosting-packages/overview.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="05c52-129">If you want to use a private feed instead of nuget.org, see the [Hosting Packages Overview](../hosting-packages/overview.md)</span></span>
