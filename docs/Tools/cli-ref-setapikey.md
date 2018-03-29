---
title: NuGet CLI setapikey コマンド |Microsoft ドキュメント
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe setapikey コマンドのリファレンス
keywords: nuget setapikey 参照、setapikey コマンド
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 696ccf9df5af487d3bf75925c1c1e0d1d1bf7f7b
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="f6bdd-104">setapikey コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f6bdd-104">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="f6bdd-105">**適用されます:**パッケージ消費、パブリッシング&bullet;**サポートされているバージョン:**すべて</span><span class="sxs-lookup"><span data-stu-id="f6bdd-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="f6bdd-106">特定のサーバー URL の API キーを保存`NuGet.Config`を後続のコマンドを入力する必要があるようにします。</span><span class="sxs-lookup"><span data-stu-id="f6bdd-106">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="f6bdd-107">使用法</span><span class="sxs-lookup"><span data-stu-id="f6bdd-107">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="f6bdd-108">ここで`<source>`サーバーを識別しますおよび`<key>`キーまたはパスワードを保存します。</span><span class="sxs-lookup"><span data-stu-id="f6bdd-108">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="f6bdd-109">場合`<source>`は省略すると、nuget.org と見なされます。</span><span class="sxs-lookup"><span data-stu-id="f6bdd-109">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="f6bdd-110">オプション</span><span class="sxs-lookup"><span data-stu-id="f6bdd-110">Options</span></span>

| <span data-ttu-id="f6bdd-111">オプション</span><span class="sxs-lookup"><span data-stu-id="f6bdd-111">Option</span></span> | <span data-ttu-id="f6bdd-112">説明</span><span class="sxs-lookup"><span data-stu-id="f6bdd-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f6bdd-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f6bdd-113">ConfigFile</span></span> | <span data-ttu-id="f6bdd-114">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="f6bdd-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f6bdd-115">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="f6bdd-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f6bdd-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f6bdd-116">ForceEnglishOutput</span></span> | <span data-ttu-id="f6bdd-117">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="f6bdd-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f6bdd-118">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="f6bdd-118">Help</span></span> | <span data-ttu-id="f6bdd-119">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="f6bdd-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="f6bdd-120">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f6bdd-120">NonInteractive</span></span> | <span data-ttu-id="f6bdd-121">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="f6bdd-121">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f6bdd-122">詳細度</span><span class="sxs-lookup"><span data-stu-id="f6bdd-122">Verbosity</span></span> | <span data-ttu-id="f6bdd-123">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="f6bdd-123">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f6bdd-124">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f6bdd-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f6bdd-125">使用例</span><span class="sxs-lookup"><span data-stu-id="f6bdd-125">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
