---
title: 署名付き NuGet パッケージをインストールする
description: 署名付き NuGet パッケージをインストールする手順およびパッケージの署名の信頼設定を構成する方法を説明します。
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 11ffaee96b6f6a9260f38c534328b6631cd96abf
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977836"
---
# <a name="install-a-signed-package"></a><span data-ttu-id="57eef-103">署名済みパッケージをインストールする</span><span class="sxs-lookup"><span data-stu-id="57eef-103">Install a signed package</span></span>

<span data-ttu-id="57eef-104">署名済みパッケージのインストールには、特定のアクションは必要ありません。ただし、署名後にコンテンツが変更された場合、インストールはエラー [NU3008](../reference/errors-and-warnings/NU3008.md) でブロックされます。</span><span class="sxs-lookup"><span data-stu-id="57eef-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="57eef-105">信頼できない証明書で署名されたパッケージは署名なしと見なされ、他の署名されていないパッケージと同様に警告やエラーなしでインストールされます。</span><span class="sxs-lookup"><span data-stu-id="57eef-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="57eef-106">パッケージの署名要件を構成する</span><span class="sxs-lookup"><span data-stu-id="57eef-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="57eef-107">NuGet 4.9.0 以上および Visual Studio バージョン 15.9 以上が Windows で必要です。</span><span class="sxs-lookup"><span data-stu-id="57eef-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="57eef-108">NuGet クライアントがパッケージの署名を検証する方法を構成するには、[nuget.config](../reference/nuget-config-file) ファイルで [`nuget config`](../tools/cli-ref-config) コマンドを使用し、`signatureValidationMode` を `require` に設定します。</span><span class="sxs-lookup"><span data-stu-id="57eef-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file) file using the [`nuget config`](../tools/cli-ref-config) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="57eef-109">このモードにより、`nuget.config` ファイルで信頼されているいずれかの証明書で、すべてのパッケージが署名されていることが検証されます。</span><span class="sxs-lookup"><span data-stu-id="57eef-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="57eef-110">このファイルでは、どの作成者およびリポジトリを信頼するか、証明書のフィンガープリントに基づいて指定できます。</span><span class="sxs-lookup"><span data-stu-id="57eef-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="57eef-111">パッケージの作成者を信頼する</span><span class="sxs-lookup"><span data-stu-id="57eef-111">Trust package author</span></span>

<span data-ttu-id="57eef-112">作成者の署名に基づいてパッケージを信頼するには、nuget.config で [`trusted-signers`](..tools/cli-ref-trusted-signers) コマンドを使用し `author` プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="57eef-112">To trust packages based on the author signature use the [`trusted-signers`](..tools/cli-ref-trusted-signers) command to set the `author` property in the nuget.config.</span></span>

```cmd
nuget.exe  trusted-signers Add -Name MyCompanyCert -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256
```

```xml
<trustedSigners>
  <author name="MyCompanyCert">
    <certificate fingerprint="CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
  </author>
</trustedSigners>
```

>[!TIP]
><span data-ttu-id="57eef-113">`nuget.exe` の [verify コマンド](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify)を使用して、証明書のフィンガープリントの `SHA256` 値を取得します。</span><span class="sxs-lookup"><span data-stu-id="57eef-113">Use the `nuget.exe` [verify command](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="57eef-114">リポジトリのパッケージをすべて信頼する</span><span class="sxs-lookup"><span data-stu-id="57eef-114">Trust all packages from a repository</span></span>

<span data-ttu-id="57eef-115">リポジトリの署名に基づいてパッケージを信頼するには、次のように `repository` 要素を使用します。</span><span class="sxs-lookup"><span data-stu-id="57eef-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="57eef-116">パッケージの所有者を信頼する</span><span class="sxs-lookup"><span data-stu-id="57eef-116">Trust Package Owners</span></span>

<span data-ttu-id="57eef-117">リポジトリの署名には、パッケージの所有者を送信時に特定するメタデータが追加で含まれています。</span><span class="sxs-lookup"><span data-stu-id="57eef-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="57eef-118">所有者の一覧に基づいてリポジトリでパッケージを制限するには、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="57eef-118">You can restrict packages from a repository based on a list of owners:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
      <owners>microsoft;nuget</owners>
  </repository>
</trustedSigners>
```

<span data-ttu-id="57eef-119">パッケージに所有者が複数いて、そのうちのいずれかの所有者が信頼されているリストに含まれる場合、パッケージは正常にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="57eef-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="57eef-120">信頼されないルート証明書</span><span class="sxs-lookup"><span data-stu-id="57eef-120">Untrusted Root certificates</span></span>

<span data-ttu-id="57eef-121">場合によっては、ローカル マシンの信頼されたルートに関連付けられていない証明書を使用した検証を有効にしたい場合があります。</span><span class="sxs-lookup"><span data-stu-id="57eef-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="57eef-122">この動作をカスタマイズするには、`allowUntrustedRoot` 属性を使用します。</span><span class="sxs-lookup"><span data-stu-id="57eef-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="57eef-123">同期リポジトリの証明書</span><span class="sxs-lookup"><span data-stu-id="57eef-123">Sync repository certificates</span></span>

<span data-ttu-id="57eef-124">パッケージ リポジトリでは、使用する証明書をその[サービス インデックス](https://docs.microsoft.com/en-us/nuget/api/service-index)で宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="57eef-124">Package repositories should announce the certificates they use in their [service index](https://docs.microsoft.com/en-us/nuget/api/service-index).</span></span> <span data-ttu-id="57eef-125">証明書の有効期限が切れるときなどに、実質的にこれらの証明書はリポジトリで更新されます。</span><span class="sxs-lookup"><span data-stu-id="57eef-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="57eef-126">これが発生した場合、特定のポリシーを使用するクライアントは、新しく追加された証明書を含めるために構成を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="57eef-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="57eef-127">リポジトリに関連付けられている信頼されている署名者は、`nuget.exe` [trusted-signers sync コマンド](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-)を使用して簡単にアップグレードできます。</span><span class="sxs-lookup"><span data-stu-id="57eef-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="57eef-128">スキーマ リファレンス</span><span class="sxs-lookup"><span data-stu-id="57eef-128">Schema reference</span></span>

<span data-ttu-id="57eef-129">クライアント ポリシーの完全なスキーマ リファレンスは、[nuget.config のリファレンス](/nuget/reference/nuget-config-file#trustedsigners-section)に関するページにあります。</span><span class="sxs-lookup"><span data-stu-id="57eef-129">The complete schema reference for the client policies can be found in the [nuget.config reference](/nuget/reference/nuget-config-file#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="57eef-130">関連記事</span><span class="sxs-lookup"><span data-stu-id="57eef-130">Related articles</span></span>

- [<span data-ttu-id="57eef-131">NuGet パッケージをインストールするためのさまざまな方法</span><span class="sxs-lookup"><span data-stu-id="57eef-131">Different ways to install a NuGet Package</span></span>](ways-to-install-a-package.md)
- [<span data-ttu-id="57eef-132">NuGet パッケージの署名</span><span class="sxs-lookup"><span data-stu-id="57eef-132">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="57eef-133">署名済みパッケージの参照</span><span class="sxs-lookup"><span data-stu-id="57eef-133">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
