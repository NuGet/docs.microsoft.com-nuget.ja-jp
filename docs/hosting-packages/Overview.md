---
title: 独自の NuGet フィードのホスティングの概要
description: ローカルまたはリモートのいずれかで、独自の NuGet パッケージ フィードまたはギャラリーをホスティングするためにオープンにされている概要です。
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 81acf15ac69d78d39d2784e77c18ba38bfea126d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "75385543"
---
# <a name="hosting-your-own-nuget-feeds"></a>独自の NuGet フィードをホスティングする

パッケージをパブリックに利用できるようにする代わりに、組織やワークグループなど、制限された対象ユーザーのみにパッケージをリリースする必要がある可能性があります。 また、一部の会社では、開発者が使用する可能性があるサードパーティ製のライブラリを制限する必要がある場合があります。そのため、開発者に nuget.org ではなく、制限されたパッケージ ソースから引き出すように指示します。

このようなすべての目的のために、NuGet では次の方法でプライベート パッケージ ソースの設定をサポートします。

- ローカル フィード: パッケージは適切なネットワーク ファイル共有に単純に配置され、`nuget init` と `nuget add` を使用して、階層フォルダー構造 (NuGet 3.3 以降) を作成するのが理想的です。 詳細については、「[ローカル フィード](../hosting-packages/local-feeds.md)」を参照してください。
- NuGet.Server: パッケージは、ローカル HTTP サーバー経由で有効にされます。 詳細については、「[NuGet.Server](../hosting-packages/nuget-server.md)」を参照してください。
- NuGet ギャラリー: パッケージは、[NuGet ギャラリー プロジェクト](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com) を使用して、インターネット サーバー上にホストされます。 NuGet ギャラリーは、nuget.org と同様に、ブラウザー内からパッケージを検索できる広範な Web UI など、ユーザーの管理や機能を備えています。

リモート プライベート フィードをサポートする [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) や [GitHub パッケージ レジストリ](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)など、他のいくつかの NuGet ホスティング製品もあります。 このような製品の一覧を次に示します。

- [Artifactory](https://www.jfrog.com/artifactory/) (JFrog)
- [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish)。これは、Team Foundation Server 2017 以降でも利用できます。
- [BaGet](https://github.com/loic-sharma/BaGet)。ASP.NET Core 上に構築された NuGet V3 サーバーのオープン ソースの実装
- [Cloudsmith](https://cloudsmith.io/l/nuget-feed/)。フル マネージド パッケージ管理の SaaS
- [GitHub パッケージ レジストリ](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- [LiGet](https://github.com/ai-traders/liget)。Docker の Kestrel 上で実行される NuGet V2 サーバーのオープン ソースの実装
- [MyGet](https://myget.org)
- [Nexus Repository OSS](https://www.sonatype.com/nexus-repository-oss) (Sonatype)。
- [NuGet Server (オープン ソース)](https://github.com/svenkle/nuget-server)。Inedo の NuGet Server と同様のオープンソースの実装
- [NuGet Server](http://nugetserver.net/)。Inedo のコミュニティ プロジェクト
- [ProGet](https://inedo.com/proget) (Inedo)
- [Sleet](https://github.com/emgarten/sleet)。オープン ソースの NuGet V3 静的フィード ジェネレーター
- [TeamCity](https://www.jetbrains.com/teamcity/) (JetBrains)

パッケージがどのようにホストされているかに関係なく、`NuGet.Config` で利用可能なソースの一覧にパッケージを追加して、アクセスします。 これは、「[パッケージ ソース](../consume-packages/install-use-packages-visual-studio.md#package-sources)」に示されているように Visual Studio で、またはコマンド ラインから [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) を使用して実行できます。 ソースへのパスは、ローカル フォルダーのパス名、ネットワーク名、または URL にすることができます。
