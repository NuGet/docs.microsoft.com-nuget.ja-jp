---
title: ネイティブ NuGet パッケージを作成する
description: C++ プロジェクト用にマネージド コードではなく、C++ コードを含むネイティブ NuGet パッケージを作成する方法に関する詳細です。
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e0ec5323f7be53bef6637ad69540a66abbf22711
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "69520522"
---
# <a name="creating-native-packages"></a>ネイティブ パッケージを作成する

ネイティブ パッケージには、マネージド アセンブリではなくネイティブ バイナリが含まれているため、C++ (または同様の) プロジェクト内で使用できます。 (「使用」セクションの「[ネイティブ C++ パッケージ](../consume-packages/finding-and-choosing-packages.md#native-c-packages)」を参照してください。)

C++ プロジェクトで使用できるようにするには、パッケージが `native` フレームワークを対象にする必要があります。 現時点では、NuGet ですべての C++ プロジェクトが同様に処理されるように、このフレームワークに関連付けられているバージョン番号はありません。

> [!Note]
> 他の開発者がタグを検索して、お客様のパッケージを見つけられるように、必ず *の* セクションに `<tags>`native`.nuspec` を含めてください。

`native` を対象とするネイティブ NuGet パッケージでは、`\build`、`\content`、および `\tools` フォルダーにファイルが提供されます。`\lib` はこの場合、使用されません (NuGet では、直接 C++ プロジェクトに参照を追加することはできません)。 パッケージには、`\build` のターゲットとプロパティ ファイルも含まれる場合があります。このファイルは、NuGet によってパッケージを使用するプロジェクトに自動的にインポートされます。 これらのファイルは、`.targets` や `.props` の拡張子を含むパッケージ ID と同じ名前になります。 たとえば、[cpprestsdk](https://nuget.org/packages/cpprestsdk/) パッケージでは、`cpprestsdk.targets` フォルダーに `\build` ファイルが含まれます。

`\build` フォルダーは、ネイティブ パッケージだけでなく、すべての NuGet パッケージに使用できます。 `\build` フォルダーでは、`\content`、`\lib`、`\tools` フォルダーと同様に、ターゲット フレームワークが尊重されます。 つまり、`\build\net40` フォルダーと `\build\net45` フォルダーを作成でき、NuGet では適切なプロパティ ファイルとターゲット ファイルがプロジェクトにインポートされるということです。 (MSBuild ターゲットをインポートするために、PowerShell スクリプトを使用する必要はありません。)
