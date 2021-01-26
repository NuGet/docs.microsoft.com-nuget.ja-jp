---
title: NuGet CLI ローカルコマンド
description: nuget.exe のローカルコマンドのリファレンス
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 25feb29c7b96c47681cedd8208b8595952d3ca49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779202"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="d33fa-103">[ローカル] コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d33fa-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="d33fa-104">**適用対象:** パッケージの使用量が &bullet; **サポートされているバージョン:** 3.3 以降</span><span class="sxs-lookup"><span data-stu-id="d33fa-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="d33fa-105">*Http キャッシュ*、*グローバルパッケージ* フォルダー、一時フォルダーなどのローカル NuGet リソースをクリアまたは一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="d33fa-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="d33fa-106">また、コマンドを使用して、 `locals` これらの場所の一覧を表示することもできます。</span><span class="sxs-lookup"><span data-stu-id="d33fa-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="d33fa-107">詳細については、「 [グローバルパッケージとキャッシュフォルダーの管理](../../consume-packages/managing-the-global-packages-and-cache-folders.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d33fa-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="d33fa-108">使用方法</span><span class="sxs-lookup"><span data-stu-id="d33fa-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="d33fa-109">ここで、 `<folder>` は `all` 、 `http-cache` 、 `packages-cache` *(3.5 以前)*、 `global-packages` 、 `temp` *(3.4 +)*、および `plugins-cache` *(4.8 +)* のいずれかです。</span><span class="sxs-lookup"><span data-stu-id="d33fa-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="d33fa-110">Options</span><span class="sxs-lookup"><span data-stu-id="d33fa-110">Options</span></span>

- **`-Clear`**

  <span data-ttu-id="d33fa-111">指定されたフォルダーをクリアします。</span><span class="sxs-lookup"><span data-stu-id="d33fa-111">Clears the specified folder.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="d33fa-112">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="d33fa-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d33fa-113">指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="d33fa-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="d33fa-114">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="d33fa-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="d33fa-115">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="d33fa-115">Displays help information for the command.</span></span>

- **`-List`**

  <span data-ttu-id="d33fa-116">指定したフォルダーの場所、または *すべて* のフォルダーを使用する場合はすべてのフォルダーの場所を一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="d33fa-116">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="d33fa-117">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="d33fa-117">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="d33fa-118">出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。</span><span class="sxs-lookup"><span data-stu-id="d33fa-118">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="d33fa-119">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="d33fa-119">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d33fa-120">例</span><span class="sxs-lookup"><span data-stu-id="d33fa-120">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="d33fa-121">その他の例については、「 [グローバルパッケージとキャッシュフォルダーの管理](../../consume-packages/managing-the-global-packages-and-cache-folders.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d33fa-121">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
