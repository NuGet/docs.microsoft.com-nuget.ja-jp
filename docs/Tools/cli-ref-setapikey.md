---
title: "NuGet CLI setapikey コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a64c0462-973d-4100-ba3f-8902a2b127f7
description: "Nuget.exe setapikey コマンドのリファレンス"
keywords: "nuget setapikey 参照、setapikey コマンド"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a07c35b8bdd57157391e391e04a90204342b1d5c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
## <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="2159b-104">setapikey コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2159b-104">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="2159b-105">**適用されます:**パッケージ消費、パブリッシング&bullet;**サポートされているバージョン:**すべて</span><span class="sxs-lookup"><span data-stu-id="2159b-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="2159b-106">特定のサーバー URL の API キーを保存`NuGet.Config`を後続のコマンドを入力する必要があるようにします。</span><span class="sxs-lookup"><span data-stu-id="2159b-106">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="2159b-107">使用方法</span><span class="sxs-lookup"><span data-stu-id="2159b-107">Usage</span></span>

```
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="2159b-108">ここで`<source>`サーバーを識別しますおよび`<key>`キーまたはパスワードを保存します。</span><span class="sxs-lookup"><span data-stu-id="2159b-108">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="2159b-109">場合`<source>`は省略すると、nuget.org と見なされます。</span><span class="sxs-lookup"><span data-stu-id="2159b-109">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="2159b-110">オプション</span><span class="sxs-lookup"><span data-stu-id="2159b-110">Options</span></span>

| <span data-ttu-id="2159b-111">オプション</span><span class="sxs-lookup"><span data-stu-id="2159b-111">Option</span></span> | <span data-ttu-id="2159b-112">説明</span><span class="sxs-lookup"><span data-stu-id="2159b-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2159b-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2159b-113">ConfigFile</span></span> | <span data-ttu-id="2159b-114">*(2.5 +)* NuGet 構成ファイルを変更します。</span><span class="sxs-lookup"><span data-stu-id="2159b-114">*(2.5+)* The NuGet configuration file to modify.</span></span> <span data-ttu-id="2159b-115">指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。</span><span class="sxs-lookup"><span data-stu-id="2159b-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="2159b-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2159b-116">ForceEnglishOutput</span></span> | <span data-ttu-id="2159b-117">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="2159b-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2159b-118">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="2159b-118">Help</span></span> | <span data-ttu-id="2159b-119">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="2159b-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="2159b-120">非対話型</span><span class="sxs-lookup"><span data-stu-id="2159b-120">NonInteractive</span></span> | <span data-ttu-id="2159b-121">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="2159b-121">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2159b-122">詳細度</span><span class="sxs-lookup"><span data-stu-id="2159b-122">Verbosity</span></span> | <span data-ttu-id="2159b-123">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、 *(2.5 以降) の詳細*です。</span><span class="sxs-lookup"><span data-stu-id="2159b-123">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="2159b-124">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2159b-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2159b-125">例</span><span class="sxs-lookup"><span data-stu-id="2159b-125">Examples</span></span>

```
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
