---
title: NuGet CLI setapikey コマンド
description: Nuget.exe setapikey コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231228"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="929a6-103">setapikey コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="929a6-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="929a6-104">**適用対象:** パッケージの使用、発行 &bullet;**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="929a6-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="929a6-105">指定されたサーバー URL の API キーを `NuGet.Config` に保存して、後続のコマンドに入力する必要がないようにします。</span><span class="sxs-lookup"><span data-stu-id="929a6-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="929a6-106">使用法</span><span class="sxs-lookup"><span data-stu-id="929a6-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="929a6-107">`<source>` はサーバーを識別し、`<key>` は保存するキーです。</span><span class="sxs-lookup"><span data-stu-id="929a6-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="929a6-108">`<source>` を省略した場合、nuget.org が想定されます。</span><span class="sxs-lookup"><span data-stu-id="929a6-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="929a6-109">API キーは、プライベートフィードでの認証には使用されません。</span><span class="sxs-lookup"><span data-stu-id="929a6-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="929a6-110">ソースで認証するための資格情報を管理するには、 [`nuget sources` のコマンド](../cli-reference/cli-ref-sources.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="929a6-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="929a6-111">API キーは、個々の NuGet サーバーから取得できます。</span><span class="sxs-lookup"><span data-stu-id="929a6-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="929a6-112">Nuget.org の APIKeys を作成および管理するには、「[発行 api キー](../../quickstart/includes/publish-api-key.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="929a6-112">To create and manage APIKeys for nuget.org refer to [publish-api-key](../../quickstart/includes/publish-api-key.md)</span></span>

## <a name="options"></a><span data-ttu-id="929a6-113">オプション</span><span class="sxs-lookup"><span data-stu-id="929a6-113">Options</span></span>

| <span data-ttu-id="929a6-114">オプション</span><span class="sxs-lookup"><span data-stu-id="929a6-114">Option</span></span> | <span data-ttu-id="929a6-115">説明</span><span class="sxs-lookup"><span data-stu-id="929a6-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="929a6-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="929a6-116">ConfigFile</span></span> | <span data-ttu-id="929a6-117">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="929a6-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="929a6-118">指定しない場合は、`%AppData%\NuGet\NuGet.Config` (Windows) または `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="929a6-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="929a6-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="929a6-119">ForceEnglishOutput</span></span> | <span data-ttu-id="929a6-120">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="929a6-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="929a6-121">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="929a6-121">Help</span></span> | <span data-ttu-id="929a6-122">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="929a6-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="929a6-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="929a6-123">NonInteractive</span></span> | <span data-ttu-id="929a6-124">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="929a6-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="929a6-125">詳細度</span><span class="sxs-lookup"><span data-stu-id="929a6-125">Verbosity</span></span> | <span data-ttu-id="929a6-126">出力に表示される詳細の量を指定します (*通常*、*非*表示、*詳細*)。</span><span class="sxs-lookup"><span data-stu-id="929a6-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="929a6-127">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="929a6-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="929a6-128">例</span><span class="sxs-lookup"><span data-stu-id="929a6-128">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
