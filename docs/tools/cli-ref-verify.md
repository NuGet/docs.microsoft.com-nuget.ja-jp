---
title: NuGet CLI コマンドを確認してください。
description: 検証コマンドを実行、nuget.exe への参照
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c80334104f7d8b2ccbf16ea2c11dc37b39408eeb
ms.sourcegitcommit: c8485dc61469511485367d2067b97d6f74b49f6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="e3410-103">コマンド (NuGet CLI) を確認してください。</span><span class="sxs-lookup"><span data-stu-id="e3410-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="e3410-104">**適用されます:** 消費をパッケージ化&bullet;**サポートされているバージョン:** 4.6 以上</span><span class="sxs-lookup"><span data-stu-id="e3410-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="e3410-105">パッケージを検証します。</span><span class="sxs-lookup"><span data-stu-id="e3410-105">Verifies a package.</span></span>

<span data-ttu-id="e3410-106">署名付きパッケージの検証は、Mono で、または Windows 以外のプラットフォーム上の .NET Core でまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="e3410-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="e3410-107">使用法</span><span class="sxs-lookup"><span data-stu-id="e3410-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="e3410-108">ここで`<package(s)>`は 1 つ以上`.nupkg`ファイル。</span><span class="sxs-lookup"><span data-stu-id="e3410-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="e3410-109">nuget を確認してください - すべて</span><span class="sxs-lookup"><span data-stu-id="e3410-109">nuget verify -All</span></span>

<span data-ttu-id="e3410-110">パッケージで可能なすべての検証を実行することを指定します。</span><span class="sxs-lookup"><span data-stu-id="e3410-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="e3410-111">nuget 署名を検証する-</span><span class="sxs-lookup"><span data-stu-id="e3410-111">nuget verify -Signatures</span></span>

<span data-ttu-id="e3410-112">パッケージの署名の確認を実行することを指定します。</span><span class="sxs-lookup"><span data-stu-id="e3410-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="e3410-113">「署名の確認-」のオプション</span><span class="sxs-lookup"><span data-stu-id="e3410-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="e3410-114">オプション</span><span class="sxs-lookup"><span data-stu-id="e3410-114">Option</span></span> | <span data-ttu-id="e3410-115">説明</span><span class="sxs-lookup"><span data-stu-id="e3410-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e3410-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="e3410-116">CertificateFingerprint</span></span> | <span data-ttu-id="e3410-117">証明書 (s) で署名されたパッケージを署名する必要がありますの 1 つまたは複数の sha-256 証明書指紋を指定します。</span><span class="sxs-lookup"><span data-stu-id="e3410-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="e3410-118">Sha-256 証明書フィンガー プリントは、証明書の SHA 256 ハッシュです。</span><span class="sxs-lookup"><span data-stu-id="e3410-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="e3410-119">複数の入力は、セミコロンで区切られたにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="e3410-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="e3410-120">オプション</span><span class="sxs-lookup"><span data-stu-id="e3410-120">Options</span></span>

| <span data-ttu-id="e3410-121">オプション</span><span class="sxs-lookup"><span data-stu-id="e3410-121">Option</span></span> | <span data-ttu-id="e3410-122">説明</span><span class="sxs-lookup"><span data-stu-id="e3410-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e3410-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e3410-123">ConfigFile</span></span> | <span data-ttu-id="e3410-124">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="e3410-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e3410-125">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="e3410-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="e3410-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e3410-126">ForceEnglishOutput</span></span> | <span data-ttu-id="e3410-127">インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="e3410-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e3410-128">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="e3410-128">Help</span></span> | <span data-ttu-id="e3410-129">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="e3410-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="e3410-130">詳細度</span><span class="sxs-lookup"><span data-stu-id="e3410-130">Verbosity</span></span> | <span data-ttu-id="e3410-131">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="e3410-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="e3410-132">使用例</span><span class="sxs-lookup"><span data-stu-id="e3410-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```