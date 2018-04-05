---
title: NuGet でパッケージのキャッシュを管理する方法 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: マシン上に存在する、パッケージのインストールや復元を行うときに使用されるさまざまな NuGet パッケージのキャッシュを管理する方法です。
keywords: NuGet パッケージのキャッシュ、パッケージのキャッシュ、NuGet キャッシュ、キャッシュの管理、ローカル NuGet キャッシュ、グローバル NuGet キャッシュ、NuGet ローカル コマンド、キャッシュのクリア
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 09b3560d67ff8a38677dd1e27d85cdf234495aae
ms.sourcegitcommit: 718e6cb88e45fa07c85d653f216bf92eaaf81625
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2018
---
# <a name="managing-the-nuget-cache"></a>NuGet のキャッシュを管理する

NuGet では、コンピューターに既に存在するパッケージがダウンロードされないように、また、オフラインのサポートを提供するために、複数のローカル キャッシュを管理します。 NuGet 以降では、ネットワーク接続なしでパッケージのインストールや再インストールを行う場合、自動的にキャッシュにフォール バックされます。

キャッシュの場所は、次の[ローカル コマンド](../tools/cli-ref-locals.md)を使用して取得できます。

```cli
nuget locals all -list
```

標準出力は次のとおりです。

```output
http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder
```

パッケージのインストールに関する問題が発生した場合、または、リモート ギャラリーからパッケージをインストールしていることを確認する場合は、`locals -clear` オプションを使用します。

```cli
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

現在、キャッシュの管理は、Visual Studio 内やパッケージ マネージャー コンソールからではなく、NuGet コマンド ラインからのみサポートされています。 また、2.x のキャッシュ管理は、NuGet 3.6 以降ではサポートされません。

`nuget locals` を使用すると、次のエラーが発生することがあります。

- **ローカル リソースをクリアできませんでした。1 つ以上のファイルを削除できません**
- **ディレクトリが空ではありません**

これらのエラーは、キャッシュ内のファイルを削除する権限がないか、キャッシュ内の 1 つ以上のファイルが他のプロセスによって使用されていることを示しています。その場合は削除する前にファイルを閉じる必要があります。
