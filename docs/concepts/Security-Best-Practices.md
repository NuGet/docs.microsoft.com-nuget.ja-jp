---
title: セキュリティで保護されたソフトウェア サプライ チェーンのベスト プラクティス
description: NuGet と GitHub を使用してソフトウェア サプライ チェーンをセキュリティで保護するためのベスト プラクティス。
author: JonDouglas
ms.author: jodou
ms.date: 02/08/2021
ms.topic: conceptual
ms.openlocfilehash: e0f235d99e41e23a4551fbf7577f6c42e3381f5b
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859227"
---
# <a name="best-practices-for-a-secure-software-supply-chain"></a><span data-ttu-id="a5550-103">セキュリティで保護されたソフトウェア サプライ チェーンのベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="a5550-103">Best practices for a secure software supply chain</span></span>

<span data-ttu-id="a5550-104">オープンソースはあらゆる場所にあります。</span><span class="sxs-lookup"><span data-stu-id="a5550-104">Open Source is everywhere.</span></span> <span data-ttu-id="a5550-105">多くの独自のコードベースやコミュニティ プロジェクトに含まれています。</span><span class="sxs-lookup"><span data-stu-id="a5550-105">It is in many proprietary codebases and community projects.</span></span> <span data-ttu-id="a5550-106">現在、組織や個人が確認しなければならないのは、オープンソース コードを使用しているかどうかではなく、どのようなオープンソース コードをどれくらい使用しているかということです。</span><span class="sxs-lookup"><span data-stu-id="a5550-106">For organizations and individuals, the question today is not whether you are or are not using open-source code, but what open-source code you are using, and how much.</span></span>

<span data-ttu-id="a5550-107">ソフトウェア サプライ チェーンの内容を把握していないと、上流の依存関係のいずれかに致命的な脆弱性があった場合、企業やその顧客が潜在的な侵害に対して脆弱になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a5550-107">If you're not aware of what is in your software supply chain, an upstream vulnerability in one of your dependencies can be fatal, making you, and your customers, vulnerable to a potential compromise.</span></span> <span data-ttu-id="a5550-108">このドキュメントでは、"ソフトウェア サプライ チェーン" という用語の意味、その重要性、プロジェクトのサプライ チェーンをベスト プラクティスで保護する方法について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="a5550-108">In this document, we will dive deeper into what the term “software supply chain” means, why it matters, and how you can help secure your project’s supply chain with best practices.</span></span>

![The State of the Octoverse 2020 - オープンソース](media/opensource-percent.png)

## <a name="dependencies"></a><span data-ttu-id="a5550-110">依存関係</span><span class="sxs-lookup"><span data-stu-id="a5550-110">Dependencies</span></span> 

<span data-ttu-id="a5550-111">ソフトウェア サプライ チェーンとは、ご利用のソフトウェアに組み込まれるすべてのものと、それがどこから来たのかを示すために使用される用語です。</span><span class="sxs-lookup"><span data-stu-id="a5550-111">The term software supply chain is used to refer to everything that goes into your software and where it comes from.</span></span> <span data-ttu-id="a5550-112">それは、ソフトウェア サプライ チェーンが依存している依存関係と、依存関係のプロパティです。</span><span class="sxs-lookup"><span data-stu-id="a5550-112">It is the dependencies and properties of your dependencies that your software supply chain depends on.</span></span> <span data-ttu-id="a5550-113">依存関係とは、ソフトウェアが実行する必要があるものです。</span><span class="sxs-lookup"><span data-stu-id="a5550-113">A dependency is what your software needs to run.</span></span> <span data-ttu-id="a5550-114">コード、バイナリ、またはその他のコンポーネントと、その取得元の場所 (リポジトリやパッケージ マネージャーなど) である場合があります。</span><span class="sxs-lookup"><span data-stu-id="a5550-114">It can be code, binaries, or other components, and where they come from, such as a repository or package manager.</span></span>

<span data-ttu-id="a5550-115">それには、誰がコードを作成したか、いつ投稿されたか、セキュリティの問題がどのように確認されたか、既知の脆弱性、サポートされているバージョン、ライセンス情報、およびプロセスの任意の時点でそれに関係するすべてのものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="a5550-115">It includes who wrote the code, when it was contributed, how it was reviewed for security issues, known vulnerabilities, supported versions, license information, and just about anything that touches it at any point of the process.</span></span>

<span data-ttu-id="a5550-116">また、サプライ チェーンには、ビルドとパッケージ化のスクリプトや、アプリケーションが依存するインフラストラクチャを実行しているソフトウェアなど、1 つのアプリケーションの範囲を超えるスタックの他の部分も含まれています。</span><span class="sxs-lookup"><span data-stu-id="a5550-116">Your supply chain also encompasses other parts of your stack beyond a single application, such as your build and packaging scripts or the software that runs the infrastructure your application relies on.</span></span>

