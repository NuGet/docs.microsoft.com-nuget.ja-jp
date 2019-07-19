---
title: NuGet CLI プッシュコマンド
description: Nuget.exe push コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 40b2b2970934bae82c46cbe69156948e90746f97
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327629"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="15a02-103">push コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="15a02-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="15a02-104">**適用対象:** パッケージ発行&bullet;が**サポートされているバージョン:** すべて。 nuget.org には、4.1.0 以降が必要です。</span><span class="sxs-lookup"><span data-stu-id="15a02-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="15a02-105">パッケージを nuget.org にプッシュするには、必要な[nuget プロトコル](../../api/nuget-protocols.md)を実装する nuget.exe v2.0 を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="15a02-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="15a02-106">パッケージをパッケージソースにプッシュして発行します。</span><span class="sxs-lookup"><span data-stu-id="15a02-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="15a02-107">NuGet の既定の構成を取得する`%AppData%\NuGet\NuGet.Config`には`.nuget\Nuget.Config` 、( `~/.nuget/NuGet/NuGet.Config` Windows) または (Mac/Linux `Nuget.Config` ) を読み込み、ドライブのルートから開始し、現在のディレクトリで終了します ([一般的な nuget を参照してください)。構成](../../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="15a02-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="15a02-108">使用法</span><span class="sxs-lookup"><span data-stu-id="15a02-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="15a02-109">は、サーバーにプッシュするパッケージを識別します。`<packagePath>`</span><span class="sxs-lookup"><span data-stu-id="15a02-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="15a02-110">オプション</span><span class="sxs-lookup"><span data-stu-id="15a02-110">Options</span></span>

| <span data-ttu-id="15a02-111">オプション</span><span class="sxs-lookup"><span data-stu-id="15a02-111">Option</span></span> | <span data-ttu-id="15a02-112">説明</span><span class="sxs-lookup"><span data-stu-id="15a02-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="15a02-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="15a02-113">ApiKey</span></span> | <span data-ttu-id="15a02-114">ターゲットリポジトリの API キー。</span><span class="sxs-lookup"><span data-stu-id="15a02-114">The API key for the target repository.</span></span> <span data-ttu-id="15a02-115">存在しない場合は、構成ファイルで指定されたものが使用されます。</span><span class="sxs-lookup"><span data-stu-id="15a02-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="15a02-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="15a02-116">ConfigFile</span></span> | <span data-ttu-id="15a02-117">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="15a02-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="15a02-118">指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="15a02-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="15a02-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="15a02-119">DisableBuffering</span></span> | <span data-ttu-id="15a02-120">メモリ使用量を減らすために HTTP (s) サーバーにプッシュするときのバッファー処理を無効にします。</span><span class="sxs-lookup"><span data-stu-id="15a02-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="15a02-121">注意: このオプションを使用すると、統合 Windows 認証が機能しない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="15a02-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="15a02-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="15a02-122">ForceEnglishOutput</span></span> | <span data-ttu-id="15a02-123">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="15a02-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="15a02-124">Help</span><span class="sxs-lookup"><span data-stu-id="15a02-124">Help</span></span> | <span data-ttu-id="15a02-125">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="15a02-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="15a02-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="15a02-126">NonInteractive</span></span> | <span data-ttu-id="15a02-127">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="15a02-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="15a02-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="15a02-128">NoSymbols</span></span> | <span data-ttu-id="15a02-129">*(3.5 +)* シンボルパッケージが存在する場合は、シンボルサーバーにプッシュされません。</span><span class="sxs-lookup"><span data-stu-id="15a02-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="15a02-130">Source</span><span class="sxs-lookup"><span data-stu-id="15a02-130">Source</span></span> | <span data-ttu-id="15a02-131">サーバー URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="15a02-131">Specifies the server URL.</span></span> <span data-ttu-id="15a02-132">NuGet は UNC またはローカルフォルダーソースを識別し、HTTP を使用してプッシュするのではなく、そこにファイルをコピーするだけです。</span><span class="sxs-lookup"><span data-stu-id="15a02-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="15a02-133">また、nuget 3.4.2 以降では、ファイルで`NuGet.Config` *defaultpushsource*値が指定されていない限り、これは必須パラメーターです (「 [NuGet の動作の構成](../../consume-packages/configuring-nuget-behavior.md)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="15a02-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="15a02-134">SkipDuplicate</span><span class="sxs-lookup"><span data-stu-id="15a02-134">SkipDuplicate</span></span> | <span data-ttu-id="15a02-135">*(5.1 以降)* パッケージとバージョンが既に存在する場合は、スキップして、プッシュ時に次のパッケージを続行します (存在する場合)。</span><span class="sxs-lookup"><span data-stu-id="15a02-135">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span> |
| <span data-ttu-id="15a02-136">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="15a02-136">SymbolSource</span></span> | <span data-ttu-id="15a02-137">*(3.5 +)* シンボルサーバーの URL を指定します。nuget.smbsrc.net は、nuget.org にプッシュするときに使用されます。</span><span class="sxs-lookup"><span data-stu-id="15a02-137">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="15a02-138">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="15a02-138">SymbolApiKey</span></span> | <span data-ttu-id="15a02-139">*(3.5 +)* で`-SymbolSource`指定された URL の API キーを指定します。</span><span class="sxs-lookup"><span data-stu-id="15a02-139">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="15a02-140">Timeout</span><span class="sxs-lookup"><span data-stu-id="15a02-140">Timeout</span></span> | <span data-ttu-id="15a02-141">サーバーにプッシュするときのタイムアウトを秒単位で指定します。</span><span class="sxs-lookup"><span data-stu-id="15a02-141">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="15a02-142">既定値は300秒 (5 分) です。</span><span class="sxs-lookup"><span data-stu-id="15a02-142">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="15a02-143">Verbosity</span><span class="sxs-lookup"><span data-stu-id="15a02-143">Verbosity</span></span> | <span data-ttu-id="15a02-144">出力に表示される詳細データの量を指定します:*通常*、 *静か*、*詳細*</span><span class="sxs-lookup"><span data-stu-id="15a02-144">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="15a02-145">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="15a02-145">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="15a02-146">使用例</span><span class="sxs-lookup"><span data-stu-id="15a02-146">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
