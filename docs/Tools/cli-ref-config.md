---
title: NuGet CLI config コマンド
description: Nuget.exe config コマンドのリファレンス
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 414eb8386f949347772f33170de881534dc71482
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="20e47-103">config コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="20e47-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="20e47-104">**適用されます:** すべて&bullet;**サポートされているバージョン**: すべて</span><span class="sxs-lookup"><span data-stu-id="20e47-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="20e47-105">取得または NuGet の構成値を設定します。</span><span class="sxs-lookup"><span data-stu-id="20e47-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="20e47-106">追加の使用率は、次を参照してください。 [NuGet の動作を構成する](../consume-packages/configuring-nuget-behavior.md)です。</span><span class="sxs-lookup"><span data-stu-id="20e47-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="20e47-107">使用可能なキー名の詳細についてを参照してください、 [NuGet config ファイル参照](../reference/nuget-config-file.md)です。</span><span class="sxs-lookup"><span data-stu-id="20e47-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="20e47-108">使用法</span><span class="sxs-lookup"><span data-stu-id="20e47-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="20e47-109">ここで`<name>`と`<value>`構成で設定するキー/値ペアを指定します。</span><span class="sxs-lookup"><span data-stu-id="20e47-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="20e47-110">必要に応じて多くのペアを指定できます。</span><span class="sxs-lookup"><span data-stu-id="20e47-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="20e47-111">値を削除するには、名前を指定し、`=`記号が、値はありません。</span><span class="sxs-lookup"><span data-stu-id="20e47-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="20e47-112">使用可能なキー名では、次を参照してください。、 [NuGet config ファイル参照](../reference/nuget-config-file.md)です。</span><span class="sxs-lookup"><span data-stu-id="20e47-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="20e47-113">NuGet 3.4 以降で`<value>`使える[環境変数](cli-ref-environment-variables.md)です。</span><span class="sxs-lookup"><span data-stu-id="20e47-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="20e47-114">オプション</span><span class="sxs-lookup"><span data-stu-id="20e47-114">Options</span></span>

| <span data-ttu-id="20e47-115">オプション</span><span class="sxs-lookup"><span data-stu-id="20e47-115">Option</span></span> | <span data-ttu-id="20e47-116">説明</span><span class="sxs-lookup"><span data-stu-id="20e47-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="20e47-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="20e47-117">AsPath</span></span> | <span data-ttu-id="20e47-118">構成は、パスとして値を返しますするときに無視`-Set`を使用します。</span><span class="sxs-lookup"><span data-stu-id="20e47-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="20e47-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="20e47-119">ConfigFile</span></span> | <span data-ttu-id="20e47-120">NuGet 構成ファイルを変更します。</span><span class="sxs-lookup"><span data-stu-id="20e47-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="20e47-121">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="20e47-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="20e47-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="20e47-122">ForceEnglishOutput</span></span> | <span data-ttu-id="20e47-123">*(3.5 +)* インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="20e47-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="20e47-124">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="20e47-124">Help</span></span> | <span data-ttu-id="20e47-125">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="20e47-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="20e47-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="20e47-126">NonInteractive</span></span> | <span data-ttu-id="20e47-127">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="20e47-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="20e47-128">詳細度</span><span class="sxs-lookup"><span data-stu-id="20e47-128">Verbosity</span></span> | <span data-ttu-id="20e47-129">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="20e47-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="20e47-130">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="20e47-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="20e47-131">使用例</span><span class="sxs-lookup"><span data-stu-id="20e47-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
