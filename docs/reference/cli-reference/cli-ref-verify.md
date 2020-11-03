---
title: NuGet CLI 確認コマンド
description: nuget.exe verify コマンドのリファレンス
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7ce08f11195437e94bfe69883ff525e9ad3a73f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238141"
---
# <a name="verify-command-nuget-cli"></a>verify コマンド (NuGet CLI)

**適用対象:** パッケージの使用量が &bullet; **サポートされているバージョン:** 4.6 以降

パッケージを検証します。

署名付きパッケージの検証は、Mono ではまだサポートされていません。

## <a name="usage"></a>使用

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

ここ `<package(s)>` で、は1つ以上の `.nupkg` ファイルです。

## <a name="nuget-verify--all"></a>nuget 検証-すべて

可能なすべての検証をパッケージに対して実行する必要があることを指定します。

## <a name="nuget-verify--signatures"></a>nuget の検証-署名

パッケージ署名の検証を実行する必要があることを指定します。

## <a name="options-for-verify--signatures"></a>"確認-署名" のオプション

- **`-CertificateFingerprint`**

  署名されたパッケージに署名する必要がある証明書の1つまたは複数の 256 SHA-1 証明書の指紋を指定します。 証明書 SHA-256 フィンガープリントは、証明書の SHA-256 ハッシュです。 複数の入力をセミコロンで区切る必要があります。

## <a name="options"></a>オプション

- **`-ConfigFile`**

  適用する NuGet 構成ファイル。 指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。

- **`-ForceEnglishOutput`**

  不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。

- **`-?|-help`**

  コマンドのヘルプ情報を表示します。

- **`-NonInteractive`**

  ユーザーの入力または確認のプロンプトを表示しません。

- **`-Verbosity [normal|quiet|detailed]`**

  出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。

## <a name="examples"></a>使用例

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```