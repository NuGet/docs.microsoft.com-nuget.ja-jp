---
title: NuGet CLI sign コマンド
description: Nuget.exe sign コマンドのリファレンス
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e596fd5eb3de8ca4802d9b7b8e7cb623568e3dcb
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231124"
---
# <a name="sign-command-nuget-cli"></a>NuGet CLI sign コマンド

**適用対象:** パッケージ作成 &bullet;**サポートされているバージョン:** 4.6 以降

最初の引数に一致するすべてのパッケージに証明書を署名します。 秘密キーを持つ証明書は、サブジェクト名または拇印を指定することによって、ファイルまたは証明書ストアにインストールされている証明書から取得できます。

> [!Note]
> パッケージの署名は、.NET Core、Mono、または Windows 以外のプラットフォームではまだサポートされていません。

## <a name="usage"></a>使用法

```cli
nuget sign <package(s)> [options]
```

ここで `<package(s)>` は1つ以上の `.nupkg` ファイルです。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| CertificateFingerprint | 証明書のローカル証明書ストアの検索に使用される証明書の SHA-1 フィンガープリントを指定します。 |
| CertificatePassword | 必要に応じて、証明書のパスワードを指定します。 証明書がパスワードで保護されていてもパスワードが指定されていない場合、-非対話オプションが渡されない限り、コマンドは実行時にパスワードの入力を求めます。 |
| CertificatePath | パッケージへの署名に使用する証明書へのファイルパスを指定します。 |
| CertificateStoreLocation | 証明書の検索に使用する x.509 証明書ストアの名前を指定します。 既定値は "CurrentUser" で、現在のユーザーが使用している x.509 証明書ストアです。 CertificateSubjectName または-CertificateFingerprint プリントオプションを使用して証明書を指定する場合は、このオプションを使用する必要があります。 |
| CertificateStoreName | 証明書の検索に使用する x.509 証明書ストアの名前を指定します。 既定値は "My" で、個人証明書の x.509 証明書ストアです。 CertificateSubjectName または-CertificateFingerprint プリントオプションを使用して証明書を指定する場合は、このオプションを使用する必要があります。 |
| CertificateSubjectName | 証明書のローカル証明書ストアの検索に使用する証明書のサブジェクト名を指定します。  検索は、指定された値を使用して、大文字と小文字を区別せずに文字列を比較します。これにより、他のサブジェクト値に関係なく、その文字列を含むサブジェクト名を持つすべての証明書が検索されます。  証明書ストアは、-証明オプションと-CertificateStoreLocation オプションで指定できます。 |
| ConfigFile | 適用する NuGet 構成ファイル。 指定しない場合は、`%AppData%\NuGet\NuGet.Config` (Windows) または `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) が使用されます。|
| ForceEnglishOutput | 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| HashAlgorithm | パッケージの署名に使用するハッシュアルゴリズム。 既定値は SHA256 です。 指定できる値は SHA256、SHA384、および SHA512 です。 |
| ヘルプ | ヘルプのコマンドの情報を表示します。 |
| NonInteractive | ユーザーの入力または確認のプロンプトを表示しません。 |
| OutputDirectory | 署名されたパッケージを保存するディレクトリを指定します。 既定では、元のパッケージは署名付きパッケージによって上書きされます。 |
| 上書き | 現在の署名を上書きするかどうかを示すには、を切り替えます。 既定では、パッケージに既に署名がある場合、コマンドは失敗します。 |
| Timestamper | RFC 3161 タイムスタンプサーバーの URL。 |
| TimestampHashAlgorithm | RFC 3161 タイムスタンプサーバーによって使用されるハッシュアルゴリズム。 既定値は SHA256 です。 |
| 詳細度 | 出力に表示される詳細の量を指定します (*通常*、*非*表示、*詳細*)。 |

## <a name="examples"></a>例

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
