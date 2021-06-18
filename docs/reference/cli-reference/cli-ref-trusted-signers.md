---
title: NuGet CLI trusted-signers コマンド
description: nuget.exe trusted-signers コマンドのリファレンス
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: a5f3564af8b96dfa673d2252aea2e77a79c184a4
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323591"
---
# <a name="trusted-signers-command-nuget-cli"></a>trusted-signers コマンド (NuGet CLI)

**適用対象: パッケージ** 消費量 &bullet; **サポートされているバージョン:** 4.9.1 以上

信頼された署名者を NuGet 構成に対して取得または設定します。 その他の使用方法については、「 [一般的な NuGet 構成」を参照してください](../../consume-packages/configuring-nuget-behavior.md)。 スキーマの構成方法nuget.configについては、NuGet 構成ファイルの [リファレンスを参照してください](../nuget-config-file.md)。

## <a name="usage"></a>使用方法

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

が指定されていない `list|add|remove|sync` 場合、コマンドは既定で になります `list` 。

## <a name="nuget-trusted-signers-list"></a>nuget trusted-signers list

構成内のすべての信頼された署名者を一覧表示します。 このオプションには、各署名者が持つすべての証明書 (指紋と指紋アルゴリズムを使用) が含まれます。 証明書に が先行する がある場合 `[U]` は、証明書エントリが に設定 `allowUntrustedRoot` されています `true` 。

このコマンドからの出力例を次に示します。

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D
        SHA256 - 5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>nuget trusted-signers add [options]

指定した名前の信頼された署名者を構成に追加します。このオプションには、信頼された作成者またはリポジトリを追加するさまざまなジェスチャがあります。

## <a name="options-for-add-based-on-a-package"></a>パッケージに基づいて追加するためのオプション

```cli
nuget trusted-signers add <package> -Name <name> [options]
```

ここで `<package>` 、 は 1 つの署名付き `.nupkg` ファイルです。

- **`-Author`**

  署名付きパッケージの作成者署名を信頼する必要がある場合に指定します。

- **`-AllowUntrustedRoot`**

  信頼された署名者の証明書を信頼されていないルートにチェーンできる必要がある場合に指定します。

- **`-Owners`**

  リポジトリの信頼をさらに制限するために、信頼できる所有者のセミコロン区切りの一覧。 オプションを使用する場合 `-Repository` にのみ有効です。

- **`-Repository`**

  署名されたパッケージのリポジトリの署名または署名を信頼する必要がある場合に指定します。

と `-Author` の `-Repository` 両方を同時に指定する機能はサポートされていません。

## <a name="options-for-add-based-on-a-service-index"></a>サービス インデックスに基づいて追加するためのオプション

```cli
nuget trusted-signers add -Name <name> [options]
```

_注_: このオプションでは、信頼されたリポジトリだけが追加されます。 

- **`-AllowUntrustedRoot`**

  信頼された署名者の証明書を信頼されていないルートにチェーンできる必要がある場合に指定します。

- **`-Owners`**

  リポジトリの信頼をさらに制限するために、信頼できる所有者のセミコロン区切りの一覧。

- **`-ServiceIndex`**

  信頼されるリポジトリの V3 サービス インデックスを指定します。 このリポジトリは、リポジトリ署名リソースをサポートする必要があります。 指定しない場合、コマンドは同じパッケージ ソースを検索し、そこから `-Name` サービス インデックスを取得します。

## <a name="options-for-add-based-on-the-certificate-information"></a>証明書情報に基づいて追加するためのオプション

```cli
nuget trusted-signers add -Name <name> [options]
```

_注_: 指定した名前の信頼された署名者が既に存在する場合は、その署名者に証明書項目が追加されます。 それ以外の場合、信頼された作成者は、指定された証明書情報の証明書項目を使用して作成されます。


- **`-AllowUntrustedRoot`**

  信頼された署名者の証明書を信頼されていないルートにチェーンできる必要がある場合に指定します。

- **`-CertificateFingerprint`**

  署名済みパッケージに署名する必要がある証明書の証明書フィンガープリントを指定します。 証明書のフィンガープリントは、証明書のハッシュです。 このハッシュの計算に使用するハッシュ アルゴリズムは、 オプションで 指定する必要 `FingerprintAlgorithm` があります。

- **`-FingerprintAlgorithm`**

  証明書のフィンガープリントの計算に使用するハッシュ アルゴリズムを指定します。 既定値は `SHA256` です。 サポートされている値は `SHA256` 、、 `SHA384` および です `SHA512` 。

## <a name="nuget-trusted-signers-remove--name-name"></a>nuget trusted-signers remove -Name \<name\>

指定した名前に一致する信頼できる署名者を削除します。

## <a name="nuget-trusted-signers-sync--name-name"></a>nuget trusted-signers sync -Name \<name\>

現在信頼されているリポジトリで使用されている証明書の最新の一覧を要求して、信頼された署名者の既存の証明書リストを更新します。

_注_: このジェスチャでは、証明書の現在の一覧が削除され、リポジトリから最新のリストに置き換えます。

## <a name="options"></a>オプション

- **`-ConfigFile`**

  適用する NuGet 構成ファイル。 指定しない場合は `%AppData%\NuGet\NuGet.Config` 、(Windows)、 `~/.nuget/NuGet/NuGet.Config` または `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。

- **`-ForceEnglishOutput`**

  インnuget.exe英語ベースのカルチャを使用して、強制的に実行します。

- **`-?|-help`**

  コマンドのヘルプ情報を表示します。

- **`-Name`**

  信頼された署名者の名前。

- **`-NonInteractive`**

  ユーザー入力または確認のプロンプトを抑制します。

- **`-Verbosity [normal|quiet|detailed]`**

  出力に表示される詳細の量 (既定値 `normal` )、、または `quiet` を指定します `detailed` 。


## <a name="examples"></a>使用例

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget trusted-signers Remove -Name TrustedRepo

nuget trusted-signers Sync -Name TrustedRepo
```
