---
title: NuGet CLI の init コマンド
description: nuget.exe init コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3b830d678a473c917b70bd46900bdb0206d3652e
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623085"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="27af6-103">init コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="27af6-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="27af6-104">**適用対象:** パッケージ作成で &bullet; **サポートされているバージョン:** 3.3 以降</span><span class="sxs-lookup"><span data-stu-id="27af6-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="27af6-105">[ [追加] コマンド](cli-ref-add.md)の説明に従って階層構造を使用して、フラットフォルダーのすべてのパッケージをコピー先フォルダーにコピーします。</span><span class="sxs-lookup"><span data-stu-id="27af6-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="27af6-106">つまり、を使用 `init` することは、 `add` フォルダー内の各パッケージに対してコマンドを使用することと同じです。</span><span class="sxs-lookup"><span data-stu-id="27af6-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="27af6-107">と同様に、 `add` コピー先はローカルフォルダーまたは UNC パスである必要があります。Nuget.org やプライベートサーバーなどの HTTP パッケージリポジトリはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="27af6-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="27af6-108">使用法</span><span class="sxs-lookup"><span data-stu-id="27af6-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="27af6-109">ここで、 `<source>` はパッケージを含むフォルダーで、 `<destination>` はパッケージのコピー先のローカルフォルダーまたは UNC パス名です。</span><span class="sxs-lookup"><span data-stu-id="27af6-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="27af6-110">Options</span><span class="sxs-lookup"><span data-stu-id="27af6-110">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="27af6-111">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="27af6-111">The NuGet configuration file to apply.</span></span> <span data-ttu-id="27af6-112">指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="27af6-112">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="27af6-113">パッケージソースに追加された各パッケージ内のすべてのファイルを追加します。コマンドと同じ `-Expand` `add` です。</span><span class="sxs-lookup"><span data-stu-id="27af6-113">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="27af6-114">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="27af6-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="27af6-115">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="27af6-115">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="27af6-116">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="27af6-116">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="27af6-117">出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。</span><span class="sxs-lookup"><span data-stu-id="27af6-117">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="27af6-118">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="27af6-118">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="27af6-119">使用例</span><span class="sxs-lookup"><span data-stu-id="27af6-119">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
