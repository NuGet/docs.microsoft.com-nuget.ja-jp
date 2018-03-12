---
title: "NuGet CLI コマンドを確認してください |Microsoft ドキュメント"
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "検証コマンドを実行、nuget.exe への参照"
keywords: "nuget の参照の検証、コマンドを確認してください。"
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: 2747491eb35d8685a44e86fcc1b572013982c754
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="3c179-104">コマンド (NuGet CLI) を確認してください。</span><span class="sxs-lookup"><span data-stu-id="3c179-104">verify command (NuGet CLI)</span></span>

<span data-ttu-id="3c179-105">**適用されます:**消費をパッケージ化&bullet;**サポートされているバージョン:** 4.6 以上</span><span class="sxs-lookup"><span data-stu-id="3c179-105">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="3c179-106">パッケージを検証します。</span><span class="sxs-lookup"><span data-stu-id="3c179-106">Verifies a package.</span></span>

## <a name="usage"></a><span data-ttu-id="3c179-107">使用法</span><span class="sxs-lookup"><span data-stu-id="3c179-107">Usage</span></span>

```cli
nuget verify <package(s)> [options]
```

<span data-ttu-id="3c179-108">ここで`<package(s)>`は 1 つ以上`.nupkg`ファイル。</span><span class="sxs-lookup"><span data-stu-id="3c179-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="3c179-109">オプション</span><span class="sxs-lookup"><span data-stu-id="3c179-109">Options</span></span>

| <span data-ttu-id="3c179-110">オプション</span><span class="sxs-lookup"><span data-stu-id="3c179-110">Option</span></span> | <span data-ttu-id="3c179-111">説明</span><span class="sxs-lookup"><span data-stu-id="3c179-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3c179-112">すべて</span><span class="sxs-lookup"><span data-stu-id="3c179-112">All</span></span> | <span data-ttu-id="3c179-113">パッケージで可能なすべての検証を実行することを指定します。</span><span class="sxs-lookup"><span data-stu-id="3c179-113">Specifies that all verifications possible should be performed on the package(s).</span></span> |
| <span data-ttu-id="3c179-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="3c179-114">CertificateFingerprint</span></span> | <span data-ttu-id="3c179-115">証明書 (s) で署名されたパッケージを署名する必要がありますの 1 つまたは複数の sha-256 証明書指紋を指定します。</span><span class="sxs-lookup"><span data-stu-id="3c179-115">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="3c179-116">Sha-256 証明書フィンガー プリントは、証明書の SHA 256 ハッシュです。</span><span class="sxs-lookup"><span data-stu-id="3c179-116">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="3c179-117">複数の入力は、セミコロンで区切られたにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="3c179-117">Multiple inputs should be semicolon separated.</span></span> |
| <span data-ttu-id="3c179-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3c179-118">ConfigFile</span></span> | <span data-ttu-id="3c179-119">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="3c179-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3c179-120">指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。</span><span class="sxs-lookup"><span data-stu-id="3c179-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="3c179-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3c179-121">ForceEnglishOutput</span></span> | <span data-ttu-id="3c179-122">インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="3c179-122">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3c179-123">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="3c179-123">Help</span></span> | <span data-ttu-id="3c179-124">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="3c179-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="3c179-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="3c179-125">NonInteractive</span></span> | <span data-ttu-id="3c179-126">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="3c179-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3c179-127">シグネチャ</span><span class="sxs-lookup"><span data-stu-id="3c179-127">Signatures</span></span> | <span data-ttu-id="3c179-128">パッケージの署名の確認を実行することを指定します。</span><span class="sxs-lookup"><span data-stu-id="3c179-128">Specifies that package signature verification should be performed.</span></span> |
| <span data-ttu-id="3c179-129">詳細度</span><span class="sxs-lookup"><span data-stu-id="3c179-129">Verbosity</span></span> | <span data-ttu-id="3c179-130">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="3c179-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="3c179-131">使用例</span><span class="sxs-lookup"><span data-stu-id="3c179-131">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```