---
title: NuGet.org でのパッケージの readme
description: NuGet.org の readme ファイルがどのようにレンダリングされるか、および問題が発生した場合の対処方法について詳しく説明します。
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a5d68329128c9e9d047fe10e08ce41f1ae0895b4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2021
ms.locfileid: "107902228"
---
# <a name="package-readme-on-nugetorg"></a><span data-ttu-id="b0788-103">NuGet.org でのパッケージの readme</span><span class="sxs-lookup"><span data-stu-id="b0788-103">Package readme on NuGet.org</span></span>

<span data-ttu-id="b0788-104">[NuGet パッケージに readme ファイルを含める](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile)ことにより、パッケージの詳細を充実させ、ユーザーにとって有益なものにすることができます。</span><span class="sxs-lookup"><span data-stu-id="b0788-104">[Include a readme file in your NuGet package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) to make your package details richer and more informative for your users!</span></span>

<span data-ttu-id="b0788-105">これは、おそらく、ユーザーが NuGet.org でパッケージの詳細ページを表示して最初の見る要素の 1 つであり、良い印象を与えるために不可欠です。</span><span class="sxs-lookup"><span data-stu-id="b0788-105">This is likely one of the first elements users will see when they view your package details page on NuGet.org and is essential to making a good impression!</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0788-106">NuGet.org でサポートされているのは、[Markdown](https://daringfireball.net/projects/markdown/) での readme ファイルと、限られたドメインのセットの画像のみです。</span><span class="sxs-lookup"><span data-stu-id="b0788-106">NuGet.org only supports readme files in [Markdown](https://daringfireball.net/projects/markdown/) and images from a limited set of domains.</span></span> <span data-ttu-id="b0788-107">NuGet.org で readme が正しく表示されるように、[画像で許可されているドメイン](#allowed-domains-for-images-and-badges)と[サポートされている Markdown 機能](#supported-markdown-features)を確認してください。</span><span class="sxs-lookup"><span data-stu-id="b0788-107">See our [allowed domains for images](#allowed-domains-for-images-and-badges) and [supported Markdown features](#supported-markdown-features) to ensure your readme renders correctly on NuGet.org.</span></span>

## <a name="what-should-my-readme-include"></a><span data-ttu-id="b0788-108">readme に含める必要があるもの</span><span class="sxs-lookup"><span data-stu-id="b0788-108">What should my readme include?</span></span>

<span data-ttu-id="b0788-109">readme には次の項目を含めることを検討してください。</span><span class="sxs-lookup"><span data-stu-id="b0788-109">Consider including the following items in your readme:</span></span>
* <span data-ttu-id="b0788-110">パッケージの概要と動作についての説明 - どのような問題が解決されるか?</span><span class="sxs-lookup"><span data-stu-id="b0788-110">An introduction to what your package is and does - what problems does it solve?</span></span>
* <span data-ttu-id="b0788-111">パッケージの使用を開始する方法 - 特定の要件があるか?</span><span class="sxs-lookup"><span data-stu-id="b0788-111">How to get started with your package - are there any specific requirements?</span></span>
* <span data-ttu-id="b0788-112">readme 自体に含まれていない場合に、より包括的なドキュメントへのリンク。</span><span class="sxs-lookup"><span data-stu-id="b0788-112">Links to more comprehensive documentation if not included in the readme itself.</span></span>
* <span data-ttu-id="b0788-113">少なくともいくつかのコード スニペットやサンプルまたは画像の例。</span><span class="sxs-lookup"><span data-stu-id="b0788-113">At least a few code snippets/samples or example images.</span></span>
* <span data-ttu-id="b0788-114">フィードバックを行う場所と方法。プロジェクトの問題、Twitter、バグ トラッカー、または他のプラットフォームへのリンクなど。</span><span class="sxs-lookup"><span data-stu-id="b0788-114">Where and how to leave feedback such as link to the project issues, Twitter, bug tracker, or other platform.</span></span>
* <span data-ttu-id="b0788-115">投稿方法 (該当する場合)。</span><span class="sxs-lookup"><span data-stu-id="b0788-115">How to contribute, if applicable.</span></span>

