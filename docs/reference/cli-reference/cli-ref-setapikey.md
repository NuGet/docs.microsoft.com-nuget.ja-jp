---
title: NuGet CLI setapikey コマンド
description: nuget.exe setapikey コマンドのリファレンス
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3e0c2f84e336e0a642b1b5e815e74a1fb0878467
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780024"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="7ebee-103">setapikey コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7ebee-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="7ebee-104">**適用対象:** パッケージの使用、 &bullet; **サポートされるバージョン** の発行: すべて</span><span class="sxs-lookup"><span data-stu-id="7ebee-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="7ebee-105">指定されたサーバー URL の API キーをに保存して、 `NuGet.Config` 後続のコマンドに入力する必要がないようにします。</span><span class="sxs-lookup"><span data-stu-id="7ebee-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="7ebee-106">使用方法</span><span class="sxs-lookup"><span data-stu-id="7ebee-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="7ebee-107">`<source>`はサーバーを識別し、 `<key>` は保存するキーです。</span><span class="sxs-lookup"><span data-stu-id="7ebee-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="7ebee-108">を省略した場合 `<source>` 、nuget.org が想定されます。</span><span class="sxs-lookup"><span data-stu-id="7ebee-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="7ebee-109">API キーは、プライベート フィードでの認証には使用されません。</span><span class="sxs-lookup"><span data-stu-id="7ebee-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="7ebee-110">ソースで認証するための資格情報を管理するには、[`nuget sources` コマンド](../cli-reference/cli-ref-sources.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7ebee-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="7ebee-111">API キーは、個々の NuGet サーバーから取得できます。</span><span class="sxs-lookup"><span data-stu-id="7ebee-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="7ebee-112">Nuget.org の APIKeys を作成して管理するには、 [api キーを取得](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)する</span><span class="sxs-lookup"><span data-stu-id="7ebee-112">To create and manage APIKeys for nuget.org refer to [acquire-an-api-key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)</span></span>

## <a name="options"></a><span data-ttu-id="7ebee-113">Options</span><span class="sxs-lookup"><span data-stu-id="7ebee-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="7ebee-114">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="7ebee-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7ebee-115">指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="7ebee-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="7ebee-116">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="7ebee-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="7ebee-117">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="7ebee-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="7ebee-118">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="7ebee-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="7ebee-119">API キーが有効なサーバー URL。</span><span class="sxs-lookup"><span data-stu-id="7ebee-119">Server URL where the API key is valid.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="7ebee-120">出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。</span><span class="sxs-lookup"><span data-stu-id="7ebee-120">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="7ebee-121">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="7ebee-121">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7ebee-122">使用例</span><span class="sxs-lookup"><span data-stu-id="7ebee-122">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
