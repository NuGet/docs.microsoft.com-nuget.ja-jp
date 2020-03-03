---
title: NuGet CLI sign コマンド
description: Nuget.exe sign コマンドのリファレンス
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e596fd5eb3de8ca4802d9b7b8e7cb623568e3dcb
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231124"
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="511c5-103">NuGet CLI sign コマンド</span><span class="sxs-lookup"><span data-stu-id="511c5-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="511c5-104">**適用対象:** パッケージ作成 &bullet;**サポートされているバージョン:** 4.6 以降</span><span class="sxs-lookup"><span data-stu-id="511c5-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="511c5-105">最初の引数に一致するすべてのパッケージに証明書を署名します。</span><span class="sxs-lookup"><span data-stu-id="511c5-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="511c5-106">秘密キーを持つ証明書は、サブジェクト名または拇印を指定することによって、ファイルまたは証明書ストアにインストールされている証明書から取得できます。</span><span class="sxs-lookup"><span data-stu-id="511c5-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

> [!Note]
> <span data-ttu-id="511c5-107">パッケージの署名は、.NET Core、Mono、または Windows 以外のプラットフォームではまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="511c5-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="511c5-108">使用法</span><span class="sxs-lookup"><span data-stu-id="511c5-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="511c5-109">ここで `<package(s)>` は1つ以上の `.nupkg` ファイルです。</span><span class="sxs-lookup"><span data-stu-id="511c5-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="511c5-110">オプション</span><span class="sxs-lookup"><span data-stu-id="511c5-110">Options</span></span>

