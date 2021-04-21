---
title: インストールされているパッケージのトラブルシューティング
description: 個々のパッケージに使用されたパッケージ ソースを見つける方法
author: JonDouglas
ms.author: jodou
ms.date: 03/26/2021
ms.topic: conceptual
ms.openlocfilehash: 22fb51ebb996c66e10b860f0158676fd2d9da295
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387531"
---
# <a name="troubleshooting-installed-packages"></a><span data-ttu-id="46bca-103">インストールされているパッケージのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="46bca-103">Troubleshooting Installed Packages</span></span>

<span data-ttu-id="46bca-104">特定のパッケージがどのソースからインストールされたかを確認したい場合があります。</span><span class="sxs-lookup"><span data-stu-id="46bca-104">Sometimes you might want to validate which source a specific package was installed from.</span></span> <span data-ttu-id="46bca-105">ここでは、いくつかの確認方法を示します。</span><span class="sxs-lookup"><span data-stu-id="46bca-105">Here are some ways you can check.</span></span>

> [!Note]
> <span data-ttu-id="46bca-106">一部のパッケージ ソースでは、アップストリーム ソースと呼ばれる概念がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="46bca-106">Some package sources support a concept known as upstream sources.</span></span> <span data-ttu-id="46bca-107">たとえば、[Azure Artifacts アップストリーム ソース](/azure/devops/artifacts/concepts/upstream-sources)です。</span><span class="sxs-lookup"><span data-stu-id="46bca-107">For example, [Azure Artifacts upstream sources](/azure/devops/artifacts/concepts/upstream-sources).</span></span> <span data-ttu-id="46bca-108">NuGet クライアントでは、パッケージがアップストリーム ソースからのものであるかどうかが認識されません。</span><span class="sxs-lookup"><span data-stu-id="46bca-108">NuGet clients do not know whether a package came from an upstream source.</span></span> <span data-ttu-id="46bca-109">そのため、パッケージ ソースのログ記録には、アップストリーム ソースではなく、構成されているソースが記載されます。</span><span class="sxs-lookup"><span data-stu-id="46bca-109">Therefore, any logging of the package source will list the configured source, not the upstream source.</span></span>

## <a name="nupkgmetadata-file-in-global-packages-folder"></a><span data-ttu-id="46bca-110">グローバル パッケージ フォルダー内の `.nupkg.metadata` ファイル</span><span class="sxs-lookup"><span data-stu-id="46bca-110">`.nupkg.metadata` file in global packages folder</span></span>

<span data-ttu-id="46bca-111">パッケージが *global-packages* フォルダーに抽出されるときに、ファイル `.nupkg.metadata` が書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="46bca-111">When a package is extracted into the *global-packages* folder, a file `.nupkg.metadata` is written.</span></span> <span data-ttu-id="46bca-112">NuGet 5.9.0 から、NuGet ではパッケージ ソースが追加されます。</span><span class="sxs-lookup"><span data-stu-id="46bca-112">Starting from NuGet 5.9.0, NuGet will add the package source.</span></span> <span data-ttu-id="46bca-113">NuGet のバージョンを Visual Studio または .NET SDK のバージョンにマップするには、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="46bca-113">See below to map NuGet versions to Visual Studio or .NET SDK versions.</span></span> <span data-ttu-id="46bca-114">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="46bca-114">For example:</span></span>

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> <span data-ttu-id="46bca-115">NuGet 5.9.0 を持つ新しいバージョンのツールにアップグレードする前に抽出したパッケージが *global-packages* フォルダーにある場合、`.nupkg.metadata` ファイルはバージョン 1 になり、パッケージ ソースは含まれません。</span><span class="sxs-lookup"><span data-stu-id="46bca-115">If your *global-packages* folder has packages extracted before you upgraded to a newer version of tools that has NuGet 5.9.0, the `.nupkg.metadata` file will be version 1 and will not contain the package source.</span></span> <span data-ttu-id="46bca-116">[*global-packages* フォルダーをクリア](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders)して、すべてのパッケージにパッケージ ソースが含まれるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="46bca-116">You can [clear your *global-packages* folder](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) to ensure all packages will contain the package source.</span></span>

