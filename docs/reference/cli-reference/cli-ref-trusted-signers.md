---
title: NuGet CLI 信頼-署名者コマンド
description: Nuget.exe の信頼された署名者コマンドのリファレンス
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 94c4c6524c1870898893b80be914477af5a14e8b
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610340"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="c4dad-103">trusted-署名者コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c4dad-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="c4dad-104">**適用対象:** パッケージ消費 &bullet;**サポートされているバージョン:** 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="c4dad-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="c4dad-105">NuGet 構成に対する信頼された署名者を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="c4dad-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="c4dad-106">その他の使用方法については、「 [Common NuGet の構成](../../consume-packages/configuring-nuget-behavior.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c4dad-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="c4dad-107">Nuget.exe スキーマの外観の詳細については、 [nuget 構成ファイルのリファレンス](../nuget-config-file.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c4dad-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="c4dad-108">使用方法</span><span class="sxs-lookup"><span data-stu-id="c4dad-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="c4dad-109">`list|add|remove|sync` が指定されていない場合、コマンドは既定で `list`になります。</span><span class="sxs-lookup"><span data-stu-id="c4dad-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="c4dad-110">nuget の信頼された署名者リスト</span><span class="sxs-lookup"><span data-stu-id="c4dad-110">nuget trusted-signers list</span></span>

