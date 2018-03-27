---
title: "ネイティブ NuGet パッケージを作成する | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "C++ プロジェクト用にマネージ コードではなく、C++ コードを含むネイティブ NuGet パッケージを作成する方法に関する詳細です。"
keywords: "NuGet ネイティブ パッケージ、NuGet C++ パッケージ、ネイティブ コード パッケージ、C++ プロジェクトを対象とする"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 71f4eca411d520630ca7d77165b8f03cd32af290
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="creating-native-packages"></a>ネイティブ パッケージを作成する

ネイティブ パッケージには、マネージ コードの代わりに、C++ プロジェクト内で使用することを可能にするネイティブ C++ コードが含まれます。 (「使用」セクションの「[ネイティブ C++ パッケージ](../consume-packages/finding-and-choosing-packages.md#native-cpp-packages)」を参照してください。)

C++ プロジェクトで使用できるようにするには、パッケージが `native` フレームワークを対象にする必要があります。 現時点では、NuGet ですべての C++ プロジェクトが同様に処理されるように、このフレームワークに関連付けられているバージョン番号はありません。

> [!Note]
> 他の開発者がタグを検索して、お客様のパッケージを見つけられるように、必ず `.nuspec` の `<tags>` セクションに *native* を含めてください。

`native` を対象とするネイティブ NuGet パッケージでは、`\build`、`\content`、および `\tools` フォルダーにファイルが提供されます。`\lib` はこの場合、使用されません (NuGet では、直接 C++ プロジェクトに参照を追加することはできません)。 パッケージには、`\build` のターゲットとプロパティ ファイルも含まれる場合があります。このファイルは、NuGet によってパッケージを使用するプロジェクトに自動的にインポートされます。 これらのファイルは、`.targets` や `.props` の拡張子を含むパッケージ ID と同じ名前になります。 たとえば、[cpprestsdk](https://nuget.org/packages/cpprestsdk/) パッケージでは、`\build` フォルダーに `cpprestsdk.targets` ファイルが含まれます。

`\build` フォルダーは、ネイティブ パッケージだけでなく、すべての NuGet パッケージに使用できます。 `\build` フォルダーでは、`\content`、`\lib`、`\tools` フォルダーと同様に、ターゲット フレームワークが尊重されます。 つまり、`\build\net40` フォルダーと `\build\net45` フォルダーを作成でき、NuGet では適切なプロパティ ファイルとターゲット ファイルがプロジェクトにインポートされるということです。 (MSBuild ターゲットをインポートするために、PowerShell スクリプトを使用する必要はありません。)
