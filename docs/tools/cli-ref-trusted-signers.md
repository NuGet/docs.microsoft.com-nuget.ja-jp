---
title: 信頼された署名の NuGet CLI コマンド
description: Nuget.exe の信頼された署名コマンドのリファレンス
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: ee4ffaa7e250cdbf313476fd794a8d87c80b69f9
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324709"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="9dea8-103">信頼された署名コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="9dea8-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="9dea8-104">**適用対象:** 消費をパッケージ化&bullet;**サポートされているバージョン。** 4.9.1+</span><span class="sxs-lookup"><span data-stu-id="9dea8-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="9dea8-105">取得または信頼できる署名者を NuGet の構成に設定します。</span><span class="sxs-lookup"><span data-stu-id="9dea8-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="9dea8-106">追加の使用状況は、[NuGet の動作を構成する](../consume-packages/configuring-nuget-behavior.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9dea8-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="9dea8-107">詳細についてを参照するくださいと同様の nuget.config スキーマの外観に、 [NuGet 構成ファイル リファレンス](../reference/nuget-config-file.md)します。</span><span class="sxs-lookup"><span data-stu-id="9dea8-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="9dea8-108">使用法</span><span class="sxs-lookup"><span data-stu-id="9dea8-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="9dea8-109">none の場合`list|add|remove|sync`を指定すると、コマンドは、既定値は`list`します。</span><span class="sxs-lookup"><span data-stu-id="9dea8-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="9dea8-110">nuget の信頼された署名の一覧</span><span class="sxs-lookup"><span data-stu-id="9dea8-110">nuget trusted-signers list</span></span>

<span data-ttu-id="9dea8-111">構成で信頼できる署名者をすべて一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="9dea8-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="9dea8-112">このオプションには、すべての証明書にが含まれます (指紋と指紋アルゴリズム) を持つ各署名者が。</span><span class="sxs-lookup"><span data-stu-id="9dea8-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="9dea8-113">証明書がある先行場合`[U]`、証明書のエントリがあることを意味`allowUntrustedRoot`として設定`true`します。</span><span class="sxs-lookup"><span data-stu-id="9dea8-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="9dea8-114">このコマンドからの出力例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="9dea8-114">Below is an example output from this command:</span></span>

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

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="9dea8-115">nuget trusted-signers add [options]</span><span class="sxs-lookup"><span data-stu-id="9dea8-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="9dea8-116">構成には、指定した名前の信頼できる署名者を追加します。このオプションは、信頼された作成者またはリポジトリを追加するさまざまなジェスチャです。</span><span class="sxs-lookup"><span data-stu-id="9dea8-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="9dea8-117">パッケージに基づく追加のオプション</span><span class="sxs-lookup"><span data-stu-id="9dea8-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="9dea8-118">場所`<package(s)>`は 1 つ以上`.nupkg`ファイル。</span><span class="sxs-lookup"><span data-stu-id="9dea8-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="9dea8-119">オプション</span><span class="sxs-lookup"><span data-stu-id="9dea8-119">Option</span></span> | <span data-ttu-id="9dea8-120">説明</span><span class="sxs-lookup"><span data-stu-id="9dea8-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9dea8-121">作成者</span><span class="sxs-lookup"><span data-stu-id="9dea8-121">Author</span></span> | <span data-ttu-id="9dea8-122">パッケージの作成者の署名が信頼があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="9dea8-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="9dea8-123">リポジトリ</span><span class="sxs-lookup"><span data-stu-id="9dea8-123">Repository</span></span> | <span data-ttu-id="9dea8-124">リポジトリの署名またはパッケージの副署名する必要がありますが信頼できることを指定します。</span><span class="sxs-lookup"><span data-stu-id="9dea8-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="9dea8-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="9dea8-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="9dea8-126">信頼されていないルートにチェーンを信頼できる署名者の証明書を許可するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="9dea8-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="9dea8-127">所有者</span><span class="sxs-lookup"><span data-stu-id="9dea8-127">Owners</span></span> | <span data-ttu-id="9dea8-128">さらに、リポジトリの信頼を制限する信頼された所有者のセミコロンで区切られたリスト。</span><span class="sxs-lookup"><span data-stu-id="9dea8-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="9dea8-129">使用する場合にのみ有効です、`-Repository`オプション。</span><span class="sxs-lookup"><span data-stu-id="9dea8-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="9dea8-130">両方を提供する`-Author`と`-Repository`と同時にはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="9dea8-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="9dea8-131">サービス インデックスに基づいて追加のオプション</span><span class="sxs-lookup"><span data-stu-id="9dea8-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="9dea8-132">_注_:このオプションは、信頼されているリポジトリをのみ追加されます。</span><span class="sxs-lookup"><span data-stu-id="9dea8-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="9dea8-133">オプション</span><span class="sxs-lookup"><span data-stu-id="9dea8-133">Option</span></span> | <span data-ttu-id="9dea8-134">説明</span><span class="sxs-lookup"><span data-stu-id="9dea8-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9dea8-135">ServiceIndex</span><span class="sxs-lookup"><span data-stu-id="9dea8-135">ServiceIndex</span></span> | <span data-ttu-id="9dea8-136">信頼できるリポジトリの V3 サービス インデックスを指定します。</span><span class="sxs-lookup"><span data-stu-id="9dea8-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="9dea8-137">このリポジトリは、リポジトリのリソースの署名をサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="9dea8-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="9dea8-138">コマンドが同じパッケージのソースを探して指定しない場合、`-Name`し、そこからサービス インデックスを取得します。</span><span class="sxs-lookup"><span data-stu-id="9dea8-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="9dea8-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="9dea8-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="9dea8-140">信頼されていないルートにチェーンを信頼できる署名者の証明書を許可するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="9dea8-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="9dea8-141">所有者</span><span class="sxs-lookup"><span data-stu-id="9dea8-141">Owners</span></span> | <span data-ttu-id="9dea8-142">さらに、リポジトリの信頼を制限する信頼された所有者のセミコロンで区切られたリスト。</span><span class="sxs-lookup"><span data-stu-id="9dea8-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="9dea8-143">証明書情報に基づいて追加のオプション</span><span class="sxs-lookup"><span data-stu-id="9dea8-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="9dea8-144">_注_:指定した名前の信頼できる署名者が既に存在する場合、証明書の項目はその署名者に追加されます。</span><span class="sxs-lookup"><span data-stu-id="9dea8-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="9dea8-145">証明書の項目で、信頼された作成者が作成されますそれ以外の場合から証明書の情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="9dea8-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="9dea8-146">オプション</span><span class="sxs-lookup"><span data-stu-id="9dea8-146">Option</span></span> | <span data-ttu-id="9dea8-147">説明</span><span class="sxs-lookup"><span data-stu-id="9dea8-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9dea8-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="9dea8-148">CertificateFingerprint</span></span> | <span data-ttu-id="9dea8-149">パッケージの署名証明書の指紋を署名する必要があります証明書を指定します。</span><span class="sxs-lookup"><span data-stu-id="9dea8-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="9dea8-150">証明書フィンガー プリントは、証明書のハッシュです。</span><span class="sxs-lookup"><span data-stu-id="9dea8-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="9dea8-151">このハッシュは計算に使用されるハッシュ アルゴリズムを指定します、`FingerprintAlgorithm`オプション。</span><span class="sxs-lookup"><span data-stu-id="9dea8-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="9dea8-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="9dea8-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="9dea8-153">証明書フィンガー プリントを計算するために使用するハッシュ アルゴリズムを指定します。</span><span class="sxs-lookup"><span data-stu-id="9dea8-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="9dea8-154">既定値は `SHA256` です。</span><span class="sxs-lookup"><span data-stu-id="9dea8-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="9dea8-155">サポートされている値は`SHA256`、`SHA384`と `SHA512`</span><span class="sxs-lookup"><span data-stu-id="9dea8-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="9dea8-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="9dea8-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="9dea8-157">信頼されていないルートにチェーンを信頼できる署名者の証明書を許可するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="9dea8-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="9dea8-158">nuget 信頼された署名の削除 - 名前 <name></span><span class="sxs-lookup"><span data-stu-id="9dea8-158">nuget trusted-signers remove -Name <name></span></span>

<span data-ttu-id="9dea8-159">指定した名前に一致する任意の信頼できる署名者を削除します。</span><span class="sxs-lookup"><span data-stu-id="9dea8-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="9dea8-160">nuget 信頼された署名は、次の同期 - 名前 <name></span><span class="sxs-lookup"><span data-stu-id="9dea8-160">nuget trusted-signers sync -Name <name></span></span>

<span data-ttu-id="9dea8-161">最新のリストを更新する現在の信頼されたリポジトリで使用される証明書を要求する、信頼できる署名者の既存の証明書のリスト。</span><span class="sxs-lookup"><span data-stu-id="9dea8-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="9dea8-162">_注_:このジェスチャは現在の証明書の一覧を削除し、リポジトリから最新の一覧に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="9dea8-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="9dea8-163">オプション</span><span class="sxs-lookup"><span data-stu-id="9dea8-163">Options</span></span>

| <span data-ttu-id="9dea8-164">オプション</span><span class="sxs-lookup"><span data-stu-id="9dea8-164">Option</span></span> | <span data-ttu-id="9dea8-165">説明</span><span class="sxs-lookup"><span data-stu-id="9dea8-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9dea8-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="9dea8-166">ConfigFile</span></span> | <span data-ttu-id="9dea8-167">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="9dea8-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="9dea8-168">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="9dea8-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="9dea8-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="9dea8-169">ForceEnglishOutput</span></span> | <span data-ttu-id="9dea8-170">インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="9dea8-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="9dea8-171">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="9dea8-171">Help</span></span> | <span data-ttu-id="9dea8-172">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="9dea8-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="9dea8-173">詳細度</span><span class="sxs-lookup"><span data-stu-id="9dea8-173">Verbosity</span></span> | <span data-ttu-id="9dea8-174">出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。</span><span class="sxs-lookup"><span data-stu-id="9dea8-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="9dea8-175">使用例</span><span class="sxs-lookup"><span data-stu-id="9dea8-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
