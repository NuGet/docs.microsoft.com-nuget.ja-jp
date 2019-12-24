---
title: NuGet クライアント SDK
description: API は進化していますが、まだ文書化されていませんが、例については Dave Glick のブログを参照してください。
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 873bde467a39653b818b49173d53bc983e99d1b9
ms.sourcegitcommit: f9645fc5f49c18978e12a292a3f832e162e069d5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72924613"
---
# <a name="nuget-client-sdk"></a>NuGet クライアント SDK

Nuget*クライアント SDK*は、 [nuget を中心](https://www.nuget.org/packages/NuGet.Packaging)に配置[された](https://www.nuget.org/packages/NuGet.Protocol)nuget パッケージのグループを参照[します](https://www.nuget.org/packages/NuGet.Commands)。 これらのパッケージは、以前の[NuGet のコア](https://www.nuget.org/packages/NuGet.Core/)ライブラリに代わるものです。

> [!Note]
>  NuGet サーバープロトコルに関するドキュメントについては、 [Nuget サーバー API](~/api/overview.md)に関するドキュメントを参照してください。

## <a name="source-code"></a>ソースコード

ソースコードは、プロジェクト[nuget/nuget. Client](https://github.com/NuGet/NuGet.Client)で GitHub に公開されています。

## <a name="third-party-documentation"></a>サードパーティのドキュメント

API の一部の例とドキュメントは、次のブログシリーズで、発行済み2016を使用して確認できます。

- [NuGet v3 ライブラリの調査、パート 1: 概要と概念](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [NuGet v3 ライブラリの調査、パート 2: パッケージの検索](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [NuGet v3 ライブラリの調査、パート 3: パッケージのインストール](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> これらのブログ投稿は、 **3.4.3**バージョンの NUGET クライアント SDK パッケージがリリースされた直後に作成されました。
> 新しいバージョンのパッケージは、ブログの投稿の情報と互換性がない可能性があります。

Martin Björkström は、次のように、nuget パッケージをインストールするための NuGet クライアント SDK の使用に関する別のアプローチを導入した、彼のブログシリーズを作成しました。

- [NuGet v3 ライブラリの再度](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
