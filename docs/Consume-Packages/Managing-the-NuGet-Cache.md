---
title: "NuGet でパッケージのキャッシュを管理する方法 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3932217d-780d-4bd1-ad15-767acd3e8870
description: "マシン上に存在する、パッケージのインストールや復元を行うときに使用されるさまざまな NuGet パッケージのキャッシュを管理する方法です。"
keywords: "NuGet パッケージのキャッシュ、パッケージのキャッシュ、NuGet キャッシュ、キャッシュの管理、ローカル NuGet キャッシュ、グローバル NuGet キャッシュ、NuGet ローカル コマンド、キャッシュのクリア"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6e76c219ba420eb285af20e67b26dcdceebb6bab
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="managing-the-nuget-cache"></a>NuGet のキャッシュを管理する

NuGet では、コンピューターに既に存在するパッケージがダウンロードされないように、また、オフラインのサポートを提供するために、複数のローカル キャッシュを管理します。 NuGet 2.8 以降では、ネットワーク接続なしでパッケージのインストールや再インストールを行う場合、自動的にキャッシュにフォール バックされます。

キャッシュの場所は、次の[ローカル コマンド](../tools/cli-ref-locals.md)を使用して取得できます。

```
nuget locals all -list
```

標準出力は次のとおりです。

    http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
    packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
    global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
    temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder

パッケージのインストールに関する問題が発生した場合、または、リモート ギャラリーからパッケージをインストールしていることを確認する場合は、`locals -clear` オプションを使用します。

```
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

現在、キャッシュの管理は、Visual Studio 内やパッケージ マネージャー コンソールからではなく、NuGet コマンド ラインからのみサポートされています。 また、2.x のキャッシュ管理は、NuGet 3.6 以降ではサポートされません。

`nuget locals` を使用すると、次のエラーが発生することがあります。

* **ローカル リソースをクリアできませんでした。1 つ以上のファイルを削除できません**
* **ディレクトリが空ではありません**

これらのエラーは、キャッシュ内のファイルを削除するアクセス許可がないか、これらのファイルを削除するために閉じる必要があるキャッシュ内の 1 つまたは複数のファイルが別のプロセスによって使用されていることを示しています。