## <a name="vulnerabilities"></a><span data-ttu-id="a5550-117">脆弱性</span><span class="sxs-lookup"><span data-stu-id="a5550-117">Vulnerabilities</span></span>

<span data-ttu-id="a5550-118">現在、ソフトウェアの依存関係は広く利用されています。</span><span class="sxs-lookup"><span data-stu-id="a5550-118">Today, software dependencies are pervasive.</span></span> <span data-ttu-id="a5550-119">プロジェクトの機能に多数のオープンソースの依存関係を使用したので、自分で作成する必要がなかった、というのは非常によくあることです。</span><span class="sxs-lookup"><span data-stu-id="a5550-119">It is quite common for your projects to use hundreds of open-source dependencies for functionality that you did not have to write yourself.</span></span> <span data-ttu-id="a5550-120">これは、アプリケーションのほとんどの部分が、自分で作成したものではないコードで構成されていることを意味する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a5550-120">This may mean that most of your application consists of code that you did not author.</span></span> 

![The State of the Octoverse 2020 - 依存関係](media/dependencies.png)

<span data-ttu-id="a5550-122">サードパーティやオープンソースの依存関係に含まれる可能性のある脆弱性は、おそらく、自分で作成したコードほど厳しく制御することができない依存関係であり、これによりサプライ チェーンに潜在的なセキュリティ リスクが生じる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a5550-122">Possible vulnerabilities in your third-party or open-source dependencies, are presumably dependencies you cannot control as tightly as the code you write, which can create potential security risks in your supply chain.</span></span>

<span data-ttu-id="a5550-123">このような依存関係のいずれかに脆弱性がある場合、それを使う側にも脆弱性がある可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a5550-123">If one of these dependencies has a vulnerability, the chances are you have a vulnerability as well.</span></span> <span data-ttu-id="a5550-124">使う側が知ることなく依存関係のいずれかが変更される可能性があるということは、恐ろしいことです。</span><span class="sxs-lookup"><span data-stu-id="a5550-124">This can be scary as one of your dependencies may change without you even knowing.</span></span> <span data-ttu-id="a5550-125">依存関係に脆弱性が存在していて、今は悪用できない場合でも、将来悪用される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a5550-125">Even if a vulnerability exists in a dependency today, but is not exploitable, it can be exploitable in the future.</span></span> 

<span data-ttu-id="a5550-126">多数のオープンソース開発者やライブラリ作成者が作ったものを利用できるということは、何千もの知らない人が自分の運用コードに直接、効果的に寄与できることを意味します。</span><span class="sxs-lookup"><span data-stu-id="a5550-126">Being able to leverage the work of thousands of open-source developers and library authors means that thousands of strangers can effectively contribute directly to your production code.</span></span> <span data-ttu-id="a5550-127">自分の製品が、ソフトウェア サプライ チェーンを通じて、修正プログラムが適用されていない脆弱性、悪意のない誤り、さらには依存関係に対する悪意のある攻撃からの影響を受けます。</span><span class="sxs-lookup"><span data-stu-id="a5550-127">Your product, through your software supply chain, is affected by unpatched vulnerabilities, innocent mistakes, or even malicious attacks against dependencies.</span></span>

## <a name="supply-chain-compromises"></a><span data-ttu-id="a5550-128">サプライ チェーンの侵害</span><span class="sxs-lookup"><span data-stu-id="a5550-128">Supply chain compromises</span></span>

<span data-ttu-id="a5550-129">サプライ チェーンの従来の定義は、製造業が基になっています。それは、何かを製造して供給するために必要なプロセスのチェーンです。</span><span class="sxs-lookup"><span data-stu-id="a5550-129">The traditional definition of a supply chain comes from manufacturing; it is the chain of processes required to make and supply something.</span></span> <span data-ttu-id="a5550-130">それには、計画、材料の供給、製造、小売が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a5550-130">It includes planning, supply of materials, manufacturing, and retail.</span></span> <span data-ttu-id="a5550-131">ソフトウェア サプライ チェーンも似ていますが、材料ではなくコードである点が異なります。</span><span class="sxs-lookup"><span data-stu-id="a5550-131">A software supply chain is similar, except instead of materials, it is code.</span></span> <span data-ttu-id="a5550-132">製造ではなく開発です。</span><span class="sxs-lookup"><span data-stu-id="a5550-132">Instead of manufacturing, it is development.</span></span> <span data-ttu-id="a5550-133">鉱石を地中から掘り出す代わりに、コードはサプライヤー、市販品、オープンソースから供給され、通常、オープンソースのコードはリポジトリから取得されます。</span><span class="sxs-lookup"><span data-stu-id="a5550-133">Instead of digging ore from the ground, code is sourced from suppliers, commercial or open source, and, in general, the open-source code comes from repositories.</span></span> <span data-ttu-id="a5550-134">リポジトリからコードを追加するということは、製品でそのコードの依存関係を取得することを意味します。</span><span class="sxs-lookup"><span data-stu-id="a5550-134">Adding code from a repository means your product takes a dependency on that code.</span></span>

