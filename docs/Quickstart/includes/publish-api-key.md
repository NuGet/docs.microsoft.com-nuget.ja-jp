1. <span data-ttu-id="81eae-101">[ご自分の nuget.org アカウントにサインインする](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)か、まだ持っていなければ、アカウントを作成します。</span><span class="sxs-lookup"><span data-stu-id="81eae-101">[Sign into your nuget.org account](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) or create an account if you don't have one already.</span></span>

1. <span data-ttu-id="81eae-102">(右上で) ユーザー名を選択し、**[API キー]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="81eae-102">Select your user name (on the upper right), then select **API Keys**.</span></span>

1. <span data-ttu-id="81eae-103">**[作成]** を選択し、キーの名前を入力し、**[API キー]** の下で **[スコープの選択]、[プッシュ]** の順に選択し、**[Glob pattern]\(glob パターン\)** に「*」を入力し、\*\*[作成]*\* を選択します。</span><span class="sxs-lookup"><span data-stu-id="81eae-103">Select **Create**, provide a name for your key, select **Select Scopes > Push**Under **API Key**, enter \* for **Glob pattern**, then select **Create**.</span></span>

1. <span data-ttu-id="81eae-104">キーが作成されたら、**[コピー]** を選択して、CLI で必要となるアクセス キーを取得します。</span><span class="sxs-lookup"><span data-stu-id="81eae-104">Once the key is created, select **Copy** to retrieve the access key you need in the CLI:</span></span>

    ![API キーをクリップボードにコピーする](../media/QS_Create-02-APIKey.png)

1. <span data-ttu-id="81eae-106">**重要**: キーは、後でもう一度コピーできないため、安全な場所に保存してください。</span><span class="sxs-lookup"><span data-stu-id="81eae-106">**Important**: Save your key in a secure location because you cannot copy the key again later on.</span></span> <span data-ttu-id="81eae-107">[API キー] ページに戻ったら、キーを再生成してコピーする必要があります。</span><span class="sxs-lookup"><span data-stu-id="81eae-107">If you return to the API key page, you need to regenerate the key to copy it.</span></span> <span data-ttu-id="81eae-108">CLI を通じてパッケージをプッシュする必要がなくなった場合は、API キーを削除することもできます。</span><span class="sxs-lookup"><span data-stu-id="81eae-108">You can also remove the API key if you no longer want to push packages via the CLI.</span></span>