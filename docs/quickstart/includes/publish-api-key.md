---
ms.openlocfilehash: 20851cd71cc5eb6735fe5e0cd8b0f314f9100be4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "68419927"
---
1. <span data-ttu-id="dff9e-101">[ご自分の nuget.org アカウントにサインインする](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)か、まだ持っていなければ、アカウントを作成します。</span><span class="sxs-lookup"><span data-stu-id="dff9e-101">[Sign into your nuget.org account](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) or create an account if you don't have one already.</span></span>

   <span data-ttu-id="dff9e-102">アカウントの作成について詳しくは、「[個人アカウント](../../nuget-org/individual-accounts.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="dff9e-102">For more information on creating your account, see [Individual accounts](../../nuget-org/individual-accounts.md).</span></span>

1. <span data-ttu-id="dff9e-103">(右上で) ユーザー名を選択し、 **[API キー]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="dff9e-103">Select your user name (on the upper right), then select **API Keys**.</span></span>

1. <span data-ttu-id="dff9e-104">**[作成]** を選択し、キーの名前を指定して、 **[スコープの選択] > [プッシュ]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="dff9e-104">Select **Create**, provide a name for your key, select **Select Scopes > Push**.</span></span> <span data-ttu-id="dff9e-105">**[glob パターン]** に「\*」と入力してから、 **[作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="dff9e-105">Enter \* for **Glob pattern**, then select **Create**.</span></span> <span data-ttu-id="dff9e-106">(スコープの詳細については、後述の説明をご覧ください。)</span><span class="sxs-lookup"><span data-stu-id="dff9e-106">(See below for more about scopes.)</span></span>

1. <span data-ttu-id="dff9e-107">キーが作成されたら、 **[コピー]** を選択して、CLI で必要となるアクセス キーを取得します。</span><span class="sxs-lookup"><span data-stu-id="dff9e-107">Once the key is created, select **Copy** to retrieve the access key you need in the CLI:</span></span>

    ![API キーをクリップボードにコピーする](../media/QS_Create-02-APIKey.png)

1. <span data-ttu-id="dff9e-109">**重要**: キーは、後でもう一度コピーできないため、安全な場所に保存してください。</span><span class="sxs-lookup"><span data-stu-id="dff9e-109">**Important**: Save your key in a secure location because you cannot copy the key again later on.</span></span> <span data-ttu-id="dff9e-110">[API キー] ページに戻ったら、キーを再生成してコピーする必要があります。</span><span class="sxs-lookup"><span data-stu-id="dff9e-110">If you return to the API key page, you need to regenerate the key to copy it.</span></span> <span data-ttu-id="dff9e-111">CLI を通じてパッケージをプッシュする必要がなくなった場合は、API キーを削除することもできます。</span><span class="sxs-lookup"><span data-stu-id="dff9e-111">You can also remove the API key if you no longer want to push packages via the CLI.</span></span>

<span data-ttu-id="dff9e-112">スコープを使用して、別の目的のために別個の API キーを作成できます。</span><span class="sxs-lookup"><span data-stu-id="dff9e-112">Scoping allows you to create separate API keys for different purposes.</span></span> <span data-ttu-id="dff9e-113">各キーは有効期限の時間枠を備え、特定のパッケージ (またはの glob パターン) に対してスコープを設定できます。</span><span class="sxs-lookup"><span data-stu-id="dff9e-113">Each key has its expiration timeframe and can be scoped to specific packages (or glob patterns).</span></span> <span data-ttu-id="dff9e-114">また、各キーは、新しいパッケージと更新のプッシュ、更新のプッシュのみ、リストからの除外など、特定の操作に対してもスコープを設定します。</span><span class="sxs-lookup"><span data-stu-id="dff9e-114">Each key is also scoped to specific operations: push of new packages and updates, push of updates only, or delisting.</span></span> <span data-ttu-id="dff9e-115">スコープを使用して、必要なアクセス許可以外は持たない組織のパッケージ管理を行う別の担当者のために、API キーを作成できます。</span><span class="sxs-lookup"><span data-stu-id="dff9e-115">Through scoping, you can create API keys for different people who manage packages for your organization such that they have only the permissions they need.</span></span> <span data-ttu-id="dff9e-116">詳しくは、「[スコープ設定された API キー](../../nuget-org/scoped-api-keys.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="dff9e-116">For more information, see [scoped API keys](../../nuget-org/scoped-api-keys.md).</span></span>