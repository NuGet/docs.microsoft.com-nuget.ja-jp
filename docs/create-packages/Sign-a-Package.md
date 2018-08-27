---
title: NuGet パッケージの署名
description: 署名済みパッケージを使用してコンテンツの整合性の検証を可能にする方法について説明します。
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 0679b60179760d6626e7ce42bfdbdfa266677ce6
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2018
ms.locfileid: "42792941"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="1549d-103">NuGet パッケージの署名</span><span class="sxs-lookup"><span data-stu-id="1549d-103">Signing NuGet Packages</span></span>

<span data-ttu-id="1549d-104">パッケージの署名は、パッケージが作成後に変更されていないことを確認するプロセスです。</span><span class="sxs-lookup"><span data-stu-id="1549d-104">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1549d-105">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="1549d-105">Prerequisites</span></span>

1. <span data-ttu-id="1549d-106">署名するパッケージ (`.nupkg` ファイル)。</span><span class="sxs-lookup"><span data-stu-id="1549d-106">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="1549d-107">[パッケージの作成](creating-a-package.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="1549d-107">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="1549d-108">nuget.exe 4.6.0 以前。</span><span class="sxs-lookup"><span data-stu-id="1549d-108">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="1549d-109">[NuGet CLI のインストール方法](../install-nuget-client-tools.md#nugetexe-cli)に関するセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="1549d-109">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="1549d-110">[コード署名証明書](../reference/signed-packages-reference.md#get-a-code-signing-certificate)。</span><span class="sxs-lookup"><span data-stu-id="1549d-110">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="1549d-111">パッケージに署名する</span><span class="sxs-lookup"><span data-stu-id="1549d-111">Sign a package</span></span>

<span data-ttu-id="1549d-112">パッケージに署名するには、[nuget sign](../tools/cli-ref-sign.md) を使用します。</span><span class="sxs-lookup"><span data-stu-id="1549d-112">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="1549d-113">コマンド リファレンスで説明したように、証明書ストアで入手できる証明書を使用するか、ファイルの証明書を使用することができます。</span><span class="sxs-lookup"><span data-stu-id="1549d-113">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="1549d-114">パッケージに署名する場合の一般的な問題</span><span class="sxs-lookup"><span data-stu-id="1549d-114">Common problems when signing a package</span></span>

- <span data-ttu-id="1549d-115">証明書がコード署名に対して有効ではありません。</span><span class="sxs-lookup"><span data-stu-id="1549d-115">The certificate is not valid for code signing.</span></span> <span data-ttu-id="1549d-116">指定した証明書に適切な拡張キー使用法 (EKU 1.3.6.1.5.5.7.3.3) があることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1549d-116">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="1549d-117">証明書が、RSA SHA-256 署名アルゴリズムや 2048 ビット以上の公開キーなどの基本要件を満たしていません。</span><span class="sxs-lookup"><span data-stu-id="1549d-117">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="1549d-118">証明書が期限切れか、失効しています。</span><span class="sxs-lookup"><span data-stu-id="1549d-118">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="1549d-119">タイムスタンプ サーバーが証明書の要件を満たしていません。</span><span class="sxs-lookup"><span data-stu-id="1549d-119">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="1549d-120">署名証明書が期限切れになったときに署名の有効な状態を維持するには、署名済みパッケージにタイムスタンプが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="1549d-120">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="1549d-121">タイムスタンプなしで署名すると、署名操作で[警告 NU3002](../reference/errors-and-warnings/NU3002.md) が生成されます。</span><span class="sxs-lookup"><span data-stu-id="1549d-121">The sign operation produce a [warning NU3002](../reference/errors-and-warnings/NU3002.md) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="1549d-122">署名済みパッケージを確認する</span><span class="sxs-lookup"><span data-stu-id="1549d-122">Verify a signed package</span></span>

<span data-ttu-id="1549d-123">指定したパッケージの署名の詳細を表示するには、[nuget verify](../tools/cli-ref-verify.md) を使用します。</span><span class="sxs-lookup"><span data-stu-id="1549d-123">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="1549d-124">署名済みパッケージをインストールする</span><span class="sxs-lookup"><span data-stu-id="1549d-124">Install a signed package</span></span>

<span data-ttu-id="1549d-125">署名済みパッケージでは、特定のアクションをインストールする必要はありません。ただし、署名後にコンテンツが変更された場合、インストールはブロックされ、[エラー NU3008](../reference/errors-and-warnings/NU3008.md) が生成されます。</span><span class="sxs-lookup"><span data-stu-id="1549d-125">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked and produces an [error NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="1549d-126">信頼できない証明書で署名されたパッケージは署名なしと見なされ、他の署名されていないパッケージと同様に警告やエラーなしでインストールされます。</span><span class="sxs-lookup"><span data-stu-id="1549d-126">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="1549d-127">関連項目</span><span class="sxs-lookup"><span data-stu-id="1549d-127">See also</span></span>

[<span data-ttu-id="1549d-128">署名済みパッケージの参照</span><span class="sxs-lookup"><span data-stu-id="1549d-128">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
