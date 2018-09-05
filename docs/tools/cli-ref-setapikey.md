---
title: NuGet CLI setapikey コマンド
description: Nuget.exe setapikey コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549221"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="34879-103">setapikey コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="34879-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="34879-104">**適用対象:** パッケージの使用、公開&bullet;**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="34879-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="34879-105">特定のサーバー URL の API キーを保存します。`NuGet.Config`後続のコマンドを入力する必要がないようにします。</span><span class="sxs-lookup"><span data-stu-id="34879-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="34879-106">使用法</span><span class="sxs-lookup"><span data-stu-id="34879-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="34879-107">場所`<source>`サーバーを識別および`<key>`はキーまたはパスワードを保存します。</span><span class="sxs-lookup"><span data-stu-id="34879-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="34879-108">場合`<source>`は省略すると、nuget.org と見なされます。</span><span class="sxs-lookup"><span data-stu-id="34879-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="34879-109">オプション</span><span class="sxs-lookup"><span data-stu-id="34879-109">Options</span></span>

| <span data-ttu-id="34879-110">オプション</span><span class="sxs-lookup"><span data-stu-id="34879-110">Option</span></span> | <span data-ttu-id="34879-111">説明</span><span class="sxs-lookup"><span data-stu-id="34879-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="34879-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="34879-112">ConfigFile</span></span> | <span data-ttu-id="34879-113">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="34879-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="34879-114">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="34879-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="34879-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="34879-115">ForceEnglishOutput</span></span> | <span data-ttu-id="34879-116">*(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="34879-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="34879-117">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="34879-117">Help</span></span> | <span data-ttu-id="34879-118">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="34879-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="34879-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="34879-119">NonInteractive</span></span> | <span data-ttu-id="34879-120">ユーザー入力や確認のプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="34879-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="34879-121">詳細度</span><span class="sxs-lookup"><span data-stu-id="34879-121">Verbosity</span></span> | <span data-ttu-id="34879-122">出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。</span><span class="sxs-lookup"><span data-stu-id="34879-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="34879-123">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="34879-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="34879-124">使用例</span><span class="sxs-lookup"><span data-stu-id="34879-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
