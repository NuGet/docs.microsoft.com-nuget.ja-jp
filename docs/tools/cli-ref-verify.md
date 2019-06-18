---
title: NuGet CLI verify コマンド
description: Nuget.exe の verify コマンドのリファレンス
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 127f7a549c0a213f319c8820293646b302830436
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545214"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="ceb12-103">verify コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ceb12-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="ceb12-104">**適用対象:** 消費をパッケージ化&bullet;**サポートされているバージョン:** 4.6 以降</span><span class="sxs-lookup"><span data-stu-id="ceb12-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="ceb12-105">パッケージを確認します。</span><span class="sxs-lookup"><span data-stu-id="ceb12-105">Verifies a package.</span></span>

<span data-ttu-id="ceb12-106">.NET Core、Mono、または Windows 以外のプラットフォーム上で、署名済みパッケージの検証がまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="ceb12-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="ceb12-107">使用法</span><span class="sxs-lookup"><span data-stu-id="ceb12-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="ceb12-108">場所`<package(s)>`は 1 つ以上`.nupkg`ファイル。</span><span class="sxs-lookup"><span data-stu-id="ceb12-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="ceb12-109">nuget 検証 - すべて</span><span class="sxs-lookup"><span data-stu-id="ceb12-109">nuget verify -All</span></span>

<span data-ttu-id="ceb12-110">パッケージで可能なすべての検証を実行することを指定します。</span><span class="sxs-lookup"><span data-stu-id="ceb12-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="ceb12-111">nuget の検証 - 署名</span><span class="sxs-lookup"><span data-stu-id="ceb12-111">nuget verify -Signatures</span></span>

<span data-ttu-id="ceb12-112">パッケージの署名の検証を実行することを指定します。</span><span class="sxs-lookup"><span data-stu-id="ceb12-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="ceb12-113">「署名の検証-」のオプション</span><span class="sxs-lookup"><span data-stu-id="ceb12-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="ceb12-114">オプション</span><span class="sxs-lookup"><span data-stu-id="ceb12-114">Option</span></span> | <span data-ttu-id="ceb12-115">説明</span><span class="sxs-lookup"><span data-stu-id="ceb12-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ceb12-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="ceb12-116">CertificateFingerprint</span></span> | <span data-ttu-id="ceb12-117">証明書 (s) で署名する署名付きパッケージの 1 つまたは複数の sha-256 証明書指紋を指定します。</span><span class="sxs-lookup"><span data-stu-id="ceb12-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="ceb12-118">Sha-256 証明書フィンガー プリントは、証明書の SHA 256 ハッシュです。</span><span class="sxs-lookup"><span data-stu-id="ceb12-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="ceb12-119">複数の入力には、セミコロンで区切った必要があります。</span><span class="sxs-lookup"><span data-stu-id="ceb12-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="ceb12-120">オプション</span><span class="sxs-lookup"><span data-stu-id="ceb12-120">Options</span></span>

| <span data-ttu-id="ceb12-121">オプション</span><span class="sxs-lookup"><span data-stu-id="ceb12-121">Option</span></span> | <span data-ttu-id="ceb12-122">説明</span><span class="sxs-lookup"><span data-stu-id="ceb12-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ceb12-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ceb12-123">ConfigFile</span></span> | <span data-ttu-id="ceb12-124">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="ceb12-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ceb12-125">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="ceb12-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ceb12-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ceb12-126">ForceEnglishOutput</span></span> | <span data-ttu-id="ceb12-127">インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="ceb12-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ceb12-128">Help</span><span class="sxs-lookup"><span data-stu-id="ceb12-128">Help</span></span> | <span data-ttu-id="ceb12-129">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="ceb12-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="ceb12-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="ceb12-130">Verbosity</span></span> | <span data-ttu-id="ceb12-131">出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*</span><span class="sxs-lookup"><span data-stu-id="ceb12-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="ceb12-132">使用例</span><span class="sxs-lookup"><span data-stu-id="ceb12-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```