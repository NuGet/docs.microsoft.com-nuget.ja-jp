---
title: NuGet CLI 確認コマンド
description: nuget.exe verify コマンドのリファレンス
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7ce08f11195437e94bfe69883ff525e9ad3a73f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238141"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="2d378-103">verify コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2d378-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="2d378-104">**適用対象:** パッケージの使用量が &bullet; **サポートされているバージョン:** 4.6 以降</span><span class="sxs-lookup"><span data-stu-id="2d378-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="2d378-105">パッケージを検証します。</span><span class="sxs-lookup"><span data-stu-id="2d378-105">Verifies a package.</span></span>

<span data-ttu-id="2d378-106">署名付きパッケージの検証は、Mono ではまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="2d378-106">Verification of signed packages is not yet supported under Mono.</span></span>

## <a name="usage"></a><span data-ttu-id="2d378-107">使用</span><span class="sxs-lookup"><span data-stu-id="2d378-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="2d378-108">ここ `<package(s)>` で、は1つ以上の `.nupkg` ファイルです。</span><span class="sxs-lookup"><span data-stu-id="2d378-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="2d378-109">nuget 検証-すべて</span><span class="sxs-lookup"><span data-stu-id="2d378-109">nuget verify -All</span></span>

<span data-ttu-id="2d378-110">可能なすべての検証をパッケージに対して実行する必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="2d378-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="2d378-111">nuget の検証-署名</span><span class="sxs-lookup"><span data-stu-id="2d378-111">nuget verify -Signatures</span></span>

<span data-ttu-id="2d378-112">パッケージ署名の検証を実行する必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="2d378-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="2d378-113">"確認-署名" のオプション</span><span class="sxs-lookup"><span data-stu-id="2d378-113">Options for "verify -Signatures"</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="2d378-114">署名されたパッケージに署名する必要がある証明書の1つまたは複数の 256 SHA-1 証明書の指紋を指定します。</span><span class="sxs-lookup"><span data-stu-id="2d378-114">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="2d378-115">証明書 SHA-256 フィンガープリントは、証明書の SHA-256 ハッシュです。</span><span class="sxs-lookup"><span data-stu-id="2d378-115">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="2d378-116">複数の入力をセミコロンで区切る必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d378-116">Multiple inputs should be semicolon separated.</span></span>

## <a name="options"></a><span data-ttu-id="2d378-117">オプション</span><span class="sxs-lookup"><span data-stu-id="2d378-117">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="2d378-118">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="2d378-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2d378-119">指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="2d378-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="2d378-120">不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="2d378-120">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="2d378-121">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="2d378-121">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="2d378-122">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="2d378-122">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="2d378-123">出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。</span><span class="sxs-lookup"><span data-stu-id="2d378-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="2d378-124">使用例</span><span class="sxs-lookup"><span data-stu-id="2d378-124">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```