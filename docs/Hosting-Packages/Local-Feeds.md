---
title: "ローカル NuGet フィードを設定する | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "ローカル ネットワーク上のフォルダーを使用して、NuGet パッケージのローカル フィードを作成する方法"
keywords: "NuGet フィード、NuGet ギャラリー、ローカル パッケージ フィード"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0b8633db78b19fecddeb057a9f287ef971aef27a
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="local-feeds"></a>ローカル フィード

ローカル NuGet パッケージのフィードは単に、パッケージを配置するローカル ネットワーク上 (または独自のコンピューターだけ) の階層フォルダー構造です。 これらのフィードは、CLI、パッケージ マネージャー UI、およびパッケージ マネージャー コンソールを使用して、その他すべての NuGet の操作でパッケージ ソースとして使用できます。

ソースを有効にするには、[パッケージ マネージャー UI](../tools/package-manager-ui.md#package-sources) または [`nuget sources`](../tools/cli-ref-sources.md) コマンドを使用して、そのパス名 (`\\myserver\packages` など) をソースの一覧に追加します。

> [!Note]
> 階層フォルダーの構造は、NuGet 3.3 以降でサポートされます。 古いバージョンの NuGet は、パフォーマンスが階層構造よりもはるかに劣る、パッケージを含む 1 つのフォルダーのみを使用します。

## <a name="initializing-and-maintaining-hierarchical-folders"></a>階層フォルダーの初期化と維持

階層でバージョン管理されたフォルダー ツリーは、次の一般的な構造になります。

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

[`nuget add`](../tools/cli-ref-add.md) コマンドを使用してパッケージをフィードにコピーすると、NuGet ではこの構造が自動的に作成されます。

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

`nuget add` コマンドは、一度に 1 つのパッケージを使用して動作します。これは、複数のパッケージを含むフィードを設定するときに、不便な場合があります。

このような場合、[`nuget init`](../tools/cli-ref-init.md) コマンドを使用して、それぞれ個別に `nuget add` を実行するように、フォルダーのすべてのパッケージをフィードにコピーします。 たとえば、次のコマンドでは、すべてのパッケージを `c:\packages` から `\\myserver\packages` の階層ツリーにコピーします。

```cli
nuget init c:\packages \\myserver\packages
```

`add` コマンドのように、`init` では、パッケージの識別子ごとにフォルダーを作成します。各フォルダーには、バージョン番号のフォルダーが含まれ、そこには適切なパッケージが含まれます。
