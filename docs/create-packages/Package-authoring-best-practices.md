---
title: パッケージ作成のベスト プラクティス
description: 高品質な NuGet パッケージを作成するためのベスト プラクティスに関する一般的なガイドです。
author: chgill-MSFT
ms.author: chgill
ms.date: 09/17/2020
ms.topic: conceptual
ms.openlocfilehash: 7475cf655876f2c127e79a16ccf67c0c723d164f
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859071"
---
# <a name="package-authoring-best-practices"></a><span data-ttu-id="1112d-103">パッケージ作成のベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="1112d-103">Package authoring best practices</span></span>

<span data-ttu-id="1112d-104">このガイダンスの目的は、NuGet パッケージの作成者に対して、高品質なパッケージを作成および発行するための簡易なリファレンスを提供することです。</span><span class="sxs-lookup"><span data-stu-id="1112d-104">This guidance is intended to give NuGet package authors a lightweight reference to create and publish high-quality packages.</span></span> <span data-ttu-id="1112d-105">ここでは主に、メタデータやパックなどのパッケージ固有のベスト プラクティスに焦点を当てます。</span><span class="sxs-lookup"><span data-stu-id="1112d-105">It will primarily focus on package-specific best practices such as metadata and packing.</span></span> <span data-ttu-id="1112d-106">高品質なライブラリを構築するためのより詳細な提案については、.NET の「[オープン ソース ライブラリのガイダンス](https://docs.microsoft.com/dotnet/standard/library-guidance/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-106">For more in-depth suggestions for building high quality libraries, see the .NET [Open-source library guidance](https://docs.microsoft.com/dotnet/standard/library-guidance/).</span></span>

## <a name="types-of-recommendations"></a><span data-ttu-id="1112d-107">推奨事項の種類</span><span class="sxs-lookup"><span data-stu-id="1112d-107">Types of recommendations</span></span>

<span data-ttu-id="1112d-108">各記事で 4 種類の推奨事項 (**実施**、**検討**、**回避**、**実施しない**) が提示されます。</span><span class="sxs-lookup"><span data-stu-id="1112d-108">Each article presents four types of recommendations: **Do**, **Consider**, **Avoid**, and **Do not**.</span></span> <span data-ttu-id="1112d-109">推奨事項の種類は、どの程度厳密に従うべきかを示しています。</span><span class="sxs-lookup"><span data-stu-id="1112d-109">The type of recommendation indicates how closely it should be followed.</span></span>

<span data-ttu-id="1112d-110">**実施** の推奨事項にはほとんど常に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="1112d-110">You should almost always follow a **Do** recommendation.</span></span> <span data-ttu-id="1112d-111">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="1112d-111">For example:</span></span>

<span data-ttu-id="1112d-112">✔️ パッケージの目的について説明する、パッケージの簡単な説明を含めてください。</span><span class="sxs-lookup"><span data-stu-id="1112d-112">✔️ DO include a short description for your package that describes what it's for.</span></span>

<span data-ttu-id="1112d-113">その一方で、**検討** の推奨事項には一般に従うべきですが、その規則には正当な例外があります。</span><span class="sxs-lookup"><span data-stu-id="1112d-113">On the other hand, **Consider** recommendations should generally be followed, but there are legitimate exceptions to the rule:</span></span>

<span data-ttu-id="1112d-114">✔️ NuGet のプレフィックスの予約[条件](https://docs.microsoft.com/nuget/reference/id-prefix-reservation)を満たしているプレフィックスを持つ NuGet パッケージ名を選択することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-114">✔️ CONSIDER choosing a NuGet package name with a prefix that meets NuGet's prefix reservation [criteria](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).</span></span>

<span data-ttu-id="1112d-115">**回避** の推奨事項は一般には良いアイデアではありませんが、規則に違反することが効果的である場合があります。</span><span class="sxs-lookup"><span data-stu-id="1112d-115">**Avoid** recommendations mention things that are generally not a good idea, but breaking the rule sometimes makes sense:</span></span>

<span data-ttu-id="1112d-116">❌ 正確なバージョンを要求する NuGet パッケージ参照は回避してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-116">❌ AVOID NuGet package references that demand an exact version.</span></span>

<span data-ttu-id="1112d-117">最後に、**実施しない** の推奨事項は、ほとんどの場合でやってはいけないことを示しています。</span><span class="sxs-lookup"><span data-stu-id="1112d-117">And finally, **Do not** recommendations indicate something you should almost never do:</span></span>

<span data-ttu-id="1112d-118">❌ `LicenseUrl` メタデータ プロパティは使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="1112d-118">❌ DO NOT use the `LicenseUrl` metadata property.</span></span>

## <a name="create-a-nuget-package"></a><span data-ttu-id="1112d-119">NuGet パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="1112d-119">Create a NuGet package</span></span>

<span data-ttu-id="1112d-120">NuGet パッケージを作成するために推奨される最新の方法は、[SDK スタイルのプロジェクト](https://docs.microsoft.com/nuget/resources/check-project-format)から作成することです。</span><span class="sxs-lookup"><span data-stu-id="1112d-120">The latest recommended way to to create a NuGet package is from an [SDK-style project](https://docs.microsoft.com/nuget/resources/check-project-format).</span></span> <span data-ttu-id="1112d-121">[ターゲット フレームワーク](https://docs.microsoft.com/dotnet/standard/frameworks)や[パッケージ メタデータ](#package-metadata)など、SDK スタイルのプロジェクトのプロパティは、[プロジェクト ファイル](https://docs.microsoft.com/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file)に定義されています。</span><span class="sxs-lookup"><span data-stu-id="1112d-121">SDK-style project properties, including [target framework](https://docs.microsoft.com/dotnet/standard/frameworks) and [package metadata](#package-metadata), are defined in the [project file](https://docs.microsoft.com/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file).</span></span>

<span data-ttu-id="1112d-122">SDK スタイルのプロジェクトからパッケージを作成するには、必要なプロパティを定義し、[Visual Studio](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli) または [dotnet CLI](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli) でパックします。</span><span class="sxs-lookup"><span data-stu-id="1112d-122">Create a package from your SDK-style project by defining the required properties and packing in [Visual Studio](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli) or the [dotnet CLI](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli).</span></span>

<span data-ttu-id="1112d-123">✔️ SDK スタイルのプロジェクトを作成し、Visual Studio または dotnet CLI を使用してパッケージを作成 (パック) してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-123">✔️ DO create an SDK-style project and create (pack) your package using Visual Studio or the dotnet CLI.</span></span>

<span data-ttu-id="1112d-124">必要なクライアント ツール、プロジェクト ファイルの例、コマンドなど、パッケージの作成に関するより詳細なガイダンスについては、「[dotnet CLI を使用して NuGet パッケージを作成する](https://docs.microsoft.com/nuget/create-packages/creating-a-package-dotnet-cli)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-124">For more detailed guidance regarding package creation including necessary client tools, project file example, and commands, see [Create a NuGet package using the dotnet CLI](https://docs.microsoft.com/nuget/create-packages/creating-a-package-dotnet-cli).</span></span>

<span data-ttu-id="1112d-125">どの .NET Framework をターゲットにするか決める際に、[クロス プラットフォーム ターゲットに関する最新のガイダンス](https://docs.microsoft.com/dotnet/standard/library-guidance/cross-platform-targeting)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-125">To help decide which .NET frameworks to target, see our [latest guidance for cross-platform targeting](https://docs.microsoft.com/dotnet/standard/library-guidance/cross-platform-targeting).</span></span>

## <a name="package-metadata"></a><span data-ttu-id="1112d-126">パッケージ メタデータ</span><span class="sxs-lookup"><span data-stu-id="1112d-126">Package metadata</span></span>

<span data-ttu-id="1112d-127">メタデータは、すべての NuGet パッケージの基本コンポーネントです。</span><span class="sxs-lookup"><span data-stu-id="1112d-127">Metadata is a foundational component of any NuGet package.</span></span> <span data-ttu-id="1112d-128">メタデータの品質は、パッケージの見つけやすさ、使いやすさ、および信頼性に大きな影響を与えます。</span><span class="sxs-lookup"><span data-stu-id="1112d-128">The quality of your metadata can vastly influence the discoverability, usability, and trustworthiness of your package.</span></span>

<span data-ttu-id="1112d-129">Visual Studio の場合、パッケージ メタデータを指定するお勧めの方法は、プロジェクト > [プロジェクト名] プロパティ > パッケージにアクセスすることです。</span><span class="sxs-lookup"><span data-stu-id="1112d-129">In Visual Studio, the recommended way to specify package metadata is to go Project > [Project Name] Properties > Package.</span></span>

<span data-ttu-id="1112d-130">パッケージ メタデータ要素は、[プロジェクト ファイルで直接指定する](https://docs.microsoft.com/nuget/create-packages/creating-a-package-msbuild#set-properties)こともできます。</span><span class="sxs-lookup"><span data-stu-id="1112d-130">Package metadata elements can also be [specified directly in the project file](https://docs.microsoft.com/nuget/create-packages/creating-a-package-msbuild#set-properties).</span></span>

<span data-ttu-id="1112d-131">次の表に、使用可能なパッケージ メタデータ要素へのマッピングと説明を示します。</span><span class="sxs-lookup"><span data-stu-id="1112d-131">Below is a table mapping and describing available package metadata elements:</span></span>

| <span data-ttu-id="1112d-132">Visual Studio のプロパティ名</span><span class="sxs-lookup"><span data-stu-id="1112d-132">Visual Studio property name</span></span>                   | [<span data-ttu-id="1112d-133">プロジェクト ファイルまたは MSBuild のプロパティ名</span><span class="sxs-lookup"><span data-stu-id="1112d-133">Project file/ MSBuild property name</span></span>](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                          | [<span data-ttu-id="1112d-134">Nuspec のプロパティ名</span><span class="sxs-lookup"><span data-stu-id="1112d-134">Nuspec property name</span></span>](https://docs.microsoft.com/nuget/reference/nuspec#general-form-and-schema) | <span data-ttu-id="1112d-135">説明</span><span class="sxs-lookup"><span data-stu-id="1112d-135">Description</span></span>                                                                                                       |
|-----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| [`Package id`](#package-id)                   | [`PackageId`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageid)                                                            | [`id`](https://docs.microsoft.com/nuget/reference/nuspec#id)                                      | <span data-ttu-id="1112d-136">パッケージの名前または識別子。</span><span class="sxs-lookup"><span data-stu-id="1112d-136">The package name or identifier.</span></span>                    |
| [`Package version`](#package-version)         | [`PackageVersion`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageversion)                                                  | [`version`](https://docs.microsoft.com/nuget/reference/nuspec#version)                            | <span data-ttu-id="1112d-137">NuGet パッケージ バージョン。</span><span class="sxs-lookup"><span data-stu-id="1112d-137">NuGet package version.</span></span>                                           |
| [`Authors`](#authors)                         | [`Authors`](https://docs.microsoft.com/dotnet/core/tools/csproj#authors)                                                                | [`authors`](https://docs.microsoft.com/nuget/reference/nuspec#authors)                            | <span data-ttu-id="1112d-138">パッケージ作成者のコンマ区切りのリスト。多くの場合、個人または組織の "わかりやすい名前" を使用します。</span><span class="sxs-lookup"><span data-stu-id="1112d-138">A comma-separated list of package authors, often using the individual's or an organization's "pretty name."</span></span>                             |
| [`Description`](#description)                 | [`Description`](https://docs.microsoft.com/dotnet/core/tools/csproj#description)                                                        | [`description`](https://docs.microsoft.com/nuget/reference/nuspec#description)                    | <span data-ttu-id="1112d-139">パッケージの説明。</span><span class="sxs-lookup"><span data-stu-id="1112d-139">A description of the package.</span></span>                                                                |
| [`Copyright`](#copyright)                     | [`Copyright`](https://docs.microsoft.com/dotnet/core/tools/csproj#copyright)                                                            | [`copyright`](https://docs.microsoft.com/nuget/reference/nuspec#copyright)                        | <span data-ttu-id="1112d-140">パッケージの著作権の詳細。</span><span class="sxs-lookup"><span data-stu-id="1112d-140">Copyright details for the package.</span></span>                                                                      |
| [`Licensing - Expression`](#licensing)        | [`PackageLicenseExpression`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file) | [`license type="expression"`](https://docs.microsoft.com/nuget/reference/nuspec#license)          | <span data-ttu-id="1112d-141">SPDX ライセンス式。</span><span class="sxs-lookup"><span data-stu-id="1112d-141">An SPDX license expression.</span></span>       |
| [`Licensing - File`](#licensing)              | [`PackageLicenseFile`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)       | [`license type="file"`](https://docs.microsoft.com/nuget/reference/nuspec#license)                | <span data-ttu-id="1112d-142">カスタム ライセンス ファイルへのパス。</span><span class="sxs-lookup"><span data-stu-id="1112d-142">Path to a custom license file.</span></span>                                               |
| [`Project URL`](#project-url)                 | `PackageProjectUrl`                                                                                                                     | [`projectUrl`](https://docs.microsoft.com/nuget/reference/nuspec#projecturl)                      | <span data-ttu-id="1112d-143">プロジェクトのホームページの URL。</span><span class="sxs-lookup"><span data-stu-id="1112d-143">A URL for the project homepage.</span></span>                                                                                   |
| [`Icon File`](#icon)                          | [`PackageIcon`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file)                                  | [`icon`](https://docs.microsoft.com/nuget/reference/nuspec#icon)                                  | <span data-ttu-id="1112d-144">パッケージのアイコン画像ファイルへのパス。</span><span class="sxs-lookup"><span data-stu-id="1112d-144">Path to the package icon image file.</span></span>                                                                      |
| [`Repository URL`](#repository-type-and-url)  | [`RepositoryUrl`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositoryurl)                                                    | [`repository url`](https://docs.microsoft.com/nuget/reference/nuspec#repository)               | <span data-ttu-id="1112d-145">パッケージのビルド元であるリポジトリの URL。</span><span class="sxs-lookup"><span data-stu-id="1112d-145">URL to the repository from which the package was built.</span></span>                                                           |
| [`Repository type`](#repository-type-and-url) | [`RepositoryType`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositorytype)                                                 | [`repository type`](https://docs.microsoft.com/nuget/reference/nuspec#repository)              | <span data-ttu-id="1112d-146">リポジトリ URL が指しているリポジトリの種類 (つまり "git")。</span><span class="sxs-lookup"><span data-stu-id="1112d-146">Type of repository the repository URL is pointing to (i.e. "git").</span></span>                                                   |
| [`Tags`](#tags)                               | [`PackageTags`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagetags)                                                        | [`tags`](https://docs.microsoft.com/nuget/reference/nuspec#tags)                                  | <span data-ttu-id="1112d-147">パッケージを説明するタグとキーワードのスペース区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="1112d-147">A space-delimited list of tags and keywords that describe the package.</span></span> <span data-ttu-id="1112d-148">タグは、パッケージを検索するときに使用されます。</span><span class="sxs-lookup"><span data-stu-id="1112d-148">Tags are used when searching for packages.</span></span> |
| [`Release notes`](#release-notes)             | [`PackageReleaseNotes`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                                          | [`releaseNotes`](https://docs.microsoft.com/nuget/reference/nuspec#releasenotes)                  | <span data-ttu-id="1112d-149">パッケージの今回のリリースで加えられた変更内容の説明。</span><span class="sxs-lookup"><span data-stu-id="1112d-149">A description of the changes made in this release of the package.</span></span>                                                 |

### <a name="package-id"></a><span data-ttu-id="1112d-150">[パッケージ ID]</span><span class="sxs-lookup"><span data-stu-id="1112d-150">Package ID</span></span>

<span data-ttu-id="1112d-151">まったく新しいパッケージを発行する場合:</span><span class="sxs-lookup"><span data-stu-id="1112d-151">If you're publishing a completely new package:</span></span>

<span data-ttu-id="1112d-152">✔️ NuGet.org において一意かつ既存のパッケージと明確に区別されるパッケージ ID を選択してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-152">✔️ DO choose a package ID that is unique and clearly differentiated from existing packages on NuGet.org.</span></span>
> <span data-ttu-id="1112d-153">パッケージ ID が一意で区別可能かどうかを確認するには、NuGet.org でその ID を検索するか、次のリンクが存在するかどうかを確認します: https://www.nuget.org/packages/<package 名\> 。</span><span class="sxs-lookup"><span data-stu-id="1112d-153">You can check if a package ID is unique and differentiable by searching for the ID on NuGet.org or checking if the following link exists: https://www.nuget.org/packages/<package name\>.</span></span>

<span data-ttu-id="1112d-154">✔️ NuGet の[プレフィックスの予約条件](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation#id-prefix-reservation-criteria)を満たしているプレフィックスを持つ NuGet パッケージ名を選択することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-154">✔️ CONSIDER choosing a NuGet package name with a prefix that meets NuGet's [prefix reservation criteria](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation#id-prefix-reservation-criteria).</span></span>
> <span data-ttu-id="1112d-155">パッケージのプレフィックス ID を予約すると、検証済みのチェック マークを取得できるようになります: ![画像](media/Verified-check-mark.png)</span><span class="sxs-lookup"><span data-stu-id="1112d-155">Reserving the prefix ID for your package will let you get the verified check mark: ![image](media/Verified-check-mark.png)</span></span>
> 
> <span data-ttu-id="1112d-156">詳細については、[「パッケージ ID プレフィックスの予約」に関するドキュメント](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-156">Check out the [Package ID prefix reservation docs](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation) to learn more.</span></span>

### <a name="package-version"></a><span data-ttu-id="1112d-157">パッケージ バージョン</span><span class="sxs-lookup"><span data-stu-id="1112d-157">Package Version</span></span>

<span data-ttu-id="1112d-158">✔️ NuGet パッケージのバージョン管理に [SemVer](https://semver.org/) を使用することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-158">✔️ CONSIDER using [SemVer](https://semver.org/) to version your NuGet package.</span></span>
> <span data-ttu-id="1112d-159">基本的に、これは Major.Minor.Patch[-prerelease] の形式を使用することを意味します。</span><span class="sxs-lookup"><span data-stu-id="1112d-159">Essentially, this means using the Major.Minor.Patch[-prerelease] format.</span></span>

<span data-ttu-id="1112d-160">✔️ パッケージが非安定版またはプレビュー版の場合は、[プレリリース パッケージ](https://docs.microsoft.com/nuget/create-packages/prerelease-packages)として発行してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-160">✔️ DO publish a package as a [pre-release package](https://docs.microsoft.com/nuget/create-packages/prerelease-packages) if it is non-stable or a preview.</span></span>

<span data-ttu-id="1112d-161">詳細なガイダンスについては、[.NET ライブラリのバージョン管理に関するガイド](https://docs.microsoft.com/dotnet/standard/library-guidance/versioning)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-161">See the [.NET library versioning guide](https://docs.microsoft.com/dotnet/standard/library-guidance/versioning) for more advanced guidance.</span></span>

### <a name="authors"></a><span data-ttu-id="1112d-162">Authors</span><span class="sxs-lookup"><span data-stu-id="1112d-162">Authors</span></span>

<span data-ttu-id="1112d-163">✔️ 作成者のフィールドは、ユーザーまたはユーザーの組織の "わかりやすい名前" のために使用してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-163">✔️ DO use the author field for your or your organization's "pretty name."</span></span>
> <span data-ttu-id="1112d-164">たとえば、NuGet.org のユーザー名が "jdoe" である場合、作成者のフィールドに "Jane Doe" を使用すると、コンシューマーがそのユーザーを作成者として認識しやすくなります。</span><span class="sxs-lookup"><span data-stu-id="1112d-164">For example, if my NuGet.org username is "jdoe" then using "Jane Doe" for the author field may help consumers recognize me as an author.</span></span> <span data-ttu-id="1112d-165">組織の NuGet.org ユーザー名が "ContosoToolkit" である場合、"Contoso Corporation" を使用したほうが認識しやすく、コンシューマーの信頼性が高くなります。</span><span class="sxs-lookup"><span data-stu-id="1112d-165">If my organization's NuGet.org username is "ContosoToolkit" then using "Contoso Corporation" may be more recognizable and inspire more consumer trust.</span></span>
### <a name="description"></a><span data-ttu-id="1112d-166">説明</span><span class="sxs-lookup"><span data-stu-id="1112d-166">Description</span></span>

<span data-ttu-id="1112d-167">✔️ パッケージについて説明する、短い説明 (最大 4000 文字) を含めてください。</span><span class="sxs-lookup"><span data-stu-id="1112d-167">✔️ DO include a short description (up to 4000 characters) to describe your package.</span></span>
> <span data-ttu-id="1112d-168">パッケージの説明は、NuGet 検索に表示される最も目立つフィールドの 1 つであり、パッケージが適切かどうかを判断するために、潜在的なコンシューマーが最初に見るものになる可能性が高くなります。</span><span class="sxs-lookup"><span data-stu-id="1112d-168">Package descriptions are one of the most prominent fields surfaced in NuGet search and will likely be the first thing potential consumers looks at to determine if a package is right for them.</span></span>

### <a name="copyright"></a><span data-ttu-id="1112d-169">Copyright</span><span class="sxs-lookup"><span data-stu-id="1112d-169">Copyright</span></span>

<span data-ttu-id="1112d-170">✔️ "Copyright (c) <名前/会社\> <年\>" を使用してパッケージを著作権で保護することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-170">✔️ CONSIDER copyrighting your package with "Copyright (c) <name/company\> <year\>."</span></span>
><span data-ttu-id="1112d-171">基本的に、著作権表記によって、お客様の作業内容はお客様の許可がないとコピーできないということが示されます。</span><span class="sxs-lookup"><span data-stu-id="1112d-171">A copyright notice essentially indicates that your work cannot be copied without your permission.</span></span> <span data-ttu-id="1112d-172">パッケージに著作権表記を含めることは簡単であり、何の害もありません。</span><span class="sxs-lookup"><span data-stu-id="1112d-172">Including a copyright notice in your package is easy and won't do any harm!</span></span>

<span data-ttu-id="1112d-173">例:Copyright (c) Contoso 2020</span><span class="sxs-lookup"><span data-stu-id="1112d-173">Example: Copyright (c) Contoso 2020</span></span>

### <a name="licensing"></a><span data-ttu-id="1112d-174">ライセンス</span><span class="sxs-lookup"><span data-stu-id="1112d-174">Licensing</span></span>

<span data-ttu-id="1112d-175">✔️ [ライセンス式またはライセンス ファイルをパッケージに含める](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)ことを実施してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-175">✔️ DO [include a license expression or license file in your package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1112d-176">ライセンスを持たないプロジェクトは、既定で[排他的な著作権](https://choosealicense.com/no-permission/)になります。これは、プロジェクトを使用する権限を誰にも付与していないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="1112d-176">A project without a license defaults to [exclusive copyright](https://choosealicense.com/no-permission/), meaning that you have not granted anyone permission to use your project.</span></span>

<span data-ttu-id="1112d-177">❌ 非推奨の `LicenseUrl` メタデータ プロパティは使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="1112d-177">❌ DO NOT use the deprecated `LicenseUrl` metadata property.</span></span>
> <span data-ttu-id="1112d-178">URL でのライセンスの変更によって、以前のパッケージ バージョンに対して表示されたライセンスが遡及的に変更されるため、法的なあいまいさが生じます。</span><span class="sxs-lookup"><span data-stu-id="1112d-178">This presents legal ambiguity as license changes at the URL will retroactively change the displayed license for previous package versions.</span></span>

#### <a name="if-your-package-is-open-source"></a><span data-ttu-id="1112d-179">パッケージが[オープンソース](https://opensource.org/osd)の場合</span><span class="sxs-lookup"><span data-stu-id="1112d-179">If your package is [open source](https://opensource.org/osd)</span></span>

<span data-ttu-id="1112d-180">✔️ パッケージをオープンソースにするために、[オープンソース ライセンスを選択してください](https://choosealicense.com/)。</span><span class="sxs-lookup"><span data-stu-id="1112d-180">✔️ DO [choose an open source license](https://choosealicense.com/) to make your package open source.</span></span>
> <span data-ttu-id="1112d-181">*"オープンソース ライセンスは、オープンソースの定義に準拠するライセンスです。簡単に言うと、ソフトウェアの自由な使用、変更、および共有を許可するということです。"*</span><span class="sxs-lookup"><span data-stu-id="1112d-181">*"Open source licenses are licenses that comply with the Open Source Definition — in brief, they allow software to be freely used, modified, and shared."*</span></span> <span data-ttu-id="1112d-182">- オープンソース イニシアチブ。</span><span class="sxs-lookup"><span data-stu-id="1112d-182">- Open Source Initiative.</span></span> <span data-ttu-id="1112d-183">オープンソース ソフトウェアとオープンソース イニシアチブの詳細については、 https://opensource.org/ を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-183">To learn more about open source software and the Open Source Initiative, check out https://opensource.org/.</span></span>

<span data-ttu-id="1112d-184">✔️ [パッケージにライセンス式を含める](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)ことを検討してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-184">✔️ CONSIDER [including a license expression in your package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).</span></span>
> <span data-ttu-id="1112d-185">ライセンス式は最も明確に表示され、コンシューマーに対して、パッケージを使用できるかどうか、またはライセンスが変更されたかどうかがより明確になります。</span><span class="sxs-lookup"><span data-stu-id="1112d-185">License expressions are surfaced the most clearly and make it more obvious to consumers if they can use your package or if the license has changed.</span></span> 
> [!Note]
> <span data-ttu-id="1112d-186">NuGet.org で受け入れられるのは、オープンソース イニシアチブまたはフリー ソフトウェア財団によって承認されたライセンスのライセンス式のみです。</span><span class="sxs-lookup"><span data-stu-id="1112d-186">NuGet.org only accepts license expressions for licenses that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

#### <a name="if-your-package-is-not-open-source"></a><span data-ttu-id="1112d-187">パッケージがオープンソースでない場合</span><span class="sxs-lookup"><span data-stu-id="1112d-187">If your package is not open source</span></span>

<span data-ttu-id="1112d-188">✔️ [ライセンス ファイルをパッケージに含める](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)ことを実施してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-188">✔️ DO [include a license file in your package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).</span></span>
> <span data-ttu-id="1112d-189">標準以外のライセンスも含め、任意のライセンス ファイル (.txt または .md) をパッケージに追加できます。</span><span class="sxs-lookup"><span data-stu-id="1112d-189">Any license file (.txt or .md) can be added to your package, including non-standard licenses.</span></span> 

### <a name="project-url"></a><span data-ttu-id="1112d-190">[プロジェクトの URL]</span><span class="sxs-lookup"><span data-stu-id="1112d-190">Project URL</span></span>

<span data-ttu-id="1112d-191">✔️ 関連付けられているプロジェクト、リポジトリ、または会社の Web サイトへのリンクを含めることを検討してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-191">✔️ CONSIDER including a link to an associated project, repository, or company website.</span></span>
> <span data-ttu-id="1112d-192">プロジェクト サイトには、パッケージについてユーザーが知りたいすべてのことが含まれている必要があります。またおそらく、ユーザーがドキュメントを探す場所となります。</span><span class="sxs-lookup"><span data-stu-id="1112d-192">Your project site should have everything users need to know about your package and will likely be where users look for documentation.</span></span>

### <a name="icon"></a><span data-ttu-id="1112d-193">アイコン</span><span class="sxs-lookup"><span data-stu-id="1112d-193">Icon</span></span>

<span data-ttu-id="1112d-194">✔️ 視覚的に区別しやすくなるように、[パッケージにアイコンを含める](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file)ことを検討してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-194">✔️ CONSIDER [including an icon with your package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file) to help visually differentiate it.</span></span> <span data-ttu-id="1112d-195">これは、パッケージの品質に関する認識を向上させることができる、比較的小さな追加です。</span><span class="sxs-lookup"><span data-stu-id="1112d-195">It's a relatively small addition that can improve perception of package quality.</span></span>
> <span data-ttu-id="1112d-196">アイコンは、個々のパッケージに固有であるか、またはブランドのロゴであることがあります。</span><span class="sxs-lookup"><span data-stu-id="1112d-196">Icons can be specific to individual packages or be a brand logo.</span></span>

<span data-ttu-id="1112d-197">✔️ 最良な表示結果になるように、128 x 128 で透明な背景を持つ画像 (PNG) を使用してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-197">✔️ DO use an image that is 128x128 and has a transparent background (PNG) for best viewing results.</span></span>
> <span data-ttu-id="1112d-198">NuGet では、表示されるクライアントに合わせて画像が自動的にスケーリングされます。</span><span class="sxs-lookup"><span data-stu-id="1112d-198">NuGet will automatically scale your image to the client it is being displayed on.</span></span>

<span data-ttu-id="1112d-199">❌ 非推奨の `IconUrl` メタデータ プロパティは使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="1112d-199">❌ DO NOT use the deprecated `IconUrl` metadata property.</span></span>

### <a name="repository-type-and-url"></a><span data-ttu-id="1112d-200">リポジトリの種類と URL</span><span class="sxs-lookup"><span data-stu-id="1112d-200">Repository Type and URL</span></span>

<span data-ttu-id="1112d-201">✔️ [ソース リンク](https://docs.microsoft.com/dotnet/standard/library-guidance/sourcelink)を設定して、ソース管理メタデータが NuGet パッケージに自動的に追加され、ライブラリのデバッグが容易になるようにすることを検討してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-201">✔️ CONSIDER setting up [Source Link](https://docs.microsoft.com/dotnet/standard/library-guidance/sourcelink) to automatically add source control metadata to your NuGet package and make your library easier to debug.</span></span>
> <span data-ttu-id="1112d-202">ソース リンクによって、`Repository URL` と `Repository Type` がパッケージ メタデータに自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="1112d-202">Source Link automatically adds `Repository URL` and `Repository Type` to the package metadata.</span></span> <span data-ttu-id="1112d-203">また、パッケージのバージョンに関連付けられている特定のコミットも追加されます。</span><span class="sxs-lookup"><span data-stu-id="1112d-203">It also adds the specific commit associated with your package version.</span></span>

### <a name="tags"></a><span data-ttu-id="1112d-204">タグ</span><span class="sxs-lookup"><span data-stu-id="1112d-204">Tags</span></span>

<span data-ttu-id="1112d-205">✔️ 見つけやすさを向上させるために、パッケージに関連する重要な用語を含むいくつかのタグを追加してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-205">✔️ DO include several tags with key terms related to your package to enhance discoverability.</span></span>
> <span data-ttu-id="1112d-206">タグは NuGet.org の検索アルゴリズムにおいて考慮されます。また、パッケージ ID に含まれていないが重要である用語のために特に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="1112d-206">Tags are taken into account in NuGet.org's search algorithm and are especially helpful for terms that are not in the Package ID but are relevant.</span></span>

<span data-ttu-id="1112d-207">たとえば、コンソールに対する文字列をログに記録するためのパッケージを発行した場合は、"ログ記録、ログ、コンソール、文字列、出力" などを含めます</span><span class="sxs-lookup"><span data-stu-id="1112d-207">For example, if I published a package to log strings to the console, I would include: "logging, log, console, string, output"</span></span>

### <a name="release-notes"></a><span data-ttu-id="1112d-208">リリース ノート</span><span class="sxs-lookup"><span data-stu-id="1112d-208">Release notes</span></span>

<span data-ttu-id="1112d-209">✔️ 各更新に、どのような変更が実施されたかを説明するリリース ノートを含めることを検討してください。</span><span class="sxs-lookup"><span data-stu-id="1112d-209">✔️ CONSIDER including release notes with each update describing what changes were made.</span></span>
> <span data-ttu-id="1112d-210">リリース ノートに必要な特定の形式はありませんが、以下を含めることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="1112d-210">While there is no specific format required for release notes, we recommend including:</span></span>
>
> 1. <span data-ttu-id="1112d-211">重大な変更</span><span class="sxs-lookup"><span data-stu-id="1112d-211">Breaking changes</span></span>
> 2. <span data-ttu-id="1112d-212">新機能</span><span class="sxs-lookup"><span data-stu-id="1112d-212">New features</span></span>
> 3. <span data-ttu-id="1112d-213">バグの修正</span><span class="sxs-lookup"><span data-stu-id="1112d-213">Bug fixes</span></span>
> 
> <span data-ttu-id="1112d-214">リポジトリ内でリリース ノートまたは変更ログを既に追跡している場合は、関連するファイルへのリンクを含めることもできます。</span><span class="sxs-lookup"><span data-stu-id="1112d-214">If you already track release notes or a changelog in your repo, you can also include a link to the relevant file.</span></span>

## <a name="related-topics"></a><span data-ttu-id="1112d-215">関連トピック</span><span class="sxs-lookup"><span data-stu-id="1112d-215">Related topics</span></span>

- [<span data-ttu-id="1112d-216">パッケージの作成と公開 (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="1112d-216">Create and publish a package (dotnet CLI)</span></span>](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli)
- [<span data-ttu-id="1112d-217">パッケージの作成と公開 (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="1112d-217">Create and publish a package (Visual Studio)</span></span>](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli)
