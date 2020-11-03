---
title: NuGet CLI 信頼-署名者コマンド
description: nuget.exe 信頼された署名者コマンドのリファレンス
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9e25f439617a76d30880bea3c10a5d063e681a41
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238154"
---
# <a name="trusted-signers-command-nuget-cli"></a>trusted-署名者コマンド (NuGet CLI)

**適用対象:** パッケージ消費が &bullet; **サポートされているバージョン:** 4.9.1 +

NuGet 構成に対する信頼された署名者を取得または設定します。 その他の使用方法については、「 [Common NuGet の構成](../../consume-packages/configuring-nuget-behavior.md)」を参照してください。 nuget.config スキーマの外観の詳細については、 [NuGet 構成ファイルのリファレンス](../nuget-config-file.md)を参照してください。

## <a name="usage"></a>使用

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

`list|add|remove|sync`が指定されていない場合、コマンドは既定でに設定され `list` ます。

## <a name="nuget-trusted-signers-list"></a>nuget の信頼された署名者リスト

構成内のすべての信頼された署名者を一覧表示します。 このオプションには、各署名者が持つすべての証明書 (指紋および指紋アルゴリズム) が含まれます。 証明書に前のが含まれている場合は `[U]` 、証明書エントリがとして設定されていることを意味し `allowUntrustedRoot` `true` ます。

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
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

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

ここ `<package(s)>` で、は1つ以上の `.nupkg` ファイルです。

- **`-Author`**

  パッケージの作成者の署名を信頼する必要があることを指定します。

- **`-AllowUntrustedRoot`**

  信頼された署名者の証明書を信頼されていないルートにチェーンできるようにするかどうかを指定します。

- **`-Owners`**

  リポジトリの信頼をさらに制限するために、信頼された所有者のセミコロンで区切られた一覧。 オプションを使用する場合にのみ有効です `-Repository` 。

- **`-Repository`**

  パッケージのリポジトリ署名または副署名を信頼する必要があることを指定します。

`-Author`との両方を `-Repository` 同時に指定することはサポートされていません。

## <a name="options-for-add-based-on-a-service-index"></a>サービスインデックスに基づく追加のオプション

```cli
nuget trusted-signers add -Name <name> [options]
```

_注_ : このオプションでは、信頼されたリポジトリのみが追加されます。 

- **`-AllowUntrustedRoot`**

  信頼された署名者の証明書を信頼されていないルートにチェーンできるようにするかどうかを指定します。

- **`-Owners`**

  リポジトリの信頼をさらに制限するために、信頼された所有者のセミコロンで区切られた一覧。

- **`-ServiceIndex`**

  信頼されるリポジトリの V3 サービスインデックスを指定します。 このリポジトリは、リポジトリ署名リソースをサポートする必要があります。 指定されていない場合、コマンドは同じを持つパッケージソースを検索 `-Name` し、そこからサービスインデックスを取得します。

## <a name="options-for-add-based-on-the-certificate-information"></a>証明書情報に基づいて追加するオプション

```cli
nuget trusted-signers add -Name <name> [options]
```

_注_ : 指定した名前の信頼された署名者が既に存在する場合、その署名者に証明書項目が追加されます。 それ以外の場合、信頼できる作成者は、指定された証明書情報から証明書項目を使用して作成されます。


- **`-AllowUntrustedRoot`**

  信頼された署名者の証明書を信頼されていないルートにチェーンできるようにするかどうかを指定します。

- **`-CertificateFingerprint`**

  署名されたパッケージに署名する必要がある証明書の証明書の指紋を指定します。 証明書のフィンガープリントは、証明書のハッシュです。 このハッシュの計算に使用されるハッシュアルゴリズムは、オプションで指定する必要があり `FingerprintAlgorithm` ます。

- **`-FingerprintAlgorithm`**

  証明書のフィンガープリントを計算するために使用するハッシュアルゴリズムを指定します。 既定値は `SHA256` です。 サポートされる値は `SHA256` 、、 `SHA384` および `SHA512` です。

## <a name="nuget-trusted-signers-remove--name-name"></a>nuget の信頼された署名者の名前の削除 \<name\>

指定した名前に一致する信頼された署名者を削除します。

## <a name="nuget-trusted-signers-sync--name-name"></a>nuget 信頼-署名者同期名 \<name\>

現在信頼されているリポジトリで使用されている最新の証明書の一覧を要求して、信頼された署名者の既存の証明書の一覧を更新します。

_注_ : このジェスチャは、現在の証明書の一覧を削除し、リポジトリの最新の一覧に置き換えます。

## <a name="options"></a>オプション

- **`-ConfigFile`**

  適用する NuGet 構成ファイル。 指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。

- **`-ForceEnglishOutput`**

  不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。

- **`-?|-help`**

  コマンドのヘルプ情報を表示します。

- **`-Name`**

  信頼された署名者の名前。

- **`-NonInteractive`**

  ユーザーの入力または確認のプロンプトを表示しません。

- **`-Verbosity [normal|quiet|detailed]`**

  出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。


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
