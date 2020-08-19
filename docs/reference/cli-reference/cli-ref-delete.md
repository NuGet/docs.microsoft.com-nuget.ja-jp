---
title: NuGet CLI の削除コマンド
description: nuget.exe delete コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: bec1a778d4986a4cb7ee87e1ef8a98550c96ed57
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622864"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="d9439-103">delete コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d9439-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="d9439-104">**適用対象:** パッケージ発行の &bullet; **サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="d9439-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d9439-105">パッケージソースからパッケージを削除または一覧から削除します。</span><span class="sxs-lookup"><span data-stu-id="d9439-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="d9439-106">Nuget.org の場合、delete コマンドを実行すると、 [パッケージの一覧](../../nuget-org/policies/deleting-packages.md)が解除されます。</span><span class="sxs-lookup"><span data-stu-id="d9439-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="d9439-107">使用法</span><span class="sxs-lookup"><span data-stu-id="d9439-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="d9439-108">`<packageID>`と `<packageVersion>` は、削除するパッケージまたは一覧から削除を指定します。</span><span class="sxs-lookup"><span data-stu-id="d9439-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="d9439-109">実際の動作は、ソースによって異なります。</span><span class="sxs-lookup"><span data-stu-id="d9439-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="d9439-110">たとえば、ローカルフォルダーの場合、パッケージは削除されます。nuget.org の場合、パッケージは一覧から削除されます。</span><span class="sxs-lookup"><span data-stu-id="d9439-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="d9439-111">Options</span><span class="sxs-lookup"><span data-stu-id="d9439-111">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="d9439-112">ターゲットリポジトリの API キー。</span><span class="sxs-lookup"><span data-stu-id="d9439-112">The API key for the target repository.</span></span> <span data-ttu-id="d9439-113">存在しない場合は、構成ファイルで指定されたものが使用されます。</span><span class="sxs-lookup"><span data-stu-id="d9439-113">If not present, the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="d9439-114">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="d9439-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d9439-115">指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="d9439-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="d9439-116">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="d9439-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="d9439-117">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="d9439-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="d9439-118">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="d9439-118">Suppresses prompts for user input or confirmations.</span></span>

 - **`-np|-NoPrompt`**

   <span data-ttu-id="d9439-119">削除時にメッセージを表示しません。</span><span class="sxs-lookup"><span data-stu-id="d9439-119">Do not prompt when deleting.</span></span>

 - <span data-ttu-id="d9439-120">**`-NoServiceEndpoint`** ソース URL に "api/v2/packages" を追加しません。</span><span class="sxs-lookup"><span data-stu-id="d9439-120">**`-NoServiceEndpoint`** Does not append "api/v2/packages" to the source URL.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="d9439-121">サーバー URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="d9439-121">Specifies the server URL.</span></span> <span data-ttu-id="d9439-122">Nuget.org の URL は `https://api.nuget.org/v3/index.json` です。</span><span class="sxs-lookup"><span data-stu-id="d9439-122">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="d9439-123">プライベートフィードの場合は、ホスト名に置き換えます (例 *% hostname%/api/v3*)。</span><span class="sxs-lookup"><span data-stu-id="d9439-123">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="d9439-124">出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。</span><span class="sxs-lookup"><span data-stu-id="d9439-124">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="d9439-125">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="d9439-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d9439-126">使用例</span><span class="sxs-lookup"><span data-stu-id="d9439-126">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
