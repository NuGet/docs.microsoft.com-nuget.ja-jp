---
title: NuGet CLI setapikey コマンド
description: Nuget.exe setapikey コマンドのリファレンス
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 66fc62074b4e7c39ff2ed6b515eee9f821530536
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817685"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="fd869-103">setapikey コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="fd869-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="fd869-104">**適用されます:** パッケージ消費、パブリッシング&bullet;**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="fd869-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="fd869-105">特定のサーバー URL の API キーを保存`NuGet.Config`を後続のコマンドを入力する必要があるようにします。</span><span class="sxs-lookup"><span data-stu-id="fd869-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="fd869-106">使用法</span><span class="sxs-lookup"><span data-stu-id="fd869-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="fd869-107">ここで`<source>`サーバーを識別しますおよび`<key>`キーまたはパスワードを保存します。</span><span class="sxs-lookup"><span data-stu-id="fd869-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="fd869-108">場合`<source>`は省略すると、nuget.org と見なされます。</span><span class="sxs-lookup"><span data-stu-id="fd869-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="fd869-109">オプション</span><span class="sxs-lookup"><span data-stu-id="fd869-109">Options</span></span>

| <span data-ttu-id="fd869-110">オプション</span><span class="sxs-lookup"><span data-stu-id="fd869-110">Option</span></span> | <span data-ttu-id="fd869-111">説明</span><span class="sxs-lookup"><span data-stu-id="fd869-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fd869-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="fd869-112">ConfigFile</span></span> | <span data-ttu-id="fd869-113">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="fd869-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fd869-114">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="fd869-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="fd869-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="fd869-115">ForceEnglishOutput</span></span> | <span data-ttu-id="fd869-116">*(3.5 +)* インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="fd869-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="fd869-117">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="fd869-117">Help</span></span> | <span data-ttu-id="fd869-118">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="fd869-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="fd869-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="fd869-119">NonInteractive</span></span> | <span data-ttu-id="fd869-120">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="fd869-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="fd869-121">詳細度</span><span class="sxs-lookup"><span data-stu-id="fd869-121">Verbosity</span></span> | <span data-ttu-id="fd869-122">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="fd869-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="fd869-123">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fd869-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fd869-124">使用例</span><span class="sxs-lookup"><span data-stu-id="fd869-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
