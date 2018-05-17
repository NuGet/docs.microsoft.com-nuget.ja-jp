---
title: NuGet CLI 記号コマンド
description: Nuget.exe 記号コマンドのリファレンス
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7e84d794b802cfd69c785f720280fd5c022a46f6
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="9409d-103">sign コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="9409d-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="9409d-104">**適用されます:** パッケージの作成&bullet;**サポートされているバージョン:** 4.6 以上</span><span class="sxs-lookup"><span data-stu-id="9409d-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="9409d-105">証明書では、最初の引数に一致するすべてのパッケージに署名します。</span><span class="sxs-lookup"><span data-stu-id="9409d-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="9409d-106">ファイルとは、サブジェクト名または拇印を提供することで、証明書ストアにインストールされている証明書から秘密キー付きの証明書を取得できます。</span><span class="sxs-lookup"><span data-stu-id="9409d-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

<span data-ttu-id="9409d-107">パッケージの署名はまだサポートされていません、Mono で、または Windows 以外のプラットフォーム上の .NET Core で。</span><span class="sxs-lookup"><span data-stu-id="9409d-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="9409d-108">使用法</span><span class="sxs-lookup"><span data-stu-id="9409d-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="9409d-109">ここで`<package(s)>`は 1 つ以上`.nupkg`ファイル。</span><span class="sxs-lookup"><span data-stu-id="9409d-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="9409d-110">オプション</span><span class="sxs-lookup"><span data-stu-id="9409d-110">Options</span></span>

