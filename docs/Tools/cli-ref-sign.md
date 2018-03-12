---
title: "NuGet CLI 記号コマンド |Microsoft ドキュメント"
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 記号コマンドのリファレンス"
keywords: "nuget 記号の参照、サインオン コマンド"
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: 109b0f6aca0ebaae2ea56fbb45226bc1b14f2ea1
ms.sourcegitcommit: df7158169e84900d135416cd5e52f937df0beb52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2018
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="99617-104">サインオン コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="99617-104">sign command (NuGet CLI)</span></span>

<span data-ttu-id="99617-105">**適用されます:**パッケージの作成&bullet;**サポートされているバージョン:** 4.6 以上</span><span class="sxs-lookup"><span data-stu-id="99617-105">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="99617-106">証明書では、最初の引数に一致するすべてのパッケージに署名します。</span><span class="sxs-lookup"><span data-stu-id="99617-106">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="99617-107">ファイルとは、サブジェクト名または拇印を提供することで、証明書ストアにインストールされている証明書から秘密キー付きの証明書を取得できます。</span><span class="sxs-lookup"><span data-stu-id="99617-107">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

<span data-ttu-id="99617-108">パッケージの署名はまだサポートされていません Mono でまたは Windows 以外のプラットフォーム。</span><span class="sxs-lookup"><span data-stu-id="99617-108">Package signing is not yet supported under Mono or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="99617-109">使用法</span><span class="sxs-lookup"><span data-stu-id="99617-109">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="99617-110">ここで`<package(s)>`は 1 つ以上`.nupkg`ファイル。</span><span class="sxs-lookup"><span data-stu-id="99617-110">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="99617-111">オプション</span><span class="sxs-lookup"><span data-stu-id="99617-111">Options</span></span>

