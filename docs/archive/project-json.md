---
title: "NuGet の project.json ファイル リファレンス | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/27/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "一部のプロジェクト タイプでは、project.json で、プロジェクトで使用される NuGet パッケージの一覧が保守管理されます。"
keywords: "NuGet project.json、NuGet パッケージ参照、NuGet の依存関係、project.lock.json"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2e2c521b18dd67e49942cc20eafef0be7f91573a
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="projectjson-reference"></a><span data-ttu-id="3b988-104">project.json 参照</span><span class="sxs-lookup"><span data-stu-id="3b988-104">project.json reference</span></span>

<span data-ttu-id="3b988-105">*NuGet 3.x 以降*</span><span class="sxs-lookup"><span data-stu-id="3b988-105">*NuGet 3.x+*</span></span>

<span data-ttu-id="3b988-106">`project.json` ファイルは、パッケージ参照形式と呼ばれるプロジェクトで使用されるパッケージのリストを保持します。</span><span class="sxs-lookup"><span data-stu-id="3b988-106">The `project.json` file maintains a list of packages used in a project, known as a package reference format.</span></span> <span data-ttu-id="3b988-107">これは `packages.config` に優先しますが、NuGet 4.0 以降では、[PackageReference](../consume-packages/package-references-in-project-files.md) によって置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="3b988-107">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="3b988-108">[`project.lock.json`](#projectlockjson) ファイル (後述) も、`project.json` を使用するプロジェクトで使用されます。</span><span class="sxs-lookup"><span data-stu-id="3b988-108">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="3b988-109">`project.json` には次の基本構造があります。4 つの最上位レベルのオブジェクトのそれぞれが任意の数の子オブジェクトを持つことができます。</span><span class="sxs-lookup"><span data-stu-id="3b988-109">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }
}
```

## <a name="dependencies"></a><span data-ttu-id="3b988-110">依存関係</span><span class="sxs-lookup"><span data-stu-id="3b988-110">Dependencies</span></span>

<span data-ttu-id="3b988-111">プロジェクトの NuGet パッケージの依存関係を次の形式でリストします。</span><span class="sxs-lookup"><span data-stu-id="3b988-111">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="3b988-112">例:</span><span class="sxs-lookup"><span data-stu-id="3b988-112">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="3b988-113">`dependencies` セクションは、NuGet パッケージ マネージャー ダイアログがプロジェクトにパッケージの依存関係を追加する場所です。</span><span class="sxs-lookup"><span data-stu-id="3b988-113">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="3b988-114">パッケージ ID は、nuget.org のパッケージ ID に対応しています。これはパッケージ マネージャー コンソールで使用される ID と同じです。`Install-Package Microsoft.NETCore`</span><span class="sxs-lookup"><span data-stu-id="3b988-114">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="3b988-115">パッケージを復元するときに、`"5.0.0"` のバージョンの制約は `>= 5.0.0` を意味します。</span><span class="sxs-lookup"><span data-stu-id="3b988-115">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="3b988-116">つまり、サーバーで 5.0.0 は使用できないが 5.0.1 は使用できる場合、NuGet は 5.0.1 をインストールし、アップグレードに関する警告を発します。</span><span class="sxs-lookup"><span data-stu-id="3b988-116">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="3b988-117">それ以外の場合は、NuGet は制約に一致するサーバー上で使用可能な最も低いバージョンを選択します。</span><span class="sxs-lookup"><span data-stu-id="3b988-117">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="3b988-118">解決ルールの詳細については、[依存関係の解決](../consume-packages/dependency-resolution.md)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="3b988-118">See [Dependency resolution](../consume-packages/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="3b988-119">依存関係アセットの管理</span><span class="sxs-lookup"><span data-stu-id="3b988-119">Managing dependency assets</span></span>

<span data-ttu-id="3b988-120">依存関係からどのアセットを最上位レベルのプロジェクトにフローするかは、依存関係の参照の `include` プロパティと `exclude` プロパティでコンマ区切りのタグのセットを指定することで制御できます。</span><span class="sxs-lookup"><span data-stu-id="3b988-120">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="3b988-121">タグを次の表に一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="3b988-121">The tags are listed the table below:</span></span>

| <span data-ttu-id="3b988-122">包含/除外タグ</span><span class="sxs-lookup"><span data-stu-id="3b988-122">Include/Exclude tag</span></span> | <span data-ttu-id="3b988-123">ターゲットの影響を受けるフォルダー</span><span class="sxs-lookup"><span data-stu-id="3b988-123">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="3b988-124">contentFiles</span><span class="sxs-lookup"><span data-stu-id="3b988-124">contentFiles</span></span> | <span data-ttu-id="3b988-125">Content</span><span class="sxs-lookup"><span data-stu-id="3b988-125">Content</span></span>  |
| <span data-ttu-id="3b988-126">ランタイム</span><span class="sxs-lookup"><span data-stu-id="3b988-126">runtime</span></span> | <span data-ttu-id="3b988-127">Runtime、Resources、FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="3b988-127">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="3b988-128">compile</span><span class="sxs-lookup"><span data-stu-id="3b988-128">compile</span></span> | <span data-ttu-id="3b988-129">lib</span><span class="sxs-lookup"><span data-stu-id="3b988-129">lib</span></span> |
| <span data-ttu-id="3b988-130">ビルド</span><span class="sxs-lookup"><span data-stu-id="3b988-130">build</span></span> | <span data-ttu-id="3b988-131">build (MSBuild のプロパティとターゲット)</span><span class="sxs-lookup"><span data-stu-id="3b988-131">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="3b988-132">native</span><span class="sxs-lookup"><span data-stu-id="3b988-132">native</span></span> | <span data-ttu-id="3b988-133">native</span><span class="sxs-lookup"><span data-stu-id="3b988-133">native</span></span> |
| <span data-ttu-id="3b988-134">none</span><span class="sxs-lookup"><span data-stu-id="3b988-134">none</span></span> | <span data-ttu-id="3b988-135">フォルダーなし</span><span class="sxs-lookup"><span data-stu-id="3b988-135">No folders</span></span> |
| <span data-ttu-id="3b988-136">すべて</span><span class="sxs-lookup"><span data-stu-id="3b988-136">all</span></span> | <span data-ttu-id="3b988-137">すべてのフォルダー</span><span class="sxs-lookup"><span data-stu-id="3b988-137">All folders</span></span> |

<span data-ttu-id="3b988-138">`exclude` で指定されているタグの方が、`include` で指定されているタグより優先されます。</span><span class="sxs-lookup"><span data-stu-id="3b988-138">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="3b988-139">たとえば、`include="runtime, compile" exclude="compile"` は `include="runtime"` と同じです。</span><span class="sxs-lookup"><span data-stu-id="3b988-139">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="3b988-140">たとえば、依存関係の `build` フォルダーと `native` フォルダーを含めるには、次を使用します。</span><span class="sxs-lookup"><span data-stu-id="3b988-140">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

<span data-ttu-id="3b988-141">依存関係の `content` フォルダーと `build` フォルダーを除外するには、次を使用します。</span><span class="sxs-lookup"><span data-stu-id="3b988-141">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a><span data-ttu-id="3b988-142">フレームワーク</span><span class="sxs-lookup"><span data-stu-id="3b988-142">Frameworks</span></span>

<span data-ttu-id="3b988-143">プロジェクトを実行するフレームワーク (`net45`、`netcoreapp`、`netstandard` など) をリストします。</span><span class="sxs-lookup"><span data-stu-id="3b988-143">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="3b988-144">`frameworks` セクションでは、1 つのエントリのみが許可されます </span><span class="sxs-lookup"><span data-stu-id="3b988-144">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="3b988-145">(例外は、使用されていない DNX ツールチェーンでビルドされた ASP.NET プロジェクトの `project.json` ファイルで、これは複数のターゲットを許可します)。</span><span class="sxs-lookup"><span data-stu-id="3b988-145">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX toolchain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="3b988-146">Runtimes</span><span class="sxs-lookup"><span data-stu-id="3b988-146">Runtimes</span></span>

<span data-ttu-id="3b988-147">アプリを実行するオペレーティング システムとアーキテクチャ (`win10-arm`、`win8-x64`、`win8-x86`) をリストします。</span><span class="sxs-lookup"><span data-stu-id="3b988-147">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

<span data-ttu-id="3b988-148">任意のランタイムで実行できる PCL を含むパッケージは、ランタイムを指定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="3b988-148">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="3b988-149">これはどの依存関係にも当てはまります。それ以外の場合は、ランタイムを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3b988-149">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="3b988-150">Supports</span><span class="sxs-lookup"><span data-stu-id="3b988-150">Supports</span></span>

<span data-ttu-id="3b988-151">パッケージの依存関係のチェックのセットを定義します。</span><span class="sxs-lookup"><span data-stu-id="3b988-151">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="3b988-152">PCL またはアプリの実行を想定している場所を定義できます。</span><span class="sxs-lookup"><span data-stu-id="3b988-152">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="3b988-153">他の場所でもコードを実行できるように、定義は制限が緩くなっています。</span><span class="sxs-lookup"><span data-stu-id="3b988-153">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="3b988-154">しかしこれらのチェックを指定すると、NuGet はリストされている TxMs ですべての依存関係が満たされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="3b988-154">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="3b988-155">この値の例には、`net46.app`、`uwp.10.0.app` などがあります。</span><span class="sxs-lookup"><span data-stu-id="3b988-155">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="3b988-156">このセクションは、ポータブル クラス ライブラリのターゲット ダイアログでエントリを選択する際に、自動的に設定される必要があります。</span><span class="sxs-lookup"><span data-stu-id="3b988-156">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="3b988-157">Imports</span><span class="sxs-lookup"><span data-stu-id="3b988-157">Imports</span></span>

<span data-ttu-id="3b988-158">Imports は、`dotnet` TxM を使用するパッケージに、dotnet TxM を宣言しないパッケージで動作することを許可するように設計されています。</span><span class="sxs-lookup"><span data-stu-id="3b988-158">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="3b988-159">プロジェクトが `dotnet` TxM を使用している場合、以下を `project.json` に追加して非 `dotnet` プラットフォームを `dotnet` 対応にしない限り、依存するすべてのパッケージにも `dotnet` TxM が必要です。</span><span class="sxs-lookup"><span data-stu-id="3b988-159">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="3b988-160">`dotnet` TxM を使用している場合、PCL プロジェクト システムは、サポートされているターゲットに基づいて適切な `imports` ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="3b988-160">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="3b988-161">ポータブル アプリと Web プロジェクトとの違い</span><span class="sxs-lookup"><span data-stu-id="3b988-161">Differences from portable apps and web projects</span></span>

<span data-ttu-id="3b988-162">NuGet によって使用される `project.json` ファイルは、ASP.NET Core プロジェクト内にあるサブセットです。</span><span class="sxs-lookup"><span data-stu-id="3b988-162">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="3b988-163">ASP.NET Core では、`project.json` がプロジェクト メタデータ、コンパイルの情報、および依存関係のために使用されます。</span><span class="sxs-lookup"><span data-stu-id="3b988-163">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="3b988-164">他のプロジェクト システムで使用する場合は、これら 3 つが個別のファイルに分割され、`project.json` に含まれる情報が少なくなります。</span><span class="sxs-lookup"><span data-stu-id="3b988-164">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="3b988-165">重要な違いは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="3b988-165">Notable differences include:</span></span>

- <span data-ttu-id="3b988-166">`frameworks` セクションには 1 つのフレームワークしか存在できません。</span><span class="sxs-lookup"><span data-stu-id="3b988-166">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="3b988-167">ファイルには、DNX `project.json` ファイルで見られる、依存関係、コンパイル オプションなどを含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="3b988-167">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="3b988-168">1 つのフレームワークしか存在できない場合は、フレームワーク固有の依存関係を入力する意味はありません。</span><span class="sxs-lookup"><span data-stu-id="3b988-168">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="3b988-169">コンパイルは MSBuild によって処理されるため、コンパイル オプション、プリプロセッサ定義などはすべて、`project.json` ではなく、MSBuild プロジェクト ファイルの一部です。</span><span class="sxs-lookup"><span data-stu-id="3b988-169">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="3b988-170">NuGet 3 以降では、Visual Studio のパッケージ マネージャー UI がコンテンツを操作するため、開発者が手動で `project.json` を編集する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="3b988-170">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="3b988-171">ただし、ファイルを編集することはできますが、プロジェクトをビルドしてパッケージの復元を開始するか、または別の方法で復元を呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="3b988-171">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="3b988-172">「[パッケージの復元](../consume-packages/package-restore.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3b988-172">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="3b988-173">project.lock.json</span><span class="sxs-lookup"><span data-stu-id="3b988-173">project.lock.json</span></span>

<span data-ttu-id="3b988-174">`project.lock.json` ファイルは、`project.json` を使用するプロジェクトで NuGet パッケージを復元する過程で生成されます。</span><span class="sxs-lookup"><span data-stu-id="3b988-174">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="3b988-175">このファイルには、NuGet がグラフ全体を処理する際に生成されたすべての情報のスナップショットが保持され、プロジェクトのすべてのパッケージのバージョン、コンテンツ、依存関係が含まれます。</span><span class="sxs-lookup"><span data-stu-id="3b988-175">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="3b988-176">ビルド システムはこれを使用して、プロジェクト自体のローカル パッケージ フォルダーに依存する代わりに、プロジェクトのビルド時に関連するグローバルな場所からパッケージを選択します。</span><span class="sxs-lookup"><span data-stu-id="3b988-176">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="3b988-177">この結果、多くの個別の `.nuspec` ファイルの代わりに、`project.lock.json` のみを読み取ればよいため、ビルド パフォーマンスが向上します。</span><span class="sxs-lookup"><span data-stu-id="3b988-177">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="3b988-178">`project.lock.json` はパッケージの復元で自動的に生成されるため、`.gitignore` ファイルと `.tfignore`ファイルに追加することで、ソース管理から省くことができます ([パッケージとソース管理](../consume-packages/packages-and-source-control.md)に関するページを参照してください)。</span><span class="sxs-lookup"><span data-stu-id="3b988-178">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="3b988-179">ただし、これをソース管理に含めると、変更履歴に時間の経過と共に解決された依存関係の変更が示されます。</span><span class="sxs-lookup"><span data-stu-id="3b988-179">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
