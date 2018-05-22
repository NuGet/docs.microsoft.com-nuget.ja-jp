---
title: NuGet packages.config ファイル参照
description: 一部のプロジェクト タイプでは、packages.config で、プロジェクトで使用される NuGet パッケージの一覧が保守管理されます。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: e10bc1625bc4cea7b7befe18caa22d33a876489b
ms.sourcegitcommit: f0b31af805183cf3a98eabb504e16d9b05223cfe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2018
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="8c0b4-103">packages.config 参照</span><span class="sxs-lookup"><span data-stu-id="8c0b4-103">packages.config reference</span></span>

<span data-ttu-id="8c0b4-104">`packages.config` ファイルは、プロジェクトで参照されるパッケージの一覧を保守管理するために、一部のプロジェクト タイプで使用されます。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-104">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="8c0b4-105">それにより、NuGet は、ビルド サーバーなど、別のコンピューターにプロジェクトを転送するとき、一部のパッケージだけでプロジェクトの依存関係を簡単に復元できます。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-105">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

<span data-ttu-id="8c0b4-106">このオプションを使用すると場合、`packages.config`は通常、プロジェクトのルートに配置します。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-106">If used, `packages.config` is typically located in a project root.</span></span> <span data-ttu-id="8c0b4-107">最初の NuGet 操作が実行すると、作成することも手動でなど、どのようなコマンドを実行する前にときに自動的に作成された`nuget restore`です。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-107">It's automatically created when the first NuGet operation is run, but can also be created manually before running any commands such as `nuget restore`.</span></span>

<span data-ttu-id="8c0b4-108">使用するプロジェクト[PackageReference](../consume-packages/Package-References-in-Project-Files.md)を使わない`packages.config`です。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-108">Projects that use [PackageReference](../consume-packages/Package-References-in-Project-Files.md) do not use `packages.config`.</span></span>

## <a name="schema"></a><span data-ttu-id="8c0b4-109">Schema</span><span class="sxs-lookup"><span data-stu-id="8c0b4-109">Schema</span></span>

<span data-ttu-id="8c0b4-110">このスキーマは単純です。標準の XML ヘッダーは、1 つまたは複数の `<packages>` 要素を含むシングル `<package>` ノードです。要素は参照ごとに 1 つになります。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-110">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="8c0b4-111">各 `<package>` 要素に次の属性を指定できます。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-111">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="8c0b4-112">属性</span><span class="sxs-lookup"><span data-stu-id="8c0b4-112">Attribute</span></span> | <span data-ttu-id="8c0b4-113">必須</span><span class="sxs-lookup"><span data-stu-id="8c0b4-113">Required</span></span> | <span data-ttu-id="8c0b4-114">説明</span><span class="sxs-lookup"><span data-stu-id="8c0b4-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8c0b4-115">ID</span><span class="sxs-lookup"><span data-stu-id="8c0b4-115">id</span></span> | <span data-ttu-id="8c0b4-116">[はい]</span><span class="sxs-lookup"><span data-stu-id="8c0b4-116">Yes</span></span> | <span data-ttu-id="8c0b4-117">Newtonsoft.json や Microsoft.AspNet.Mvc など、パッケージの識別子。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-117">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="8c0b4-118">version</span><span class="sxs-lookup"><span data-stu-id="8c0b4-118">version</span></span> | <span data-ttu-id="8c0b4-119">[はい]</span><span class="sxs-lookup"><span data-stu-id="8c0b4-119">Yes</span></span> | <span data-ttu-id="8c0b4-120">3.1.1 や 4.2.5.11-beta など、インストールするパッケージの正確なバージョン。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-120">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="8c0b4-121">バージョン文字列には少なくとも 3 つの数字を含める必要があります。4 番目はプレリリース サフィックスであり、任意です。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-121">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="8c0b4-122">範囲は許可されません。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-122">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="8c0b4-123">targetFramework</span><span class="sxs-lookup"><span data-stu-id="8c0b4-123">targetFramework</span></span> | <span data-ttu-id="8c0b4-124">いいえ</span><span class="sxs-lookup"><span data-stu-id="8c0b4-124">No</span></span> | <span data-ttu-id="8c0b4-125">[ターゲット フレームワーク モニカー (TFM)](target-frameworks.md) はパッケージのインストール時に適用されます。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-125">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="8c0b4-126">パッケージのインストール時、これは最初、プロジェクトのターゲットに設定されます。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-126">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="8c0b4-127">結果的に、異なる `<package>` 要素に異なる TFM が与えられます。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-127">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="8c0b4-128">たとえば、.NET 4.5.2 を対象とするプロジェクトを作成する場合、そのポイントでインストールされたパッケージは net452 の TFM を使用します。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-128">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="8c0b4-129">後でプロジェクトのターゲットを .NET 4.6 に変更し、パッケージを追加する場合、net46 の TFM が使用されます。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-129">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="8c0b4-130">プロジェクトのターゲットと `targetFramework` 属性に不一致があると警告が出ます。その場合、影響が出たパッケージを再インストールできます。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-130">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="8c0b4-131">allowedVersions</span><span class="sxs-lookup"><span data-stu-id="8c0b4-131">allowedVersions</span></span> | <span data-ttu-id="8c0b4-132">いいえ</span><span class="sxs-lookup"><span data-stu-id="8c0b4-132">No</span></span> | <span data-ttu-id="8c0b4-133">パッケージ更新中に適用された、このパッケージの許可されるバージョンの範囲 ([アップグレード バージョンの制約](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)ページをご覧ください)。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-133">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="8c0b4-134">インストール操作中または復元操作中にインストールされるパッケージには影響を*与えません*。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-134">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="8c0b4-135">構文については、「[Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards)」(パッケージのバージョン管理) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-135">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for syntax.</span></span> <span data-ttu-id="8c0b4-136">PackageManager UI も、許可される範囲外のすべてのバージョンを無効にします。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-136">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="8c0b4-137">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="8c0b4-137">developmentDependency</span></span> | <span data-ttu-id="8c0b4-138">いいえ</span><span class="sxs-lookup"><span data-stu-id="8c0b4-138">No</span></span> | <span data-ttu-id="8c0b4-139">コンシューミング プロジェクト自体で NuGet パッケージが作成される場合、依存関係に対してこれを `true` に設定すると、そのパッケージがコンシューミング パッケージの作成時に含まれません。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-139">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="8c0b4-140">既定値は、`false` です。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-140">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="8c0b4-141">使用例</span><span class="sxs-lookup"><span data-stu-id="8c0b4-141">Examples</span></span>

<span data-ttu-id="8c0b4-142">次の `packages.config` は 2 つの依存関係を参照します。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-142">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="8c0b4-143">次の `packages.config` は 9 つのパッケージを参照しますが、`developmentDependency` 属性に起因し、`Microsoft.Net.Compilers` はコンシューミング パッケージのビルド時に含まれません。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-143">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="8c0b4-144">Newtonsoft.Json の参照はまた、更新を 8.x バージョンと 9.x バージョンのみに制限します。</span><span class="sxs-lookup"><span data-stu-id="8c0b4-144">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
