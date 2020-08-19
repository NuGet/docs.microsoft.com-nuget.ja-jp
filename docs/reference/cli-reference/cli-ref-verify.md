---
title: NuGet CLI 確認コマンド
description: nuget.exe verify コマンドのリファレンス
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 2c501753a16820c5d027441001561c6b637ccda9
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622604"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="2ad6b-103">verify コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2ad6b-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="2ad6b-104">**適用対象:** パッケージの使用量が &bullet; **サポートされているバージョン:** 4.6 以降</span><span class="sxs-lookup"><span data-stu-id="2ad6b-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="2ad6b-105">パッケージを検証します。</span><span class="sxs-lookup"><span data-stu-id="2ad6b-105">Verifies a package.</span></span>

<span data-ttu-id="2ad6b-106">署名付きパッケージの検証は、.NET Core、Mono、または Windows 以外のプラットフォームではまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="2ad6b-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="2ad6b-107">使用法</span><span class="sxs-lookup"><span data-stu-id="2ad6b-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="2ad6b-108">ここ `<package(s)>` で、は1つ以上の `.nupkg` ファイルです。</span><span class="sxs-lookup"><span data-stu-id="2ad6b-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="2ad6b-109">nuget 検証-すべて</span><span class="sxs-lookup"><span data-stu-id="2ad6b-109">nuget verify -All</span></span>

<span data-ttu-id="2ad6b-110">パッケージに対して可能なすべての検証を実行することを指定します。</span><span class="sxs-lookup"><span data-stu-id="2ad6b-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="2ad6b-111">nuget の検証-署名</span><span class="sxs-lookup"><span data-stu-id="2ad6b-111">nuget verify -Signatures</span></span>

<span data-ttu-id="2ad6b-112">パッケージ署名の検証を実行する必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="2ad6b-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="2ad6b-113">"確認-署名" のオプション</span><span class="sxs-lookup"><span data-stu-id="2ad6b-113">Options for "verify -Signatures"</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="2ad6b-114">署名されたパッケージに署名する必要がある証明書の1つまたは複数の 256 SHA-1 証明書の指紋を指定します。</span><span class="sxs-lookup"><span data-stu-id="2ad6b-114">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="2ad6b-115">証明書 SHA-256 フィンガープリントは、証明書の SHA-256 ハッシュです。</span><span class="sxs-lookup"><span data-stu-id="2ad6b-115">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="2ad6b-116">複数の入力をセミコロンで区切る必要があります。</span><span class="sxs-lookup"><span data-stu-id="2ad6b-116">Multiple inputs should be semicolon separated.</span></span>

## <a name="options"></a><span data-ttu-id="2ad6b-117">Options</span><span class="sxs-lookup"><span data-stu-id="2ad6b-117">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="2ad6b-118">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="2ad6b-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2ad6b-119">指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="2ad6b-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="2ad6b-120">不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="2ad6b-120">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="2ad6b-121">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="2ad6b-121">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="2ad6b-122">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="2ad6b-122">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="2ad6b-123">出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。</span><span class="sxs-lookup"><span data-stu-id="2ad6b-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="2ad6b-124">使用例</span><span class="sxs-lookup"><span data-stu-id="2ad6b-124">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```