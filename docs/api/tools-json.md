---
title: nuget.exe バージョンを検出するための tools.js
description: のエンドポイント
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: eb28ccbc4460663b0f149d2d08e9b47dd69847c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773815"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>nuget.exe バージョンを検出するための tools.js

現在、コンピューター上の最新バージョンの nuget.exe をスクリプトによって取得する方法はいくつかあります。 たとえば、nuget.org からパッケージをダウンロードして抽出することができ [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) ます。これにはいくつかの複雑さがあります。これは、既に nuget.exe (の場合) を持っている必要があるか、 `nuget.exe install` または基本的な解凍ツールを使用して nupkg を解凍し、内部でバイナリを検索する必要があるためです。

既に nuget.exe がある場合は、を使用することもでき `nuget.exe update -self` ますが、nuget.exe の既存のコピーが必要です。 この方法では、最新バージョンも更新されます。 特定のバージョンを使用することはできません。

`tools.json`エンドポイントは、ブートストラップの問題を解決し、ダウンロードする nuget.exe のバージョンを制御できるようにするために使用できます。 これは、CI/CD 環境またはカスタムスクリプトで使用して、nuget.exe のリリースバージョンを検出してダウンロードすることができます。

`tools.json`エンドポイントは、認証されていない HTTP 要求 (PowerShell やなど) を使用してフェッチでき `Invoke-WebRequest` `wget` ます。 JSON デシリアライザーを使用して解析できます。それ以降の nuget.exe ダウンロード Url は、認証されていない HTTP 要求を使用してフェッチすることもできます。

エンドポイントは、メソッドを使用してフェッチでき `GET` ます。

```
GET https://dist.nuget.org/tools.json
```

エンドポイントの [JSON スキーマ](https://json-schema.org/) については、次を参照してください。

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a>応答

応答は、使用可能なすべてのバージョンの nuget.exe を含む JSON ドキュメントです。

ルート JSON オブジェクトには、次のプロパティがあります。

名前      | Type             | 必須
--------- | ---------------- | --------
nuget.exe | オブジェクトの配列 | はい

配列内の各オブジェクト `nuget.exe` には、次のプロパティがあります。

名前     | Type   | 必須 | Notes
-------- | ------ | -------- | -----
version  | string | はい      | SemVer 2.0.0 文字列
url      | string | はい      | このバージョンの nuget.exe をダウンロードするための絶対 URL
準備    | string | はい      | 列挙型文字列
アップロード | string | はい      | バージョンが使用可能になったときの ISO 8601 の概算タイムスタンプ

配列内の項目は、SemVer 2.0.0 order の降順で並べ替えられます。 この保証は、最も高いバージョン番号に関心のあるクライアントの負担を軽減することを目的としています。 ただし、これは、リストが時系列順に並べ替えられていないことを意味します。 たとえば、古いメジャーバージョンが上位のメジャーバージョンより後の日付でサービスされている場合、このサービスバージョンは一覧の先頭に表示されません。 *タイムスタンプ* によって最新バージョンがリリースされるようにするには、単に文字列で配列を並べ替え `uploaded` ます。 これは、 `uploaded` タイムスタンプが [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) 形式であり、辞書式並べ替え (つまり、単純な文字列の並べ替え) を使用して時系列で並べ替えることができるためです。

プロパティは、 `stage` このバージョンのツールがどのように吟味されるかを示します。 

段階              | 意味
------------------ | ------
EarlyAccessPreview | [ダウンロード web ページ](https://www.nuget.org/downloads)にはまだ表示されていないため、パートナーが検証する必要があります
リリース済み           | ダウンロードサイトで利用できますが、大規模な消費にはまだ推奨されていません。
ReleasedAndBlessed | ダウンロードサイトで利用可能であり、使用することをお勧めします。

最新の推奨バージョンを使用するための簡単な方法の1つは、リストの値がである最初のバージョンを取得することです `stage` `ReleasedAndBlessed` 。 これは、バージョンが SemVer 2.0.0 order で並べ替えられているために機能します。

`NuGet.CommandLine`Nuget.org のパッケージは、通常、バージョンでのみ更新され `ReleasedAndBlessed` ます。

### <a name="sample-request"></a>要求のサンプル

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [tools-json.json](./_data/tools-json.json)]
