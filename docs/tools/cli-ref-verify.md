---
title: NuGet CLI verify コマンド
description: Nuget.exe の verify コマンドのリファレンス
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 127f7a549c0a213f319c8820293646b302830436
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545214"
---
# <a name="verify-command-nuget-cli"></a>verify コマンド (NuGet CLI)

**適用対象:** 消費をパッケージ化&bullet;**サポートされているバージョン:** 4.6 以降

パッケージを確認します。

.NET Core、Mono、または Windows 以外のプラットフォーム上で、署名済みパッケージの検証がまだサポートされていません。

## <a name="usage"></a>使用法

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

場所`<package(s)>`は 1 つ以上`.nupkg`ファイル。

## <a name="nuget-verify--all"></a>nuget 検証 - すべて

パッケージで可能なすべての検証を実行することを指定します。

## <a name="nuget-verify--signatures"></a>nuget の検証 - 署名

パッケージの署名の検証を実行することを指定します。

## <a name="options-for-verify--signatures"></a>「署名の検証-」のオプション

| オプション | 説明 |
| --- | --- |
| CertificateFingerprint | 証明書 (s) で署名する署名付きパッケージの 1 つまたは複数の sha-256 証明書指紋を指定します。 Sha-256 証明書フィンガー プリントは、証明書の SHA 256 ハッシュです。 複数の入力には、セミコロンで区切った必要があります。 |

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。|
| ForceEnglishOutput | インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。 |

## <a name="examples"></a>使用例

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```
