---
title: NuGet CLI setapikey コマンド
description: Nuget.exe setapikey コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e2119953e6d07cd3571f156fa0b2665de49f963
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383970"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="2ded4-103">setapikey コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2ded4-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="2ded4-104">**適用対象:** パッケージの使用、発行 &bullet;**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="2ded4-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="2ded4-105">指定されたサーバー URL の API キーを `NuGet.Config` に保存して、後続のコマンドに入力する必要がないようにします。</span><span class="sxs-lookup"><span data-stu-id="2ded4-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="2ded4-106">使用状況</span><span class="sxs-lookup"><span data-stu-id="2ded4-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="2ded4-107">`<source>` はサーバーを識別し、`<key>` は保存するキーまたはパスワードです。</span><span class="sxs-lookup"><span data-stu-id="2ded4-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="2ded4-108">`<source>` を省略した場合、nuget.org が想定されます。</span><span class="sxs-lookup"><span data-stu-id="2ded4-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

> [!NOTE]
> <span data-ttu-id="2ded4-109">API キーは、プライベートフィードでの認証には使用されません。</span><span class="sxs-lookup"><span data-stu-id="2ded4-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="2ded4-110">ソースで認証するための資格情報を管理するには、 [`nuget sources` のコマンド](../cli-reference/cli-ref-sources.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2ded4-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>

## <a name="options"></a><span data-ttu-id="2ded4-111">[オプション]</span><span class="sxs-lookup"><span data-stu-id="2ded4-111">Options</span></span>

| <span data-ttu-id="2ded4-112">オプション</span><span class="sxs-lookup"><span data-stu-id="2ded4-112">Option</span></span> | <span data-ttu-id="2ded4-113">説明</span><span class="sxs-lookup"><span data-stu-id="2ded4-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2ded4-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2ded4-114">ConfigFile</span></span> | <span data-ttu-id="2ded4-115">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="2ded4-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2ded4-116">指定しない場合は、`%AppData%\NuGet\NuGet.Config` (Windows) または `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="2ded4-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2ded4-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2ded4-117">ForceEnglishOutput</span></span> | <span data-ttu-id="2ded4-118">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="2ded4-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2ded4-119">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="2ded4-119">Help</span></span> | <span data-ttu-id="2ded4-120">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="2ded4-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="2ded4-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="2ded4-121">NonInteractive</span></span> | <span data-ttu-id="2ded4-122">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="2ded4-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2ded4-123">詳細度</span><span class="sxs-lookup"><span data-stu-id="2ded4-123">Verbosity</span></span> | <span data-ttu-id="2ded4-124">出力に表示される詳細データの量を指定します:*normal*、*quiet*、*detailed*</span><span class="sxs-lookup"><span data-stu-id="2ded4-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="2ded4-125">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="2ded4-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2ded4-126">使用例</span><span class="sxs-lookup"><span data-stu-id="2ded4-126">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
