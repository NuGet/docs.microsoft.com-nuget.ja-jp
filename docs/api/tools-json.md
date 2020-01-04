---
title: nuget.exeバージョンを検出するためのtools.json
description: のエンドポイント
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: a186db9727bdfd1b55bf73a1f29283352555dede
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611030"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>nuget.exeバージョンを検出するためのtools.json

現在、コンピューター上の最新バージョンの nuget.exe をスクリプト可能な方法で入手するには、いくつかの方法があります。 たとえば、nuget.org から[`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/)パッケージをダウンロードして抽出することができます。これにはいくつかの複雑さがあります。これは、既に nuget.exe がある (`nuget.exe install`) 必要があるか、または基本的な解凍ツールを使用して nupkg を解凍し、内部でバイナリを検索する必要があるためです。

既に nuget.exe を持っている場合は、`nuget.exe update -self`を使用することもできますが、これには nuget.exe の既存のコピーが必要です。 この方法では、最新バージョンも更新されます。 特定のバージョンを使用することはできません。

`tools.json` エンドポイントを使用して、ブートストラップの問題を解決し、ダウンロードする nuget.exe のバージョンを制御することができます。 これは、CI/CD 環境またはカスタムスクリプトで使用して、任意のリリースバージョンの nuget.exe を検出してダウンロードすることができます。

`tools.json` エンドポイントは、認証されていない HTTP 要求 (PowerShell や `wget`の `Invoke-WebRequest` など) を使用してフェッチできます。 これは、JSON デシリアライザーを使用して解析できます。その後の nuget ダウンロード Url は、認証されていない HTTP 要求を使用してフェッチすることもできます。

エンドポイントは、`GET` メソッドを使用してフェッチできます。

    GET https://dist.nuget.org/tools.json

エンドポイントの[JSON スキーマ](https://json-schema.org/)については、次を参照してください。

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a>応答

応答は、使用可能なすべてのバージョンの nuget.exe を含む JSON ドキュメントです。

ルート JSON オブジェクトには、次のプロパティがあります。

名      | [種類]             | 必要
--------- | ---------------- | --------
nuget.exe | オブジェクトの配列 | 可

`nuget.exe` 配列の各オブジェクトには、次のプロパティがあります。

名     | [種類]   | 必要 | ノート
-------- | ------ | -------- | -----
version  | string | 可      | SemVer 2.0.0 文字列
url      | string | 可      | このバージョンの nuget.exe をダウンロードするための絶対 URL
stage    | string | 可      | 列挙型文字列
uploaded | string | 可      | バージョンが使用可能になったときの ISO 8601 の概算タイムスタンプ

配列内の項目は、SemVer 2.0.0 order の降順で並べ替えられます。 この保証は、最も高いバージョン番号に関心のあるクライアントの負担を軽減することを目的としています。 ただし、これは、リストが時系列順に並べ替えられていないことを意味します。 たとえば、古いメジャーバージョンが上位のメジャーバージョンより後の日付でサービスされている場合、このサービスバージョンは一覧の先頭に表示されません。 *タイムスタンプ*によって最新バージョンがリリースされるようにするには、単に `uploaded` 文字列で配列を並べ替えます。 これは、`uploaded` タイムスタンプが[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)形式であり、辞書式並べ替え (つまり、単純な文字列の並べ替え) を使用して時系列で並べ替えることができるためです。

`stage` プロパティは、このバージョンのツールがどのように吟味されるかを示します。 

段階              | 説明
------------------ | ------
EarlyAccessPreview | [ダウンロード web ページ](https://www.nuget.org/downloads)にはまだ表示されていないため、パートナーが検証する必要があります
Released           | ダウンロードサイトで利用できますが、大規模な消費にはまだ推奨されていません。
ReleasedAndBlessed | ダウンロードサイトで利用可能であり、使用することをお勧めします。

最新の推奨バージョンを使用するための簡単な方法の1つは、リスト内の `stage` 値が `ReleasedAndBlessed`の最初のバージョンを取得することです。 これは、バージョンが SemVer 2.0.0 order で並べ替えられているために機能します。

Nuget.org の `NuGet.CommandLine` パッケージは、通常、`ReleasedAndBlessed` バージョンでのみ更新されます。

### <a name="sample-request"></a>要求のサンプル

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [tools-json.json](./_data/tools-json.json)]
