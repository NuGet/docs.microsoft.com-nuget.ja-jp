---
title: NuGet CLI verify コマンド
description: Nuget.exe の verify コマンドのリファレンス
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327499"
---
# <a name="verify-command-nuget-cli"></a>verify コマンド (NuGet CLI)

**適用対象:** パッケージ消費&bullet;が**サポートされているバージョン:** 4.6 +

パッケージを検証します。

署名付きパッケージの検証は、.NET Core、Mono、または Windows 以外のプラットフォームではまだサポートされていません。

## <a name="usage"></a>使用法

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

ここ`<package(s)>` で`.nupkg` 、は1つ以上のファイルです。

## <a name="nuget-verify--all"></a>nuget verify -All

パッケージに対して可能なすべての検証を実行することを指定します。

## <a name="nuget-verify--signatures"></a>nuget verify -Signatures

パッケージ署名の検証を実行する必要があることを指定します。

## <a name="options-for-verify--signatures"></a>"verify -Signatures" のオプション

| オプション | 説明 |
| --- | --- |
| CertificateFingerprint | 署名されたパッケージに署名する必要がある証明書の1つまたは複数の 256 SHA-1 証明書の指紋を指定します。 証明書 SHA-256 フィンガープリントは、証明書の SHA-256 ハッシュです。 複数の入力をセミコロンで区切る必要があります。 |

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。|
| ForceEnglishOutput | 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*normal*、*quiet*、*detailed* |

## <a name="examples"></a>使用例

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```
