---
title: NuGet パッケージの署名 | Microsoft Docs
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 署名済みパッケージを使用してコンテンツの整合性の検証を可能にする方法について説明します。
keywords: NuGet パッケージの署名, NuGet セキュリティ, 署名済みパッケージの作成
ms.reviewer:
- karann-msft
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 61d90066e8cf75c8f49c7cc9390d45e1cd8afd0d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="signing-nuget-packages"></a>NuGet パッケージの署名

パッケージの署名は、パッケージが作成後に変更されていないことを確認するプロセスです。

## <a name="prerequisites"></a>必須コンポーネント

1. 署名するパッケージ (`.nupkg` ファイル)。 [パッケージの作成](creating-a-package.md)に関するページを参照してください。

1. nuget.exe 4.6.0 以前。 [NuGet CLI のインストール方法](../install-nuget-client-tools.md#nugetexe-cli)に関するセクションを参照してください。

1. [コード署名証明書](../reference/signed-packages-reference.md#get-a-code-signing-certificate)。

> [!Warning]
> 現在、nuget.org は署名済みパッケージを受け付けていません。 カスタム フィードに公開する場合はパッケージに署名することができます。

## <a name="sign-a-package"></a>パッケージに署名する

パッケージに署名するには、[nuget sign](../tools/cli-ref-sign.md) を使用します。

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

コマンド リファレンスで説明したように、証明書ストアで入手できる証明書を使用するか、ファイルの証明書を使用することができます。

### <a name="common-problems-when-signing-a-package"></a>パッケージに署名する場合の一般的な問題

- 証明書がコード署名に対して有効ではありません。 指定した証明書に適切な拡張キー使用法 (EKU 1.3.6.1.5.5.7.3.3) があることを確認する必要があります。
- 証明書が、RSA SHA-256 署名アルゴリズムや 2048 ビット以上の公開キーなどの基本要件を満たしていません。
- 証明書が期限切れか、失効しています。
- タイムスタンプ サーバーが証明書の要件を満たしていません。

> [!Note]
> 署名証明書が期限切れになったときに署名の有効な状態を維持するには、署名済みパッケージにタイムスタンプが含まれている必要があります。 タイムスタンプなしで署名すると、署名操作で[警告 NU3002](../reference/Errors-and-Warnings.md#nu3002) が生成されます。

## <a name="verify-a-signed-package"></a>署名済みパッケージを確認する

指定したパッケージの署名の詳細を表示するには、[nuget verify](../tools/cli-ref-verify.md) を使用します。

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a>署名済みパッケージをインストールする

署名済みパッケージでは、特定のアクションをインストールする必要はありません。ただし、署名後にコンテンツが変更された場合、インストールはブロックされ、[エラー NU3008](../reference/Errors-and-Warnings.md#nu3008) が生成されます。

> [!Warning]
> 信頼できない証明書で署名されたパッケージは署名なしと見なされ、他の署名されていないパッケージと同様に警告やエラーなしでインストールされます。

## <a name="see-also"></a>関連項目

[署名済みパッケージの参照](../reference/Signed-Packages-Reference.md)
