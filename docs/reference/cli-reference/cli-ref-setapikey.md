---
title: NuGet CLI setapikey コマンド
description: Nuget.exe setapikey コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327609"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="3402c-103">setapikey コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3402c-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="3402c-104">**適用対象:** パッケージの使用、 &bullet; **サポートされるバージョン**の発行: すべて</span><span class="sxs-lookup"><span data-stu-id="3402c-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="3402c-105">指定されたサーバー URL の API キーを`NuGet.Config`に保存して、後続のコマンドに入力する必要がないようにします。</span><span class="sxs-lookup"><span data-stu-id="3402c-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="3402c-106">使用法</span><span class="sxs-lookup"><span data-stu-id="3402c-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="3402c-107">はサーバーを`<key>`識別し、は保存するキーまたはパスワードです。 `<source>`</span><span class="sxs-lookup"><span data-stu-id="3402c-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="3402c-108">を`<source>`省略した場合、nuget.org が想定されます。</span><span class="sxs-lookup"><span data-stu-id="3402c-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="3402c-109">オプション</span><span class="sxs-lookup"><span data-stu-id="3402c-109">Options</span></span>

| <span data-ttu-id="3402c-110">オプション</span><span class="sxs-lookup"><span data-stu-id="3402c-110">Option</span></span> | <span data-ttu-id="3402c-111">説明</span><span class="sxs-lookup"><span data-stu-id="3402c-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3402c-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3402c-112">ConfigFile</span></span> | <span data-ttu-id="3402c-113">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="3402c-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3402c-114">指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="3402c-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="3402c-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3402c-115">ForceEnglishOutput</span></span> | <span data-ttu-id="3402c-116">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="3402c-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3402c-117">Help</span><span class="sxs-lookup"><span data-stu-id="3402c-117">Help</span></span> | <span data-ttu-id="3402c-118">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="3402c-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="3402c-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="3402c-119">NonInteractive</span></span> | <span data-ttu-id="3402c-120">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="3402c-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3402c-121">Verbosity</span><span class="sxs-lookup"><span data-stu-id="3402c-121">Verbosity</span></span> | <span data-ttu-id="3402c-122">出力に表示される詳細データの量を指定します: *normal*、*quiet*、*detailed*</span><span class="sxs-lookup"><span data-stu-id="3402c-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="3402c-123">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="3402c-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3402c-124">使用例</span><span class="sxs-lookup"><span data-stu-id="3402c-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