> [!Tip]
> <span data-ttu-id="46bca-117">NuGet によって `.nupkg.metadata` ファイルが書き込まれるのは、*global-packages* フォルダーに対してのみです。</span><span class="sxs-lookup"><span data-stu-id="46bca-117">NuGet writes the `.nupkg.metadata` file to the *global-packages* folder only.</span></span> <span data-ttu-id="46bca-118">`packages.config` を使用するプロジェクトではソリューション パッケージ フォルダーが使用されますが、`.nupkg.metadata` ファイルは作成されません。</span><span class="sxs-lookup"><span data-stu-id="46bca-118">Projects using `packages.config` use a solution packages folder, which does not create a `.nupkg.metadata` file.</span></span>

## <a name="installed-package-log-message"></a><span data-ttu-id="46bca-119">インストールされたパッケージのログ メッセージ</span><span class="sxs-lookup"><span data-stu-id="46bca-119">Installed package log message</span></span>

<span data-ttu-id="46bca-120">NuGet 5.9.0 から、NuGet では、パッケージがインストールされたことを通知する復元メッセージに、パッケージ ソースが出力されます。</span><span class="sxs-lookup"><span data-stu-id="46bca-120">Starting from NuGet 5.9.0, NuGet outputs the package source in the restore message informing that a package was installed.</span></span> <span data-ttu-id="46bca-121">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="46bca-121">For example:</span></span>

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> <span data-ttu-id="46bca-122">このメッセージは、通常または情報の詳細度で出力されます。</span><span class="sxs-lookup"><span data-stu-id="46bca-122">This message is output at normal/informational verbosity.</span></span> <span data-ttu-id="46bca-123">Visual Studio と `dotnet` CLI では最小の詳細度に既定値が設定されるため、このメッセージは既定では表示されません。</span><span class="sxs-lookup"><span data-stu-id="46bca-123">Visual Studio and the `dotnet` CLI default to minimal verbosity, so this message will not be visible by default.</span></span> <span data-ttu-id="46bca-124">`msbuild` と `nuget` CLI ツールでは通常の詳細度に既定値が設定されるため、このメッセージは既定で表示されます。</span><span class="sxs-lookup"><span data-stu-id="46bca-124">The `msbuild` and `nuget` CLI tools default to normal verbosity, so this message will be visible by default.</span></span>

## <a name="http-log-message"></a><span data-ttu-id="46bca-125">HTTP ログ メッセージ</span><span class="sxs-lookup"><span data-stu-id="46bca-125">HTTP log message</span></span>

<span data-ttu-id="46bca-126">パッケージをローカルで利用できない場合は、*global-packages* フォルダー、フォールバック フォルダー、またはローカル ファイル ソースのいずれかに、NuGet によって、任意の構成されたパッケージ ソースから HTTP 経由でパッケージがダウンロードされます。</span><span class="sxs-lookup"><span data-stu-id="46bca-126">When a package is not available locally, either in the *global-packages* folder, a fallback folder, or a local file source, NuGet will download it from any configured package source over HTTP.</span></span> <span data-ttu-id="46bca-127">HTTP 要求と応答は通常の詳細度レベルでログに記録されます。また、パッケージのバージョンごとに 1 つの要求と応答のみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="46bca-127">HTTP requests and responses are logged at the normal verbosity level, and you should see only a single request and response per package version.</span></span> <span data-ttu-id="46bca-128">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="46bca-128">For example:</span></span>

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

<span data-ttu-id="46bca-129">ファイルが最近ダウンロードされていた場合は、NuGet の *http-cache* から取得される可能性があります</span><span class="sxs-lookup"><span data-stu-id="46bca-129">If the files were recently downloaded, they might be retrieved from NuGet's *http-cache*</span></span>

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

<span data-ttu-id="46bca-130">URL 形式は、異なる NuGet HTTP サーバーの実装や、NuGet V2 または V3 HTTP プロトコルが実装されているかどうかによって、異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="46bca-130">The URL format may be different for different NuGet HTTP server implementations, and whether it's implementing NuGet V2 or V3 HTTP protocol.</span></span>

