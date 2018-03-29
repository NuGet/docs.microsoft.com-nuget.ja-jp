---
title: NuGet CLI コマンドを確認してください |Microsoft ドキュメント
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 検証コマンドを実行、nuget.exe への参照
keywords: nuget の参照の検証、コマンドを確認してください。
ms.reviewer:
- karann
- rmpablos
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 4423e491e0ab5dc1e13982440db42bc9b0e85c38
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="5f296-104">コマンド (NuGet CLI) を確認してください。</span><span class="sxs-lookup"><span data-stu-id="5f296-104">verify command (NuGet CLI)</span></span>

<span data-ttu-id="5f296-105">**適用されます:**消費をパッケージ化&bullet;**サポートされているバージョン:** 4.6 以上</span><span class="sxs-lookup"><span data-stu-id="5f296-105">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="5f296-106">パッケージを検証します。</span><span class="sxs-lookup"><span data-stu-id="5f296-106">Verifies a package.</span></span>

## <a name="usage"></a><span data-ttu-id="5f296-107">使用法</span><span class="sxs-lookup"><span data-stu-id="5f296-107">Usage</span></span>

```cli
nuget verify <package(s)> [options]
```

<span data-ttu-id="5f296-108">ここで`<package(s)>`は 1 つ以上`.nupkg`ファイル。</span><span class="sxs-lookup"><span data-stu-id="5f296-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="5f296-109">オプション</span><span class="sxs-lookup"><span data-stu-id="5f296-109">Options</span></span>

| <span data-ttu-id="5f296-110">オプション</span><span class="sxs-lookup"><span data-stu-id="5f296-110">Option</span></span> | <span data-ttu-id="5f296-111">説明</span><span class="sxs-lookup"><span data-stu-id="5f296-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5f296-112">すべて</span><span class="sxs-lookup"><span data-stu-id="5f296-112">All</span></span> | <span data-ttu-id="5f296-113">パッケージで可能なすべての検証を実行することを指定します。</span><span class="sxs-lookup"><span data-stu-id="5f296-113">Specifies that all verifications possible should be performed on the package(s).</span></span> |
| <span data-ttu-id="5f296-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="5f296-114">CertificateFingerprint</span></span> | <span data-ttu-id="5f296-115">証明書 (s) で署名されたパッケージを署名する必要がありますの 1 つまたは複数の sha-256 証明書指紋を指定します。</span><span class="sxs-lookup"><span data-stu-id="5f296-115">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="5f296-116">Sha-256 証明書フィンガー プリントは、証明書の SHA 256 ハッシュです。</span><span class="sxs-lookup"><span data-stu-id="5f296-116">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="5f296-117">複数の入力は、セミコロンで区切られたにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="5f296-117">Multiple inputs should be semicolon separated.</span></span> |
| <span data-ttu-id="5f296-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5f296-118">ConfigFile</span></span> | <span data-ttu-id="5f296-119">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="5f296-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5f296-120">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="5f296-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5f296-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5f296-121">ForceEnglishOutput</span></span> | <span data-ttu-id="5f296-122">インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="5f296-122">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5f296-123">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="5f296-123">Help</span></span> | <span data-ttu-id="5f296-124">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="5f296-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="5f296-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="5f296-125">NonInteractive</span></span> | <span data-ttu-id="5f296-126">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="5f296-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5f296-127">シグネチャ</span><span class="sxs-lookup"><span data-stu-id="5f296-127">Signatures</span></span> | <span data-ttu-id="5f296-128">パッケージの署名の確認を実行することを指定します。</span><span class="sxs-lookup"><span data-stu-id="5f296-128">Specifies that package signature verification should be performed.</span></span> |
| <span data-ttu-id="5f296-129">詳細度</span><span class="sxs-lookup"><span data-stu-id="5f296-129">Verbosity</span></span> | <span data-ttu-id="5f296-130">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="5f296-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="5f296-131">使用例</span><span class="sxs-lookup"><span data-stu-id="5f296-131">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```