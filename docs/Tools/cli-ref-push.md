---
title: NuGet CLI プッシュ コマンド
description: Nuget.exe プッシュ コマンドのリファレンス
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 959b539fc20bc47f38946cb660375a6652582a0d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="b2e87-103">push コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b2e87-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="b2e87-104">**適用されます:** パッケージの発行&bullet;**サポートされているバージョン:** すべて; nuget.org に必要な 4.1.0+</span><span class="sxs-lookup"><span data-stu-id="b2e87-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="b2e87-105">Nuget.org をパッケージにプッシュするを使用する必要があります nuget.exe v4.1.0 以降、必須を実装する[NuGet プロトコル](../api/nuget-protocols.md)です。</span><span class="sxs-lookup"><span data-stu-id="b2e87-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="b2e87-106">パッケージをパッケージ ソースにプッシュし、それを公開します。</span><span class="sxs-lookup"><span data-stu-id="b2e87-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="b2e87-107">NuGet の既定の構成を読み込むことにより取得`%AppData%\NuGet\NuGet.Config`(Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) が、読み込み、`Nuget.Config`または`.nuget\Nuget.Config`ドライブのルートから開始し、現在のディレクトリで終わるファイル (を参照してください[構成NuGet 動作](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="b2e87-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="b2e87-108">使用法</span><span class="sxs-lookup"><span data-stu-id="b2e87-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="b2e87-109">ここで`<packagePath>`サーバーにプッシュするパッケージを識別します。</span><span class="sxs-lookup"><span data-stu-id="b2e87-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="b2e87-110">オプション</span><span class="sxs-lookup"><span data-stu-id="b2e87-110">Options</span></span>

| <span data-ttu-id="b2e87-111">オプション</span><span class="sxs-lookup"><span data-stu-id="b2e87-111">Option</span></span> | <span data-ttu-id="b2e87-112">説明</span><span class="sxs-lookup"><span data-stu-id="b2e87-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b2e87-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="b2e87-113">ApiKey</span></span> | <span data-ttu-id="b2e87-114">ターゲットのリポジトリの API キー。</span><span class="sxs-lookup"><span data-stu-id="b2e87-114">The API key for the target repository.</span></span> <span data-ttu-id="b2e87-115">存在しない場合は、構成ファイルで指定されているが使用されます。</span><span class="sxs-lookup"><span data-stu-id="b2e87-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="b2e87-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b2e87-116">ConfigFile</span></span> | <span data-ttu-id="b2e87-117">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="b2e87-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b2e87-118">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="b2e87-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b2e87-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="b2e87-119">DisableBuffering</span></span> | <span data-ttu-id="b2e87-120">メモリの使用量を削減する http (s) サーバーへのプッシュ時にバッファー処理を無効にします。</span><span class="sxs-lookup"><span data-stu-id="b2e87-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="b2e87-121">注意: このオプションを使用すると、統合 Windows 認証動かないことがあります。</span><span class="sxs-lookup"><span data-stu-id="b2e87-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="b2e87-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b2e87-122">ForceEnglishOutput</span></span> | <span data-ttu-id="b2e87-123">*(3.5 +)* インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="b2e87-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b2e87-124">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="b2e87-124">Help</span></span> | <span data-ttu-id="b2e87-125">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="b2e87-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="b2e87-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b2e87-126">NonInteractive</span></span> | <span data-ttu-id="b2e87-127">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="b2e87-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b2e87-128">シンボルなし</span><span class="sxs-lookup"><span data-stu-id="b2e87-128">NoSymbols</span></span> | <span data-ttu-id="b2e87-129">*(3.5 +)* シンボル パッケージが存在する場合にプッシュされませんシンボル サーバーにします。</span><span class="sxs-lookup"><span data-stu-id="b2e87-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="b2e87-130">ソース</span><span class="sxs-lookup"><span data-stu-id="b2e87-130">Source</span></span> | <span data-ttu-id="b2e87-131">サーバー URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="b2e87-131">Specifies the server URL.</span></span> <span data-ttu-id="b2e87-132">NuGet は、UNC またはローカル フォルダーのソースを識別し、単に HTTP を使用して、プッシュされずにあるファイルをコピーします。</span><span class="sxs-lookup"><span data-stu-id="b2e87-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="b2e87-133">また、NuGet 3.4.2 から始めて、これは必須のパラメーターを除いて、`NuGet.Config`ファイルを指定します、 *DefaultPushSource*値 (を参照してください[構成 NuGet 動作](../consume-packages/configuring-nuget-behavior.md))。</span><span class="sxs-lookup"><span data-stu-id="b2e87-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="b2e87-134">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="b2e87-134">SymbolSource</span></span> | <span data-ttu-id="b2e87-135">*(3.5 +)* シンボル サーバーの URL を指定します; は、プッシュ nuget.org するときに使用する nuget.smbsrc.net</span><span class="sxs-lookup"><span data-stu-id="b2e87-135">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="b2e87-136">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="b2e87-136">SymbolApiKey</span></span> | <span data-ttu-id="b2e87-137">*(3.5 +)* で指定された URL では、API キーを指定`-SymbolSource`です。</span><span class="sxs-lookup"><span data-stu-id="b2e87-137">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="b2e87-138">Timeout</span><span class="sxs-lookup"><span data-stu-id="b2e87-138">Timeout</span></span> | <span data-ttu-id="b2e87-139">(秒単位) をサーバーにプッシュするためのタイムアウト値を指定します。</span><span class="sxs-lookup"><span data-stu-id="b2e87-139">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="b2e87-140">既定では 300 秒 (5 分) です。</span><span class="sxs-lookup"><span data-stu-id="b2e87-140">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="b2e87-141">詳細度</span><span class="sxs-lookup"><span data-stu-id="b2e87-141">Verbosity</span></span> | <span data-ttu-id="b2e87-142">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="b2e87-142">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b2e87-143">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b2e87-143">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b2e87-144">使用例</span><span class="sxs-lookup"><span data-stu-id="b2e87-144">Examples</span></span>

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