<span data-ttu-id="a5550-135">ソフトウェア サプライ チェーン攻撃の一例として、悪意のあるコードが依存関係に意図的に追加され、その依存関係のサプライ チェーンを使用して犠牲者にコードが配布される場合があります。</span><span class="sxs-lookup"><span data-stu-id="a5550-135">One example of a software supply chain attack occurs when malicious code is purposefully added to a dependency, using the supply chain of that dependency to distribute the code to its victims.</span></span> <span data-ttu-id="a5550-136">サプライ チェーン攻撃は現実のものです。</span><span class="sxs-lookup"><span data-stu-id="a5550-136">Supply chain attacks are real.</span></span> <span data-ttu-id="a5550-137">サプライ チェーンを攻撃する方法は多数あります。新しい共同作成者として悪意のあるコードを直接挿入したり、他の人が気付かないうちに共同作成者のアカウントを乗っ取ったり、さらには署名キーを侵害して依存関係の正式な一部ではないソフトウェアを配布することさえあります。</span><span class="sxs-lookup"><span data-stu-id="a5550-137">There are many methods to attack a supply chain, from directly inserting malicious code as a new contributor, to taking over a contributor’s account without others noticing, or even compromising a signing key to distribute software that is not officially part of the dependency.</span></span>

<span data-ttu-id="a5550-138">ソフトウェア サプライ チェーン攻撃は、それ自体が最終的な目標であることはあまりなく、攻撃者がマルウェアを挿入したり、後でアクセスできるようにバックドアを用意したりするための機会の始まりです。</span><span class="sxs-lookup"><span data-stu-id="a5550-138">A software supply chain attack is in and of itself rarely the end goal, rather it is the beginning of an opportunity for an attacker to insert malware or provide a backdoor for future access.</span></span>

![The State of the Octoverse 2020 - 脆弱性のライフサイクル](media/vulnerability-lifecycle.png)

## <a name="unpatched-software"></a><span data-ttu-id="a5550-140">修正プログラムが適用されていないソフトウェア</span><span class="sxs-lookup"><span data-stu-id="a5550-140">Unpatched software</span></span>

<span data-ttu-id="a5550-141">現在、オープンソースの使用は広く行われており、近いうちに下火になるとは思われません。</span><span class="sxs-lookup"><span data-stu-id="a5550-141">The use of open source today is significant and is not expected to slow down anytime soon.</span></span> <span data-ttu-id="a5550-142">オープンソース ソフトウェアの使用が止まることがないとすると、修正プログラムが適用されていないソフトウェアがサプライ チェーンのセキュリティに対する脅威になります。</span><span class="sxs-lookup"><span data-stu-id="a5550-142">Given that we are not going to stop using open-source software, the threat to supply chain security is unpatched software.</span></span> <span data-ttu-id="a5550-143">では、プロジェクトの依存関係に脆弱性があるというリスクに対処するには、どうすればよいでしょうか。</span><span class="sxs-lookup"><span data-stu-id="a5550-143">Knowing that, how can you address the risk that a dependency of your project has a vulnerability?</span></span>

- <span data-ttu-id="a5550-144">**環境内にあるものを把握する。**</span><span class="sxs-lookup"><span data-stu-id="a5550-144">**Knowing what is in your environment.**</span></span> <span data-ttu-id="a5550-145">これには、依存関係とすべての推移的な依存関係を検出して、脆弱性やライセンスの制限など、それらの依存関係のリスクを理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5550-145">This requires discovering your dependencies and any transitive dependencies to understand the risks of those dependencies such as vulnerabilities or licensing restrictions.</span></span>
- <span data-ttu-id="a5550-146">**依存関係を管理する。**</span><span class="sxs-lookup"><span data-stu-id="a5550-146">**Manage your dependencies.**</span></span> <span data-ttu-id="a5550-147">新しいセキュリティ脆弱性が発見されたら、影響を受けるかどうかを判断し、受ける場合は、利用可能な最新バージョンとセキュリティ修正プログラムに更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5550-147">When a new security vulnerability is discovered, you must determine whether you are impacted, and if so, update to the latest version and security patch available.</span></span> <span data-ttu-id="a5550-148">これは、新しい依存関係が導入される変更を確認したり、古い依存関係を定期的に監査したりする場合に特に重要です。</span><span class="sxs-lookup"><span data-stu-id="a5550-148">This is especially important to review changes that introduce new dependencies or regularly auditing older dependencies.</span></span>
- <span data-ttu-id="a5550-149">**サプライ チェーンを監視する。**</span><span class="sxs-lookup"><span data-stu-id="a5550-149">**Monitor your supply chain.**</span></span> <span data-ttu-id="a5550-150">そのためには、依存関係を管理するために設けられている制御を監査します。</span><span class="sxs-lookup"><span data-stu-id="a5550-150">This is by auditing the controls you have in place to manage your dependencies.</span></span> <span data-ttu-id="a5550-151">これは、依存関係に対してより制限の厳しい条件を適用するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a5550-151">This will help you enforce more restrictive conditions to be met for your dependencies.</span></span>

