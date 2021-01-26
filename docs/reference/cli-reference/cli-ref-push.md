---
title: NuGet CLI プッシュコマンド
description: nuget.exe push コマンドのリファレンス
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 54a09361173ae10040433b05fcfae7304e39452e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779187"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="7e008-103">push コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7e008-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="7e008-104">**適用対象:** パッケージ発行が &bullet; **サポートされているバージョン:** すべて。 nuget.org には、4.1.0 以降が必要です。</span><span class="sxs-lookup"><span data-stu-id="7e008-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="7e008-105">Nuget.org にパッケージをプッシュするには、必要な [nuget プロトコル](../../api/nuget-protocols.md)を実装する nuget.exe v2.0 + を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e008-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="7e008-106">パッケージをパッケージソースにプッシュして発行します。</span><span class="sxs-lookup"><span data-stu-id="7e008-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="7e008-107">NuGet の既定の構成を取得するには `%AppData%\NuGet\NuGet.Config` 、(Windows) または `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) を読み込み、 `Nuget.Config` `.nuget\Nuget.Config` ドライブのルートから開始し、現在のディレクトリで終了します ( [一般的な nuget 構成](../../consume-packages/configuring-nuget-behavior.md)を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="7e008-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="7e008-108">使用方法</span><span class="sxs-lookup"><span data-stu-id="7e008-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="7e008-109">は、 `<packagePath>` サーバーにプッシュするパッケージを識別します。</span><span class="sxs-lookup"><span data-stu-id="7e008-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="7e008-110">Options</span><span class="sxs-lookup"><span data-stu-id="7e008-110">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="7e008-111">ターゲットリポジトリの API キー。</span><span class="sxs-lookup"><span data-stu-id="7e008-111">The API key for the target repository.</span></span> <span data-ttu-id="7e008-112">存在しない場合は、構成ファイルで指定されたものが使用されます。</span><span class="sxs-lookup"><span data-stu-id="7e008-112">If not present,  the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="7e008-113">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="7e008-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7e008-114">指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="7e008-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DisableBuffering`**

  <span data-ttu-id="7e008-115">メモリ使用量を減らすために HTTP (s) サーバーにプッシュするときのバッファー処理を無効にします。</span><span class="sxs-lookup"><span data-stu-id="7e008-115">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="7e008-116">注意: このオプションを使用すると、統合 Windows 認証が機能しない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7e008-116">Caution: when this option is used, integrated Windows authentication might not work.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="7e008-117">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="7e008-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="7e008-118">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="7e008-118">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="7e008-119">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="7e008-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoServiceEndpoint`**

  <span data-ttu-id="7e008-120">は、ソース URL に追加されません `api/v2/packages` 。</span><span class="sxs-lookup"><span data-stu-id="7e008-120">Does not append `api/v2/packages` to the source URL.</span></span>

- **`-NoSymbols`**

  <span data-ttu-id="7e008-121">*(3.5 +)* シンボルパッケージが存在する場合は、シンボルサーバーにプッシュされません。</span><span class="sxs-lookup"><span data-stu-id="7e008-121">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="7e008-122">サーバー URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="7e008-122">Specifies the server URL.</span></span> <span data-ttu-id="7e008-123">NuGet によって UNC またはローカル フォルダー ソースが識別され、HTTP を使用してファイルがプッシュされるのではなく、単にそこにファイルがコピーされます。</span><span class="sxs-lookup"><span data-stu-id="7e008-123">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="7e008-124">また、NuGet 3.4.2 以降では、ファイルで Defaultpushsource 値が指定されていない限り、これは必須パラメーターです `NuGet.Config` (「 [NuGet の動作の構成](../../consume-packages/configuring-nuget-behavior.md)」を参照してください)。 </span><span class="sxs-lookup"><span data-stu-id="7e008-124">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span>

- **`-SkipDuplicate`**

  <span data-ttu-id="7e008-125">*(5.1 以降)* パッケージとバージョンが既に存在する場合は、スキップして、プッシュ時に次のパッケージを続行します (存在する場合)。</span><span class="sxs-lookup"><span data-stu-id="7e008-125">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span>

- **`-SymbolSource`**

  <span data-ttu-id="7e008-126">*(3.5 +)* シンボルサーバーの URL を指定します。nuget.smbsrc.net は、nuget.org にプッシュするときに使用されます。</span><span class="sxs-lookup"><span data-stu-id="7e008-126">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span>

- **`-SymbolApiKey`**

  <span data-ttu-id="7e008-127">*(3.5 +)* で指定された URL の API キーを指定し `-SymbolSource` ます。</span><span class="sxs-lookup"><span data-stu-id="7e008-127">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span>

- **`-Timeout`**

  <span data-ttu-id="7e008-128">サーバーにプッシュするときのタイムアウトを秒単位で指定します。</span><span class="sxs-lookup"><span data-stu-id="7e008-128">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="7e008-129">設定値の既定は 300 秒 (5 分) です。</span><span class="sxs-lookup"><span data-stu-id="7e008-129">The default is 300 seconds (5 minutes).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="7e008-130">出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。</span><span class="sxs-lookup"><span data-stu-id="7e008-130">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


<span data-ttu-id="7e008-131">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="7e008-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7e008-132">使用例</span><span class="sxs-lookup"><span data-stu-id="7e008-132">Examples</span></span>

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
