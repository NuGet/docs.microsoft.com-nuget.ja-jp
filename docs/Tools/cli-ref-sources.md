---
title: "NuGet CLI コマンドをソース |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 997ce736-91ba-4cd2-88c9-b4b168e3130a
description: "ソースのコマンドを nuget.exe への参照"
keywords: "nuget のソースの参照、コマンドをソース"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 52c46dba168e7395d50cb8d8f9775839389e614c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="d55b0-104">ソースのコマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d55b0-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="d55b0-105">**適用されます:**パッケージ消費、パブリッシング&bullet;**サポートされているバージョン:**すべて</span><span class="sxs-lookup"><span data-stu-id="d55b0-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d55b0-106">あるソースの一覧を管理する`%AppData%\NuGet\NuGet.Config`または指定した構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="d55b0-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

## <a name="usage"></a><span data-ttu-id="d55b0-107">使用方法</span><span class="sxs-lookup"><span data-stu-id="d55b0-107">Usage</span></span>

```
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="d55b0-108">ここで`<operation>`の 1 つ*を一覧表示、追加、削除、有効化、無効化、*または*更新*、 `<name>` 、ソースの名前を指定および`<source>`ソースの URL は、します。</span><span class="sxs-lookup"><span data-stu-id="d55b0-108">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>


## <a name="options"></a><span data-ttu-id="d55b0-109">オプション</span><span class="sxs-lookup"><span data-stu-id="d55b0-109">Options</span></span>

| <span data-ttu-id="d55b0-110">オプション</span><span class="sxs-lookup"><span data-stu-id="d55b0-110">Option</span></span> | <span data-ttu-id="d55b0-111">説明</span><span class="sxs-lookup"><span data-stu-id="d55b0-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d55b0-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d55b0-112">ConfigFile</span></span> | <span data-ttu-id="d55b0-113">*(2.5 +)* NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="d55b0-113">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="d55b0-114">指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。</span><span class="sxs-lookup"><span data-stu-id="d55b0-114">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="d55b0-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d55b0-115">ForceEnglishOutput</span></span> | <span data-ttu-id="d55b0-116">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="d55b0-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d55b0-117">形式</span><span class="sxs-lookup"><span data-stu-id="d55b0-117">Format</span></span> | <span data-ttu-id="d55b0-118">適用されます、`list`アクションを指定できます`Detailed`(既定) または`Short`です。</span><span class="sxs-lookup"><span data-stu-id="d55b0-118">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="d55b0-119">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="d55b0-119">Help</span></span> | <span data-ttu-id="d55b0-120">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="d55b0-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="d55b0-121">非対話型</span><span class="sxs-lookup"><span data-stu-id="d55b0-121">NonInteractive</span></span> | <span data-ttu-id="d55b0-122">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="d55b0-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d55b0-123">パスワード</span><span class="sxs-lookup"><span data-stu-id="d55b0-123">Password</span></span> | <span data-ttu-id="d55b0-124">ソースと認証のパスワードを指定します。</span><span class="sxs-lookup"><span data-stu-id="d55b0-124">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="d55b0-125">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="d55b0-125">StorePasswordInClearText</span></span> | <span data-ttu-id="d55b0-126">暗号化された形式を格納する既定の動作ではなく暗号化されていないテキストでパスワードを保存することを示します。</span><span class="sxs-lookup"><span data-stu-id="d55b0-126">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="d55b0-127">UserName</span><span class="sxs-lookup"><span data-stu-id="d55b0-127">UserName</span></span> | <span data-ttu-id="d55b0-128">ソースと認証のユーザー名を指定します。</span><span class="sxs-lookup"><span data-stu-id="d55b0-128">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="d55b0-129">詳細度</span><span class="sxs-lookup"><span data-stu-id="d55b0-129">Verbosity</span></span> | <span data-ttu-id="d55b0-130">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、 *(2.5 以降) の詳細*です。</span><span class="sxs-lookup"><span data-stu-id="d55b0-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

> [!Note]
> <span data-ttu-id="d55b0-131">必ず、nuget.exe は後でパッケージ ソースへのアクセスに使用されるため、同じユーザーのコンテキストで、ソースのパスワードを追加してください。</span><span class="sxs-lookup"><span data-stu-id="d55b0-131">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="d55b0-132">パスワードは、config ファイルで暗号化されて格納され、できますのみ復号化、同じユーザー コンテキストで暗号化されていたとします。</span><span class="sxs-lookup"><span data-stu-id="d55b0-132">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="d55b0-133">したがって、たとえば使用する場合、ビルド サーバー ビルド サーバーのタスクを実行する同じ Windows ユーザーがパスワードを暗号化する必要があります NuGet パッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="d55b0-133">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="d55b0-134">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d55b0-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d55b0-135">例</span><span class="sxs-lookup"><span data-stu-id="d55b0-135">Examples</span></span>

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