| <span data-ttu-id="99617-112">オプション</span><span class="sxs-lookup"><span data-stu-id="99617-112">Option</span></span> | <span data-ttu-id="99617-113">説明</span><span class="sxs-lookup"><span data-stu-id="99617-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="99617-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="99617-114">CertificateFingerprint</span></span> | <span data-ttu-id="99617-115">ローカルの証明書ストア、証明書を検索するために使用する証明書の sha-1 フィンガー プリントを指定します。</span><span class="sxs-lookup"><span data-stu-id="99617-115">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span> |
| <span data-ttu-id="99617-116">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="99617-116">CertificatePassword</span></span> | <span data-ttu-id="99617-117">必要な場合は、証明書のパスワードを指定します。</span><span class="sxs-lookup"><span data-stu-id="99617-117">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="99617-118">証明書はパスワードで保護されたパスワードが指定されていない場合、コマンドはパスワードを要求、実行時にしない限り、非対話型のオプションが渡されました。</span><span class="sxs-lookup"><span data-stu-id="99617-118">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the -NonInteractive option is passed.</span></span> |
| <span data-ttu-id="99617-119">CertificatePath</span><span class="sxs-lookup"><span data-stu-id="99617-119">CertificatePath</span></span> | <span data-ttu-id="99617-120">パッケージの署名に使用する証明書へのファイル パスを指定します。</span><span class="sxs-lookup"><span data-stu-id="99617-120">Specifies the file path to the certificate to be used in signing the package.</span></span> |
| <span data-ttu-id="99617-121">CertificateStoreLocation</span><span class="sxs-lookup"><span data-stu-id="99617-121">CertificateStoreLocation</span></span> | <span data-ttu-id="99617-122">証明書を検索する X.509 証明書ストアの使用の名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="99617-122">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="99617-123">既定値は、現在のユーザーによって使用される X.509 証明書ストアである"CurrentUser"です。</span><span class="sxs-lookup"><span data-stu-id="99617-123">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="99617-124">CertificateSubjectName - または - CertificateFingerprint オプションを使用して証明書を指定する場合、このオプションを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="99617-124">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="99617-125">CertificateStoreName</span><span class="sxs-lookup"><span data-stu-id="99617-125">CertificateStoreName</span></span> | <span data-ttu-id="99617-126">使用して証明書を検索する X.509 証明書ストアの名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="99617-126">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="99617-127">既定値は"My"、個人証明書の X.509 証明書ストア。</span><span class="sxs-lookup"><span data-stu-id="99617-127">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="99617-128">CertificateSubjectName - または - CertificateFingerprint オプションを使用して証明書を指定する場合、このオプションを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="99617-128">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="99617-129">CertificateSubjectName</span><span class="sxs-lookup"><span data-stu-id="99617-129">CertificateSubjectName</span></span> | <span data-ttu-id="99617-130">ローカルの証明書ストア、証明書を検索するために使用する証明書のサブジェクト名を指定します。</span><span class="sxs-lookup"><span data-stu-id="99617-130">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="99617-131">検索では、サブジェクト名の他のサブジェクト値に関係なく、その文字列を含むすべての証明書を見つけることが指定された値を使用して、大文字と小文字の文字列比較。</span><span class="sxs-lookup"><span data-stu-id="99617-131">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="99617-132">-証明および - CertificateStoreLocation オプションでは、証明書ストアを指定できます。</span><span class="sxs-lookup"><span data-stu-id="99617-132">The certificate store can be specified by -CertificateStoreName and -CertificateStoreLocation options.</span></span> |
| <span data-ttu-id="99617-133">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="99617-133">ConfigFile</span></span> | <span data-ttu-id="99617-134">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="99617-134">The NuGet configuration file to apply.</span></span> <span data-ttu-id="99617-135">指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。</span><span class="sxs-lookup"><span data-stu-id="99617-135">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="99617-136">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="99617-136">ForceEnglishOutput</span></span> | <span data-ttu-id="99617-137">インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="99617-137">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="99617-138">HashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="99617-138">HashAlgorithm</span></span> | <span data-ttu-id="99617-139">パッケージの署名に使用するハッシュ アルゴリズム。</span><span class="sxs-lookup"><span data-stu-id="99617-139">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="99617-140">既定値は SHA256 です。</span><span class="sxs-lookup"><span data-stu-id="99617-140">Defaults to SHA256.</span></span> |
| <span data-ttu-id="99617-141">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="99617-141">Help</span></span> | <span data-ttu-id="99617-142">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="99617-142">Displays help information for the command.</span></span> |
| <span data-ttu-id="99617-143">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="99617-143">NonInteractive</span></span> | <span data-ttu-id="99617-144">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="99617-144">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="99617-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="99617-145">OutputDirectory</span></span> | <span data-ttu-id="99617-146">署名されたパッケージを保存するディレクトリを指定します。</span><span class="sxs-lookup"><span data-stu-id="99617-146">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="99617-147">既定では、元のパッケージは、署名されたパッケージによって上書きされます。</span><span class="sxs-lookup"><span data-stu-id="99617-147">By default the original package is overwritten by the signed package.</span></span> |
| <span data-ttu-id="99617-148">上書き</span><span class="sxs-lookup"><span data-stu-id="99617-148">Overwrite</span></span> | <span data-ttu-id="99617-149">かどうか、現在の署名を上書きするかを示すスイッチです。</span><span class="sxs-lookup"><span data-stu-id="99617-149">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="99617-150">既定では、パッケージが署名を既に存在する場合に、コマンドが失敗します。</span><span class="sxs-lookup"><span data-stu-id="99617-150">By default the command will fail if the package already has a signature.</span></span> |
| <span data-ttu-id="99617-151">Timestamper</span><span class="sxs-lookup"><span data-stu-id="99617-151">Timestamper</span></span> | <span data-ttu-id="99617-152">RFC 3161 タイム スタンプ サーバーの URL。</span><span class="sxs-lookup"><span data-stu-id="99617-152">URL to an RFC 3161 timestamping server.</span></span> |
| <span data-ttu-id="99617-153">TimestampHashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="99617-153">TimestampHashAlgorithm</span></span> | <span data-ttu-id="99617-154">RFC 3161 タイム スタンプ サーバーで使用されるハッシュ アルゴリズム。</span><span class="sxs-lookup"><span data-stu-id="99617-154">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="99617-155">既定値は SHA256 です。</span><span class="sxs-lookup"><span data-stu-id="99617-155">Defaults to SHA256.</span></span> |
| <span data-ttu-id="99617-156">詳細度</span><span class="sxs-lookup"><span data-stu-id="99617-156">Verbosity</span></span> | <span data-ttu-id="99617-157">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="99617-157">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="99617-158">使用例</span><span class="sxs-lookup"><span data-stu-id="99617-158">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```