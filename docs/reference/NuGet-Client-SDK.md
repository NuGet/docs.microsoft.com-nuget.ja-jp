---
title: NuGet クライアント SDK
description: API は進化し、まだ文書化されたが例としては、Dave Glick のブログでご確認いただけます。
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 97ed3ec7d41d2847c0521af69373a1871eb585dd
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324683"
---
# <a name="nuget-client-sdk"></a>NuGet クライアント SDK

> [!Note]
> 混同しないように、 [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)

*NuGet クライアント SDK*を中心とした .NET ライブラリのグループを指す[NuGet.Client](https://www.nuget.org/packages/NuGet.Client)、 [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging)、および[NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol). これらのパッケージが、以前に置き換える[NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)ライブラリ。

すぐに文書化される安定した領域があることに取り組んでいます。

## <a name="source-code"></a>ソース コード

プロジェクトのソース コードが GitHub で公開されて[NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client)します。

## <a name="third-party-documentation"></a>サード パーティのドキュメント

Dave Glick、2016 を発行して、次のブログ シリーズでは、例、および API の一部のドキュメントを見つけることができます。

- [NuGet v3 ライブラリ、第 1 部を表示するには。概要と概念](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [NuGet v3 ライブラリ、第 2 部を表示するには。パッケージを検索](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [NuGet v3 ライブラリ、第 3 部を表示するには。パッケージをインストールします。](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> 次のブログ投稿は、直後に記述された、 **3.4.3**クライアント SDK パッケージがリリースされた NuGet のバージョン。
> 新しいバージョンのパッケージは、ブログの投稿の情報と互換性のあることがあります。

Martin Björkström では、NuGet クライアント SDK を使用して NuGet パッケージをインストールするために、別のアプローチを紹介しています Dave Glick のブログ シリーズをフォロー アップのブログの投稿を行いました。

- [NuGet v3 ライブラリの再考](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
