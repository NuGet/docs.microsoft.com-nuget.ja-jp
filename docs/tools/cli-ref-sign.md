---
title: 記号の NuGet CLI コマンド
description: Nuget.exe のサインオン コマンドのリファレンス
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546364"
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="4d9b0-103">sign コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="4d9b0-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="4d9b0-104">**適用対象:** パッケージの作成&bullet;**サポートされているバージョン:** 4.6 以降</span><span class="sxs-lookup"><span data-stu-id="4d9b0-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="4d9b0-105">証明書では、最初の引数に一致するすべてのパッケージに署名します。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="4d9b0-106">ファイルから、またはサブジェクト名または拇印を提供することで、証明書ストアにインストールされている証明書から秘密キーで証明書を取得できます。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

<span data-ttu-id="4d9b0-107">パッケージの署名はまだサポートされていませんで .NET Core、Mono、または Windows 以外のプラットフォームで。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="4d9b0-108">使用法</span><span class="sxs-lookup"><span data-stu-id="4d9b0-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="4d9b0-109">場所`<package(s)>`は 1 つ以上`.nupkg`ファイル。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="4d9b0-110">オプション</span><span class="sxs-lookup"><span data-stu-id="4d9b0-110">Options</span></span>

| <span data-ttu-id="4d9b0-111">オプション</span><span class="sxs-lookup"><span data-stu-id="4d9b0-111">Option</span></span> | <span data-ttu-id="4d9b0-112">説明</span><span class="sxs-lookup"><span data-stu-id="4d9b0-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4d9b0-113">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="4d9b0-113">CertificateFingerprint</span></span> | <span data-ttu-id="4d9b0-114">証明書のローカル証明書ストアを検索するために使用する証明書の sha-1 で指紋を指定します。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-114">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span> |
| <span data-ttu-id="4d9b0-115">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="4d9b0-115">CertificatePassword</span></span> | <span data-ttu-id="4d9b0-116">必要な場合は、証明書のパスワードを指定します。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-116">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="4d9b0-117">証明書がパスワードで保護されたパスワードが指定されていない場合、コマンドはパスワードを要求、実行時にしない限り、非対話型のオプションが渡されます。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-117">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the -NonInteractive option is passed.</span></span> |
| <span data-ttu-id="4d9b0-118">CertificatePath</span><span class="sxs-lookup"><span data-stu-id="4d9b0-118">CertificatePath</span></span> | <span data-ttu-id="4d9b0-119">パッケージの署名に使用される証明書へのファイル パスを指定します。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-119">Specifies the file path to the certificate to be used in signing the package.</span></span> |
| <span data-ttu-id="4d9b0-120">CertificateStoreLocation</span><span class="sxs-lookup"><span data-stu-id="4d9b0-120">CertificateStoreLocation</span></span> | <span data-ttu-id="4d9b0-121">証明書を検索する X.509 証明書ストアの使用の名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-121">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="4d9b0-122">既定値は"CurrentUser"、現在のユーザーによって使用される X.509 証明書ストアです。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-122">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="4d9b0-123">CertificateSubjectName - または - CertificateFingerprint オプションを使用して証明書を指定するときに、このオプションを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-123">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="4d9b0-124">CertificateStoreName</span><span class="sxs-lookup"><span data-stu-id="4d9b0-124">CertificateStoreName</span></span> | <span data-ttu-id="4d9b0-125">使用して証明書を検索する X.509 証明書ストアの名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-125">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="4d9b0-126">"My"、個人用証明書の X.509 証明書ストアに既定値です。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-126">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="4d9b0-127">CertificateSubjectName - または - CertificateFingerprint オプションを使用して証明書を指定するときに、このオプションを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-127">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="4d9b0-128">CertificateSubjectName</span><span class="sxs-lookup"><span data-stu-id="4d9b0-128">CertificateSubjectName</span></span> | <span data-ttu-id="4d9b0-129">証明書のローカル証明書ストアを検索するために使用する証明書のサブジェクト名を指定します。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-129">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="4d9b0-130">検索では、サブジェクト名の他のサブジェクト値に関係なく、その文字列を含むすべての証明書を検索、指定された値を使用して、大文字の文字列比較。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-130">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="4d9b0-131">-CertificateStoreName および - CertificateStoreLocation オプションでは、証明書ストアを指定できます。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-131">The certificate store can be specified by -CertificateStoreName and -CertificateStoreLocation options.</span></span> |
| <span data-ttu-id="4d9b0-132">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="4d9b0-132">ConfigFile</span></span> | <span data-ttu-id="4d9b0-133">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-133">The NuGet configuration file to apply.</span></span> <span data-ttu-id="4d9b0-134">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-134">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="4d9b0-135">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4d9b0-135">ForceEnglishOutput</span></span> | <span data-ttu-id="4d9b0-136">インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-136">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4d9b0-137">HashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="4d9b0-137">HashAlgorithm</span></span> | <span data-ttu-id="4d9b0-138">パッケージの署名に使用するハッシュ アルゴリズム。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-138">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="4d9b0-139">既定値は SHA256 です。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-139">Defaults to SHA256.</span></span> |
| <span data-ttu-id="4d9b0-140">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="4d9b0-140">Help</span></span> | <span data-ttu-id="4d9b0-141">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-141">Displays help information for the command.</span></span> |
| <span data-ttu-id="4d9b0-142">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="4d9b0-142">NonInteractive</span></span> | <span data-ttu-id="4d9b0-143">ユーザー入力や確認のプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-143">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="4d9b0-144">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="4d9b0-144">OutputDirectory</span></span> | <span data-ttu-id="4d9b0-145">署名付きパッケージを保存するディレクトリを指定します。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-145">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="4d9b0-146">既定では、元のパッケージは署名付きパッケージによって上書きされます。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-146">By default the original package is overwritten by the signed package.</span></span> |
| <span data-ttu-id="4d9b0-147">上書き</span><span class="sxs-lookup"><span data-stu-id="4d9b0-147">Overwrite</span></span> | <span data-ttu-id="4d9b0-148">スイッチを示すかどうかは、現在の署名を上書きする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-148">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="4d9b0-149">既定では、パッケージが既に署名する場合に、コマンドが失敗します。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-149">By default the command will fail if the package already has a signature.</span></span> |
| <span data-ttu-id="4d9b0-150">Timestamper</span><span class="sxs-lookup"><span data-stu-id="4d9b0-150">Timestamper</span></span> | <span data-ttu-id="4d9b0-151">RFC 3161 タイム スタンプ サーバーの URL。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-151">URL to an RFC 3161 timestamping server.</span></span> |
| <span data-ttu-id="4d9b0-152">TimestampHashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="4d9b0-152">TimestampHashAlgorithm</span></span> | <span data-ttu-id="4d9b0-153">RFC 3161 タイム スタンプ サーバーで使用されるハッシュ アルゴリズム。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-153">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="4d9b0-154">既定値は SHA256 です。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-154">Defaults to SHA256.</span></span> |
| <span data-ttu-id="4d9b0-155">詳細度</span><span class="sxs-lookup"><span data-stu-id="4d9b0-155">Verbosity</span></span> | <span data-ttu-id="4d9b0-156">出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。</span><span class="sxs-lookup"><span data-stu-id="4d9b0-156">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="4d9b0-157">使用例</span><span class="sxs-lookup"><span data-stu-id="4d9b0-157">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```