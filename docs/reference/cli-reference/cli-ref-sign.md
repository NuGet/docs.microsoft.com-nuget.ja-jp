---
title: NuGet CLI sign コマンド
description: nuget.exe sign コマンドのリファレンス
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 84386f1752b98688f1fd34e453f5b72ae8afdd92
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622773"
---
# <a name="sign-command-nuget-cli"></a>sign コマンド (NuGet CLI)

**適用対象:** パッケージ作成で &bullet; **サポートされているバージョン:** 4.6 以降

最初の引数に一致するすべてのパッケージに証明書を署名します。 秘密キーを持つ証明書は、サブジェクト名または拇印を指定することによって、ファイルまたは証明書ストアにインストールされている証明書から取得できます。

> [!Note]
> パッケージの署名は、.NET Core、Mono、または Windows 以外のプラットフォームではまだサポートされていません。

## <a name="usage"></a>使用法

```cli
nuget sign <package(s)> [options]
```

ここ `<package(s)>` で、は1つ以上の `.nupkg` ファイルです。

## <a name="options"></a>Options

- **`-CertificateFingerprint`**

  証明書のローカル証明書ストアの検索に使用される証明書の SHA-1 フィンガープリントを指定します。

- **`-CertificatePassword`**

  必要に応じて、証明書のパスワードを指定します。 証明書がパスワードで保護されていてもパスワードが指定されていない場合、オプションが渡されない限り、コマンドは実行時にパスワードの入力を求め `-NonInteractive` ます。

- **`-CertificatePath`**

  パッケージへの署名に使用する証明書へのファイルパスを指定します。

- **`-CertificateStoreLocation`**

  証明書の検索に使用する x.509 証明書ストアの名前を指定します。 既定値は "CurrentUser" で、現在のユーザーが使用している x.509 証明書ストアです。 またはオプションを使用して証明書を指定する場合は、このオプションを使用する必要があり `-CertificateSubjectName` `-CertificateFingerprint` ます。

- **`-CertificateStoreName`**

  証明書の検索に使用する x.509 証明書ストアの名前を指定します。 既定値は "My" で、個人証明書の x.509 証明書ストアです。 またはオプションを使用して証明書を指定する場合は、このオプションを使用する必要があり `-CertificateSubjectName` `-CertificateFingerprint` ます。

- **`-CertificateSubjectName`**

  証明書のローカル証明書ストアの検索に使用する証明書のサブジェクト名を指定します。  検索は、指定された値を使用して、大文字と小文字を区別せずに文字列を比較します。これにより、他のサブジェクト値に関係なく、その文字列を含むサブジェクト名を持つすべての証明書が検索されます。  証明書ストアは、 `-CertificateStoreName` オプションとオプションで指定でき `-CertificateStoreLocation` ます。

- **`-ConfigFile`**

  適用する NuGet 構成ファイル。 指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。

- **`-ForceEnglishOutput`**

  不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。

- **`-HashAlgorithm`**

  パッケージの署名に使用するハッシュアルゴリズム。 既定値は SHA256 です。 指定できる値は SHA256、SHA384、および SHA512 です。

- **`-?|-help`**

  コマンドのヘルプ情報を表示します。

- **`-NonInteractive`**

  ユーザーの入力または確認のプロンプトを表示しません。

- **`-OutputDirectory`**

  署名されたパッケージを保存するディレクトリを指定します。 既定では、元のパッケージは署名付きパッケージによって上書きされます。

- **`-Overwrite`**

  現在の署名を上書きするかどうかを示すには、を切り替えます。 既定では、パッケージに既に署名がある場合、コマンドは失敗します。

- **`-Timestamper`**

  RFC 3161 タイムスタンプサーバーの URL。

- **`-TimestampHashAlgorithm`**

  RFC 3161 タイムスタンプサーバーによって使用されるハッシュアルゴリズム。 既定値は SHA256 です。

- **`-Verbosity [normal|quiet|detailed]`**

  出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。

## <a name="examples"></a>使用例

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