![The State of the Octoverse 2020 - 勧告](media/advisories.png)

<span data-ttu-id="a5550-153">以降では、NuGet と GitHub に用意されているさまざまなツールと手法について説明します。それらを使用して、プロジェクト内の潜在的なリスクに対処できます。</span><span class="sxs-lookup"><span data-stu-id="a5550-153">We will cover various tools and techniques that NuGet and GitHub provides, which you can use today to address potential risks inside your project.</span></span> 

## <a name="knowing-what-is-in-your-environment"></a><span data-ttu-id="a5550-154">環境内にあるものを把握する</span><span class="sxs-lookup"><span data-stu-id="a5550-154">Knowing what is in your environment</span></span>

### <a name="nuget-dependency-graph"></a><span data-ttu-id="a5550-155">NuGet の依存関係グラフ</span><span class="sxs-lookup"><span data-stu-id="a5550-155">NuGet dependency graph</span></span>

<span data-ttu-id="a5550-156">**📦 パッケージ利用者**</span><span class="sxs-lookup"><span data-stu-id="a5550-156">**📦 Package Consumer**</span></span>

<span data-ttu-id="a5550-157">プロジェクトでの NuGet の依存関係は、該当するプロジェクト ファイルを直接見ることで確認できます。</span><span class="sxs-lookup"><span data-stu-id="a5550-157">You can view your NuGet dependencies in your project by looking directly at the respective project file.</span></span>

<span data-ttu-id="a5550-158">通常、これは次の 2 つの場所のいずれかにあります。</span><span class="sxs-lookup"><span data-stu-id="a5550-158">This is typically found in one of two places:</span></span>

-   <span data-ttu-id="a5550-159">[`packages.config`](../reference/packages-config.md) – プロジェクトのルートにあります。</span><span class="sxs-lookup"><span data-stu-id="a5550-159">[`packages.config`](../reference/packages-config.md) – Located in the project root.</span></span>
-   <span data-ttu-id="a5550-160">[`<PackageReference>`](../consume-packages/package-references-in-project-files.md) – プロジェクト ファイルにあります。</span><span class="sxs-lookup"><span data-stu-id="a5550-160">[`<PackageReference>`](../consume-packages/package-references-in-project-files.md) – Located in the project file.</span></span> 

