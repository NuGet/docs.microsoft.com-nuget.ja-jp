---
title: NuGet CLI push コマンド
description: Nuget.exe push コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 125671ca3f695f82bd74f8097e590c3972003e22
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548344"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="3b633-103">プッシュ コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3b633-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="3b633-104">**適用されます:** パッケージ公開&bullet;**サポートされているバージョン:** すべて; nuget.org に必要な 4.1.0 以降</span><span class="sxs-lookup"><span data-stu-id="3b633-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="3b633-105">Nuget.org にパッケージをプッシュするを使用する必要があります nuget.exe v4.1.0 以降、実装に必要な[NuGet プロトコル](../api/nuget-protocols.md)します。</span><span class="sxs-lookup"><span data-stu-id="3b633-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="3b633-106">パッケージ ソースに、パッケージをプッシュして発行します。</span><span class="sxs-lookup"><span data-stu-id="3b633-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="3b633-107">NuGet の既定の構成が読み込むことによって取得`%AppData%\NuGet\NuGet.Config`(Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) が、読み込み、`Nuget.Config`または`.nuget\Nuget.Config`ドライブのルートから開始し、現在のディレクトリで終わるファイル (を参照してください[構成NuGet の動作を](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="3b633-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="3b633-108">使用法</span><span class="sxs-lookup"><span data-stu-id="3b633-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="3b633-109">場所`<packagePath>`サーバーにプッシュするパッケージを識別します。</span><span class="sxs-lookup"><span data-stu-id="3b633-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="3b633-110">オプション</span><span class="sxs-lookup"><span data-stu-id="3b633-110">Options</span></span>

| <span data-ttu-id="3b633-111">オプション</span><span class="sxs-lookup"><span data-stu-id="3b633-111">Option</span></span> | <span data-ttu-id="3b633-112">説明</span><span class="sxs-lookup"><span data-stu-id="3b633-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3b633-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="3b633-113">ApiKey</span></span> | <span data-ttu-id="3b633-114">ターゲットのリポジトリの API キー。</span><span class="sxs-lookup"><span data-stu-id="3b633-114">The API key for the target repository.</span></span> <span data-ttu-id="3b633-115">存在しない場合は、構成ファイルで指定された 1 つが使用されます。</span><span class="sxs-lookup"><span data-stu-id="3b633-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="3b633-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3b633-116">ConfigFile</span></span> | <span data-ttu-id="3b633-117">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="3b633-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3b633-118">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="3b633-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="3b633-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="3b633-119">DisableBuffering</span></span> | <span data-ttu-id="3b633-120">メモリの使用量を減らす、http (s) サーバーにプッシュするときのバッファリングを無効にします。</span><span class="sxs-lookup"><span data-stu-id="3b633-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="3b633-121">注意: このオプションを使用すると、統合 Windows 認証が機能しません。</span><span class="sxs-lookup"><span data-stu-id="3b633-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="3b633-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3b633-122">ForceEnglishOutput</span></span> | <span data-ttu-id="3b633-123">*(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="3b633-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3b633-124">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="3b633-124">Help</span></span> | <span data-ttu-id="3b633-125">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="3b633-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="3b633-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="3b633-126">NonInteractive</span></span> | <span data-ttu-id="3b633-127">ユーザー入力や確認のプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="3b633-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3b633-128">シンボルなし</span><span class="sxs-lookup"><span data-stu-id="3b633-128">NoSymbols</span></span> | <span data-ttu-id="3b633-129">*(3.5 以降)* シンボル パッケージが存在する場合にプッシュされませんシンボル サーバーにします。</span><span class="sxs-lookup"><span data-stu-id="3b633-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="3b633-130">ソース</span><span class="sxs-lookup"><span data-stu-id="3b633-130">Source</span></span> | <span data-ttu-id="3b633-131">サーバー URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="3b633-131">Specifies the server URL.</span></span> <span data-ttu-id="3b633-132">NuGet では、UNC またはローカル フォルダーのソースを識別し、単純に HTTP を使用してプッシュではなく、ファイルの存在をコピーします。</span><span class="sxs-lookup"><span data-stu-id="3b633-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="3b633-133">また、NuGet 3.4.2 以降、これは、必須パラメーターしない限り、`NuGet.Config`ファイルを指定します、 *DefaultPushSource*値 (を参照してください[NuGet の構成の動作を](../consume-packages/configuring-nuget-behavior.md))。</span><span class="sxs-lookup"><span data-stu-id="3b633-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="3b633-134">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="3b633-134">SymbolSource</span></span> | <span data-ttu-id="3b633-135">*(3.5 以降)* シンボル サーバーの URL を指定します nuget.org にプッシュするときに nuget.smbsrc.net が使用されます。</span><span class="sxs-lookup"><span data-stu-id="3b633-135">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="3b633-136">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="3b633-136">SymbolApiKey</span></span> | <span data-ttu-id="3b633-137">*(3.5 以降)* で指定された URL の API キーを指定します`-SymbolSource`します。</span><span class="sxs-lookup"><span data-stu-id="3b633-137">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="3b633-138">Timeout</span><span class="sxs-lookup"><span data-stu-id="3b633-138">Timeout</span></span> | <span data-ttu-id="3b633-139">サーバーにプッシュするための秒単位のタイムアウトを指定します。</span><span class="sxs-lookup"><span data-stu-id="3b633-139">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="3b633-140">既定では 300 秒 (5 分) です。</span><span class="sxs-lookup"><span data-stu-id="3b633-140">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="3b633-141">詳細度</span><span class="sxs-lookup"><span data-stu-id="3b633-141">Verbosity</span></span> | <span data-ttu-id="3b633-142">出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。</span><span class="sxs-lookup"><span data-stu-id="3b633-142">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="3b633-143">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3b633-143">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3b633-144">使用例</span><span class="sxs-lookup"><span data-stu-id="3b633-144">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
