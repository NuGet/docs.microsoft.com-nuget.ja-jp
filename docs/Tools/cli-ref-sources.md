---
title: "NuGet CLI コマンドをソース |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "ソースのコマンドを nuget.exe への参照"
keywords: "nuget のソースの参照、コマンドをソース"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c1cd909c0c35d52f0269d267367669df46f9db55
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="ce286-104">ソースのコマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ce286-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="ce286-105">**適用されます:**パッケージ消費、パブリッシング&bullet;**サポートされているバージョン:**すべて</span><span class="sxs-lookup"><span data-stu-id="ce286-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ce286-106">あるソースの一覧を管理する`%AppData%\NuGet\NuGet.Config`または指定した構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="ce286-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

<span data-ttu-id="ce286-107">ここで、nuget.org のソース URL は `https://api.nuget.org/v3/index.json` となります。</span><span class="sxs-lookup"><span data-stu-id="ce286-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="ce286-108">使用法</span><span class="sxs-lookup"><span data-stu-id="ce286-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="ce286-109">ここで`<operation>`の 1 つ*を一覧表示、追加、削除、有効化、無効化、*または*更新*、 `<name>` 、ソースの名前を指定および`<source>`ソースの URL は、します。</span><span class="sxs-lookup"><span data-stu-id="ce286-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="ce286-110">オプション</span><span class="sxs-lookup"><span data-stu-id="ce286-110">Options</span></span>

| <span data-ttu-id="ce286-111">オプション</span><span class="sxs-lookup"><span data-stu-id="ce286-111">Option</span></span> | <span data-ttu-id="ce286-112">説明</span><span class="sxs-lookup"><span data-stu-id="ce286-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ce286-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ce286-113">ConfigFile</span></span> | <span data-ttu-id="ce286-114">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="ce286-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ce286-115">指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。</span><span class="sxs-lookup"><span data-stu-id="ce286-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="ce286-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ce286-116">ForceEnglishOutput</span></span> | <span data-ttu-id="ce286-117">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="ce286-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ce286-118">形式</span><span class="sxs-lookup"><span data-stu-id="ce286-118">Format</span></span> | <span data-ttu-id="ce286-119">適用されます、`list`アクションを指定できます`Detailed`(既定) または`Short`です。</span><span class="sxs-lookup"><span data-stu-id="ce286-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="ce286-120">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="ce286-120">Help</span></span> | <span data-ttu-id="ce286-121">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="ce286-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="ce286-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="ce286-122">NonInteractive</span></span> | <span data-ttu-id="ce286-123">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="ce286-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ce286-124">パスワード</span><span class="sxs-lookup"><span data-stu-id="ce286-124">Password</span></span> | <span data-ttu-id="ce286-125">ソースと認証のパスワードを指定します。</span><span class="sxs-lookup"><span data-stu-id="ce286-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="ce286-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="ce286-126">StorePasswordInClearText</span></span> | <span data-ttu-id="ce286-127">暗号化された形式を格納する既定の動作ではなく暗号化されていないテキストでパスワードを保存することを示します。</span><span class="sxs-lookup"><span data-stu-id="ce286-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="ce286-128">UserName</span><span class="sxs-lookup"><span data-stu-id="ce286-128">UserName</span></span> | <span data-ttu-id="ce286-129">ソースと認証のユーザー名を指定します。</span><span class="sxs-lookup"><span data-stu-id="ce286-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="ce286-130">詳細度</span><span class="sxs-lookup"><span data-stu-id="ce286-130">Verbosity</span></span> | <span data-ttu-id="ce286-131">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="ce286-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="ce286-132">必ず、nuget.exe は後でパッケージ ソースへのアクセスに使用されるため、同じユーザーのコンテキストで、ソースのパスワードを追加してください。</span><span class="sxs-lookup"><span data-stu-id="ce286-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="ce286-133">パスワードは、config ファイルで暗号化されて格納され、できますのみ復号化、同じユーザー コンテキストで暗号化されていたとします。</span><span class="sxs-lookup"><span data-stu-id="ce286-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="ce286-134">したがって、たとえば使用する場合、ビルド サーバー ビルド サーバーのタスクを実行する同じ Windows ユーザーがパスワードを暗号化する必要があります NuGet パッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="ce286-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="ce286-135">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ce286-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ce286-136">使用例</span><span class="sxs-lookup"><span data-stu-id="ce286-136">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
