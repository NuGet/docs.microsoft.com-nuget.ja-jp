---
title: NuGet CLI trusted-signers コマンド
description: Nuget.exe の trusted-signers コマンドのリファレンス
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 197f2eaeed1a4a11f0f3ed426534807a0136271e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327539"
---
# <a name="trusted-signers-command-nuget-cli"></a>trusted-signers コマンド (NuGet CLI)

**適用対象:** パッケージ消費&bullet;が**サポートされているバージョン:** 4.9.1 +

NuGet 構成に対する信頼された署名者を取得または設定します。 その他の使用方法については、「 [Common NuGet の構成](../../consume-packages/configuring-nuget-behavior.md)」を参照してください。 Nuget.exe スキーマの外観の詳細については、 [nuget 構成ファイルのリファレンス](../nuget-config-file.md)を参照してください。

## <a name="usage"></a>使用法

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

が指定されていない場合、コマンドは`list`既定でに設定されます。 `list|add|remove|sync`

## <a name="nuget-trusted-signers-list"></a>nuget の信頼された署名者リスト

構成内のすべての信頼された署名者を一覧表示します。 このオプションには、各署名者が持つすべての証明書 (指紋および指紋アルゴリズム) が含まれます。 証明書に前`[U]`のが含まれている場合は、証明書エントリが`allowUntrustedRoot`として`true`設定されていることを意味します。

このコマンドからの出力例を次に示します。

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>nuget の信頼済み-署名者の追加 [オプション]

指定された名前の信頼された署名者を構成に追加します。このオプションでは、信頼された作成者またはリポジトリを追加するジェスチャは異なります。

## <a name="options-for-add-based-on-a-package"></a>パッケージに基づいて追加するためのオプション

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

ここ`<package(s)>` で`.nupkg` 、は1つ以上のファイルです。

| オプション | 説明 |
| --- | --- |
| Author | パッケージの作成者の署名を信頼する必要があることを指定します。 |
| Repository | パッケージのリポジトリ署名または副署名を信頼する必要があることを指定します。 |
| AllowUntrustedRoot | 信頼された署名者の証明書を信頼されていないルートにチェーンできるようにするかどうかを指定します。 |
| Owners | リポジトリの信頼をさらに制限するために、信頼された所有者のセミコロンで区切られた一覧。 `-Repository`オプションを使用する場合にのみ有効です。 |

`-Author` と`-Repository`の両方を同時に指定することはサポートされていません。

## <a name="options-for-add-based-on-a-service-index"></a>サービスインデックスに基づく追加のオプション

```cli
nuget trusted-signers add -Name <name> [options]
```

_注_:このオプションでは、信頼されたリポジトリのみが追加されます。 

| オプション | 説明 |
| --- | --- |
| ServiceIndex | 信頼されるリポジトリの V3 サービスインデックスを指定します。 このリポジトリは、リポジトリ署名リソースをサポートする必要があります。 指定されていない場合、コマンドは同じ`-Name`を持つパッケージソースを検索し、そこからサービスインデックスを取得します。 |
| AllowUntrustedRoot | 信頼された署名者の証明書を信頼されていないルートにチェーンできるようにするかどうかを指定します。 |
| Owners | リポジトリの信頼をさらに制限するために、信頼された所有者のセミコロンで区切られた一覧。 |

## <a name="options-for-add-based-on-the-certificate-information"></a>証明書情報に基づいて追加するオプション

```cli
nuget trusted-signers add -Name <name> [options]
```

_注_:指定した名前の信頼された署名者が既に存在する場合、その署名者に証明書項目が追加されます。 それ以外の場合、信頼できる作成者は、指定された証明書情報から証明書項目を使用して作成されます。

| オプション | 説明 |
| --- | --- |
| CertificateFingerprint | 署名されたパッケージに署名する必要がある証明書の証明書の指紋を指定します。 証明書のフィンガープリントは、証明書のハッシュです。 このハッシュの計算に使用されるハッシュアルゴリズムは、 `FingerprintAlgorithm`オプションで指定する必要があります。 |
| FingerprintAlgorithm | 証明書のフィンガープリントを計算するために使用するハッシュアルゴリズムを指定します。 既定値は `SHA256` です。 サポートされる`SHA256`値`SHA384`は、、およびです。`SHA512` |
| AllowUntrustedRoot | 信頼された署名者の証明書を信頼されていないルートにチェーンできるようにするかどうかを指定します。 |

## <a name="nuget-trusted-signers-remove--name-name"></a>nuget の信頼された署名者の名前の削除<name>

指定した名前に一致する信頼された署名者を削除します。

## <a name="nuget-trusted-signers-sync--name-name"></a>nuget 信頼-署名者同期名<name>

現在信頼されているリポジトリで使用されている最新の証明書の一覧を要求して、信頼された署名者の既存の証明書の一覧を更新します。

_注_:このジェスチャは、現在の証明書の一覧を削除し、リポジトリから最新の一覧に置き換えます。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。|
| ForceEnglishOutput | 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細* |

## <a name="examples"></a>使用例

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