| <span data-ttu-id="511c5-111">オプション</span><span class="sxs-lookup"><span data-stu-id="511c5-111">Option</span></span> | <span data-ttu-id="511c5-112">説明</span><span class="sxs-lookup"><span data-stu-id="511c5-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="511c5-113">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="511c5-113">CertificateFingerprint</span></span> | <span data-ttu-id="511c5-114">証明書のローカル証明書ストアの検索に使用される証明書の SHA-1 フィンガープリントを指定します。</span><span class="sxs-lookup"><span data-stu-id="511c5-114">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span> |
| <span data-ttu-id="511c5-115">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="511c5-115">CertificatePassword</span></span> | <span data-ttu-id="511c5-116">必要に応じて、証明書のパスワードを指定します。</span><span class="sxs-lookup"><span data-stu-id="511c5-116">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="511c5-117">証明書がパスワードで保護されていてもパスワードが指定されていない場合、-非対話オプションが渡されない限り、コマンドは実行時にパスワードの入力を求めます。</span><span class="sxs-lookup"><span data-stu-id="511c5-117">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the -NonInteractive option is passed.</span></span> |
| <span data-ttu-id="511c5-118">CertificatePath</span><span class="sxs-lookup"><span data-stu-id="511c5-118">CertificatePath</span></span> | <span data-ttu-id="511c5-119">パッケージへの署名に使用する証明書へのファイルパスを指定します。</span><span class="sxs-lookup"><span data-stu-id="511c5-119">Specifies the file path to the certificate to be used in signing the package.</span></span> |
| <span data-ttu-id="511c5-120">CertificateStoreLocation</span><span class="sxs-lookup"><span data-stu-id="511c5-120">CertificateStoreLocation</span></span> | <span data-ttu-id="511c5-121">証明書の検索に使用する x.509 証明書ストアの名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="511c5-121">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="511c5-122">既定値は "CurrentUser" で、現在のユーザーが使用している x.509 証明書ストアです。</span><span class="sxs-lookup"><span data-stu-id="511c5-122">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="511c5-123">CertificateSubjectName または-CertificateFingerprint プリントオプションを使用して証明書を指定する場合は、このオプションを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="511c5-123">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="511c5-124">CertificateStoreName</span><span class="sxs-lookup"><span data-stu-id="511c5-124">CertificateStoreName</span></span> | <span data-ttu-id="511c5-125">証明書の検索に使用する x.509 証明書ストアの名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="511c5-125">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="511c5-126">既定値は "My" で、個人証明書の x.509 証明書ストアです。</span><span class="sxs-lookup"><span data-stu-id="511c5-126">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="511c5-127">CertificateSubjectName または-CertificateFingerprint プリントオプションを使用して証明書を指定する場合は、このオプションを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="511c5-127">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="511c5-128">CertificateSubjectName</span><span class="sxs-lookup"><span data-stu-id="511c5-128">CertificateSubjectName</span></span> | <span data-ttu-id="511c5-129">証明書のローカル証明書ストアの検索に使用する証明書のサブジェクト名を指定します。</span><span class="sxs-lookup"><span data-stu-id="511c5-129">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="511c5-130">検索は、指定された値を使用して、大文字と小文字を区別せずに文字列を比較します。これにより、他のサブジェクト値に関係なく、その文字列を含むサブジェクト名を持つすべての証明書が検索されます。</span><span class="sxs-lookup"><span data-stu-id="511c5-130">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="511c5-131">証明書ストアは、-証明オプションと-CertificateStoreLocation オプションで指定できます。</span><span class="sxs-lookup"><span data-stu-id="511c5-131">The certificate store can be specified by -CertificateStoreName and -CertificateStoreLocation options.</span></span> |
| <span data-ttu-id="511c5-132">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="511c5-132">ConfigFile</span></span> | <span data-ttu-id="511c5-133">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="511c5-133">The NuGet configuration file to apply.</span></span> <span data-ttu-id="511c5-134">指定しない場合は、`%AppData%\NuGet\NuGet.Config` (Windows) または `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="511c5-134">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="511c5-135">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="511c5-135">ForceEnglishOutput</span></span> | <span data-ttu-id="511c5-136">不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="511c5-136">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="511c5-137">HashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="511c5-137">HashAlgorithm</span></span> | <span data-ttu-id="511c5-138">パッケージの署名に使用するハッシュアルゴリズム。</span><span class="sxs-lookup"><span data-stu-id="511c5-138">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="511c5-139">既定値は SHA256 です。</span><span class="sxs-lookup"><span data-stu-id="511c5-139">Defaults to SHA256.</span></span> <span data-ttu-id="511c5-140">指定できる値は SHA256、SHA384、および SHA512 です。</span><span class="sxs-lookup"><span data-stu-id="511c5-140">Possible values are SHA256, SHA384, and SHA512.</span></span> |
| <span data-ttu-id="511c5-141">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="511c5-141">Help</span></span> | <span data-ttu-id="511c5-142">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="511c5-142">Displays help information for the command.</span></span> |
| <span data-ttu-id="511c5-143">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="511c5-143">NonInteractive</span></span> | <span data-ttu-id="511c5-144">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="511c5-144">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="511c5-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="511c5-145">OutputDirectory</span></span> | <span data-ttu-id="511c5-146">署名されたパッケージを保存するディレクトリを指定します。</span><span class="sxs-lookup"><span data-stu-id="511c5-146">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="511c5-147">既定では、元のパッケージは署名付きパッケージによって上書きされます。</span><span class="sxs-lookup"><span data-stu-id="511c5-147">By default the original package is overwritten by the signed package.</span></span> |
| <span data-ttu-id="511c5-148">上書き</span><span class="sxs-lookup"><span data-stu-id="511c5-148">Overwrite</span></span> | <span data-ttu-id="511c5-149">現在の署名を上書きするかどうかを示すには、を切り替えます。</span><span class="sxs-lookup"><span data-stu-id="511c5-149">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="511c5-150">既定では、パッケージに既に署名がある場合、コマンドは失敗します。</span><span class="sxs-lookup"><span data-stu-id="511c5-150">By default the command will fail if the package already has a signature.</span></span> |
| <span data-ttu-id="511c5-151">Timestamper</span><span class="sxs-lookup"><span data-stu-id="511c5-151">Timestamper</span></span> | <span data-ttu-id="511c5-152">RFC 3161 タイムスタンプサーバーの URL。</span><span class="sxs-lookup"><span data-stu-id="511c5-152">URL to an RFC 3161 timestamping server.</span></span> |
| <span data-ttu-id="511c5-153">TimestampHashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="511c5-153">TimestampHashAlgorithm</span></span> | <span data-ttu-id="511c5-154">RFC 3161 タイムスタンプサーバーによって使用されるハッシュアルゴリズム。</span><span class="sxs-lookup"><span data-stu-id="511c5-154">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="511c5-155">既定値は SHA256 です。</span><span class="sxs-lookup"><span data-stu-id="511c5-155">Defaults to SHA256.</span></span> |
| <span data-ttu-id="511c5-156">詳細度</span><span class="sxs-lookup"><span data-stu-id="511c5-156">Verbosity</span></span> | <span data-ttu-id="511c5-157">出力に表示される詳細の量を指定します (*通常*、*非*表示、*詳細*)。</span><span class="sxs-lookup"><span data-stu-id="511c5-157">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="511c5-158">例</span><span class="sxs-lookup"><span data-stu-id="511c5-158">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