| <span data-ttu-id="9409d-111">オプション</span><span class="sxs-lookup"><span data-stu-id="9409d-111">Option</span></span> | <span data-ttu-id="9409d-112">説明</span><span class="sxs-lookup"><span data-stu-id="9409d-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9409d-113">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="9409d-113">CertificateFingerprint</span></span> | <span data-ttu-id="9409d-114">ローカルの証明書ストア、証明書を検索するために使用する証明書の sha-1 フィンガー プリントを指定します。</span><span class="sxs-lookup"><span data-stu-id="9409d-114">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span> |
| <span data-ttu-id="9409d-115">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="9409d-115">CertificatePassword</span></span> | <span data-ttu-id="9409d-116">必要な場合は、証明書のパスワードを指定します。</span><span class="sxs-lookup"><span data-stu-id="9409d-116">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="9409d-117">証明書はパスワードで保護されたパスワードが指定されていない場合、コマンドはパスワードを要求、実行時にしない限り、非対話型のオプションが渡されました。</span><span class="sxs-lookup"><span data-stu-id="9409d-117">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the -NonInteractive option is passed.</span></span> |
| <span data-ttu-id="9409d-118">CertificatePath</span><span class="sxs-lookup"><span data-stu-id="9409d-118">CertificatePath</span></span> | <span data-ttu-id="9409d-119">パッケージの署名に使用する証明書へのファイル パスを指定します。</span><span class="sxs-lookup"><span data-stu-id="9409d-119">Specifies the file path to the certificate to be used in signing the package.</span></span> |
| <span data-ttu-id="9409d-120">CertificateStoreLocation</span><span class="sxs-lookup"><span data-stu-id="9409d-120">CertificateStoreLocation</span></span> | <span data-ttu-id="9409d-121">証明書を検索する X.509 証明書ストアの使用の名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="9409d-121">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="9409d-122">既定値は、現在のユーザーによって使用される X.509 証明書ストアである"CurrentUser"です。</span><span class="sxs-lookup"><span data-stu-id="9409d-122">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="9409d-123">CertificateSubjectName - または - CertificateFingerprint オプションを使用して証明書を指定する場合、このオプションを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9409d-123">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="9409d-124">CertificateStoreName</span><span class="sxs-lookup"><span data-stu-id="9409d-124">CertificateStoreName</span></span> | <span data-ttu-id="9409d-125">使用して証明書を検索する X.509 証明書ストアの名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="9409d-125">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="9409d-126">既定値は"My"、個人証明書の X.509 証明書ストア。</span><span class="sxs-lookup"><span data-stu-id="9409d-126">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="9409d-127">CertificateSubjectName - または - CertificateFingerprint オプションを使用して証明書を指定する場合、このオプションを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9409d-127">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="9409d-128">CertificateSubjectName</span><span class="sxs-lookup"><span data-stu-id="9409d-128">CertificateSubjectName</span></span> | <span data-ttu-id="9409d-129">ローカルの証明書ストア、証明書を検索するために使用する証明書のサブジェクト名を指定します。</span><span class="sxs-lookup"><span data-stu-id="9409d-129">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="9409d-130">検索では、サブジェクト名の他のサブジェクト値に関係なく、その文字列を含むすべての証明書を見つけることが指定された値を使用して、大文字と小文字の文字列比較。</span><span class="sxs-lookup"><span data-stu-id="9409d-130">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="9409d-131">-証明および - CertificateStoreLocation オプションでは、証明書ストアを指定できます。</span><span class="sxs-lookup"><span data-stu-id="9409d-131">The certificate store can be specified by -CertificateStoreName and -CertificateStoreLocation options.</span></span> |
| <span data-ttu-id="9409d-132">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="9409d-132">ConfigFile</span></span> | <span data-ttu-id="9409d-133">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="9409d-133">The NuGet configuration file to apply.</span></span> <span data-ttu-id="9409d-134">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="9409d-134">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="9409d-135">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="9409d-135">ForceEnglishOutput</span></span> | <span data-ttu-id="9409d-136">インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="9409d-136">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="9409d-137">HashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="9409d-137">HashAlgorithm</span></span> | <span data-ttu-id="9409d-138">パッケージの署名に使用するハッシュ アルゴリズム。</span><span class="sxs-lookup"><span data-stu-id="9409d-138">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="9409d-139">既定値は SHA256 です。</span><span class="sxs-lookup"><span data-stu-id="9409d-139">Defaults to SHA256.</span></span> |
| <span data-ttu-id="9409d-140">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="9409d-140">Help</span></span> | <span data-ttu-id="9409d-141">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="9409d-141">Displays help information for the command.</span></span> |
| <span data-ttu-id="9409d-142">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="9409d-142">NonInteractive</span></span> | <span data-ttu-id="9409d-143">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="9409d-143">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="9409d-144">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="9409d-144">OutputDirectory</span></span> | <span data-ttu-id="9409d-145">署名されたパッケージを保存するディレクトリを指定します。</span><span class="sxs-lookup"><span data-stu-id="9409d-145">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="9409d-146">既定では、元のパッケージは、署名されたパッケージによって上書きされます。</span><span class="sxs-lookup"><span data-stu-id="9409d-146">By default the original package is overwritten by the signed package.</span></span> |
| <span data-ttu-id="9409d-147">上書き</span><span class="sxs-lookup"><span data-stu-id="9409d-147">Overwrite</span></span> | <span data-ttu-id="9409d-148">かどうか、現在の署名を上書きするかを示すスイッチです。</span><span class="sxs-lookup"><span data-stu-id="9409d-148">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="9409d-149">既定では、パッケージが署名を既に存在する場合に、コマンドが失敗します。</span><span class="sxs-lookup"><span data-stu-id="9409d-149">By default the command will fail if the package already has a signature.</span></span> |
| <span data-ttu-id="9409d-150">Timestamper</span><span class="sxs-lookup"><span data-stu-id="9409d-150">Timestamper</span></span> | <span data-ttu-id="9409d-151">RFC 3161 タイム スタンプ サーバーの URL。</span><span class="sxs-lookup"><span data-stu-id="9409d-151">URL to an RFC 3161 timestamping server.</span></span> |
| <span data-ttu-id="9409d-152">TimestampHashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="9409d-152">TimestampHashAlgorithm</span></span> | <span data-ttu-id="9409d-153">RFC 3161 タイム スタンプ サーバーで使用されるハッシュ アルゴリズム。</span><span class="sxs-lookup"><span data-stu-id="9409d-153">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="9409d-154">既定値は SHA256 です。</span><span class="sxs-lookup"><span data-stu-id="9409d-154">Defaults to SHA256.</span></span> |
| <span data-ttu-id="9409d-155">詳細度</span><span class="sxs-lookup"><span data-stu-id="9409d-155">Verbosity</span></span> | <span data-ttu-id="9409d-156">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="9409d-156">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="9409d-157">使用例</span><span class="sxs-lookup"><span data-stu-id="9409d-157">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```