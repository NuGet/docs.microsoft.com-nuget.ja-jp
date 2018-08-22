---
title: nuget.exe のバージョンを検出するための tools.json
description: エンドポイント
author: jver
ms.author: jver
manager: skofman
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d11e79cd9109e1760189e848e35ff322be026a4d
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2018
ms.locfileid: "40248356"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>nuget.exe のバージョンを検出するための tools.json

今日では、これにはスクリプト可能な方法でコンピューターに最新バージョンの nuget.exe を取得するいくつかの方法があります。 たとえば、ダウンロードして抽出、 [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) nuget.org からパッケージ。Nuget.exe があるかが何らかの複雑性があります (の`nuget.exe install`) か、基本的な解凍ツールを使用して .nupkg を解凍し、バイナリの内側の検索にあります。

Nuget.exe 既にある場合も行えます`nuget.exe update -self`nuget.exe の既存のコピーをしなくても必要です。 このアプローチでは、最新バージョンにしても更新されます。 特定のバージョンの使用はできません。

`tools.json`エンドポイントがあるブートス トラップの問題を解決両方をダウンロードする nuget.exe のバージョンを制御できるようにするとします。 これは、できます CI/CD 環境や、カスタム スクリプトで検出し、任意のリリース バージョンの nuget.exe をダウンロードします。

`tools.json`エンドポイントは、認証されていない HTTP 要求を使用して取得できます (例: `Invoke-WebRequest` powershell または`wget`)。 JSON デシリアライザーを使用して解析できを使用して Url をフェッチすることも、後続の nuget.exe ダウンロードには、HTTP 要求が認証されていません。

使用して、エンドポイントをフェッチすることができます、`GET`メソッド。

    GET https://dist.nuget.org/tools.json

[JSON スキーマ](http://json-schema.org/)のエンドポイントは、ここで使用します。

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a>応答

応答は、すべての利用可能なバージョンの nuget.exe を含む JSON ドキュメントです。

ルート JSON オブジェクトには、次のプロパティがあります。

name      | 種類             | 必須
--------- | ---------------- | --------
nuget.exe | オブジェクトの配列 | 可

内の各オブジェクト、`nuget.exe`配列は、次のプロパティ。

name     | 種類   | 必須 | メモ
-------- | ------ | -------- | -----
version  | string | 可      | SemVer 2.0.0 文字列
url      | string | 可      | このバージョンの nuget.exe をダウンロードするための絶対 URL
ステージ    | string | 可      | 列挙型の文字列
アップロード | string | 可      | バージョンを利用可能であった場合のおおよそのタイムスタンプ

配列内の項目は SemVer 2.0.0 の順序を降順で並べ替えられます。 この保証は、最新バージョンのクライアント上の負担を軽減します。 

`stage`プロパティ vettect このバージョンのツールを示します。 

段階              | 説明
------------------ | ------
EarlyAccessPreview | まだ表示されない、[ダウンロード web ページ](https://www.nuget.org/downloads)とパートナーで検証する必要があります
リリース済み           | まだ広く使用されている使用量のことをお勧めしますのダウンロード サイトで利用可能
ReleasedAndBlessed | ダウンロード サイトで使用可能な従量課金のためお勧め

リストを持つ最初のバージョンを最新の 1 つの簡単な方法、推奨されるバージョンは、 `stage` @property`ReleasedAndBlessed`します。

`NuGet.CommandLine`で nuget.org でパッケージがのみ更新通常`ReleasedAndBlessed`バージョン。

### <a name="sample-request"></a>要求のサンプル

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [tools-json.json](./_data/tools-json.json)]
