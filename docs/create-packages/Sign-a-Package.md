---
title: NuGet パッケージの署名
description: 署名済みパッケージを使用してコンテンツの整合性の検証を可能にする方法について説明します。
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 9900db1970a89de129d9074e5900e0aa048101de
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2018
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="ed9f6-103">NuGet パッケージの署名</span><span class="sxs-lookup"><span data-stu-id="ed9f6-103">Signing NuGet Packages</span></span>

<span data-ttu-id="ed9f6-104">パッケージの署名は、パッケージが作成後に変更されていないことを確認するプロセスです。</span><span class="sxs-lookup"><span data-stu-id="ed9f6-104">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed9f6-105">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="ed9f6-105">Prerequisites</span></span>

1. <span data-ttu-id="ed9f6-106">署名するパッケージ (`.nupkg` ファイル)。</span><span class="sxs-lookup"><span data-stu-id="ed9f6-106">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="ed9f6-107">[パッケージの作成](creating-a-package.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="ed9f6-107">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="ed9f6-108">nuget.exe 4.6.0 以前。</span><span class="sxs-lookup"><span data-stu-id="ed9f6-108">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="ed9f6-109">[NuGet CLI のインストール方法](../install-nuget-client-tools.md#nugetexe-cli)に関するセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="ed9f6-109">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="ed9f6-110">[コード署名証明書](../reference/signed-packages-reference.md#get-a-code-signing-certificate)。</span><span class="sxs-lookup"><span data-stu-id="ed9f6-110">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="ed9f6-111">パッケージに署名する</span><span class="sxs-lookup"><span data-stu-id="ed9f6-111">Sign a package</span></span>

<span data-ttu-id="ed9f6-112">パッケージに署名するには、[nuget sign](../tools/cli-ref-sign.md) を使用します。</span><span class="sxs-lookup"><span data-stu-id="ed9f6-112">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="ed9f6-113">コマンド リファレンスで説明したように、証明書ストアで入手できる証明書を使用するか、ファイルの証明書を使用することができます。</span><span class="sxs-lookup"><span data-stu-id="ed9f6-113">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="ed9f6-114">パッケージに署名する場合の一般的な問題</span><span class="sxs-lookup"><span data-stu-id="ed9f6-114">Common problems when signing a package</span></span>

- <span data-ttu-id="ed9f6-115">証明書がコード署名に対して有効ではありません。</span><span class="sxs-lookup"><span data-stu-id="ed9f6-115">The certificate is not valid for code signing.</span></span> <span data-ttu-id="ed9f6-116">指定した証明書に適切な拡張キー使用法 (EKU 1.3.6.1.5.5.7.3.3) があることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed9f6-116">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="ed9f6-117">証明書が、RSA SHA-256 署名アルゴリズムや 2048 ビット以上の公開キーなどの基本要件を満たしていません。</span><span class="sxs-lookup"><span data-stu-id="ed9f6-117">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="ed9f6-118">証明書が期限切れか、失効しています。</span><span class="sxs-lookup"><span data-stu-id="ed9f6-118">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="ed9f6-119">タイムスタンプ サーバーが証明書の要件を満たしていません。</span><span class="sxs-lookup"><span data-stu-id="ed9f6-119">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="ed9f6-120">署名証明書が期限切れになったときに署名の有効な状態を維持するには、署名済みパッケージにタイムスタンプが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed9f6-120">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="ed9f6-121">タイムスタンプなしで署名すると、署名操作で[警告 NU3002](../reference/Errors-and-Warnings.md#nu3002) が生成されます。</span><span class="sxs-lookup"><span data-stu-id="ed9f6-121">The sign operation produce a [warning NU3002](../reference/Errors-and-Warnings.md#nu3002) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="ed9f6-122">署名済みパッケージを確認する</span><span class="sxs-lookup"><span data-stu-id="ed9f6-122">Verify a signed package</span></span>

<span data-ttu-id="ed9f6-123">指定したパッケージの署名の詳細を表示するには、[nuget verify](../tools/cli-ref-verify.md) を使用します。</span><span class="sxs-lookup"><span data-stu-id="ed9f6-123">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="ed9f6-124">署名済みパッケージをインストールする</span><span class="sxs-lookup"><span data-stu-id="ed9f6-124">Install a signed package</span></span>

<span data-ttu-id="ed9f6-125">署名済みパッケージでは、特定のアクションをインストールする必要はありません。ただし、署名後にコンテンツが変更された場合、インストールはブロックされ、[エラー NU3008](../reference/Errors-and-Warnings.md#nu3008) が生成されます。</span><span class="sxs-lookup"><span data-stu-id="ed9f6-125">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation be blocked and produces a [error NU3008](../reference/Errors-and-Warnings.md#nu3008).</span></span>

> [!Warning]
> <span data-ttu-id="ed9f6-126">信頼できない証明書で署名されたパッケージは署名なしと見なされ、他の署名されていないパッケージと同様に警告やエラーなしでインストールされます。</span><span class="sxs-lookup"><span data-stu-id="ed9f6-126">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="ed9f6-127">関連項目</span><span class="sxs-lookup"><span data-stu-id="ed9f6-127">See also</span></span>

[<span data-ttu-id="ed9f6-128">署名済みパッケージの参照</span><span class="sxs-lookup"><span data-stu-id="ed9f6-128">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
