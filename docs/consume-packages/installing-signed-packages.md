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
# <a name="install-a-signed-package"></a>署名済みパッケージをインストールする

署名済みパッケージのインストールには、特定のアクションは必要ありません。ただし、署名後にコンテンツが変更された場合、インストールはエラー [NU3008](../reference/errors-and-warnings/NU3008.md) でブロックされます。

> [!Warning]
> 信頼できない証明書で署名されたパッケージは署名なしと見なされ、他の署名されていないパッケージと同様に警告やエラーなしでインストールされます。

## <a name="configure-package-signature-requirements"></a>パッケージの署名要件を構成する

> [!Note]
> NuGet 4.9.0 以上および Visual Studio バージョン 15.9 以上が Windows で必要です。

NuGet クライアントがパッケージの署名を検証する方法を構成するには、[nuget.config](../reference/nuget-config-file) ファイルで [`nuget config`](../tools/cli-ref-config) コマンドを使用し、`signatureValidationMode` を `require` に設定します。

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

このモードにより、`nuget.config` ファイルで信頼されているいずれかの証明書で、すべてのパッケージが署名されていることが検証されます。 このファイルでは、どの作成者およびリポジトリを信頼するか、証明書のフィンガープリントに基づいて指定できます。

### <a name="trust-package-author"></a>パッケージの作成者を信頼する

作成者の署名に基づいてパッケージを信頼するには、nuget.config で [`trusted-signers`](..tools/cli-ref-trusted-signers) コマンドを使用し `author` プロパティを設定します。

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
>`nuget.exe` の [verify コマンド](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify)を使用して、証明書のフィンガープリントの `SHA256` 値を取得します。


### <a name="trust-all-packages-from-a-repository"></a>リポジトリのパッケージをすべて信頼する

リポジトリの署名に基づいてパッケージを信頼するには、次のように `repository` 要素を使用します。

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a>パッケージの所有者を信頼する

リポジトリの署名には、パッケージの所有者を送信時に特定するメタデータが追加で含まれています。 所有者の一覧に基づいてリポジトリでパッケージを制限するには、次のようにします。

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

パッケージに所有者が複数いて、そのうちのいずれかの所有者が信頼されているリストに含まれる場合、パッケージは正常にインストールされます。

### <a name="untrusted-root-certificates"></a>信頼されないルート証明書

場合によっては、ローカル マシンの信頼されたルートに関連付けられていない証明書を使用した検証を有効にしたい場合があります。 この動作をカスタマイズするには、`allowUntrustedRoot` 属性を使用します。

### <a name="sync-repository-certificates"></a>同期リポジトリの証明書

パッケージ リポジトリでは、使用する証明書をその[サービス インデックス](https://docs.microsoft.com/en-us/nuget/api/service-index)で宣言する必要があります。 証明書の有効期限が切れるときなどに、実質的にこれらの証明書はリポジトリで更新されます。 これが発生した場合、特定のポリシーを使用するクライアントは、新しく追加された証明書を含めるために構成を更新する必要があります。 リポジトリに関連付けられている信頼されている署名者は、`nuget.exe` [trusted-signers sync コマンド](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-)を使用して簡単にアップグレードできます。

### <a name="schema-reference"></a>スキーマ リファレンス

クライアント ポリシーの完全なスキーマ リファレンスは、[nuget.config のリファレンス](/nuget/reference/nuget-config-file#trustedsigners-section)に関するページにあります。

## <a name="related-articles"></a>関連記事

- [NuGet パッケージをインストールするためのさまざまな方法](ways-to-install-a-package.md)
- [NuGet パッケージの署名](../create-packages/Sign-a-Package.md)
- [署名済みパッケージの参照](../reference/Signed-Packages-Reference.md)
