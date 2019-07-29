---
title: NuGet CLI verify コマンド
description: Nuget.exe の verify コマンドのリファレンス
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327499"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="85ed8-103">verify コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="85ed8-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="85ed8-104">**適用対象:** パッケージ消費&bullet;が**サポートされているバージョン:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="85ed8-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="85ed8-105">パッケージを検証します。</span><span class="sxs-lookup"><span data-stu-id="85ed8-105">Verifies a package.</span></span>

<span data-ttu-id="85ed8-106">署名付きパッケージの検証は、.NET Core、Mono、または Windows 以外のプラットフォームではまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="85ed8-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="85ed8-107">使用法</span><span class="sxs-lookup"><span data-stu-id="85ed8-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="85ed8-108">ここ`<package(s)>` で`.nupkg` 、は1つ以上のファイルです。</span><span class="sxs-lookup"><span data-stu-id="85ed8-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="85ed8-109">nuget 検証-すべて</span><span class="sxs-lookup"><span data-stu-id="85ed8-109">nuget verify -All</span></span>

<span data-ttu-id="85ed8-110">パッケージに対して可能なすべての検証を実行することを指定します。</span><span class="sxs-lookup"><span data-stu-id="85ed8-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="85ed8-111">nuget の検証-署名</span><span class="sxs-lookup"><span data-stu-id="85ed8-111">nuget verify -Signatures</span></span>

<span data-ttu-id="85ed8-112">パッケージ署名の検証を実行する必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="85ed8-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="85ed8-113">"確認-署名" のオプション</span><span class="sxs-lookup"><span data-stu-id="85ed8-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="85ed8-114">オプション</span><span class="sxs-lookup"><span data-stu-id="85ed8-114">Option</span></span> | <span data-ttu-id="85ed8-115">説明</span><span class="sxs-lookup"><span data-stu-id="85ed8-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="85ed8-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="85ed8-116">CertificateFingerprint</span></span> | <span data-ttu-id="85ed8-117">署名されたパッケージに署名する必要がある証明書の1つまたは複数の 256 SHA-1 証明書の指紋を指定します。</span><span class="sxs-lookup"><span data-stu-id="85ed8-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="85ed8-118">証明書 SHA-256 フィンガープリントは、証明書の SHA-256 ハッシュです。</span><span class="sxs-lookup"><span data-stu-id="85ed8-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="85ed8-119">複数の入力をセミコロンで区切る必要があります。</span><span class="sxs-lookup"><span data-stu-id="85ed8-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="85ed8-120">オプション</span><span class="sxs-lookup"><span data-stu-id="85ed8-120">Options</span></span>

| <span data-ttu-id="85ed8-121">オプション</span><span class="sxs-lookup"><span data-stu-id="85ed8-121">Option</span></span> | <span data-ttu-id="85ed8-122">説明</span><span class="sxs-lookup"><span data-stu-id="85ed8-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="85ed8-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="85ed8-123">ConfigFile</span></span> | <span data-ttu-id="85ed8-124">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="85ed8-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="85ed8-125">指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="85ed8-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="85ed8-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="85ed8-126">ForceEnglishOutput</span></span> | <span data-ttu-id="85ed8-127">不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="85ed8-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="85ed8-128">Help</span><span class="sxs-lookup"><span data-stu-id="85ed8-128">Help</span></span> | <span data-ttu-id="85ed8-129">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="85ed8-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="85ed8-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="85ed8-130">Verbosity</span></span> | <span data-ttu-id="85ed8-131">出力に表示される詳細データの量を指定します: *normal*、*quiet*、*detailed*</span><span class="sxs-lookup"><span data-stu-id="85ed8-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="85ed8-132">使用例</span><span class="sxs-lookup"><span data-stu-id="85ed8-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```