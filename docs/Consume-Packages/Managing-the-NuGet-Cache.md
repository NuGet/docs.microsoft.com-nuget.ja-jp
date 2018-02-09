---
title: "NuGet でパッケージのキャッシュを管理する方法 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "マシン上に存在する、パッケージのインストールや復元を行うときに使用されるさまざまな NuGet パッケージのキャッシュを管理する方法です。"
keywords: "NuGet パッケージのキャッシュ、パッケージのキャッシュ、NuGet キャッシュ、キャッシュの管理、ローカル NuGet キャッシュ、グローバル NuGet キャッシュ、NuGet ローカル コマンド、キャッシュのクリア"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 84bc34e02572a912fb86ce1a5cf54d8ff212ac6e
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="managing-the-nuget-cache"></a><span data-ttu-id="653dd-104">NuGet のキャッシュを管理する</span><span class="sxs-lookup"><span data-stu-id="653dd-104">Managing the NuGet cache</span></span>

<span data-ttu-id="653dd-105">NuGet では、コンピューターに既に存在するパッケージがダウンロードされないように、また、オフラインのサポートを提供するために、複数のローカル キャッシュを管理します。</span><span class="sxs-lookup"><span data-stu-id="653dd-105">NuGet manages several local caches to avoid downloading packages that are already on the computer, and to provide offline support.</span></span> <span data-ttu-id="653dd-106">NuGet 以降では、ネットワーク接続なしでパッケージのインストールや再インストールを行う場合、自動的にキャッシュにフォール バックされます。</span><span class="sxs-lookup"><span data-stu-id="653dd-106">NuGet automatically falls back to the cache when installing or reinstalling packages without a network connection.</span></span>

<span data-ttu-id="653dd-107">キャッシュの場所は、次の[ローカル コマンド](../tools/cli-ref-locals.md)を使用して取得できます。</span><span class="sxs-lookup"><span data-stu-id="653dd-107">Cache locations are available using the [locals command](../tools/cli-ref-locals.md):</span></span>

```cli
nuget locals all -list
```

<span data-ttu-id="653dd-108">標準出力は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="653dd-108">Typical output is as follows:</span></span>

```output
http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder
```

<span data-ttu-id="653dd-109">パッケージのインストールに関する問題が発生した場合、または、リモート ギャラリーからパッケージをインストールしていることを確認する場合は、`locals -clear` オプションを使用します。</span><span class="sxs-lookup"><span data-stu-id="653dd-109">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals -clear` option:</span></span>

```cli
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

<span data-ttu-id="653dd-110">現在、キャッシュの管理は、Visual Studio 内やパッケージ マネージャー コンソールからではなく、NuGet コマンド ラインからのみサポートされています。</span><span class="sxs-lookup"><span data-stu-id="653dd-110">Note that managing the cache is presently supported only from the NuGet command line, and not within Visual Studio or through the Package Manager Console.</span></span> <span data-ttu-id="653dd-111">また、2.x のキャッシュ管理は、NuGet 3.6 以降ではサポートされません。</span><span class="sxs-lookup"><span data-stu-id="653dd-111">Also, managing the 2.x cache is not supported in NuGet 3.6 and later.</span></span>

<span data-ttu-id="653dd-112">`nuget locals` を使用すると、次のエラーが発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="653dd-112">The following errors can occur when using `nuget locals`:</span></span>

- <span data-ttu-id="653dd-113">**ローカル リソースをクリアできませんでした。1 つ以上のファイルを削除できません**</span><span class="sxs-lookup"><span data-stu-id="653dd-113">**Clearing local resources failed: Unable to delete one or more files**</span></span>
- <span data-ttu-id="653dd-114">**ディレクトリが空ではありません**</span><span class="sxs-lookup"><span data-stu-id="653dd-114">**The directory is not empty**</span></span>

<span data-ttu-id="653dd-115">これらのエラーは、キャッシュ内のファイルを削除するアクセス許可がないか、これらのファイルを削除するために閉じる必要があるキャッシュ内の 1 つまたは複数のファイルが別のプロセスによって使用されていることを示しています。</span><span class="sxs-lookup"><span data-stu-id="653dd-115">These indicate that you either do not have permission to delete files in the cache, or that one or more files in the cache are in use by another process, which must be closed before the those files can be removed.</span></span>
