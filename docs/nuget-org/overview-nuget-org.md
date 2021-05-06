---
title: NuGet.org の概要
description: NuGet.org の概要
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 2dac6ebd6367f3ed1a5ef9e81d843867a4a22f62
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901877"
---
# <a name="overview-of-nugetorg"></a>NuGet.org の概要

NuGet.org は毎日数百万の .NET および .NET Core 開発者に採用されている NuGet パッケージのパブリック ホストです。

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a>NuGet エコシステムでの NuGet.org の役割

NuGet.org 自体にパブリック ホストとしての役割があり、100,000 を超える個別パッケージの中央リポジトリが [nuget.org](https://www.nuget.org) に保持されています。NuGet.org はパッケージ用の唯一のホストではありません。 また、NuGet テクノロジを使用すると、クラウド (Azure DevOps 上など)、プライベート ネットワーク、さらにはご利用のローカル ファイル システムで、プライベートにパッケージをホストすることもできます。 別のホストまたはホスティング オプションに関心がある場合は、「[独自の NuGet フィードをホスティングする](../hosting-packages/overview.md)」を参照してください。

NuGet.org は、NuGet パッケージの他のホストと同様に、パッケージの "*作成者*" とパッケージの "*コンシューマー*" の間の接続ポイントとして機能します。 作成者は便利な NuGet パッケージを作成して公開します。 利用者は、アクセスできるホストで役に立ち互換性のあるパッケージを検索し、ダウンロードしてプロジェクトに組み込みます。 プロジェクトにインストールされたパッケージの API は、プロジェクト コードの他の部分から利用できます。

![パッケージ作成者、パッケージ ホスト、パッケージ利用者の間の関係](media/nuget-roles.png)

## <a name="accounts"></a>[アカウント]

NuGet.org 上でパッケージを公開するには、まず[個人 (ユーザー) アカウント](individual-accounts.md)を作成します。 これが NuGet.org でのお客様の ID になります。

NuGet.org では[組織アカウント](organizations-on-nuget-org.md)を作成することもできます。 組織アカウントには、そのメンバーとして 1 つまたは複数の個人アカウントが含まれます。 メンバーは、所有権用の単一の ID を維持しながら一連のパッケージを管理することができます。 ご自分の個人アカウントによって、任意の数の組織のメンバーになることができます。

パッケージは、個人アカウントに属することができるのと同様に、組織アカウントに属することもできます。 パッケージ コンシューマーには、個人アカウントと組織アカウントの違いは表示されません。どちらもパッケージ `owners` として表示されます。

## <a name="api-keys"></a>API キー

公開する NuGet パッケージ (*.nupkg* ファイル) の用意ができたら、nuget.exe CLI または dotnet.exe CLI のいずれかと、NuGet.org から取得した [API キー](scoped-api-keys.md)を使用して、パッケージを NuGet.org に公開します。

[パッケージを公開](../create-packages/creating-a-package.md)するときには、CLI コマンドに API キー値を含めます。

## <a name="id-prefixes"></a>ID プレフィックス

パッケージを公開するときには、[ID プレフィックスを予約](id-prefix-reservation.md)することにより、ご自分の ID を予約し保護することができます。 パッケージをインストールするとき、パッケージのコンシューマーには、ご使用になるパッケージが詐欺的なものでないことをその識別プロパティで示す追加情報が提供されます。

## <a name="api-endpoint-for-nugetorg"></a>NuGet.org 用の API エンドポイント

NuGet クライアントで NuGet.org をパッケージ リポジトリとして使用するには、次の V3 API エンドポイントを使用する必要があります。 

`https://api.nuget.org/v3/index.json`

より古いクライアントでは、引き続き V2 プロトコルを使用して NuGet.org に到達できます。ただし、V2 プロトコルを使用した場合、NuGet クライアント 3.0 以降でサービスの動作が遅くなり、信頼性が低下します。

`https://www.nuget.org/api/v2` (**V2 プロトコルは非推奨になっています**)