<span data-ttu-id="c4dad-111">構成内のすべての信頼された署名者を一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="c4dad-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="c4dad-112">このオプションには、各署名者が持つすべての証明書 (指紋および指紋アルゴリズム) が含まれます。</span><span class="sxs-lookup"><span data-stu-id="c4dad-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="c4dad-113">証明書に前の `[U]`が含まれている場合は、証明書エントリが `true`として `allowUntrustedRoot` 設定されていることを意味します。</span><span class="sxs-lookup"><span data-stu-id="c4dad-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="c4dad-114">このコマンドからの出力例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="c4dad-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="c4dad-115">nuget の信頼済み-署名者の追加 [オプション]</span><span class="sxs-lookup"><span data-stu-id="c4dad-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="c4dad-116">指定された名前の信頼された署名者を構成に追加します。このオプションでは、信頼された作成者またはリポジトリを追加するジェスチャは異なります。</span><span class="sxs-lookup"><span data-stu-id="c4dad-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="c4dad-117">パッケージに基づいて追加するためのオプション</span><span class="sxs-lookup"><span data-stu-id="c4dad-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="c4dad-118">ここで `<package(s)>` は1つ以上の `.nupkg` ファイルです。</span><span class="sxs-lookup"><span data-stu-id="c4dad-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="c4dad-119">オプション</span><span class="sxs-lookup"><span data-stu-id="c4dad-119">Option</span></span> | <span data-ttu-id="c4dad-120">説明</span><span class="sxs-lookup"><span data-stu-id="c4dad-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c4dad-121">作成者</span><span class="sxs-lookup"><span data-stu-id="c4dad-121">Author</span></span> | <span data-ttu-id="c4dad-122">パッケージの作成者の署名を信頼する必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="c4dad-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="c4dad-123">リポジトリ</span><span class="sxs-lookup"><span data-stu-id="c4dad-123">Repository</span></span> | <span data-ttu-id="c4dad-124">パッケージのリポジトリ署名または副署名を信頼する必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="c4dad-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="c4dad-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="c4dad-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="c4dad-126">信頼された署名者の証明書を信頼されていないルートにチェーンできるようにするかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="c4dad-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="c4dad-127">所有者</span><span class="sxs-lookup"><span data-stu-id="c4dad-127">Owners</span></span> | <span data-ttu-id="c4dad-128">リポジトリの信頼をさらに制限するために、信頼された所有者のセミコロンで区切られた一覧。</span><span class="sxs-lookup"><span data-stu-id="c4dad-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="c4dad-129">`-Repository` オプションを使用する場合にのみ有効です。</span><span class="sxs-lookup"><span data-stu-id="c4dad-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="c4dad-130">`-Author` と `-Repository` の両方を同時に指定することはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="c4dad-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="c4dad-131">サービスインデックスに基づく追加のオプション</span><span class="sxs-lookup"><span data-stu-id="c4dad-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="c4dad-132">_注_: このオプションでは、信頼されたリポジトリのみが追加されます。</span><span class="sxs-lookup"><span data-stu-id="c4dad-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="c4dad-133">オプション</span><span class="sxs-lookup"><span data-stu-id="c4dad-133">Option</span></span> | <span data-ttu-id="c4dad-134">説明</span><span class="sxs-lookup"><span data-stu-id="c4dad-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c4dad-135">ServiceIndex</span><span class="sxs-lookup"><span data-stu-id="c4dad-135">ServiceIndex</span></span> | <span data-ttu-id="c4dad-136">信頼されるリポジトリの V3 サービスインデックスを指定します。</span><span class="sxs-lookup"><span data-stu-id="c4dad-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="c4dad-137">このリポジトリは、リポジトリ署名リソースをサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4dad-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="c4dad-138">指定しない場合、コマンドは同じ `-Name` を持つパッケージソースを検索し、そこからサービスインデックスを取得します。</span><span class="sxs-lookup"><span data-stu-id="c4dad-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="c4dad-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="c4dad-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="c4dad-140">信頼された署名者の証明書を信頼されていないルートにチェーンできるようにするかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="c4dad-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="c4dad-141">所有者</span><span class="sxs-lookup"><span data-stu-id="c4dad-141">Owners</span></span> | <span data-ttu-id="c4dad-142">リポジトリの信頼をさらに制限するために、信頼された所有者のセミコロンで区切られた一覧。</span><span class="sxs-lookup"><span data-stu-id="c4dad-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="c4dad-143">証明書情報に基づいて追加するオプション</span><span class="sxs-lookup"><span data-stu-id="c4dad-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="c4dad-144">_注_: 指定した名前の信頼された署名者が既に存在する場合、その署名者に証明書項目が追加されます。</span><span class="sxs-lookup"><span data-stu-id="c4dad-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="c4dad-145">それ以外の場合、信頼できる作成者は、指定された証明書情報から証明書項目を使用して作成されます。</span><span class="sxs-lookup"><span data-stu-id="c4dad-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="c4dad-146">オプション</span><span class="sxs-lookup"><span data-stu-id="c4dad-146">Option</span></span> | <span data-ttu-id="c4dad-147">説明</span><span class="sxs-lookup"><span data-stu-id="c4dad-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c4dad-148">CertificateFingerprint プリント</span><span class="sxs-lookup"><span data-stu-id="c4dad-148">CertificateFingerprint</span></span> | <span data-ttu-id="c4dad-149">署名されたパッケージに署名する必要がある証明書の証明書の指紋を指定します。</span><span class="sxs-lookup"><span data-stu-id="c4dad-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="c4dad-150">証明書のフィンガープリントは、証明書のハッシュです。</span><span class="sxs-lookup"><span data-stu-id="c4dad-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="c4dad-151">このハッシュの計算に使用されるハッシュアルゴリズムは、`FingerprintAlgorithm` オプションで指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4dad-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="c4dad-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="c4dad-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="c4dad-153">証明書のフィンガープリントを計算するために使用するハッシュアルゴリズムを指定します。</span><span class="sxs-lookup"><span data-stu-id="c4dad-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="c4dad-154">既定値は `SHA256` です。</span><span class="sxs-lookup"><span data-stu-id="c4dad-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="c4dad-155">サポートされている値は、`SHA256`、`SHA384`、および `SHA512`</span><span class="sxs-lookup"><span data-stu-id="c4dad-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="c4dad-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="c4dad-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="c4dad-157">信頼された署名者の証明書を信頼されていないルートにチェーンできるようにするかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="c4dad-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="c4dad-158">nuget の信頼された署名者名の削除 \<名前\></span><span class="sxs-lookup"><span data-stu-id="c4dad-158">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="c4dad-159">指定した名前に一致する信頼された署名者を削除します。</span><span class="sxs-lookup"><span data-stu-id="c4dad-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="c4dad-160">nuget で信頼されている-署名者の同期-名前 \<名前\></span><span class="sxs-lookup"><span data-stu-id="c4dad-160">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="c4dad-161">現在信頼されているリポジトリで使用されている最新の証明書の一覧を要求して、信頼された署名者の既存の証明書の一覧を更新します。</span><span class="sxs-lookup"><span data-stu-id="c4dad-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="c4dad-162">_注_: このジェスチャは、現在の証明書の一覧を削除し、リポジトリの最新の一覧に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c4dad-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="c4dad-163">オプション</span><span class="sxs-lookup"><span data-stu-id="c4dad-163">Options</span></span>

| <span data-ttu-id="c4dad-164">オプション</span><span class="sxs-lookup"><span data-stu-id="c4dad-164">Option</span></span> | <span data-ttu-id="c4dad-165">説明</span><span class="sxs-lookup"><span data-stu-id="c4dad-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c4dad-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c4dad-166">ConfigFile</span></span> | <span data-ttu-id="c4dad-167">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="c4dad-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c4dad-168">指定しない場合は、`%AppData%\NuGet\NuGet.Config` (Windows) または `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="c4dad-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c4dad-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c4dad-169">ForceEnglishOutput</span></span> | <span data-ttu-id="c4dad-170">不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="c4dad-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c4dad-171">[Help]</span><span class="sxs-lookup"><span data-stu-id="c4dad-171">Help</span></span> | <span data-ttu-id="c4dad-172">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="c4dad-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="c4dad-173">詳細度</span><span class="sxs-lookup"><span data-stu-id="c4dad-173">Verbosity</span></span> | <span data-ttu-id="c4dad-174">出力に表示される詳細の量を指定します (*通常*、*非*表示、*詳細*)。</span><span class="sxs-lookup"><span data-stu-id="c4dad-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="c4dad-175">使用例</span><span class="sxs-lookup"><span data-stu-id="c4dad-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