<span data-ttu-id="46bca-131">`nuget.config` に複数の HTTP ソースが定義されている場合は、各パッケージの `index.json` ファイルに対して複数の要求が表示されます (各ソースにつき 1 つ)。</span><span class="sxs-lookup"><span data-stu-id="46bca-131">If your `nuget.config` has multiple HTTP sources defined, you will see multiple requests to each package's `index.json` file, one for each source.</span></span> <span data-ttu-id="46bca-132">ただし、パッケージの各バージョンについて、ダウンロードされるのは 1 つの `nupkg` だけになります。</span><span class="sxs-lookup"><span data-stu-id="46bca-132">But there will be only a single `nupkg` download for each version of the package.</span></span>

## <a name="package-signature-log-message"></a><span data-ttu-id="46bca-133">パッケージの署名のログ メッセージ</span><span class="sxs-lookup"><span data-stu-id="46bca-133">Package signature log message</span></span>

<span data-ttu-id="46bca-134">ダウンロードするパッケージが署名されている場合、NuGet によって署名が検証され、詳細度が高い場合は次のメッセージが記録されます。</span><span class="sxs-lookup"><span data-stu-id="46bca-134">If the package being downloaded is signed, NuGet will validate the signature and will log the following message at detailed verbosity:</span></span>

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

<span data-ttu-id="46bca-135">このメッセージでは、パッケージが HTTP パッケージ ソースからダウンロードされたか、またはローカル パッケージ ソースからコピーされたかが報告されます。</span><span class="sxs-lookup"><span data-stu-id="46bca-135">This message will be reported whether the package was downloaded from an HTTP package source, or copied from a local package source.</span></span> <span data-ttu-id="46bca-136">パッケージが *global-packages* フォルダーまたはフォールバック フォルダーで既に使用可能な場合は、出力されません。</span><span class="sxs-lookup"><span data-stu-id="46bca-136">It will not be output if the package is already available in the *global-packages* folder or a fallback folder.</span></span>

> [!Important]
> <span data-ttu-id="46bca-137">[VeriSign CA の信頼の削除](https://github.com/dotnet/announcements/issues/180)により、NuGet では、特定のプラットフォームで、特定のバージョンの NuGet および .NET SDK において、署名付きパッケージの検証が無効になっています。</span><span class="sxs-lookup"><span data-stu-id="46bca-137">Due to [removal of trust of VeriSign CA](https://github.com/dotnet/announcements/issues/180) NuGet has disabled signed package verification on certain platforms, in certain versions of NuGet and the .NET SDK.</span></span> <span data-ttu-id="46bca-138">そのため、復元を実行しているプラットフォームや、使用している .NET または NuGet のバージョンによっては、同じパッケージに `PackageSignatureVerificationLog` ログがある場合と、それらのログが見つからない場合があります。</span><span class="sxs-lookup"><span data-stu-id="46bca-138">Therefore, the same packages may have `PackageSignatureVerificationLog` logs, or those logs may be missing, depending on what platform you're running restore on, and which version of .NET or NuGet you're using.</span></span>

## <a name="nuget-version-map"></a><span data-ttu-id="46bca-139">NuGet のバージョンのマップ</span><span class="sxs-lookup"><span data-stu-id="46bca-139">NuGet Version Map</span></span>

<span data-ttu-id="46bca-140">次のバージョンの NuGet には、パッケージ ソースのログに関する重要な変更点があります。</span><span class="sxs-lookup"><span data-stu-id="46bca-140">The following versions of NuGet have important changes regarding package source logging:</span></span>

|<span data-ttu-id="46bca-141">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="46bca-141">NuGet Version</span></span>|<span data-ttu-id="46bca-142">Visual Studio のバージョン</span><span class="sxs-lookup"><span data-stu-id="46bca-142">Visual Studio Version</span></span>|<span data-ttu-id="46bca-143">.NET SDK のバージョン</span><span class="sxs-lookup"><span data-stu-id="46bca-143">.NET SDK Version</span></span>|
|---|---|---|
|<span data-ttu-id="46bca-144">NuGet 5.9.0</span><span class="sxs-lookup"><span data-stu-id="46bca-144">NuGet 5.9.0</span></span>|<span data-ttu-id="46bca-145">Visual Studio 2019 16.9.0</span><span class="sxs-lookup"><span data-stu-id="46bca-145">Visual Studio 2019 16.9.0</span></span>|<span data-ttu-id="46bca-146">.NET 5 SDK 5.0.200</span><span class="sxs-lookup"><span data-stu-id="46bca-146">.NET 5 SDK 5.0.200</span></span>|
