---
title: NuGet CLI 信頼-署名者コマンド
description: nuget.exe 信頼された署名者コマンドのリファレンス
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9e25f439617a76d30880bea3c10a5d063e681a41
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238154"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="2bf4a-103">trusted-署名者コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2bf4a-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="2bf4a-104">**適用対象:** パッケージ消費が &bullet; **サポートされているバージョン:** 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="2bf4a-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="2bf4a-105">NuGet 構成に対する信頼された署名者を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="2bf4a-106">その他の使用方法については、「 [Common NuGet の構成](../../consume-packages/configuring-nuget-behavior.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="2bf4a-107">nuget.config スキーマの外観の詳細については、 [NuGet 構成ファイルのリファレンス](../nuget-config-file.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="2bf4a-108">使用</span><span class="sxs-lookup"><span data-stu-id="2bf4a-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="2bf4a-109">`list|add|remove|sync`が指定されていない場合、コマンドは既定でに設定され `list` ます。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="2bf4a-110">nuget の信頼された署名者リスト</span><span class="sxs-lookup"><span data-stu-id="2bf4a-110">nuget trusted-signers list</span></span>

<span data-ttu-id="2bf4a-111">構成内のすべての信頼された署名者を一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="2bf4a-112">このオプションには、各署名者が持つすべての証明書 (指紋および指紋アルゴリズム) が含まれます。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="2bf4a-113">証明書に前のが含まれている場合は `[U]` 、証明書エントリがとして設定されていることを意味し `allowUntrustedRoot` `true` ます。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="2bf4a-114">このコマンドからの出力例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-114">Below is an example output from this command:</span></span>

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
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="2bf4a-115">nuget の信頼済み-署名者の追加 [オプション]</span><span class="sxs-lookup"><span data-stu-id="2bf4a-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="2bf4a-116">指定された名前の信頼された署名者を構成に追加します。このオプションでは、信頼された作成者またはリポジトリを追加するジェスチャは異なります。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="2bf4a-117">パッケージに基づいて追加するためのオプション</span><span class="sxs-lookup"><span data-stu-id="2bf4a-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="2bf4a-118">ここ `<package(s)>` で、は1つ以上の `.nupkg` ファイルです。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

- **`-Author`**

  <span data-ttu-id="2bf4a-119">パッケージの作成者の署名を信頼する必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-119">Specifies that the author signature of the package(s) should be trusted.</span></span>

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="2bf4a-120">信頼された署名者の証明書を信頼されていないルートにチェーンできるようにするかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-120">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="2bf4a-121">リポジトリの信頼をさらに制限するために、信頼された所有者のセミコロンで区切られた一覧。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-121">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="2bf4a-122">オプションを使用する場合にのみ有効です `-Repository` 。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-122">Only valid when using the `-Repository` option.</span></span>

- **`-Repository`**

  <span data-ttu-id="2bf4a-123">パッケージのリポジトリ署名または副署名を信頼する必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-123">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span>

<span data-ttu-id="2bf4a-124">`-Author`との両方を `-Repository` 同時に指定することはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-124">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="2bf4a-125">サービスインデックスに基づく追加のオプション</span><span class="sxs-lookup"><span data-stu-id="2bf4a-125">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="2bf4a-126">_注_ : このオプションでは、信頼されたリポジトリのみが追加されます。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-126">_Note_ : This option will only add trusted repositories.</span></span> 

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="2bf4a-127">信頼された署名者の証明書を信頼されていないルートにチェーンできるようにするかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-127">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="2bf4a-128">リポジトリの信頼をさらに制限するために、信頼された所有者のセミコロンで区切られた一覧。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span>

- **`-ServiceIndex`**

  <span data-ttu-id="2bf4a-129">信頼されるリポジトリの V3 サービスインデックスを指定します。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-129">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="2bf4a-130">このリポジトリは、リポジトリ署名リソースをサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-130">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="2bf4a-131">指定されていない場合、コマンドは同じを持つパッケージソースを検索 `-Name` し、そこからサービスインデックスを取得します。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-131">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span>

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="2bf4a-132">証明書情報に基づいて追加するオプション</span><span class="sxs-lookup"><span data-stu-id="2bf4a-132">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="2bf4a-133">_注_ : 指定した名前の信頼された署名者が既に存在する場合、その署名者に証明書項目が追加されます。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-133">_Note_ : If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="2bf4a-134">それ以外の場合、信頼できる作成者は、指定された証明書情報から証明書項目を使用して作成されます。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-134">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>


- **`-AllowUntrustedRoot`**

  <span data-ttu-id="2bf4a-135">信頼された署名者の証明書を信頼されていないルートにチェーンできるようにするかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-135">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="2bf4a-136">署名されたパッケージに署名する必要がある証明書の証明書の指紋を指定します。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-136">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="2bf4a-137">証明書のフィンガープリントは、証明書のハッシュです。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-137">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="2bf4a-138">このハッシュの計算に使用されるハッシュアルゴリズムは、オプションで指定する必要があり `FingerprintAlgorithm` ます。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-138">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span>

- **`-FingerprintAlgorithm`**

  <span data-ttu-id="2bf4a-139">証明書のフィンガープリントを計算するために使用するハッシュアルゴリズムを指定します。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-139">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="2bf4a-140">既定値は `SHA256` です。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-140">Defaults to `SHA256`.</span></span> <span data-ttu-id="2bf4a-141">サポートされる値は `SHA256` 、、 `SHA384` および `SHA512` です。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-141">Values supported are `SHA256`, `SHA384` and `SHA512`.</span></span>

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="2bf4a-142">nuget の信頼された署名者の名前の削除 \<name\></span><span class="sxs-lookup"><span data-stu-id="2bf4a-142">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="2bf4a-143">指定した名前に一致する信頼された署名者を削除します。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-143">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="2bf4a-144">nuget 信頼-署名者同期名 \<name\></span><span class="sxs-lookup"><span data-stu-id="2bf4a-144">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="2bf4a-145">現在信頼されているリポジトリで使用されている最新の証明書の一覧を要求して、信頼された署名者の既存の証明書の一覧を更新します。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-145">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="2bf4a-146">_注_ : このジェスチャは、現在の証明書の一覧を削除し、リポジトリの最新の一覧に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-146">_Note_ : This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="2bf4a-147">オプション</span><span class="sxs-lookup"><span data-stu-id="2bf4a-147">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="2bf4a-148">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-148">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2bf4a-149">指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-149">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="2bf4a-150">不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-150">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="2bf4a-151">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-151">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="2bf4a-152">信頼された署名者の名前。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-152">Name of the trusted signer.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="2bf4a-153">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-153">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="2bf4a-154">出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。</span><span class="sxs-lookup"><span data-stu-id="2bf4a-154">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


## <a name="examples"></a><span data-ttu-id="2bf4a-155">使用例</span><span class="sxs-lookup"><span data-stu-id="2bf4a-155">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
