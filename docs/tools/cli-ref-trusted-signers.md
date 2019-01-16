---
title: 信頼された署名の NuGet CLI コマンド
description: Nuget.exe の信頼された署名コマンドのリファレンス
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: ee4ffaa7e250cdbf313476fd794a8d87c80b69f9
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324709"
---
# <a name="trusted-signers-command-nuget-cli"></a>信頼された署名コマンド (NuGet CLI)

**適用対象:** 消費をパッケージ化&bullet;**サポートされているバージョン。** 4.9.1+

取得または信頼できる署名者を NuGet の構成に設定します。 追加の使用状況は、次を参照してください。 [NuGet の動作を構成する](../consume-packages/configuring-nuget-behavior.md)します。 詳細についてを参照するくださいと同様の nuget.config スキーマの外観に、 [NuGet 構成ファイル リファレンス](../reference/nuget-config-file.md)します。

## <a name="usage"></a>使用法

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

none の場合`list|add|remove|sync`を指定すると、コマンドは、既定値は`list`します。

## <a name="nuget-trusted-signers-list"></a>nuget の信頼された署名の一覧

構成で信頼できる署名者をすべて一覧表示します。 このオプションには、すべての証明書にが含まれます (指紋と指紋アルゴリズム) を持つ各署名者が。 証明書がある先行場合`[U]`、証明書のエントリがあることを意味`allowUntrustedRoot`として設定`true`します。

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

## <a name="nuget-trusted-signers-add-options"></a>nuget trusted-signers add [options]

構成には、指定した名前の信頼できる署名者を追加します。このオプションは、信頼された作成者またはリポジトリを追加するさまざまなジェスチャです。

## <a name="options-for-add-based-on-a-package"></a>パッケージに基づく追加のオプション

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

場所`<package(s)>`は 1 つ以上`.nupkg`ファイル。

| オプション | 説明 |
| --- | --- |
| 作成者 | パッケージの作成者の署名が信頼があることを指定します。 |
| リポジトリ | リポジトリの署名またはパッケージの副署名する必要がありますが信頼できることを指定します。 |
| AllowUntrustedRoot | 信頼されていないルートにチェーンを信頼できる署名者の証明書を許可するかどうかを指定します。 |
| 所有者 | さらに、リポジトリの信頼を制限する信頼された所有者のセミコロンで区切られたリスト。 使用する場合にのみ有効です、`-Repository`オプション。 |

両方を提供する`-Author`と`-Repository`と同時にはサポートされていません。

## <a name="options-for-add-based-on-a-service-index"></a>サービス インデックスに基づいて追加のオプション

```cli
nuget trusted-signers add -Name <name> [options]
```

_注_:このオプションは、信頼されているリポジトリをのみ追加されます。 

| オプション | 説明 |
| --- | --- |
| ServiceIndex | 信頼できるリポジトリの V3 サービス インデックスを指定します。 このリポジトリは、リポジトリのリソースの署名をサポートする必要があります。 コマンドが同じパッケージのソースを探して指定しない場合、`-Name`し、そこからサービス インデックスを取得します。 |
| AllowUntrustedRoot | 信頼されていないルートにチェーンを信頼できる署名者の証明書を許可するかどうかを指定します。 |
| 所有者 | さらに、リポジトリの信頼を制限する信頼された所有者のセミコロンで区切られたリスト。 |

## <a name="options-for-add-based-on-the-certificate-information"></a>証明書情報に基づいて追加のオプション

```cli
nuget trusted-signers add -Name <name> [options]
```

_注_:指定した名前の信頼できる署名者が既に存在する場合、証明書の項目はその署名者に追加されます。 証明書の項目で、信頼された作成者が作成されますそれ以外の場合から証明書の情報を指定します。

| オプション | 説明 |
| --- | --- |
| CertificateFingerprint | パッケージの署名証明書の指紋を署名する必要があります証明書を指定します。 証明書フィンガー プリントは、証明書のハッシュです。 このハッシュは計算に使用されるハッシュ アルゴリズムを指定します、`FingerprintAlgorithm`オプション。 |
| FingerprintAlgorithm | 証明書フィンガー プリントを計算するために使用するハッシュ アルゴリズムを指定します。 既定値は `SHA256` です。 サポートされている値は`SHA256`、`SHA384`と `SHA512` |
| AllowUntrustedRoot | 信頼されていないルートにチェーンを信頼できる署名者の証明書を許可するかどうかを指定します。 |

## <a name="nuget-trusted-signers-remove--name-name"></a>nuget 信頼された署名の削除 - 名前 <name>

指定した名前に一致する任意の信頼できる署名者を削除します。

## <a name="nuget-trusted-signers-sync--name-name"></a>nuget 信頼された署名は、次の同期 - 名前 <name>

最新のリストを更新する現在の信頼されたリポジトリで使用される証明書を要求する、信頼できる署名者の既存の証明書のリスト。

_注_:このジェスチャは現在の証明書の一覧を削除し、リポジトリから最新の一覧に置き換えます。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。|
| ForceEnglishOutput | インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプのコマンドの情報を表示します。 |
| 詳細度 | 出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。 |

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
