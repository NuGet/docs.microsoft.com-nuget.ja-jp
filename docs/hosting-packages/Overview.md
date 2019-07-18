---
title: 独自の NuGet フィードのホスティングの概要
description: ローカルまたはリモートのいずれかで、独自の NuGet パッケージ フィードまたはギャラリーをホスティングするためにオープンにされている概要です。
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: f05c3a7a51bdc0760097422004cfc4339bf9ee2c
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426608"
---
# <a name="hosting-your-own-nuget-feeds"></a>独自の NuGet フィードをホスティングする

パッケージをパブリックに利用できるようにする代わりに、組織やワークグループなど、制限された対象ユーザーのみにパッケージをリリースする必要がある可能性があります。 また、一部の会社では、開発者が使用する可能性があるサードパーティ製のライブラリを制限する必要がある場合があります。そのため、開発者に nuget.org ではなく、制限されたパッケージ ソースから引き出すように指示します。

このようなすべての目的のために、NuGet では次の方法でプライベート パッケージ ソースの設定をサポートします。

- ローカル フィード:パッケージは適切なネットワーク ファイル共有に単純に配置され、`nuget init` と `nuget add` を使用して、階層フォルダー構造 (NuGet 3.3 以降) を作成するのが理想的です。 詳細については、「[ローカル フィード](../hosting-packages/local-feeds.md)」を参照してください。
- NuGet.Server:パッケージは、ローカル HTTP サーバー経由で有効にされます。 詳細については、「[NuGet.Server](../hosting-packages/nuget-server.md)」を参照してください。
- NuGet ギャラリー:パッケージは、[NuGet ギャラリー プロジェクト](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com) を使用して、インターネット サーバー上にホストされます。 NuGet ギャラリーは、nuget.org と同様に、ブラウザー内からパッケージを検索できる広範な Web UI など、ユーザーの管理や機能を備えています。

また、次のようなその他のいくつかの NuGet ホスティング製品でも、リモート プライベート フィードをサポートします。

- [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish)。これは、Team Foundation Server 2017 以降でも利用できます。
- [MyGet](http://myget.org)
- [ProGet](http://inedo.com/proget) (Inedo)
- [GitHub パッケージ レジストリ](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- [NuGet Server](http://nugetserver.net/)。Inedo のコミュニティ プロジェクト
- [NuGet Server (オープン ソース)](http://nuget-server.net)。Inedo の NuGet Server と同様のオープンソースの実装
- [LiGet](https://github.com/ai-traders/liget)。Docker の Kestrel 上で実行される NuGet V2 サーバーのオープン ソースの実装
- [BaGet](https://github.com/loic-sharma/BaGet)。ASP.NET Core 上に構築された NuGet V3 サーバーのオープン ソースの実装
- [Sleet](https://github.com/emgarten/sleet)。オープン ソースの NuGet V3 静的フィード ジェネレーター
- [Artifactory](https://www.jfrog.com/artifactory/) (JFrog)
- [Nexus](http://www.sonatype.org/nexus/) (Sonatype)
- [TeamCity](https://www.jetbrains.com/teamcity/) (JetBrains)

パッケージがどのようにホストされているかに関係なく、`NuGet.Config` で利用可能なソースの一覧にパッケージを追加して、アクセスします。 これは、「[パッケージ ソース](../tools/package-manager-ui.md#package-sources)」に示されているように Visual Studio で、またはコマンド ラインから [`nuget sources`](../tools/cli-ref-sources.md) を使用して実行できます。 ソースへのパスは、ローカル フォルダーのパス名、ネットワーク名、または URL にすることができます。
