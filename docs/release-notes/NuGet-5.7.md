---
title: NuGet 5.7 リリースノート
description: 新機能、バグ修正、および DCRs を含む NuGet 5.7 のリリースノート。
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 6c821091983ab0b5d59b759e1ee9930cf449fd9d
ms.sourcegitcommit: 6cda91f135e58cf57a2471b0c7c4a2f748f40024
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "89364152"
---
# <a name="nuget-57-release-notes"></a><span data-ttu-id="5fd56-103">NuGet 5.7 リリースノート</span><span class="sxs-lookup"><span data-stu-id="5fd56-103">NuGet 5.7 Release Notes</span></span>

<span data-ttu-id="5fd56-104">NuGet 配布の種類:</span><span class="sxs-lookup"><span data-stu-id="5fd56-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="5fd56-105">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="5fd56-105">NuGet version</span></span> | <span data-ttu-id="5fd56-106">利用可能な Visual Studio バージョン</span><span class="sxs-lookup"><span data-stu-id="5fd56-106">Available in Visual Studio version</span></span> | <span data-ttu-id="5fd56-107">利用可能な .NET SDK</span><span class="sxs-lookup"><span data-stu-id="5fd56-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="5fd56-108">**5.7.0**</span><span class="sxs-lookup"><span data-stu-id="5fd56-108">**5.7.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="5fd56-109">Visual Studio 2019 バージョン 16.7</span><span class="sxs-lookup"><span data-stu-id="5fd56-109">Visual Studio 2019 version 16.7</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="5fd56-110">[3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="5fd56-110">[3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="5fd56-111"><sup>1</sup> Visual Studio 2019 と .net Core ワークロードと共にインストールされる</span><span class="sxs-lookup"><span data-stu-id="5fd56-111"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-57"></a><span data-ttu-id="5fd56-112">概要: 5.7 の新機能</span><span class="sxs-lookup"><span data-stu-id="5fd56-112">Summary: What's New in 5.7</span></span>

### <a name="features-added-in-this-release"></a><span data-ttu-id="5fd56-113">このリリースで追加された機能</span><span class="sxs-lookup"><span data-stu-id="5fd56-113">Features added in this release</span></span>

* <span data-ttu-id="5fd56-114">NuGet パッケージ参照の extern エイリアスサポートを追加しました- [#4989](https://github.com/NuGet/Home/issues/4989)</span><span class="sxs-lookup"><span data-stu-id="5fd56-114">Added extern alias support for NuGet package references - [#4989](https://github.com/NuGet/Home/issues/4989)</span></span>

* <span data-ttu-id="5fd56-115">では、データソースを共有し、resfreshing を減らすことができる[#8294](https://github.com/NuGet/Home/issues/8294)ので、インストールされているタブと更新プログラムのタブを迅速に切り替えることができました。</span><span class="sxs-lookup"><span data-stu-id="5fd56-115">Made switching between Installed and Updates tabs faster by allowing them to share a data source and reducing resfreshing - [#8294](https://github.com/NuGet/Home/issues/8294)</span></span>

* <span data-ttu-id="5fd56-116">MSBuild スタティック Graph api (dotnet.exe) を呼び出すことにより、復元時間を短縮し、評価を高速化します。 [#9644](https://github.com/NuGet/Home/issues/9644)</span><span class="sxs-lookup"><span data-stu-id="5fd56-116">Make restore faster - speed up evaluations by calling MSBuild Static Graph apis (dotnet.exe) - [#9644](https://github.com/NuGet/Home/issues/9644)</span></span>

* <span data-ttu-id="5fd56-117">PackageReference プロジェクトの Visual Studio 部分復元を追加しました (非 op + +)- [#9513](https://github.com/NuGet/Home/issues/9513)</span><span class="sxs-lookup"><span data-stu-id="5fd56-117">Added Visual Studio partial restore for PackageReference projects (no-op++) - [#9513](https://github.com/NuGet/Home/issues/9513)</span></span>

* <span data-ttu-id="5fd56-118">HTTP 要求ごとに要求された数を超える結果を返す、不適切なパッケージソースを検索すると、Visual Studio パッケージマネージャー UI がクラッシュする頻度が低くなります。</span><span class="sxs-lookup"><span data-stu-id="5fd56-118">Visual Studio Package Manager UI will crash less often when searching misbehaving package sources that return more than the requested number of results per HTTP request.</span></span><span data-ttu-id="5fd56-119"> - [#8478](https://github.com/NuGet/Home/issues/8478)</span><span class="sxs-lookup"><span data-stu-id="5fd56-119"> - [#8478](https://github.com/NuGet/Home/issues/8478)</span></span>

* <span data-ttu-id="5fd56-120">VS [#9236](https://github.com/NuGet/Home/issues/9236)での非 SDK スタイルプロジェクトの PackageVersion 情報の統合を追加しました</span><span class="sxs-lookup"><span data-stu-id="5fd56-120">Added integration of PackageVersion information for non-SDK style projects in VS restore  - [#9236](https://github.com/NuGet/Home/issues/9236)</span></span>

* <span data-ttu-id="5fd56-121">nuget.exe update のサポートが追加されました `-self -Source` https://feed  -  [#1783](https://github.com/NuGet/Home/issues/1783)</span><span class="sxs-lookup"><span data-stu-id="5fd56-121">Added support for nuget.exe update `-self -Source` https://feed - [#1783](https://github.com/NuGet/Home/issues/1783)</span></span>

* <span data-ttu-id="5fd56-122">% Appdata% uget ディレクトリに複数の構成ファイルのサポートが追加されました- [#9394](https://github.com/NuGet/Home/issues/9394)</span><span class="sxs-lookup"><span data-stu-id="5fd56-122">Added support for multiple config files in %APPDATA%\NuGet directory - [#9394](https://github.com/NuGet/Home/issues/9394)</span></span>

* <span data-ttu-id="5fd56-123">DeterministicSourcePaths では、NuGet ソースパッケージをアカウントに [#9431](https://github.com/NuGet/Home/issues/9431)</span><span class="sxs-lookup"><span data-stu-id="5fd56-123">DeterministicSourcePaths now takes NuGet source packages into account - [#9431](https://github.com/NuGet/Home/issues/9431)</span></span>

* <span data-ttu-id="5fd56-124">INuGetProjectService 非同期機能拡張 API が追加されました- [#9702](https://github.com/NuGet/Home/issues/9702)</span><span class="sxs-lookup"><span data-stu-id="5fd56-124">Added INuGetProjectService.GetInstalledPackagesAsync extensibility API - [#9702](https://github.com/NuGet/Home/issues/9702)</span></span>

* <span data-ttu-id="5fd56-125">ソリューションまたはプロジェクトを必要とせずに、フォールバックフォルダーを列挙する相互運用 API を追加しました。 [#9395](https://github.com/NuGet/Home/issues/9395)</span><span class="sxs-lookup"><span data-stu-id="5fd56-125">Added interop API to enumerate fallback folders without requiring a solution/project - [#9395](https://github.com/NuGet/Home/issues/9395)</span></span>

* <span data-ttu-id="5fd56-126">`latest`#8808 のオプション `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)を追加しました</span><span class="sxs-lookup"><span data-stu-id="5fd56-126">Added `latest` option for `-MSBuildVersion` - [#8808](https://github.com/NuGet/Home/issues/8808)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="5fd56-127">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="5fd56-127">Issues fixed in this release</span></span>

<span data-ttu-id="5fd56-128">**バグ**</span><span class="sxs-lookup"><span data-stu-id="5fd56-128">**Bugs:**</span></span>

* <span data-ttu-id="5fd56-129">Dotnet CLI の復元で、資格情報プラグインを起動するときに、 `DOTNET_HOST_PATH`  環境変数が定義されていない場合は、システムパスで DOTNET CLI を試してみてください。</span><span class="sxs-lookup"><span data-stu-id="5fd56-129">In a dotnet CLI restore, when launching credential plugins, try the dotnet CLI on the system path if the `DOTNET_HOST_PATH`  environment variable is not defined.</span></span><span data-ttu-id="5fd56-130"> - [#7438](https://github.com/NuGet/Home/issues/7438)</span><span class="sxs-lookup"><span data-stu-id="5fd56-130"> - [#7438](https://github.com/NuGet/Home/issues/7438)</span></span>

* <span data-ttu-id="5fd56-131">nuget.exe spec は、ハードコーディングされたテキストを使用して著作権タグを生成し、その代わりに著作権情報 YYYY を入力 `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)</span><span class="sxs-lookup"><span data-stu-id="5fd56-131">nuget.exe spec generates a copyright tag with hard-coded text of Copyright YYYY Instead of `$copyright$` - [#8696](https://github.com/NuGet/Home/issues/8696)</span></span>

* <span data-ttu-id="5fd56-132">NuGet.exe は、アセンブリ名が変更された場合、プレースホルダーおよび assemblyinfo 属性を無視して、.csproj のパック中に "authors required" という例外をスローし [#4234](https://github.com/NuGet/Home/issues/4234)</span><span class="sxs-lookup"><span data-stu-id="5fd56-132">NuGet.exe throws exception 'authors required' during pack of a csproj ignoring placeholders and assemblyinfo attributes if the assembly name is changed - [#4234](https://github.com/NuGet/Home/issues/4234)</span></span>

* <span data-ttu-id="5fd56-133">HttpRequestMessage は、 [#8661](https://github.com/NuGet/Home/issues/8661) SocketHttpHandler でサポートされていない複数回再利用を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="5fd56-133">HttpRequestMessage gets reused multiple times which is not supported with the SocketHttpHandler - [#8661](https://github.com/NuGet/Home/issues/8661)</span></span>

* <span data-ttu-id="5fd56-134">5.6.0 preview 3 以降のインデックス作成では、別の公開キートークンを使用して [#9481](https://github.com/NuGet/Home/issues/9481)</span><span class="sxs-lookup"><span data-stu-id="5fd56-134">NuGet.Indexing 5.6.0 preview 3 and later use a different public key token - [#9481](https://github.com/NuGet/Home/issues/9481)</span></span>

* <span data-ttu-id="5fd56-135">NuGet パッケージの作成時に TreatWarningsAsErrors を優先する- [#7404](https://github.com/NuGet/Home/issues/7404)</span><span class="sxs-lookup"><span data-stu-id="5fd56-135">Honor TreatWarningsAsErrors during NuGet Package creation - [#7404](https://github.com/NuGet/Home/issues/7404)</span></span>

* <span data-ttu-id="5fd56-136">[CPVM]複数の p2p プロジェクトの誤ったパッケージダウングレード- [#9549](https://github.com/NuGet/Home/issues/9549)</span><span class="sxs-lookup"><span data-stu-id="5fd56-136">[CPVM] Spurious package downgrades for multiple p2p projects  - [#9549](https://github.com/NuGet/Home/issues/9549)</span></span>

* <span data-ttu-id="5fd56-137">[参照] タブは、検索ボックスに左揃えになっていません- [#9559](https://github.com/NuGet/Home/issues/9559)</span><span class="sxs-lookup"><span data-stu-id="5fd56-137">The “Browse” tab is not aligned left with search box - [#9559](https://github.com/NuGet/Home/issues/9559)</span></span>

* <span data-ttu-id="5fd56-138">インストールされているバージョンが、複数のバージョンがインストールされている1つのパッケージ id について、ソリューションレベル PM の UI に埋め込まれたアイコンと一致しません- [#9321](https://github.com/NuGet/Home/issues/9321)</span><span class="sxs-lookup"><span data-stu-id="5fd56-138">The installed version is inconsistent with the embedded icon in the solution level PM UI for one package id with multiple versions installed - [#9321](https://github.com/NuGet/Home/issues/9321)</span></span>

* <span data-ttu-id="5fd56-139">リーク: Partのポリシー ("共有しないポリシー................. RestoreOperationLogger- [#9595](https://github.com/NuGet/Home/issues/9595)</span><span class="sxs-lookup"><span data-stu-id="5fd56-139">Leak: PartCreationPolicy(CreationPolicy.NonShared) NuGet.SolutionRestoreManager.RestoreOperationLogger - [#9595](https://github.com/NuGet/Home/issues/9595)</span></span>

* <span data-ttu-id="5fd56-140">操作なしの復元でアセットファイルを読み取らないようにする- [#9693](https://github.com/NuGet/Home/issues/9693)</span><span class="sxs-lookup"><span data-stu-id="5fd56-140">Avoid reading the assets file in no-op restores - [#9693](https://github.com/NuGet/Home/issues/9693)</span></span>

* <span data-ttu-id="5fd56-141">NuGet. プロトコルは、検索からバージョンのダウンロード数を取得することをサポートしていません [#9086](https://github.com/NuGet/Home/issues/9086)</span><span class="sxs-lookup"><span data-stu-id="5fd56-141">NuGet.Protocol does not support getting a version's download count from search - [#9086](https://github.com/NuGet/Home/issues/9086)</span></span>

* <span data-ttu-id="5fd56-142">JObject の依存関係を減らすことで PackageMetadataResourceV3 のメモリパフォーマンスを向上させる- [#9719](https://github.com/NuGet/Home/issues/9719)</span><span class="sxs-lookup"><span data-stu-id="5fd56-142">Improve memory performance of PackageMetadataResourceV3 by reducing the JObject dependencies - [#9719](https://github.com/NuGet/Home/issues/9719)</span></span>

<span data-ttu-id="5fd56-143">**変更要求のデザイン:**</span><span class="sxs-lookup"><span data-stu-id="5fd56-143">**Design change requests:**</span></span>

* <span data-ttu-id="5fd56-144">`<owners>`冗長である場合に要素を抑制した[#5134](https://github.com/NuGet/Home/issues/5134)</span><span class="sxs-lookup"><span data-stu-id="5fd56-144">Suppressed the `<owners>` element when it is redundant - [#5134](https://github.com/NuGet/Home/issues/5134)</span></span>

* <span data-ttu-id="5fd56-145">ETW イベントとしてのログ IntervalTrackers- [#9593](https://github.com/NuGet/Home/issues/9593)</span><span class="sxs-lookup"><span data-stu-id="5fd56-145">Log IntervalTrackers as ETW events - [#9593](https://github.com/NuGet/Home/issues/9593)</span></span>

* <span data-ttu-id="5fd56-146">機能がプレビュー中であることを CPVM ユーザーに通知するために、復元時に情報メッセージを追加しました- [#9340](https://github.com/NuGet/Home/issues/9340)</span><span class="sxs-lookup"><span data-stu-id="5fd56-146">Added an informational message on restore to inform CPVM users that the feature is in preview - [#9340](https://github.com/NuGet/Home/issues/9340)</span></span>

* <span data-ttu-id="5fd56-147">アセットファイルからソリューションエクスプローラーパッケージ/プロジェクトの推移的な依存関係を設定する- [#9580](https://github.com/NuGet/Home/issues/9580)</span><span class="sxs-lookup"><span data-stu-id="5fd56-147">Populate Solution Explorer package/project transitive dependencies from assets file - [#9580](https://github.com/NuGet/Home/issues/9580)</span></span>

* <span data-ttu-id="5fd56-148">[インストールされたパッケージ] タブでパッケージの一覧を改ページすることはありません- [#6995](https://github.com/NuGet/Home/issues/6995)</span><span class="sxs-lookup"><span data-stu-id="5fd56-148">Installed packages tab shouldn't paginate the packages list - [#6995](https://github.com/NuGet/Home/issues/6995)</span></span>

<span data-ttu-id="5fd56-149">**[このリリースで修正されるすべての問題の一覧-5.7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**</span><span class="sxs-lookup"><span data-stu-id="5fd56-149">**[List of all issues fixed in this release - 5.7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**</span></span>

### <a name="community-contributions"></a><span data-ttu-id="5fd56-150">コミュニティからの投稿</span><span class="sxs-lookup"><span data-stu-id="5fd56-150">Community contributions</span></span>

<span data-ttu-id="5fd56-151">この NuGet のリリースに役立ったすべての共同作成者に感謝します。</span><span class="sxs-lookup"><span data-stu-id="5fd56-151">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="5fd56-152">担当者</span><span class="sxs-lookup"><span data-stu-id="5fd56-152">Who</span></span>|<span data-ttu-id="5fd56-153">Pr</span><span class="sxs-lookup"><span data-stu-id="5fd56-153">PRs</span></span>|<span data-ttu-id="5fd56-154">issue</span><span class="sxs-lookup"><span data-stu-id="5fd56-154">Issues</span></span>|
|----|----|----|
|[<span data-ttu-id="5fd56-155">campersau</span><span class="sxs-lookup"><span data-stu-id="5fd56-155">campersau</span></span>](https://github.com/campersau)|<span data-ttu-id="5fd56-156">[3433](https://github.com/NuGet/NuGet.Client/pull/3433)、 [3120](https://github.com/NuGet/NuGet.Client/pull/3120)</span><span class="sxs-lookup"><span data-stu-id="5fd56-156">[3433](https://github.com/NuGet/NuGet.Client/pull/3433), [3120](https://github.com/NuGet/NuGet.Client/pull/3120)</span></span>|<span data-ttu-id="5fd56-157">NuGet. プロトコルは、検索からバージョンのダウンロード数を取得することをサポートしていません [#9086](https://github.com/NuGet/Home/issues/9086)</span><span class="sxs-lookup"><span data-stu-id="5fd56-157">NuGet.Protocol does not support getting a version's download count from search - [#9086](https://github.com/NuGet/Home/issues/9086)</span></span> </br><span data-ttu-id="5fd56-158">HttpRequestMessage は、 [#8661](https://github.com/NuGet/Home/issues/8661) SocketHttpHandler でサポートされていない複数回再利用を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="5fd56-158">HttpRequestMessage gets reused multiple times which is not supported with the SocketHttpHandler - [#8661](https://github.com/NuGet/Home/issues/8661)</span></span>|
|[<span data-ttu-id="5fd56-159">ジョセフ・マス・ Ser (jnm2)</span><span class="sxs-lookup"><span data-stu-id="5fd56-159">Joseph Musser (jnm2)</span></span>](https://github.com/jnm2)|[<span data-ttu-id="5fd56-160">3241</span><span class="sxs-lookup"><span data-stu-id="5fd56-160">3241</span></span>](https://github.com/NuGet/NuGet.Client/pull/3241)|<span data-ttu-id="5fd56-161">`<owners>`冗長である場合に要素を抑制した[#5134](https://github.com/NuGet/Home/issues/5134)</span><span class="sxs-lookup"><span data-stu-id="5fd56-161">Suppressed the `<owners>` element when it is redundant - [#5134](https://github.com/NuGet/Home/issues/5134)</span></span>|
|[<span data-ttu-id="5fd56-162">Volodymyr Shkolka (BlackGad)</span><span class="sxs-lookup"><span data-stu-id="5fd56-162">Volodymyr Shkolka (BlackGad)</span></span>](https://github.com/BlackGad)|[<span data-ttu-id="5fd56-163">3273</span><span class="sxs-lookup"><span data-stu-id="5fd56-163">3273</span></span>](https://github.com/NuGet/NuGet.Client/pull/3273)|<span data-ttu-id="5fd56-164">NuGet では、クライアント証明書を必要とする HTTPS ソースからは復元できません- [#5773](https://github.com/NuGet/Home/issues/5773)</span><span class="sxs-lookup"><span data-stu-id="5fd56-164">NuGet cannot restore from HTTPS sources that require Client Certificates - [#5773](https://github.com/NuGet/Home/issues/5773)</span></span>|
|[<span data-ttu-id="5fd56-165">Marius Ungureanu (ole Zok)</span><span class="sxs-lookup"><span data-stu-id="5fd56-165">Marius Ungureanu (Therzok)</span></span>](https://github.com/Therzok)|[<span data-ttu-id="5fd56-166">3357</span><span class="sxs-lookup"><span data-stu-id="5fd56-166">3357</span></span>](https://github.com/NuGet/NuGet.Client/pull/3357)|<span data-ttu-id="5fd56-167">HttpSourceAuthenticationHandler SemaphoreSlim 未来の校正- [#9463](https://github.com/NuGet/Home/issues/9463)</span><span class="sxs-lookup"><span data-stu-id="5fd56-167">HttpSourceAuthenticationHandler SemaphoreSlim future proofing - [#9463](https://github.com/NuGet/Home/issues/9463)</span></span>|
|[<span data-ttu-id="5fd56-168">Sunner ()</span><span class="sxs-lookup"><span data-stu-id="5fd56-168">Sunner (SuNNjek)</span></span>](https://github.com/SuNNjek)|[<span data-ttu-id="5fd56-169">3088</span><span class="sxs-lookup"><span data-stu-id="5fd56-169">3088</span></span>](https://github.com/NuGet/NuGet.Client/pull/3088)|<span data-ttu-id="5fd56-170">nuget.exe spec は、ハードコーディングされたテキストを使用して著作権タグを生成し、その代わりに著作権情報 YYYY を入力 `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)</span><span class="sxs-lookup"><span data-stu-id="5fd56-170">nuget.exe spec generates a copyright tag with hard-coded text of Copyright YYYY Instead of `$copyright$` - [#8696](https://github.com/NuGet/Home/issues/8696)</span></span>|
|[<span data-ttu-id="5fd56-171">Olivier Spinelli (olivier-spinelli)</span><span class="sxs-lookup"><span data-stu-id="5fd56-171">Olivier Spinelli (olivier-spinelli)</span></span>](https://github.com/olivier-spinelli)|[<span data-ttu-id="5fd56-172">3335</span><span class="sxs-lookup"><span data-stu-id="5fd56-172">3335</span></span>](https://github.com/NuGet/NuGet.Client/pull/3335)|<span data-ttu-id="5fd56-173">Dotnet CLI の復元で、資格情報プラグインを起動するときに、 `DOTNET_HOST_PATH`  環境変数が定義されていない場合は、システムパスで DOTNET CLI を試してみてください。</span><span class="sxs-lookup"><span data-stu-id="5fd56-173">In a dotnet CLI restore, when launching credential plugins, try the dotnet CLI on the system path if the `DOTNET_HOST_PATH`  environment variable is not defined.</span></span><span data-ttu-id="5fd56-174"> - [#7438](https://github.com/NuGet/Home/issues/7438)</span><span class="sxs-lookup"><span data-stu-id="5fd56-174"> - [#7438](https://github.com/NuGet/Home/issues/7438)</span></span>|
|[<span data-ttu-id="5fd56-175">goyzhang</span><span class="sxs-lookup"><span data-stu-id="5fd56-175">goyzhang</span></span>](https://github.com/goyzhang)|[<span data-ttu-id="5fd56-176">3370</span><span class="sxs-lookup"><span data-stu-id="5fd56-176">3370</span></span>](https://github.com/NuGet/NuGet.Client/pull/3370)|<span data-ttu-id="5fd56-177">`latest`#8808 のオプション `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)を追加しました</span><span class="sxs-lookup"><span data-stu-id="5fd56-177">Added `latest` option for `-MSBuildVersion` - [#8808](https://github.com/NuGet/Home/issues/8808)</span></span>|
