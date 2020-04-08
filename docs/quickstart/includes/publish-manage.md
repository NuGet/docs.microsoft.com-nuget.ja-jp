---
ms.openlocfilehash: 9c3cb22c8c220a7297eb88db6ff0941e4c11c914
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495967"
---
<span data-ttu-id="290bf-101">nuget.org のプロファイルから、 **[パッケージの管理]** を選択して、公開したパッケージを確認します。</span><span class="sxs-lookup"><span data-stu-id="290bf-101">From your profile on nuget.org, select **Manage Packages** to see the one you just published.</span></span> <span data-ttu-id="290bf-102">確認メールも送信されます。</span><span class="sxs-lookup"><span data-stu-id="290bf-102">You also receive a confirmation email.</span></span> <span data-ttu-id="290bf-103">パッケージがインデックス作成され、他のユーザーが検索して検索結果に表示されるようになるまでには、時間がかかる場合があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="290bf-103">Note that it might take a while for your package to be indexed and appear in search results where others can find it.</span></span> <span data-ttu-id="290bf-104">この間、パッケージのページに次のメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="290bf-104">During that time your package page shows the message below:</span></span>

![このパッケージはまだインデックスされていません。](../media/QS_Create-03-NotIndexed.png)

<span data-ttu-id="290bf-107">これで終了です。</span><span class="sxs-lookup"><span data-stu-id="290bf-107">And that's it!</span></span> <span data-ttu-id="290bf-108">最初の NuGet パッケージが nuget.org に公開され、他の開発者はそれを自身のプロジェクトで使用することができます。</span><span class="sxs-lookup"><span data-stu-id="290bf-108">You've just published your first NuGet package to nuget.org that other developers can use in their own projects.</span></span>

<span data-ttu-id="290bf-109">このチュートリアルで作成したパッケージが、実際に有用ではない場合 (空のクラス ライブラリを使用して作成されたパッケージなど)、そのパッケージを*一覧から削除*して、検索結果に表示されないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="290bf-109">If in this walkthrough you created a package that isn't actually useful (such as a package created with an empty class library), you should *unlist* the package to hide it from search results:</span></span>

1. <span data-ttu-id="290bf-110">nuget.org で、ユーザー名 (ページの右上) を選択し、 **[パッケージの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="290bf-110">On nuget.org, select your user name (upper right of the page), then select **Manage Packages**.</span></span>

1. <span data-ttu-id="290bf-111">**[公開済み]** の一覧から削除するパッケージを見つけて、右側のごみ箱のアイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="290bf-111">Locate the package you want to unlist under **Published** and select the trash can icon on the right:</span></span>

    ![nuget.org のパッケージの一覧に表示されたごみ箱のアイコン](../media/qs_create-vs-03-trash-can.png)

1. <span data-ttu-id="290bf-113">後続のページで、 **[List (package-name) in search results]\(検索結果に (パッケージ名) をリストする\)** というラベルの付いたボックスをオフにし、 **[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="290bf-113">On the subsequent page, clear the box labeled **List (package-name) in search results** and select **Save**:</span></span>

    ![nuget.org でパッケージの [リストする] チェックボックスをクリア](../media/qs_create-vs-04-unlist.png)