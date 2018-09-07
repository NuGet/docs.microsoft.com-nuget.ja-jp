---
title: NuGet パッケージの公開方法
description: NuGet パッケージを nuget.org やプライベート フィードに公開する方法と nuget.org でパッケージ所有権を管理する方法に関する詳細。
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: bd36ae311da1ec824726c5d73670b1232a3f89e0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549587"
---
# <a name="publishing-packages"></a><span data-ttu-id="ef9c8-103">パッケージを公開する</span><span class="sxs-lookup"><span data-stu-id="ef9c8-103">Publishing packages</span></span>

<span data-ttu-id="ef9c8-104">パッケージを作成し、`.nupkg` ファイルを入手している場合は、このプロセスにより、他の開発者がパッケージを簡単に利用できるようにすることができます。公開または非公開のいずれかを選択できます。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-104">Once you have created a package and have your `.nupkg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="ef9c8-105">公開パッケージの場合、この記事で説明するように、[nuget.org](https://www.nuget.org/packages/manage/upload) 経由で世界中の開発者が利用できます (NuGet 4.1.0 以降が必要です)。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-105">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this article (requires NuGet 4.1.0+).</span></span>
- <span data-ttu-id="ef9c8-106">非公開パッケージの場合、ファイル共有、プライベート NuGet サーバー、 [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish)、あるいは myget、ProGet、Nexus Repository、Artifactory のようなサードパーティ リポジトリで保存することで、チームや組織だけが利用できます。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-106">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="ef9c8-107">詳細については、「[Hosting Packages Overview](../hosting-packages/overview.md)」 (パッケージ ホストの概要) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-107">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="ef9c8-108">この記事では、nuget.org に公開する方法を取り上げます。Visual Studio Team Services に公開する方法については、「[Package Management](https://www.visualstudio.com/docs/package/nuget/publish)」(パッケージ管理) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-108">This article covers publishing to nuget.org; for publishing to Visual Studio Team Services, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="ef9c8-109">nuget.org に公開する</span><span class="sxs-lookup"><span data-stu-id="ef9c8-109">Publish to nuget.org</span></span>

<span data-ttu-id="ef9c8-110">Nuget.org の場合、Microsoft アカウントでサインインする必要があります。このアカウントで、nuget.org でのアカウント登録を行うよう求められます。また、古いバージョンのポータルを使用して作成された nuget.org アカウントで、サインインすることも可能です。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-110">For nuget.org, you must sign in with a Microsoft account, with which you'll be asked to register the account with nuget.org. You can also sign in with a nuget.org account created using older versions of the portal.</span></span>

![NuGet サインインの場所](media/publish_NuGetSignIn.png)

<span data-ttu-id="ef9c8-112">次に、次のセクションで説明するように、nuget.org Web ポータルを使用する方法、コマンド ラインから nuget.org にプッシュする (`nuget.exe` 4.1.0 以降が必要) 方法、または Visual Studio Team Services を介して CI/CD プロセスの一環として発行する方法のいずれかでパッケージをアップロードできます。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-112">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Visual Studio Team Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="ef9c8-113">Web ポータル: nuget.org の [パッケージのアップロード] を使用</span><span class="sxs-lookup"><span data-stu-id="ef9c8-113">Web portal: use the Upload Package tab on nuget.org</span></span>

1. <span data-ttu-id="ef9c8-114">nuget.org の上部メニューで **[アップロード]** を選択して、パッケージの場所を参照します。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-114">Select **Upload** on the top menu of nuget.org and browse to the package location.</span></span>

    ![nuget.org 上でパッケージをアップロードする](media/publish_UploadYourPackage.PNG)

1. <span data-ttu-id="ef9c8-116">nuget.org では、パッケージ名が使用可能かどうかが示されます。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-116">nuget.org tells you if the package name is available.</span></span> <span data-ttu-id="ef9c8-117">使用できない場合、お使いのプロジェクトのパッケージ ID を変更し、リビルドしてから、アップロードをもう一度やり直してください。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-117">If it isn't, change the package identifier in your project, rebuild, and try the upload again.</span></span>

1. <span data-ttu-id="ef9c8-118">パッケージ名が使用可能な場合、nuget.org では、パッケージ マニフェストからメタデータを確認できる **[確認]** セクションを開きます。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-118">If the package name is available, nuget.org opens a **Verify** section in which you can review the metadata from the package manifest.</span></span> <span data-ttu-id="ef9c8-119">いずれかのメタデータを変更するには、お使いのプロジェクト (プロジェクト ファイルまたは `.nuspec` ファイル) を編集し、リビルドし、パッケージを再作成して、もう一度アップロードします。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-119">To change any of the metadata, edit your project (project file or `.nuspec` file), rebuild, recreate the package, and upload again.</span></span>

1. <span data-ttu-id="ef9c8-120">**[Import Documentation]\(ドキュメントのインポート\)** では、マークダウンを貼り付けて、URL でドキュメントを参照したり、ドキュメント ファイルをアップロードしたりできます。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-120">Under **Import Documentation** you can paste Markdown, point to your docs with a URL, or upload a documentation file.</span></span>

1. <span data-ttu-id="ef9c8-121">すべての情報が準備できたら、**[送信]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-121">When all the information is ready, select the **Submit** button</span></span>

### <a name="command-line"></a><span data-ttu-id="ef9c8-122">コマンド ライン</span><span class="sxs-lookup"><span data-stu-id="ef9c8-122">Command line</span></span>

<span data-ttu-id="ef9c8-123">nuget.org にパッケージをプッシュするには、[nuget.exe v4.1.0 以降](https://www.nuget.org/downloads)を使用する必要があります。これは必須の [NuGet プロトコル](../api/nuget-protocols.md)を実装します。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-123">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span> <span data-ttu-id="ef9c8-124">また、nuget.org 上で作成される API キーも必要です。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-124">You also need an API key, which is created on nuget.org.</span></span>

#### <a name="create-api-keys"></a><span data-ttu-id="ef9c8-125">API キーの作成</span><span class="sxs-lookup"><span data-stu-id="ef9c8-125">Create API keys</span></span>

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="ef9c8-126">dotnet nuget push を使用して公開する</span><span class="sxs-lookup"><span data-stu-id="ef9c8-126">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a><span data-ttu-id="ef9c8-127">nuget push を使用して公開する</span><span class="sxs-lookup"><span data-stu-id="ef9c8-127">Publish with nuget push</span></span>

1. <span data-ttu-id="ef9c8-128">コマンド プロンプトで次のコマンドを実行して、`<your_API_key>` を nuget.org から取得したキーに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-128">At a command prompt, run the following command, replacing `<your_API_key>` with the key obtained from nuget.org:</span></span>

    ```cli
    nuget setApiKey <your_API_key>
    ```

    <span data-ttu-id="ef9c8-129">このコマンドはお使いの NuGet 構成に API キーを格納します。そのため、同じコンピューター上でこの手順をもう一度繰り返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-129">This command stores your API key in your NuGet configuration so that you need repeat this step again on the same computer.</span></span>

1. <span data-ttu-id="ef9c8-130">以下のコマンドを使用して、NuGet ギャラリーにパッケージをプッシュします。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-130">Push your package to NuGet Gallery using the following command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a><span data-ttu-id="ef9c8-131">署名付きパッケージの公開</span><span class="sxs-lookup"><span data-stu-id="ef9c8-131">Publish signed packages</span></span>

<span data-ttu-id="ef9c8-132">署名付きパッケージを送信するには、最初にパッケージの署名に使用する[証明書を登録する](../reference/Signed-Packages-Reference.md#register-certificate-on-nugetorg)必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-132">To submit signed packages, you must first [register the certificate](../reference/Signed-Packages-Reference.md#register-certificate-on-nugetorg) used for signing the packages.</span></span> 

> [!Warning]
> <span data-ttu-id="ef9c8-133">[署名付きパッケージの要件](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg)を満たしていないパッケージは、nuget.org に拒否されます。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-133">nuget.org rejects packages that don't satisfy the [signed package requirements](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).</span></span>

### <a name="package-validation-and-indexing"></a><span data-ttu-id="ef9c8-134">パッケージの検証とインデックスの作成</span><span class="sxs-lookup"><span data-stu-id="ef9c8-134">Package validation and indexing</span></span>

<span data-ttu-id="ef9c8-135">nuget.org にプッシュされたパッケージは、ウィルス チェックなど、いくつかの検証を受けます。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-135">Packages pushed to nuget.org undergo several validations, such as virus checks.</span></span> <span data-ttu-id="ef9c8-136">(Nuget.org 上のすべてのパッケージが定期的にスキャンされます。)</span><span class="sxs-lookup"><span data-stu-id="ef9c8-136">(All packages on nuget.org are periodically scanned.)</span></span>

<span data-ttu-id="ef9c8-137">である必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-137">.</span></span> <span data-ttu-id="ef9c8-138">パッケージがすべての検証に合格すると、インデックスが作成され、検索結果に表示されるようになりますが、それには時間がかかることがあります。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-138">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="ef9c8-139">インデックスの作成が完了すると、パッケージが正常に公開されたことを示す確認の電子メールが届きます。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-139">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="ef9c8-140">パッケージが検証で不合格になった場合、パッケージの詳細ページが更新され、関連するエラーが表示されます。それに関する電子メールも届きます。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-140">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="ef9c8-141">パッケージの検証とインデックスの作成は、通常、15 以内で完了します。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-141">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="ef9c8-142">パッケージ公開に予想以上の時間がかかる場合、[status.nuget.org](https://status.nuget.org/) にアクセスし、nuget.org に中断が発生していないか確認してください。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-142">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="ef9c8-143">すべてのシステムが動作しているとき、1 時間以内にパッケージが正常に公開されない場合、nuget.org にログインし、パッケージ ページの [Contact Support] リンクからお問い合わせください。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-143">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package page.</span></span>

<span data-ttu-id="ef9c8-144">パッケージのステータスを表示するには、nuget.org でアカウント名の下にある **[パッケージの管理]** を選択します。検証が完了すると、確認の電子メールを受信します。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-144">To see the status of a package, select **Manage packages** under your account name on nuget.org. You receive a confirmation email when validation is complete.</span></span>

<span data-ttu-id="ef9c8-145">パッケージにインデックスが付けられ、検索結果に表示されるようになり、他のユーザーが検索可能になるまで時間がかかることがあります。その間、パッケージ ページには次のメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-145">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

![パッケージがまだ公開されていないことを示すメッセージ](media/publish_NotYetIndexed.png)

### <a name="visual-studio-team-services-cicd"></a><span data-ttu-id="ef9c8-147">Visual Studio Team Services (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="ef9c8-147">Visual Studio Team Services (CI/CD)</span></span>

<span data-ttu-id="ef9c8-148">継続的インテグレーション/配置プロセスの一部として Visual Studio Team Services を利用して nuget.org にパッケージをプッシュする場合、NuGet タスクで `nuget.exe` 4.1 以上を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-148">If you push packages to nuget.org using Visual Studio Team Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="ef9c8-149">詳細は、Microsoft DevOps ブログの「[Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/)」 (ビルドで最新の NuGet を利用する) にあります。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-149">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="ef9c8-150">nuget.org でパッケージ所有者を管理する</span><span class="sxs-lookup"><span data-stu-id="ef9c8-150">Managing package owners on nuget.org</span></span>

<span data-ttu-id="ef9c8-151">各 NuGet パッケージの `.nuspec` はパッケージの作成者を定義するものですが、nuget.org ギャラリーでは、所有権の定義にそのメタデータは使用されません。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-151">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="ef9c8-152">nuget.org では、パッケージを公開した人に最初の所有権が割り当てられます。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-152">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="ef9c8-153">これは nuget.org UI からパッケージをアップロードしたログイン ユーザーになるか、`nuget SetApiKey` または `nuget push` と共に API キーが使用されたユーザーになります。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-153">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="ef9c8-154">パッケージ所有者にはすべて、パッケージの完全アクセス許可が与えられます。他の所有者を追加したり、削除したり、更新内容を公開したりできます。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-154">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="ef9c8-155">パッケージの所有権は次のように変更します。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-155">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="ef9c8-156">パッケージの現在の所有者になっているアカウントで nuget.org にサインインします。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-156">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="ef9c8-157">自分のアカウント名を選択し、**[パッケージの管理]** を選択し、**[Published Packages]\(公開されたパッケージ\)** を展開します。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-157">Select your account name, select **Manage packages**, and expand **Published Packages**.</span></span>
1. <span data-ttu-id="ef9c8-158">管理するパッケージを選択し、右側にある **[Manage owners]\(所有者を管理する\)** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-158">Select on the package you want to manage, then on the right side select **Manage owners**.</span></span>

<span data-ttu-id="ef9c8-159">ここにはいくつかのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-159">From here you have several options:</span></span>

1. <span data-ttu-id="ef9c8-160">**[Current Owners]\(現在の所有者\)** に一覧表示されたいずれかの所有者を削除します。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-160">Remove any owner listed under **Current Owners**.</span></span>
1. <span data-ttu-id="ef9c8-161">ユーザー名、メッセージを入力して **[追加]** を選択し、**[所有者の追加]** に所有者を追加します。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-161">Add an owner under **Add Owner** by entering their user name, a message, and selecting **Add**.</span></span> <span data-ttu-id="ef9c8-162">この動作でその新しい共同所有者に確認リンクを含む電子メールが送信されます。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-162">This action sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="ef9c8-163">確認後、その人に所有者を追加したり、削除したりできる完全アクセス許可が与えられます。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-163">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="ef9c8-164">(確認されるまで、**[Current Owners]\(現在の所有者\)** セクションにはその人が承認待ちとして表示されます。)</span><span class="sxs-lookup"><span data-stu-id="ef9c8-164">(Until confirmed, the **Current Owners** section indicates pending approval for that person.)</span></span>
1. <span data-ttu-id="ef9c8-165">所有権を譲渡するには (所有権が変更された場合や間違ったアカウントでパッケージが公開された場合)、新しい所有者を追加します。新しい所有者は所有権を確認したら、一覧から他の所有者を削除できます。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-165">To transfer ownership (as when ownership changes or a package was published under the wrong account), add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="ef9c8-166">会社またはグループに所有権を割り当てるには、適切なチーム メンバーに転送される電子メール エイリアスを利用して nuget.org アカウントを作成します。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-166">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="ef9c8-167">たとえば、そのようなエイリアスである [microsoft](http://nuget.org/profiles/microsoft) アカウントや [aspnet](http://nuget.org/profiles/aspnet) アカウントでさまざまな Microsoft ASP.NET パッケージが共同所有されています。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-167">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="ef9c8-168">パッケージ所有権を回復する</span><span class="sxs-lookup"><span data-stu-id="ef9c8-168">Recovering package ownership</span></span>

<span data-ttu-id="ef9c8-169">パッケージにアクティブな所有者が与えられていないことがあります。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-169">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="ef9c8-170">たとえば、パッケージを作る会社を元々の所有者が去った場合、nuget.org 資格情報をなくした場合、ギャラリーの早期のバグが原因でパッケージが所有者なしになった場合などです。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-170">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="ef9c8-171">自分がパッケージの正当な所有者であり、所有権を取り戻す必要がある場合、nuget.org の[問い合わせフォーム](https://www.nuget.org/policies/Contact)を利用し、NuGet チームに状況を説明してください。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-171">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="ef9c8-172">その後、パッケージの所有権を検証するプロセスが開始します。パッケージのプロジェクト URL、Twitter、電子メール、その他の手段で既存の所有者が確認されます。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-172">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="ef9c8-173">いずれの方法でも確認できない場合、所有者になるための新しい招待を送信します。</span><span class="sxs-lookup"><span data-stu-id="ef9c8-173">But if all else fails, we can send you a new invite to become an owner.</span></span>
