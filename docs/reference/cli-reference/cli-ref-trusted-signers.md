---
title: NuGet CLI trusted-signers コマンド
description: nuget.exe trusted-signers コマンドのリファレンス
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: a5f3564af8b96dfa673d2252aea2e77a79c184a4
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323591"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="62cd6-103">trusted-signers コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="62cd6-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="62cd6-104">**適用対象: パッケージ** 消費量 &bullet; **サポートされているバージョン:** 4.9.1 以上</span><span class="sxs-lookup"><span data-stu-id="62cd6-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="62cd6-105">信頼された署名者を NuGet 構成に対して取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="62cd6-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="62cd6-106">その他の使用方法については、「 [一般的な NuGet 構成」を参照してください](../../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="62cd6-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="62cd6-107">スキーマの構成方法nuget.configについては、NuGet 構成ファイルの [リファレンスを参照してください](../nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="62cd6-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="62cd6-108">使用方法</span><span class="sxs-lookup"><span data-stu-id="62cd6-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="62cd6-109">が指定されていない `list|add|remove|sync` 場合、コマンドは既定で になります `list` 。</span><span class="sxs-lookup"><span data-stu-id="62cd6-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="62cd6-110">nuget trusted-signers list</span><span class="sxs-lookup"><span data-stu-id="62cd6-110">nuget trusted-signers list</span></span>

<span data-ttu-id="62cd6-111">構成内のすべての信頼された署名者を一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="62cd6-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="62cd6-112">このオプションには、各署名者が持つすべての証明書 (指紋と指紋アルゴリズムを使用) が含まれます。</span><span class="sxs-lookup"><span data-stu-id="62cd6-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="62cd6-113">証明書に が先行する がある場合 `[U]` は、証明書エントリが に設定 `allowUntrustedRoot` されています `true` 。</span><span class="sxs-lookup"><span data-stu-id="62cd6-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="62cd6-114">このコマンドからの出力例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="62cd6-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D
        SHA256 - 5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="62cd6-115">nuget trusted-signers add [options]</span><span class="sxs-lookup"><span data-stu-id="62cd6-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="62cd6-116">指定した名前の信頼された署名者を構成に追加します。このオプションには、信頼された作成者またはリポジトリを追加するさまざまなジェスチャがあります。</span><span class="sxs-lookup"><span data-stu-id="62cd6-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="62cd6-117">パッケージに基づいて追加するためのオプション</span><span class="sxs-lookup"><span data-stu-id="62cd6-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package> -Name <name> [options]
```

<span data-ttu-id="62cd6-118">ここで `<package>` 、 は 1 つの署名付き `.nupkg` ファイルです。</span><span class="sxs-lookup"><span data-stu-id="62cd6-118">where `<package>` is one signed `.nupkg` file.</span></span>

- **`-Author`**

  <span data-ttu-id="62cd6-119">署名付きパッケージの作成者署名を信頼する必要がある場合に指定します。</span><span class="sxs-lookup"><span data-stu-id="62cd6-119">Specifies that the author signature of the signed package should be trusted.</span></span>

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="62cd6-120">信頼された署名者の証明書を信頼されていないルートにチェーンできる必要がある場合に指定します。</span><span class="sxs-lookup"><span data-stu-id="62cd6-120">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="62cd6-121">リポジトリの信頼をさらに制限するために、信頼できる所有者のセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="62cd6-121">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="62cd6-122">オプションを使用する場合 `-Repository` にのみ有効です。</span><span class="sxs-lookup"><span data-stu-id="62cd6-122">Only valid when using the `-Repository` option.</span></span>

- **`-Repository`**

  <span data-ttu-id="62cd6-123">署名されたパッケージのリポジトリの署名または署名を信頼する必要がある場合に指定します。</span><span class="sxs-lookup"><span data-stu-id="62cd6-123">Specifies that the repository signature or countersignature of the signed package should be trusted.</span></span>

<span data-ttu-id="62cd6-124">と `-Author` の `-Repository` 両方を同時に指定する機能はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="62cd6-124">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="62cd6-125">サービス インデックスに基づいて追加するためのオプション</span><span class="sxs-lookup"><span data-stu-id="62cd6-125">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="62cd6-126">_注_: このオプションでは、信頼されたリポジトリだけが追加されます。</span><span class="sxs-lookup"><span data-stu-id="62cd6-126">_Note_: This option will only add trusted repositories.</span></span> 

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="62cd6-127">信頼された署名者の証明書を信頼されていないルートにチェーンできる必要がある場合に指定します。</span><span class="sxs-lookup"><span data-stu-id="62cd6-127">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="62cd6-128">リポジトリの信頼をさらに制限するために、信頼できる所有者のセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="62cd6-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span>

- **`-ServiceIndex`**

  <span data-ttu-id="62cd6-129">信頼されるリポジトリの V3 サービス インデックスを指定します。</span><span class="sxs-lookup"><span data-stu-id="62cd6-129">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="62cd6-130">このリポジトリは、リポジトリ署名リソースをサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="62cd6-130">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="62cd6-131">指定しない場合、コマンドは同じパッケージ ソースを検索し、そこから `-Name` サービス インデックスを取得します。</span><span class="sxs-lookup"><span data-stu-id="62cd6-131">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span>

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="62cd6-132">証明書情報に基づいて追加するためのオプション</span><span class="sxs-lookup"><span data-stu-id="62cd6-132">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="62cd6-133">_注_: 指定した名前の信頼された署名者が既に存在する場合は、その署名者に証明書項目が追加されます。</span><span class="sxs-lookup"><span data-stu-id="62cd6-133">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="62cd6-134">それ以外の場合、信頼された作成者は、指定された証明書情報の証明書項目を使用して作成されます。</span><span class="sxs-lookup"><span data-stu-id="62cd6-134">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>


- **`-AllowUntrustedRoot`**

  <span data-ttu-id="62cd6-135">信頼された署名者の証明書を信頼されていないルートにチェーンできる必要がある場合に指定します。</span><span class="sxs-lookup"><span data-stu-id="62cd6-135">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="62cd6-136">署名済みパッケージに署名する必要がある証明書の証明書フィンガープリントを指定します。</span><span class="sxs-lookup"><span data-stu-id="62cd6-136">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="62cd6-137">証明書のフィンガープリントは、証明書のハッシュです。</span><span class="sxs-lookup"><span data-stu-id="62cd6-137">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="62cd6-138">このハッシュの計算に使用するハッシュ アルゴリズムは、 オプションで 指定する必要 `FingerprintAlgorithm` があります。</span><span class="sxs-lookup"><span data-stu-id="62cd6-138">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span>

- **`-FingerprintAlgorithm`**

  <span data-ttu-id="62cd6-139">証明書のフィンガープリントの計算に使用するハッシュ アルゴリズムを指定します。</span><span class="sxs-lookup"><span data-stu-id="62cd6-139">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="62cd6-140">既定値は `SHA256` です。</span><span class="sxs-lookup"><span data-stu-id="62cd6-140">Defaults to `SHA256`.</span></span> <span data-ttu-id="62cd6-141">サポートされている値は `SHA256` 、、 `SHA384` および です `SHA512` 。</span><span class="sxs-lookup"><span data-stu-id="62cd6-141">Values supported are `SHA256`, `SHA384` and `SHA512`.</span></span>

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="62cd6-142">nuget trusted-signers remove -Name \<name\></span><span class="sxs-lookup"><span data-stu-id="62cd6-142">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="62cd6-143">指定した名前に一致する信頼できる署名者を削除します。</span><span class="sxs-lookup"><span data-stu-id="62cd6-143">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="62cd6-144">nuget trusted-signers sync -Name \<name\></span><span class="sxs-lookup"><span data-stu-id="62cd6-144">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="62cd6-145">現在信頼されているリポジトリで使用されている証明書の最新の一覧を要求して、信頼された署名者の既存の証明書リストを更新します。</span><span class="sxs-lookup"><span data-stu-id="62cd6-145">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="62cd6-146">_注_: このジェスチャでは、証明書の現在の一覧が削除され、リポジトリから最新のリストに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="62cd6-146">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="62cd6-147">オプション</span><span class="sxs-lookup"><span data-stu-id="62cd6-147">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="62cd6-148">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="62cd6-148">The NuGet configuration file to apply.</span></span> <span data-ttu-id="62cd6-149">指定しない場合は `%AppData%\NuGet\NuGet.Config` 、(Windows)、 `~/.nuget/NuGet/NuGet.Config` または `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="62cd6-149">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="62cd6-150">インnuget.exe英語ベースのカルチャを使用して、強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="62cd6-150">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="62cd6-151">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="62cd6-151">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="62cd6-152">信頼された署名者の名前。</span><span class="sxs-lookup"><span data-stu-id="62cd6-152">Name of the trusted signer.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="62cd6-153">ユーザー入力または確認のプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="62cd6-153">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="62cd6-154">出力に表示される詳細の量 (既定値 `normal` )、、または `quiet` を指定します `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="62cd6-154">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


## <a name="examples"></a><span data-ttu-id="62cd6-155">使用例</span><span class="sxs-lookup"><span data-stu-id="62cd6-155">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget trusted-signers Remove -Name TrustedRepo

nuget trusted-signers Sync -Name TrustedRepo
```
