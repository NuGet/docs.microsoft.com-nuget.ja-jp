---
title: NuGet CLI config コマンド
description: Nuget.exe の config コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 376b69186ad22d4d94a1df51146b833a1f6f9bd9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546479"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="78073-103">構成コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="78073-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="78073-104">**適用対象:** すべて&bullet;**サポートされているバージョン**: すべて</span><span class="sxs-lookup"><span data-stu-id="78073-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="78073-105">取得または NuGet の構成値を設定します。</span><span class="sxs-lookup"><span data-stu-id="78073-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="78073-106">追加の使用状況は、[NuGet の動作を構成する](../consume-packages/configuring-nuget-behavior.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="78073-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="78073-107">詳細については、使用可能なキー名を参照してください、 [NuGet 構成ファイル リファレンス](../reference/nuget-config-file.md)します。</span><span class="sxs-lookup"><span data-stu-id="78073-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="78073-108">使用法</span><span class="sxs-lookup"><span data-stu-id="78073-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="78073-109">場所`<name>`と`<value>`構成で設定するキー/値ペアを指定します。</span><span class="sxs-lookup"><span data-stu-id="78073-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="78073-110">必要に応じて、多くのペアを指定できます。</span><span class="sxs-lookup"><span data-stu-id="78073-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="78073-111">値を削除するには、名前を指定し、`=`記号が、値はありません。</span><span class="sxs-lookup"><span data-stu-id="78073-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="78073-112">使用可能なキー名では、、 [NuGet 構成ファイル リファレンス](../reference/nuget-config-file.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="78073-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="78073-113">NuGet 3.4 以降で`<value>`使える[環境変数](cli-ref-environment-variables.md)します。</span><span class="sxs-lookup"><span data-stu-id="78073-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="78073-114">オプション</span><span class="sxs-lookup"><span data-stu-id="78073-114">Options</span></span>

| <span data-ttu-id="78073-115">オプション</span><span class="sxs-lookup"><span data-stu-id="78073-115">Option</span></span> | <span data-ttu-id="78073-116">説明</span><span class="sxs-lookup"><span data-stu-id="78073-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="78073-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="78073-117">AsPath</span></span> | <span data-ttu-id="78073-118">ときに、パスとして、構成の値を返しますが無視されます`-Set`使用されます。</span><span class="sxs-lookup"><span data-stu-id="78073-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="78073-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="78073-119">ConfigFile</span></span> | <span data-ttu-id="78073-120">NuGet 構成ファイルを変更します。</span><span class="sxs-lookup"><span data-stu-id="78073-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="78073-121">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="78073-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="78073-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="78073-122">ForceEnglishOutput</span></span> | <span data-ttu-id="78073-123">*(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="78073-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="78073-124">Help</span><span class="sxs-lookup"><span data-stu-id="78073-124">Help</span></span> | <span data-ttu-id="78073-125">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="78073-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="78073-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="78073-126">NonInteractive</span></span> | <span data-ttu-id="78073-127">ユーザー入力や確認のプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="78073-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="78073-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="78073-128">Verbosity</span></span> | <span data-ttu-id="78073-129">出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。</span><span class="sxs-lookup"><span data-stu-id="78073-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="78073-130">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="78073-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="78073-131">使用例</span><span class="sxs-lookup"><span data-stu-id="78073-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
