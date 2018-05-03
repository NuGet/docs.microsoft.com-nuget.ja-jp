---
title: NuGet CLI コマンドを確認してください。
description: 検証コマンドを実行、nuget.exe への参照
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c2c31b71358bc50a1fb9aab8905c279cd1235b07
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="96a8c-103">コマンド (NuGet CLI) を確認してください。</span><span class="sxs-lookup"><span data-stu-id="96a8c-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="96a8c-104">**適用されます:** 消費をパッケージ化&bullet;**サポートされているバージョン:** 4.6 以上</span><span class="sxs-lookup"><span data-stu-id="96a8c-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="96a8c-105">パッケージを検証します。</span><span class="sxs-lookup"><span data-stu-id="96a8c-105">Verifies a package.</span></span>

<span data-ttu-id="96a8c-106">署名付きパッケージの検証は、Mono で、または Windows 以外のプラットフォーム上の .NET Core でまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="96a8c-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="96a8c-107">使用法</span><span class="sxs-lookup"><span data-stu-id="96a8c-107">Usage</span></span>

```cli
nuget verify <package(s)> [options]
```

<span data-ttu-id="96a8c-108">ここで`<package(s)>`は 1 つ以上`.nupkg`ファイル。</span><span class="sxs-lookup"><span data-stu-id="96a8c-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="96a8c-109">オプション</span><span class="sxs-lookup"><span data-stu-id="96a8c-109">Options</span></span>

| <span data-ttu-id="96a8c-110">オプション</span><span class="sxs-lookup"><span data-stu-id="96a8c-110">Option</span></span> | <span data-ttu-id="96a8c-111">説明</span><span class="sxs-lookup"><span data-stu-id="96a8c-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="96a8c-112">すべて</span><span class="sxs-lookup"><span data-stu-id="96a8c-112">All</span></span> | <span data-ttu-id="96a8c-113">パッケージで可能なすべての検証を実行することを指定します。</span><span class="sxs-lookup"><span data-stu-id="96a8c-113">Specifies that all verifications possible should be performed on the package(s).</span></span> |
| <span data-ttu-id="96a8c-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="96a8c-114">CertificateFingerprint</span></span> | <span data-ttu-id="96a8c-115">証明書 (s) で署名されたパッケージを署名する必要がありますの 1 つまたは複数の sha-256 証明書指紋を指定します。</span><span class="sxs-lookup"><span data-stu-id="96a8c-115">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="96a8c-116">Sha-256 証明書フィンガー プリントは、証明書の SHA 256 ハッシュです。</span><span class="sxs-lookup"><span data-stu-id="96a8c-116">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="96a8c-117">複数の入力は、セミコロンで区切られたにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="96a8c-117">Multiple inputs should be semicolon separated.</span></span> |
| <span data-ttu-id="96a8c-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="96a8c-118">ConfigFile</span></span> | <span data-ttu-id="96a8c-119">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="96a8c-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="96a8c-120">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="96a8c-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="96a8c-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="96a8c-121">ForceEnglishOutput</span></span> | <span data-ttu-id="96a8c-122">インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="96a8c-122">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="96a8c-123">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="96a8c-123">Help</span></span> | <span data-ttu-id="96a8c-124">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="96a8c-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="96a8c-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="96a8c-125">NonInteractive</span></span> | <span data-ttu-id="96a8c-126">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="96a8c-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="96a8c-127">シグネチャ</span><span class="sxs-lookup"><span data-stu-id="96a8c-127">Signatures</span></span> | <span data-ttu-id="96a8c-128">パッケージの署名の確認を実行することを指定します。</span><span class="sxs-lookup"><span data-stu-id="96a8c-128">Specifies that package signature verification should be performed.</span></span> |
| <span data-ttu-id="96a8c-129">詳細度</span><span class="sxs-lookup"><span data-stu-id="96a8c-129">Verbosity</span></span> | <span data-ttu-id="96a8c-130">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="96a8c-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="96a8c-131">使用例</span><span class="sxs-lookup"><span data-stu-id="96a8c-131">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```