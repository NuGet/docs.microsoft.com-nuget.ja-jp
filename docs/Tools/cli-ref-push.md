---
title: NuGet CLI プッシュ コマンド |Microsoft ドキュメント
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe プッシュ コマンドのリファレンス
keywords: nuget プッシュ参照、プッシュ コマンド
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 832f7aeb2b485acbb83e5213916fc3423df961ab
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="66395-104">push コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="66395-104">push command (NuGet CLI)</span></span>

<span data-ttu-id="66395-105">**適用されます:**パッケージの発行&bullet;**サポートされているバージョン:**すべて; nuget.org に必要な 4.1.0+</span><span class="sxs-lookup"><span data-stu-id="66395-105">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="66395-106">Nuget.org をパッケージにプッシュするを使用する必要があります nuget.exe v4.1.0 以降、必須を実装する[NuGet プロトコル](../api/nuget-protocols.md)です。</span><span class="sxs-lookup"><span data-stu-id="66395-106">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="66395-107">パッケージをパッケージ ソースにプッシュし、それを公開します。</span><span class="sxs-lookup"><span data-stu-id="66395-107">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="66395-108">NuGet の既定の構成を読み込むことにより取得`%AppData%\NuGet\NuGet.Config`(Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) が、読み込み、`Nuget.Config`または`.nuget\Nuget.Config`ドライブのルートから開始し、現在のディレクトリで終わるファイル (を参照してください[構成NuGet 動作](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="66395-108">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="66395-109">使用法</span><span class="sxs-lookup"><span data-stu-id="66395-109">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="66395-110">ここで`<packagePath>`サーバーにプッシュするパッケージを識別します。</span><span class="sxs-lookup"><span data-stu-id="66395-110">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="66395-111">オプション</span><span class="sxs-lookup"><span data-stu-id="66395-111">Options</span></span>

| <span data-ttu-id="66395-112">オプション</span><span class="sxs-lookup"><span data-stu-id="66395-112">Option</span></span> | <span data-ttu-id="66395-113">説明</span><span class="sxs-lookup"><span data-stu-id="66395-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="66395-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="66395-114">ApiKey</span></span> | <span data-ttu-id="66395-115">ターゲットのリポジトリの API キー。</span><span class="sxs-lookup"><span data-stu-id="66395-115">The API key for the target repository.</span></span> <span data-ttu-id="66395-116">存在しない場合は、構成ファイルで指定されているが使用されます。</span><span class="sxs-lookup"><span data-stu-id="66395-116">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="66395-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="66395-117">ConfigFile</span></span> | <span data-ttu-id="66395-118">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="66395-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="66395-119">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="66395-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="66395-120">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="66395-120">DisableBuffering</span></span> | <span data-ttu-id="66395-121">メモリの使用量を削減する http (s) サーバーへのプッシュ時にバッファー処理を無効にします。</span><span class="sxs-lookup"><span data-stu-id="66395-121">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="66395-122">注意: このオプションを使用すると、統合 Windows 認証動かないことがあります。</span><span class="sxs-lookup"><span data-stu-id="66395-122">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="66395-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="66395-123">ForceEnglishOutput</span></span> | <span data-ttu-id="66395-124">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="66395-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="66395-125">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="66395-125">Help</span></span> | <span data-ttu-id="66395-126">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="66395-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="66395-127">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="66395-127">NonInteractive</span></span> | <span data-ttu-id="66395-128">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="66395-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="66395-129">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="66395-129">NoSymbols</span></span> | <span data-ttu-id="66395-130">*(3.5 +)*シンボル パッケージが存在する場合にプッシュされませんシンボル サーバーにします。</span><span class="sxs-lookup"><span data-stu-id="66395-130">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="66395-131">ソース</span><span class="sxs-lookup"><span data-stu-id="66395-131">Source</span></span> | <span data-ttu-id="66395-132">サーバー URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="66395-132">Specifies the server URL.</span></span> <span data-ttu-id="66395-133">NuGet は、UNC またはローカル フォルダーのソースを識別し、単に HTTP を使用して、プッシュされずにあるファイルをコピーします。</span><span class="sxs-lookup"><span data-stu-id="66395-133">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="66395-134">また、NuGet 3.4.2 から始めて、これは必須のパラメーターを除いて、`NuGet.Config`ファイルを指定します、 *DefaultPushSource*値 (を参照してください[構成 NuGet 動作](../consume-packages/configuring-nuget-behavior.md))。</span><span class="sxs-lookup"><span data-stu-id="66395-134">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="66395-135">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="66395-135">SymbolSource</span></span> | <span data-ttu-id="66395-136">*(3.5 +)*シンボル サーバーの URL を指定します; は、プッシュ nuget.org するときに使用する nuget.smbsrc.net</span><span class="sxs-lookup"><span data-stu-id="66395-136">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="66395-137">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="66395-137">SymbolApiKey</span></span> | <span data-ttu-id="66395-138">*(3.5 +)*で指定された URL では、API キーを指定`-SymbolSource`です。</span><span class="sxs-lookup"><span data-stu-id="66395-138">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="66395-139">Timeout</span><span class="sxs-lookup"><span data-stu-id="66395-139">Timeout</span></span> | <span data-ttu-id="66395-140">(秒単位) をサーバーにプッシュするためのタイムアウト値を指定します。</span><span class="sxs-lookup"><span data-stu-id="66395-140">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="66395-141">既定では 300 秒 (5 分) です。</span><span class="sxs-lookup"><span data-stu-id="66395-141">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="66395-142">詳細度</span><span class="sxs-lookup"><span data-stu-id="66395-142">Verbosity</span></span> | <span data-ttu-id="66395-143">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="66395-143">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="66395-144">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="66395-144">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="66395-145">使用例</span><span class="sxs-lookup"><span data-stu-id="66395-145">Examples</span></span>

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
