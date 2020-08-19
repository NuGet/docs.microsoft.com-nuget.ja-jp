---
title: NuGet CLI sign コマンド
description: nuget.exe sign コマンドのリファレンス
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 84386f1752b98688f1fd34e453f5b72ae8afdd92
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622773"
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="b2cbc-103">sign コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b2cbc-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="b2cbc-104">**適用対象:** パッケージ作成で &bullet; **サポートされているバージョン:** 4.6 以降</span><span class="sxs-lookup"><span data-stu-id="b2cbc-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="b2cbc-105">最初の引数に一致するすべてのパッケージに証明書を署名します。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="b2cbc-106">秘密キーを持つ証明書は、サブジェクト名または拇印を指定することによって、ファイルまたは証明書ストアにインストールされている証明書から取得できます。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

> [!Note]
> <span data-ttu-id="b2cbc-107">パッケージの署名は、.NET Core、Mono、または Windows 以外のプラットフォームではまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="b2cbc-108">使用法</span><span class="sxs-lookup"><span data-stu-id="b2cbc-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="b2cbc-109">ここ `<package(s)>` で、は1つ以上の `.nupkg` ファイルです。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="b2cbc-110">Options</span><span class="sxs-lookup"><span data-stu-id="b2cbc-110">Options</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="b2cbc-111">証明書のローカル証明書ストアの検索に使用される証明書の SHA-1 フィンガープリントを指定します。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-111">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span>

- **`-CertificatePassword`**

  <span data-ttu-id="b2cbc-112">必要に応じて、証明書のパスワードを指定します。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-112">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="b2cbc-113">証明書がパスワードで保護されていてもパスワードが指定されていない場合、オプションが渡されない限り、コマンドは実行時にパスワードの入力を求め `-NonInteractive` ます。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-113">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the `-NonInteractive` option is passed.</span></span>

- **`-CertificatePath`**

  <span data-ttu-id="b2cbc-114">パッケージへの署名に使用する証明書へのファイルパスを指定します。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-114">Specifies the file path to the certificate to be used in signing the package.</span></span>

- **`-CertificateStoreLocation`**

  <span data-ttu-id="b2cbc-115">証明書の検索に使用する x.509 証明書ストアの名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-115">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="b2cbc-116">既定値は "CurrentUser" で、現在のユーザーが使用している x.509 証明書ストアです。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-116">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="b2cbc-117">またはオプションを使用して証明書を指定する場合は、このオプションを使用する必要があり `-CertificateSubjectName` `-CertificateFingerprint` ます。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-117">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateStoreName`**

  <span data-ttu-id="b2cbc-118">証明書の検索に使用する x.509 証明書ストアの名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-118">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="b2cbc-119">既定値は "My" で、個人証明書の x.509 証明書ストアです。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-119">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="b2cbc-120">またはオプションを使用して証明書を指定する場合は、このオプションを使用する必要があり `-CertificateSubjectName` `-CertificateFingerprint` ます。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-120">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateSubjectName`**

  <span data-ttu-id="b2cbc-121">証明書のローカル証明書ストアの検索に使用する証明書のサブジェクト名を指定します。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-121">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="b2cbc-122">検索は、指定された値を使用して、大文字と小文字を区別せずに文字列を比較します。これにより、他のサブジェクト値に関係なく、その文字列を含むサブジェクト名を持つすべての証明書が検索されます。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-122">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="b2cbc-123">証明書ストアは、 `-CertificateStoreName` オプションとオプションで指定でき `-CertificateStoreLocation` ます。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-123">The certificate store can be specified by `-CertificateStoreName` and `-CertificateStoreLocation` options.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="b2cbc-124">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b2cbc-125">指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="b2cbc-126">不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-126">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-HashAlgorithm`**

  <span data-ttu-id="b2cbc-127">パッケージの署名に使用するハッシュアルゴリズム。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-127">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="b2cbc-128">既定値は SHA256 です。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-128">Defaults to SHA256.</span></span> <span data-ttu-id="b2cbc-129">指定できる値は SHA256、SHA384、および SHA512 です。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-129">Possible values are SHA256, SHA384, and SHA512.</span></span>

- **`-?|-help`**

  <span data-ttu-id="b2cbc-130">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-130">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="b2cbc-131">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-131">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="b2cbc-132">署名されたパッケージを保存するディレクトリを指定します。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-132">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="b2cbc-133">既定では、元のパッケージは署名付きパッケージによって上書きされます。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-133">By default the original package is overwritten by the signed package.</span></span>

- **`-Overwrite`**

  <span data-ttu-id="b2cbc-134">現在の署名を上書きするかどうかを示すには、を切り替えます。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-134">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="b2cbc-135">既定では、パッケージに既に署名がある場合、コマンドは失敗します。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-135">By default the command will fail if the package already has a signature.</span></span>

- **`-Timestamper`**

  <span data-ttu-id="b2cbc-136">RFC 3161 タイムスタンプサーバーの URL。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-136">URL to an RFC 3161 timestamping server.</span></span>

- **`-TimestampHashAlgorithm`**

  <span data-ttu-id="b2cbc-137">RFC 3161 タイムスタンプサーバーによって使用されるハッシュアルゴリズム。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-137">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="b2cbc-138">既定値は SHA256 です。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-138">Defaults to SHA256.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="b2cbc-139">出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。</span><span class="sxs-lookup"><span data-stu-id="b2cbc-139">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="b2cbc-140">使用例</span><span class="sxs-lookup"><span data-stu-id="b2cbc-140">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
