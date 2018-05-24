---
title: NuGet CLI コマンドを確認してください。
description: 検証コマンドを実行、nuget.exe への参照
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c80334104f7d8b2ccbf16ea2c11dc37b39408eeb
ms.sourcegitcommit: c8485dc61469511485367d2067b97d6f74b49f6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2018
---
# <a name="verify-command-nuget-cli"></a>コマンド (NuGet CLI) を確認してください。

**適用されます:** 消費をパッケージ化&bullet;**サポートされているバージョン:** 4.6 以上

パッケージを検証します。

署名付きパッケージの検証は、Mono で、または Windows 以外のプラットフォーム上の .NET Core でまだサポートされていません。

## <a name="usage"></a>使用法

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

ここで`<package(s)>`は 1 つ以上`.nupkg`ファイル。

## <a name="nuget-verify--all"></a>nuget を確認してください - すべて

パッケージで可能なすべての検証を実行することを指定します。

## <a name="nuget-verify--signatures"></a>nuget 署名を検証する-

パッケージの署名の確認を実行することを指定します。

## <a name="options-for-verify--signatures"></a>「署名の確認-」のオプション

| オプション | 説明 |
| --- | --- |
| CertificateFingerprint | 証明書 (s) で署名されたパッケージを署名する必要がありますの 1 つまたは複数の sha-256 証明書指紋を指定します。 Sha-256 証明書フィンガー プリントは、証明書の SHA 256 ハッシュです。 複数の入力は、セミコロンで区切られたにする必要があります。 |

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | NuGet 構成ファイルを適用します。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。|
| ForceEnglishOutput | インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。 |

## <a name="examples"></a>使用例

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```