---
title: sign コマンド (NuGet CLI)
description: Nuget.exe のサインオン コマンドのリファレンス
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546364"
---
# <a name="sign-command-nuget-cli"></a>sign コマンド (NuGet CLI)

**適用対象:** パッケージの作成&bullet;**サポートされているバージョン:** 4.6 以降

証明書では、最初の引数に一致するすべてのパッケージに署名します。 ファイルから、またはサブジェクト名または拇印を提供することで、証明書ストアにインストールされている証明書から秘密キーで証明書を取得できます。

パッケージの署名はまだサポートされていませんで .NET Core、Mono、または Windows 以外のプラットフォームで。

## <a name="usage"></a>使用法

```cli
nuget sign <package(s)> [options]
```

場所`<package(s)>`は 1 つ以上`.nupkg`ファイル。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| CertificateFingerprint | 証明書のローカル証明書ストアを検索するために使用する証明書の sha-1 で指紋を指定します。 |
| CertificatePassword | 必要な場合は、証明書のパスワードを指定します。 証明書がパスワードで保護されたパスワードが指定されていない場合、コマンドはパスワードを要求、実行時にしない限り、非対話型のオプションが渡されます。 |
| CertificatePath | パッケージの署名に使用される証明書へのファイル パスを指定します。 |
| CertificateStoreLocation | 証明書を検索する X.509 証明書ストアの使用の名前を指定します。 既定値は"CurrentUser"、現在のユーザーによって使用される X.509 証明書ストアです。 CertificateSubjectName - または - CertificateFingerprint オプションを使用して証明書を指定するときに、このオプションを使用する必要があります。 |
| CertificateStoreName | 使用して証明書を検索する X.509 証明書ストアの名前を指定します。 "My"、個人用証明書の X.509 証明書ストアに既定値です。 CertificateSubjectName - または - CertificateFingerprint オプションを使用して証明書を指定するときに、このオプションを使用する必要があります。 |
| CertificateSubjectName | 証明書のローカル証明書ストアを検索するために使用する証明書のサブジェクト名を指定します。  検索では、サブジェクト名の他のサブジェクト値に関係なく、その文字列を含むすべての証明書を検索、指定された値を使用して、大文字の文字列比較。  -CertificateStoreName および - CertificateStoreLocation オプションでは、証明書ストアを指定できます。 |
| ConfigFile | 適用する NuGet 構成ファイル。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。|
| ForceEnglishOutput | インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| HashAlgorithm | パッケージの署名に使用するハッシュ アルゴリズム。 既定値は SHA256 です。 |
| ヘルプ | ヘルプのコマンドの情報を表示します。 |
| NonInteractive | ユーザー入力や確認のプロンプトを抑制します。 |
| OutputDirectory | 署名付きパッケージを保存するディレクトリを指定します。 既定では、元のパッケージは署名付きパッケージによって上書きされます。 |
| 上書き | スイッチを示すかどうかは、現在の署名を上書きする必要があります。 既定では、パッケージが既に署名する場合に、コマンドが失敗します。 |
| Timestamper | RFC 3161 タイム スタンプ サーバーの URL。 |
| TimestampHashAlgorithm | RFC 3161 タイム スタンプ サーバーで使用されるハッシュ アルゴリズム。 既定値は SHA256 です。 |
| 詳細度 | 出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。 |

## <a name="examples"></a>使用例

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