<span data-ttu-id="b0788-116">高品質の readme は、さまざまな形式、形状、サイズで提供されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b0788-116">Keep in mind, high quality readmes can come in a wide variety of formats, shapes, and sizes!</span></span> <span data-ttu-id="b0788-117">NuGet.org で使用可能なパッケージが既にある場合は、リポジトリに `readme.md` や他のドキュメント ファイルが既に存在し、それが NuGet.org の詳細ページに追加するのに適している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b0788-117">If you already have a package available on NuGet.org, chances are that you already have a `readme.md` or other documentation file in your repository that would be a great addition to your NuGet.org details page.</span></span>

## <a name="preview-your-readme"></a><span data-ttu-id="b0788-118">readme をプレビューする</span><span class="sxs-lookup"><span data-stu-id="b0788-118">Preview your readme</span></span>

<span data-ttu-id="b0788-119">NuGet.org で公開される前に readme ファイルをプレビューするには、[NuGet.org のパッケージのアップロード Web ポータル](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg)を使用してパッケージをアップロードし、メタデータ プレビューの [Readme File]\(readme ファイル\) セクションまで下にスクロールします。</span><span class="sxs-lookup"><span data-stu-id="b0788-119">To preview your readme file before it's live on NuGet.org, upload your package using the [Upload Package web portal on NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) and scroll down to the "Readme File" section of the metadata preview.</span></span> <span data-ttu-id="b0788-120">次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="b0788-120">It should look something like this:</span></span>

![readme ファイルのプレビュー](media\readme-upload-preview.PNG)

