---
title: NuGet CLI 構成コマンド
description: Nuget.exe config コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 51c4c9937483e7f8a57356515c06a60c0f9e6f62
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327849"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="92339-103">configコマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="92339-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="92339-104">**適用対象:** &bullet; **サポートされている**すべてのバージョン: すべて</span><span class="sxs-lookup"><span data-stu-id="92339-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="92339-105">NuGet 構成値を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="92339-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="92339-106">その他の使用方法については、「 [Common NuGet の構成](../../consume-packages/configuring-nuget-behavior.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="92339-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="92339-107">使用可能なキー名の詳細については、 [NuGet 構成ファイルのリファレンス](../nuget-config-file.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="92339-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="92339-108">使用法</span><span class="sxs-lookup"><span data-stu-id="92339-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="92339-109">`<name>` と`<value>`は、構成で設定されるキーと値のペアを指定します。</span><span class="sxs-lookup"><span data-stu-id="92339-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="92339-110">必要に応じて、ペアをいくつでも指定できます。</span><span class="sxs-lookup"><span data-stu-id="92339-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="92339-111">値を削除するには、名前と`=`符号を指定しますが、値は指定しません。</span><span class="sxs-lookup"><span data-stu-id="92339-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="92339-112">使用可能なキー名については、 [NuGet 構成ファイルのリファレンス](../nuget-config-file.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="92339-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="92339-113">NuGet 3.4 以降では`<value>` 、は[環境変数](cli-ref-environment-variables.md)を使用できます。</span><span class="sxs-lookup"><span data-stu-id="92339-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="92339-114">オプション</span><span class="sxs-lookup"><span data-stu-id="92339-114">Options</span></span>

| <span data-ttu-id="92339-115">オプション</span><span class="sxs-lookup"><span data-stu-id="92339-115">Option</span></span> | <span data-ttu-id="92339-116">説明</span><span class="sxs-lookup"><span data-stu-id="92339-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="92339-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="92339-117">AsPath</span></span> | <span data-ttu-id="92339-118">構成値をパスとして返します。 `-Set`が使用されている場合は無視されます。</span><span class="sxs-lookup"><span data-stu-id="92339-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="92339-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="92339-119">ConfigFile</span></span> | <span data-ttu-id="92339-120">変更する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="92339-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="92339-121">指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="92339-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="92339-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="92339-122">ForceEnglishOutput</span></span> | <span data-ttu-id="92339-123">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="92339-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="92339-124">Help</span><span class="sxs-lookup"><span data-stu-id="92339-124">Help</span></span> | <span data-ttu-id="92339-125">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="92339-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="92339-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="92339-126">NonInteractive</span></span> | <span data-ttu-id="92339-127">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="92339-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="92339-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="92339-128">Verbosity</span></span> | <span data-ttu-id="92339-129">出力に表示される詳細データの量を指定します:*通常*、 *静か*、*詳細*</span><span class="sxs-lookup"><span data-stu-id="92339-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="92339-130">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="92339-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="92339-131">使用例</span><span class="sxs-lookup"><span data-stu-id="92339-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
