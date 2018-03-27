---
title: "NuGet CLI コマンドを確認してください |Microsoft ドキュメント"
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "検証コマンドを実行、nuget.exe への参照"
keywords: "nuget の参照の検証、コマンドを確認してください。"
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: 096c79670267d9b602dd6ad30640e832441c31c5
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2018
---
# <a name="verify-command-nuget-cli"></a>コマンド (NuGet CLI) を確認してください。

**適用されます:**消費をパッケージ化&bullet;**サポートされているバージョン:** 4.6 以上

パッケージを検証します。

## <a name="usage"></a>使用法

```cli
nuget verify <package(s)> [options]
```

ここで`<package(s)>`は 1 つ以上`.nupkg`ファイル。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| すべて | パッケージで可能なすべての検証を実行することを指定します。 |
| CertificateFingerprint | 証明書 (s) で署名されたパッケージを署名する必要がありますの 1 つまたは複数の sha-256 証明書指紋を指定します。 Sha-256 証明書フィンガー プリントは、証明書の SHA 256 ハッシュです。 複数の入力は、セミコロンで区切られたにする必要があります。 |
| ConfigFile | NuGet 構成ファイルを適用します。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。|
| ForceEnglishOutput | インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| NonInteractive | ユーザー入力または確認を要求するプロンプトを抑制します。 |
| シグネチャ | パッケージの署名の確認を実行することを指定します。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。 |

## <a name="examples"></a>使用例

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```