<span data-ttu-id="a5550-161">NuGet の依存関係の管理に使用する方法に応じて、Visual Studio の[ソリューション エクスプローラー](/visualstudio/ide/solutions-and-projects-in-visual-studio#solution-explorer)または [NuGet パッケージ マネージャー](../consume-packages/install-use-packages-visual-studio.md)を使用して依存関係を直接見ることもできます。</span><span class="sxs-lookup"><span data-stu-id="a5550-161">Depending on what method you use to manage your NuGet dependencies, you can also use Visual Studio to view your dependencies directly in [Solution Explorer](/visualstudio/ide/solutions-and-projects-in-visual-studio#solution-explorer) or [NuGet Package Manager](../consume-packages/install-use-packages-visual-studio.md).</span></span>

<span data-ttu-id="a5550-162">CLI 環境の場合は、[`dotnet list package`](/dotnet/core/tools/dotnet-list-package) コマンドを使用して、プロジェクトまたはソリューションの依存関係の一覧を表示できます。</span><span class="sxs-lookup"><span data-stu-id="a5550-162">For CLI environments, you can use the [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) command to list out your project or solution’s dependencies.</span></span> 

<span data-ttu-id="a5550-163">NuGet の依存関係の管理に関する詳細については、[こちらのドキュメントを参照してください](../consume-packages/overview-and-workflow.md)。</span><span class="sxs-lookup"><span data-stu-id="a5550-163">For more information on managing NuGet dependencies, [see the following documentation](../consume-packages/overview-and-workflow.md).</span></span>

### <a name="github-dependency-graph"></a><span data-ttu-id="a5550-164">GitHub の依存関係グラフ</span><span class="sxs-lookup"><span data-stu-id="a5550-164">GitHub dependency graph</span></span> 

<span data-ttu-id="a5550-165">**📦 パッケージ利用者 | 📦🖊 パッケージ作成者**</span><span class="sxs-lookup"><span data-stu-id="a5550-165">**📦 Package Consumer | 📦🖊 Package Author**</span></span>

<span data-ttu-id="a5550-166">GitHub の依存関係グラフを使用して、プロジェクトが依存しているパッケージと、それに依存するリポジトリを確認できます。</span><span class="sxs-lookup"><span data-stu-id="a5550-166">You can use GitHub’s dependency graph to see the packages your project depends on and the repositories that depend on it.</span></span> <span data-ttu-id="a5550-167">これは、その依存関係で検出された脆弱性を確認するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a5550-167">This can help you see any vulnerabilities detected in its dependencies.</span></span>

<span data-ttu-id="a5550-168">GitHub リポジトリの依存関係の詳細については、[こちらのドキュメントを参照してください](https://github.co/dependency-graph)。</span><span class="sxs-lookup"><span data-stu-id="a5550-168">For more information on GitHub repository dependencies, [see the following documentation](https://github.co/dependency-graph).</span></span>

### <a name="dependency-versions"></a><span data-ttu-id="a5550-169">依存関係のバージョン</span><span class="sxs-lookup"><span data-stu-id="a5550-169">Dependency versions</span></span>

<span data-ttu-id="a5550-170">**📦 パッケージ利用者 | 📦🖊 パッケージ作成者**</span><span class="sxs-lookup"><span data-stu-id="a5550-170">**📦 Package Consumer | 📦🖊 Package Author**</span></span>

<span data-ttu-id="a5550-171">依存関係のサプライ チェーンをセキュリティで保護するには、すべての依存関係とツールが最新の安定したバージョンに定期的に更新される必要があります。それらには、最新の機能と、既知の脆弱性に対するセキュリティ修正プログラムが含まれることが多いためです。</span><span class="sxs-lookup"><span data-stu-id="a5550-171">To ensure a secure supply chain of dependencies, you will want to ensure that all of your dependencies & tooling are regularly updated to the latest stable version as they will often include the latest functionality and security patches to known vulnerabilities.</span></span> <span data-ttu-id="a5550-172">依存関係には、依存しているコード、利用するバイナリ、使用するツール、その他のコンポーネントが含まれる場合があります。</span><span class="sxs-lookup"><span data-stu-id="a5550-172">Your dependencies can include code you depend on, binaries you consume, tooling you use, and other components.</span></span> <span data-ttu-id="a5550-173">次のような場合が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a5550-173">This may include:</span></span>

-   [<span data-ttu-id="a5550-174">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a5550-174">Visual Studio</span></span>](https://visualstudio.microsoft.com/downloads/)
-   [<span data-ttu-id="a5550-175">.NET SDK とランタイム</span><span class="sxs-lookup"><span data-stu-id="a5550-175">.NET SDK & Runtime</span></span>](https://dotnet.microsoft.com/download)
-   [<span data-ttu-id="a5550-176">NuGet</span><span class="sxs-lookup"><span data-stu-id="a5550-176">NuGet</span></span>](https://www.nuget.org/downloads)
-   [<span data-ttu-id="a5550-177">NuGet パッケージ</span><span class="sxs-lookup"><span data-stu-id="a5550-177">NuGet packages</span></span>](../consume-packages/reinstalling-and-updating-packages.md)

## <a name="manage-your-dependencies"></a><span data-ttu-id="a5550-178">依存関係を管理する</span><span class="sxs-lookup"><span data-stu-id="a5550-178">Manage your dependencies</span></span>

### <a name="nuget-deprecated-and-vulnerable-dependencies"></a><span data-ttu-id="a5550-179">NuGet の非推奨および脆弱な依存関係</span><span class="sxs-lookup"><span data-stu-id="a5550-179">NuGet deprecated and vulnerable dependencies</span></span>

<span data-ttu-id="a5550-180">**📦 パッケージ利用者 | 📦🖊 パッケージ作成者**</span><span class="sxs-lookup"><span data-stu-id="a5550-180">**📦 Package Consumer | 📦🖊 Package Author**</span></span>

<span data-ttu-id="a5550-181">[dotnet CLI](/dotnet/core/tools/dotnet-list-package) を使用して、プロジェクトまたはソリューションに存在する可能性がある、既知の非推奨、または脆弱な依存関係の一覧を表示できます。</span><span class="sxs-lookup"><span data-stu-id="a5550-181">You can use the [dotnet CLI](/dotnet/core/tools/dotnet-list-package) to list any known deprecated or vulnerable dependencies you may have inside your project or solution.</span></span> <span data-ttu-id="a5550-182">`dotnet list package --deprecated` または `dotnet list package --vulnerable` コマンドを使用すると、既知の非推奨、または脆弱性の一覧が提供されます。</span><span class="sxs-lookup"><span data-stu-id="a5550-182">You can use the command `dotnet list package --deprecated` or `dotnet list package --vulnerable` to provide you a list of any known deprecations or vulnerabilities.</span></span>

### <a name="github-vulnerable-dependencies"></a><span data-ttu-id="a5550-183">GitHub の脆弱な依存関係</span><span class="sxs-lookup"><span data-stu-id="a5550-183">GitHub vulnerable dependencies</span></span>

<span data-ttu-id="a5550-184">**📦 パッケージ利用者 | 📦🖊 パッケージ作成者**</span><span class="sxs-lookup"><span data-stu-id="a5550-184">**📦 Package Consumer | 📦🖊 Package Author**</span></span>

<span data-ttu-id="a5550-185">プロジェクトが GitHub でホストされている場合、[GitHub Security](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors) を利用して、プロジェクト内のセキュリティ脆弱性とエラーを見つけることができます。また、コードベースに対する pull request をオープンすることで、Dependabot によってこれらが修正されます。</span><span class="sxs-lookup"><span data-stu-id="a5550-185">If your project is hosted on GitHub, you can leverage [GitHub Security](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors) to find security vulnerabilities and errors in your project and Dependabot will fix them by opening up a pull request against your codebase.</span></span> 

<span data-ttu-id="a5550-186">持ち込まれる前に脆弱な依存関係を検出することは、["シフト レフト"](https://en.wikipedia.org/wiki/Shift-left_testing) 活動の 1 つの目標です。</span><span class="sxs-lookup"><span data-stu-id="a5550-186">Catching vulnerable dependencies before they are introduced is one goal of the [“Shift Left”](https://en.wikipedia.org/wiki/Shift-left_testing) movement.</span></span> <span data-ttu-id="a5550-187">ライセンス、推移的な依存関係、依存関係の経過期間など、依存関係に関する情報を取得できるようにすることは、そのために役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a5550-187">Being able to have information about your dependencies such as their license, transitive dependencies, and the age of dependencies helps you do just that.</span></span>

<span data-ttu-id="a5550-188">Dependabot のアラートとセキュリティ更新プログラムの詳細については、[こちらのドキュメントを参照してください](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies)。</span><span class="sxs-lookup"><span data-stu-id="a5550-188">For more information about Dependabot alerts & security updates, [see the following documentation](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies).</span></span>

### <a name="nuget-feeds"></a><span data-ttu-id="a5550-189">NuGet フィード</span><span class="sxs-lookup"><span data-stu-id="a5550-189">NuGet feeds</span></span>

<span data-ttu-id="a5550-190">**📦 パッケージ利用者**</span><span class="sxs-lookup"><span data-stu-id="a5550-190">**📦 Package Consumer**</span></span>

<span data-ttu-id="a5550-191">パブリックとプライベートの複数の NuGet ソース フィードを使用している場合は、任意のフィードからパッケージをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="a5550-191">When using multiple public & private NuGet source feeds, a package can be downloaded from any of the feeds.</span></span> <span data-ttu-id="a5550-192">[依存関係かく乱](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610)などの既知の攻撃をビルドで予測してセキュリティ保護できるようにするには、パッケージの取得元である特定のフィードを把握するのがベスト プラクティスです。</span><span class="sxs-lookup"><span data-stu-id="a5550-192">To ensure your build is predictable and secure from known attacks such as [Dependency Confusion](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610), knowing what specific feed(s) your packages are coming from is a best practice.</span></span> <span data-ttu-id="a5550-193">保護のためには上流の機能で単一のフィードまたはプライベート フィードを使用できます。</span><span class="sxs-lookup"><span data-stu-id="a5550-193">You can use a single feed or private feed with upstreaming capabilities for protection.</span></span>

<span data-ttu-id="a5550-194">パッケージ フィードのセキュリティ保護の詳細については、「[プライベート パッケージ フィードを使用するときにリスクを軽減する 3 つの方法](https://azure.microsoft.com/en-us/resources/3-ways-to-mitigate-risk-using-private-package-feeds/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a5550-194">For more information to secure your package feeds, see [3 Ways to Mitigate Risk When Using Private Package Feeds](https://azure.microsoft.com/en-us/resources/3-ways-to-mitigate-risk-using-private-package-feeds/).</span></span>

### <a name="client-trust-policies"></a><span data-ttu-id="a5550-195">クライアント信頼ポリシー</span><span class="sxs-lookup"><span data-stu-id="a5550-195">Client trust policies</span></span>

<span data-ttu-id="a5550-196">**📦 パッケージ利用者**</span><span class="sxs-lookup"><span data-stu-id="a5550-196">**📦 Package Consumer**</span></span>

<span data-ttu-id="a5550-197">使用するパッケージで署名が必要なポリシーをオプトインすることができます。</span><span class="sxs-lookup"><span data-stu-id="a5550-197">There are policies that you can opt-into in which you require the packages you use to be signed.</span></span> <span data-ttu-id="a5550-198">これにより、作成者によって署名されている場合に限りパッケージの作成者を信頼したり、NuGet.org によって署名されたリポジトリである特定のユーザーまたはアカウントによって所有されている場合にパッケージを信頼したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="a5550-198">This allows you to trust a package author, as long as it is author signed, or trust a package if it is owned by a specific user or account that is repository signed by NuGet.org.</span></span>

<span data-ttu-id="a5550-199">クライアント信頼ポリシーを構成するには、[こちらのドキュメントを参照してください](../consume-packages/installing-signed-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="a5550-199">To configure client trust policies, [see the following documentation](../consume-packages/installing-signed-packages.md).</span></span>

### <a name="lock-files"></a><span data-ttu-id="a5550-200">ロック ファイル</span><span class="sxs-lookup"><span data-stu-id="a5550-200">Lock files</span></span>

<span data-ttu-id="a5550-201">**📦 パッケージ利用者**</span><span class="sxs-lookup"><span data-stu-id="a5550-201">**📦 Package Consumer**</span></span>

<span data-ttu-id="a5550-202">ロック ファイルには、パッケージのコンテンツ ハッシュが格納されます。</span><span class="sxs-lookup"><span data-stu-id="a5550-202">Lock files store the hash of your package’s content.</span></span> <span data-ttu-id="a5550-203">インストールしようとするパッケージのコンテンツ ハッシュがロック ファイルと一致する場合は、パッケージの再現性が保証されます。</span><span class="sxs-lookup"><span data-stu-id="a5550-203">If the content hash of a package you want to install matches with the lock file, it will ensure package repeatability.</span></span>

<span data-ttu-id="a5550-204">ロック ファイルを有効にするには、[こちらのドキュメントを参照してください](../consume-packages/package-references-in-project-files.md#locking-dependencies)。</span><span class="sxs-lookup"><span data-stu-id="a5550-204">To enable lock files, [see the following documentation](../consume-packages/package-references-in-project-files.md#locking-dependencies).</span></span>

## <a name="monitor-your-supply-chain"></a><span data-ttu-id="a5550-205">サプライ チェーンを監視する</span><span class="sxs-lookup"><span data-stu-id="a5550-205">Monitor your supply chain</span></span>

### <a name="github-secret-scanning"></a><span data-ttu-id="a5550-206">GitHub シークレット スキャン</span><span class="sxs-lookup"><span data-stu-id="a5550-206">GitHub secret scanning</span></span>

<span data-ttu-id="a5550-207">**📦🖊 パッケージ作成者**</span><span class="sxs-lookup"><span data-stu-id="a5550-207">**📦🖊 Package Author**</span></span>

<span data-ttu-id="a5550-208">誤ってコミットされたシークレットが不正に使用されるのを防ぐため、GitHub によりリポジトリで NuGet API キーがスキャンされます。</span><span class="sxs-lookup"><span data-stu-id="a5550-208">GitHub scans repositories for NuGet API keys to prevent fraudulent uses of secrets that were accidentally committed.</span></span> 

<span data-ttu-id="a5550-209">シークレット スキャンの詳細については、「[シークレット スキャンニングについて](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a5550-209">To learn more about secret scanning, see [About secret scanning](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning).</span></span>

### <a name="author-package-signing"></a><span data-ttu-id="a5550-210">作成者によるパッケージへの署名</span><span class="sxs-lookup"><span data-stu-id="a5550-210">Author Package Signing</span></span>

<span data-ttu-id="a5550-211">**📦🖊 パッケージ作成者**</span><span class="sxs-lookup"><span data-stu-id="a5550-211">**📦🖊 Package Author**</span></span>

<span data-ttu-id="a5550-212">[作成者署名](../reference/signed-packages-reference.md)を使用すると、パッケージの作成者はパッケージに自分の ID をスタンプでき、利用者は身元を確認することができます。</span><span class="sxs-lookup"><span data-stu-id="a5550-212">[Author signing](../reference/signed-packages-reference.md) allows a package author to stamp their identity on a package and for a consumer to verify it came from you.</span></span> <span data-ttu-id="a5550-213">これにより、内容の改ざんから保護され、パッケージの提供元とパッケージの信頼性に関する単一の正しい情報源として機能します。</span><span class="sxs-lookup"><span data-stu-id="a5550-213">This protects you against content tampering and serves as a single source of truth about the origin of the package and the package authenticity.</span></span> <span data-ttu-id="a5550-214">クライアント信頼ポリシーと組み合わせると、パッケージが特定の作成者からのものであることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="a5550-214">When combined with client trust policies, you can verify a package came from a specific author.</span></span>

<span data-ttu-id="a5550-215">作成者によるパッケージへの署名については、[パッケージへの署名](../create-packages/sign-a-package.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="a5550-215">To author sign a package, see [Sign a package](../create-packages/sign-a-package.md).</span></span>

### <a name="two-factor-authentication-2fa"></a><span data-ttu-id="a5550-216">2 要素認証 (2FA)</span><span class="sxs-lookup"><span data-stu-id="a5550-216">Two-Factor Authentication (2FA)</span></span>

<span data-ttu-id="a5550-217">**📦🖊 パッケージ作成者**</span><span class="sxs-lookup"><span data-stu-id="a5550-217">**📦🖊 Package Author**</span></span>

<span data-ttu-id="a5550-218">2 要素認証 (2FA) を有効にすると、[GitHub アカウントへのログイン](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa)または [NuGet.org パブリック パッケージ リポジトリへのログイン](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa)のときに、セキュリティ レイヤーを追加できます。</span><span class="sxs-lookup"><span data-stu-id="a5550-218">Enabling two-factor authentication (2FA) can add an extra layer of security when [logging into your GitHub account](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa) or the [NuGet.org public package repository](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa).</span></span> <span data-ttu-id="a5550-219">アカウントを保護するため、2 要素認証を有効にすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a5550-219">It is recommended that you enable two-factor authentication to protect your account.</span></span>

### <a name="package-id-prefix-reservation"></a><span data-ttu-id="a5550-220">パッケージ ID プレフィックスの予約</span><span class="sxs-lookup"><span data-stu-id="a5550-220">Package ID prefix reservation</span></span> 

<span data-ttu-id="a5550-221">**📦🖊 パッケージ作成者**</span><span class="sxs-lookup"><span data-stu-id="a5550-221">**📦🖊 Package Author**</span></span>

<span data-ttu-id="a5550-222">パッケージの ID を保護するため、対応する名前空間でパッケージ ID プレフィックスを予約し、パッケージ ID プレフィックスが[指定した条件](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria)を満たしている場合、一致する所有者を関連付けることができます。</span><span class="sxs-lookup"><span data-stu-id="a5550-222">To protect the identity of your packages, you can reserve a package ID prefix with your respective namespace to associate a matching owner if your package ID prefix properly falls under the [specified criteria](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria).</span></span> 

<span data-ttu-id="a5550-223">ID プレフィックスの予約の詳細については、「[パッケージ ID プレフィックスの予約](../nuget-org/id-prefix-reservation.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a5550-223">To learn about reserving ID prefixes, see [Package ID prefix reservation](../nuget-org/id-prefix-reservation.md).</span></span>

### <a name="deprecating-and-unlisting-a-vulnerable-package"></a><span data-ttu-id="a5550-224">脆弱なパッケージの非推奨化と一覧からの削除</span><span class="sxs-lookup"><span data-stu-id="a5550-224">Deprecating and unlisting a vulnerable package</span></span>

<span data-ttu-id="a5550-225">**📦🖊 パッケージ作成者**</span><span class="sxs-lookup"><span data-stu-id="a5550-225">**📦🖊 Package Author**</span></span>

<span data-ttu-id="a5550-226">作成したパッケージに脆弱性があることがわかっている場合に .NET パッケージ エコシステムを保護するには、パッケージを非推奨にして一覧から削除し、パッケージを検索するユーザーに表示されないようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a5550-226">To protect the .NET package ecosystem when you are aware of a vulnerability in a package you have authored, do your best to deprecate and unlist the package so it is hidden from users searching for packages.</span></span> <span data-ttu-id="a5550-227">非推奨で一覧にないパッケージを使用している場合は、パッケージの使用を避ける必要があります。</span><span class="sxs-lookup"><span data-stu-id="a5550-227">If you are consuming a package that is deprecated and unlisted, you should avoid using the package.</span></span>

<span data-ttu-id="a5550-228">パッケージを非推奨にして一覧から削除する方法については、パッケージの[非推奨](../nuget-org/deprecate-packages.md)と[一覧からの削除](../nuget-org/policies/deleting-packages.md#unlisting-a-package)に関するドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="a5550-228">To learn how to deprecate and unlist a package, see the following documentation on [deprecating](../nuget-org/deprecate-packages.md) and [unlisting packages](../nuget-org/policies/deleting-packages.md#unlisting-a-package).</span></span>

## <a name="summary"></a><span data-ttu-id="a5550-229">まとめ</span><span class="sxs-lookup"><span data-stu-id="a5550-229">Summary</span></span>

<span data-ttu-id="a5550-230">ソフトウェア サプライ チェーンは、コードに組み込まれたり影響したりするすべてのものです。</span><span class="sxs-lookup"><span data-stu-id="a5550-230">Your software supply chain is anything that goes into or affects your code.</span></span> <span data-ttu-id="a5550-231">サプライ チェーンの侵害は現実であり、一般に広がりつつありますが、それでもまだまれです。そのため、実施できる最も重要なことは、**依存関係を把握し、依存関係を管理し、** **サプライ チェーンを監視する** ことにより、サプライ チェーンを保護することです。</span><span class="sxs-lookup"><span data-stu-id="a5550-231">Even though supply chain compromises are real and growing in popularity, they are still rare; so the most important thing you can do is protect your supply chain by **being aware of your dependencies, managing your dependencies** and **monitoring your supply chain.**</span></span>

<span data-ttu-id="a5550-232">ここでは、サプライ チェーンをより効果的に表示、管理、監視するために NuGet と [GitHub](/learn/modules/maintain-secure-repository-github/) で現在使用できるさまざまな方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="a5550-232">You learned about various methods that NuGet and [GitHub](/learn/modules/maintain-secure-repository-github/) provide that are available to you today to be more effective in viewing, managing, and monitoring your supply chain.</span></span>

<span data-ttu-id="a5550-233">世界中のソフトウェアのセキュリティ保護の詳細については、[The State of the Octoverse 2020 のセキュリティ レポート](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="a5550-233">For more information about securing the world's software, see [The State of the Octoverse 2020 Security Report](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf).</span></span>
