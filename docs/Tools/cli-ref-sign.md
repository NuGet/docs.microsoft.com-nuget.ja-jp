---
title: NuGet CLI 記号コマンド
description: Nuget.exe 記号コマンドのリファレンス
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7e84d794b802cfd69c785f720280fd5c022a46f6
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="sign-command-nuget-cli"></a>サインオン コマンド (NuGet CLI)

**適用されます:** パッケージの作成&bullet;**サポートされているバージョン:** 4.6 以上

証明書では、最初の引数に一致するすべてのパッケージに署名します。 ファイルとは、サブジェクト名または拇印を提供することで、証明書ストアにインストールされている証明書から秘密キー付きの証明書を取得できます。

パッケージの署名はまだサポートされていません、Mono で、または Windows 以外のプラットフォーム上の .NET Core で。

## <a name="usage"></a>使用法

```cli
nuget sign <package(s)> [options]
```

ここで`<package(s)>`は 1 つ以上`.nupkg`ファイル。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| CertificateFingerprint | ローカルの証明書ストア、証明書を検索するために使用する証明書の sha-1 フィンガー プリントを指定します。 |
| CertificatePassword | 必要な場合は、証明書のパスワードを指定します。 証明書はパスワードで保護されたパスワードが指定されていない場合、コマンドはパスワードを要求、実行時にしない限り、非対話型のオプションが渡されました。 |
| CertificatePath | パッケージの署名に使用する証明書へのファイル パスを指定します。 |
| CertificateStoreLocation | 証明書を検索する X.509 証明書ストアの使用の名前を指定します。 既定値は、現在のユーザーによって使用される X.509 証明書ストアである"CurrentUser"です。 CertificateSubjectName - または - CertificateFingerprint オプションを使用して証明書を指定する場合、このオプションを使用する必要があります。 |
| CertificateStoreName | 使用して証明書を検索する X.509 証明書ストアの名前を指定します。 既定値は"My"、個人証明書の X.509 証明書ストア。 CertificateSubjectName - または - CertificateFingerprint オプションを使用して証明書を指定する場合、このオプションを使用する必要があります。 |
| CertificateSubjectName | ローカルの証明書ストア、証明書を検索するために使用する証明書のサブジェクト名を指定します。  検索では、サブジェクト名の他のサブジェクト値に関係なく、その文字列を含むすべての証明書を見つけることが指定された値を使用して、大文字と小文字の文字列比較。  -証明および - CertificateStoreLocation オプションでは、証明書ストアを指定できます。 |
| ConfigFile | NuGet 構成ファイルを適用します。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。|
| ForceEnglishOutput | インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| HashAlgorithm | パッケージの署名に使用するハッシュ アルゴリズム。 既定値は SHA256 です。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| NonInteractive | ユーザー入力または確認を要求するプロンプトを抑制します。 |
| OutputDirectory | 署名されたパッケージを保存するディレクトリを指定します。 既定では、元のパッケージは、署名されたパッケージによって上書きされます。 |
| 上書き | かどうか、現在の署名を上書きするかを示すスイッチです。 既定では、パッケージが署名を既に存在する場合に、コマンドが失敗します。 |
| Timestamper | RFC 3161 タイム スタンプ サーバーの URL。 |
| TimestampHashAlgorithm | RFC 3161 タイム スタンプ サーバーで使用されるハッシュ アルゴリズム。 既定値は SHA256 です。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。 |

## <a name="examples"></a>使用例

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```