<span data-ttu-id="b0788-122">時間をかけて、[画像のコンプライアンス](#allowed-domains-for-images-and-badges)と[サポートされている書式設定](#supported-markdown-features)について readme ファイルを繰り返しプレビューし、潜在的なユーザーに優れた印象を与えられることを確認することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="b0788-122">Consider taking time to review and preview your readme file for [image compliance](#allowed-domains-for-images-and-badges) and [supported formatting](#supported-markdown-features) to make sure it gives a great first impression to potential users!</span></span> <span data-ttu-id="b0788-123">NuGet.org に公開した後でパッケージの readme の誤りを修正するには、修正プログラムを使用して、更新されたパッケージのバージョンをプッシュする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b0788-123">To correct mistakes on your package readme once it's published to NuGet.org, you will need to push an updated package version with the fix.</span></span> <span data-ttu-id="b0788-124">すべてに問題がないことを事前に確認することで、将来の頭痛の種を取り除くことができます。</span><span class="sxs-lookup"><span data-stu-id="b0788-124">Making sure everything looks good in advance may save you headache down the road.</span></span>
## <a name="allowed-domains-for-images-and-badges"></a><span data-ttu-id="b0788-125">画像とバッジに許可されているドメイン</span><span class="sxs-lookup"><span data-stu-id="b0788-125">Allowed domains for images and badges</span></span>

<span data-ttu-id="b0788-126">セキュリティとプライバシーの問題により、NuGet.org では、画像やバッジをレンダリングできるドメインが、信頼されたホストに制限されています。</span><span class="sxs-lookup"><span data-stu-id="b0788-126">Due to security and privacy concerns, NuGet.org restricts the domains from which images and badges can be rendered to trusted hosts.</span></span> 

<span data-ttu-id="b0788-127">NuGet.org によりレンダリングが許可されているのは、次の信頼されたドメインのバッジを含むすべての画像です。</span><span class="sxs-lookup"><span data-stu-id="b0788-127">NuGet.org allows all images, including badges, from the following trusted domains to be rendered:</span></span>
* <span data-ttu-id="b0788-128">api.bintray.com</span><span class="sxs-lookup"><span data-stu-id="b0788-128">api.bintray.com</span></span>
* <span data-ttu-id="b0788-129">api.codacy.com</span><span class="sxs-lookup"><span data-stu-id="b0788-129">api.codacy.com</span></span>
* <span data-ttu-id="b0788-130">api.codeclimate.com</span><span class="sxs-lookup"><span data-stu-id="b0788-130">api.codeclimate.com</span></span>
* <span data-ttu-id="b0788-131">api.dependabot.com</span><span class="sxs-lookup"><span data-stu-id="b0788-131">api.dependabot.com</span></span>
* <span data-ttu-id="b0788-132">api.travis-ci.com</span><span class="sxs-lookup"><span data-stu-id="b0788-132">api.travis-ci.com</span></span>
* <span data-ttu-id="b0788-133">api.travis-ci.org</span><span class="sxs-lookup"><span data-stu-id="b0788-133">api.travis-ci.org</span></span>
* <span data-ttu-id="b0788-134">app.fossa.io</span><span class="sxs-lookup"><span data-stu-id="b0788-134">app.fossa.io</span></span>
* <span data-ttu-id="b0788-135">badge.fury.io</span><span class="sxs-lookup"><span data-stu-id="b0788-135">badge.fury.io</span></span>
* <span data-ttu-id="b0788-136">badgen.net</span><span class="sxs-lookup"><span data-stu-id="b0788-136">badgen.net</span></span>
* <span data-ttu-id="b0788-137">badges.gitter.im</span><span class="sxs-lookup"><span data-stu-id="b0788-137">badges.gitter.im</span></span>
* <span data-ttu-id="b0788-138">bettercodehub.com</span><span class="sxs-lookup"><span data-stu-id="b0788-138">bettercodehub.com</span></span>
* <span data-ttu-id="b0788-139">buildstats.info</span><span class="sxs-lookup"><span data-stu-id="b0788-139">buildstats.info</span></span>
* <span data-ttu-id="b0788-140">camo.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="b0788-140">camo.githubusercontent.com</span></span>
* <span data-ttu-id="b0788-141">ci.appveyor.com</span><span class="sxs-lookup"><span data-stu-id="b0788-141">ci.appveyor.com</span></span>
* <span data-ttu-id="b0788-142">circleci.com</span><span class="sxs-lookup"><span data-stu-id="b0788-142">circleci.com</span></span>
* <span data-ttu-id="b0788-143">codecov.io</span><span class="sxs-lookup"><span data-stu-id="b0788-143">codecov.io</span></span>
* <span data-ttu-id="b0788-144">codefactor.io</span><span class="sxs-lookup"><span data-stu-id="b0788-144">codefactor.io</span></span>
* <span data-ttu-id="b0788-145">coveralls.io</span><span class="sxs-lookup"><span data-stu-id="b0788-145">coveralls.io</span></span>
* <span data-ttu-id="b0788-146">dev.azure.com</span><span class="sxs-lookup"><span data-stu-id="b0788-146">dev.azure.com</span></span>
* <span data-ttu-id="b0788-147">github.com/.../workflows/.../badge.svg</span><span class="sxs-lookup"><span data-stu-id="b0788-147">github.com/.../workflows/.../badge.svg</span></span>
* <span data-ttu-id="b0788-148">gitlab.com</span><span class="sxs-lookup"><span data-stu-id="b0788-148">gitlab.com</span></span>
* <span data-ttu-id="b0788-149">img.shields.io</span><span class="sxs-lookup"><span data-stu-id="b0788-149">img.shields.io</span></span>
* <span data-ttu-id="b0788-150">isitmaintained.com</span><span class="sxs-lookup"><span data-stu-id="b0788-150">isitmaintained.com</span></span>
* <span data-ttu-id="b0788-151">opencollective.com</span><span class="sxs-lookup"><span data-stu-id="b0788-151">opencollective.com</span></span>
* <span data-ttu-id="b0788-152">raw.github.com</span><span class="sxs-lookup"><span data-stu-id="b0788-152">raw.github.com</span></span>
* <span data-ttu-id="b0788-153">raw.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="b0788-153">raw.githubusercontent.com</span></span>
* <span data-ttu-id="b0788-154">snyk.io</span><span class="sxs-lookup"><span data-stu-id="b0788-154">snyk.io</span></span>
* <span data-ttu-id="b0788-155">sonarcloud.io</span><span class="sxs-lookup"><span data-stu-id="b0788-155">sonarcloud.io</span></span>
* <span data-ttu-id="b0788-156">user-images.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="b0788-156">user-images.githubusercontent.com</span></span>

<span data-ttu-id="b0788-157">別のドメインを許可リストに追加する必要があると思われる場合は、遠慮なく[問題を提出](https://github.com/NuGet/NuGetGallery/issues)してください。エンジニアリング チームによって、プライバシーとセキュリティのコンプライアンスに関するレビューが行われます。</span><span class="sxs-lookup"><span data-stu-id="b0788-157">If you feel that another domain should be added to the allow-list, please feel free to [file an issue](https://github.com/NuGet/NuGetGallery/issues) and it will be reviewed by our engineering team for privacy and security compliance.</span></span> <span data-ttu-id="b0788-158">相対ローカル パスで指定された画像と、サポートされていないドメインからホストされている画像はレンダリングされず、パッケージ所有者にのみ表示される readme ファイルのプレビューとパッケージ詳細ページで警告が発生します。</span><span class="sxs-lookup"><span data-stu-id="b0788-158">Images with relative local paths and images hosted from unsupported domains will not be rendered and will produce a warning on the readme file preview and package details page that is only visible to the package owners.</span></span>

## <a name="supported-markdown-features"></a><span data-ttu-id="b0788-159">サポートされている Markdown 機能</span><span class="sxs-lookup"><span data-stu-id="b0788-159">Supported Markdown features</span></span>
<span data-ttu-id="b0788-160">[Markdown](https://daringfireball.net/projects/markdown/) は、プレーン テキスト形式の構文を使用する軽量のマークアップ言語です。</span><span class="sxs-lookup"><span data-stu-id="b0788-160">[Markdown](https://daringfireball.net/projects/markdown/) is a lightweight markup language with plain text formatting syntax.</span></span> <span data-ttu-id="b0788-161">NuGet.org の readme では、[Markdig](https://github.com/lunet-io/markdig) 解析エンジンによる [CommonMark](https://commonmark.org/) 準拠の Markdown がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="b0788-161">NuGet.org readmes support [CommonMark](https://commonmark.org/) compliant Markdown through the [Markdig](https://github.com/lunet-io/markdig) parsing engine.</span></span>

<span data-ttu-id="b0788-162">現在、NuGet.org によってサポートされている Markdown の機能は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="b0788-162">NuGet.org currently supports the following Markdown features:</span></span>
* [<span data-ttu-id="b0788-163">ヘッダー</span><span class="sxs-lookup"><span data-stu-id="b0788-163">Headers</span></span>](https://spec.commonmark.org/0.29/#atx-headings)
* [<span data-ttu-id="b0788-164">イメージ</span><span class="sxs-lookup"><span data-stu-id="b0788-164">Images</span></span>](https://spec.commonmark.org/0.29/#images)
* [<span data-ttu-id="b0788-165">追加の強調</span><span class="sxs-lookup"><span data-stu-id="b0788-165">Extra emphasis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [<span data-ttu-id="b0788-166">リスト</span><span class="sxs-lookup"><span data-stu-id="b0788-166">Lists</span></span>](https://spec.commonmark.org/0.29/#lists)
* [<span data-ttu-id="b0788-167">リンク</span><span class="sxs-lookup"><span data-stu-id="b0788-167">Links</span></span>](https://spec.commonmark.org/0.29/#links)
* [<span data-ttu-id="b0788-168">ブロック引用</span><span class="sxs-lookup"><span data-stu-id="b0788-168">Block quotes</span></span>](https://spec.commonmark.org/0.29/#block-quotes)
* [<span data-ttu-id="b0788-169">円記号によるエスケープ</span><span class="sxs-lookup"><span data-stu-id="b0788-169">Backslash escapes</span></span>](https://spec.commonmark.org/0.29/#backslash-escapes)
* [<span data-ttu-id="b0788-170">コード スパン</span><span class="sxs-lookup"><span data-stu-id="b0788-170">Code spans</span></span>](https://spec.commonmark.org/0.29/#code-spans)
* [<span data-ttu-id="b0788-171">タスク リスト</span><span class="sxs-lookup"><span data-stu-id="b0788-171">Task lists</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [<span data-ttu-id="b0788-172">テーブル</span><span class="sxs-lookup"><span data-stu-id="b0788-172">Tables</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [<span data-ttu-id="b0788-173">絵文字</span><span class="sxs-lookup"><span data-stu-id="b0788-173">Emojis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [<span data-ttu-id="b0788-174">自動リンク</span><span class="sxs-lookup"><span data-stu-id="b0788-174">Auto-links</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

