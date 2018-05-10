---
title: ネイティブ NuGet パッケージを作成する
description: C++ プロジェクト用にマネージ コードではなく、C++ コードを含むネイティブ NuGet パッケージを作成する方法に関する詳細です。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 1fa8bf23a3fbed686b99f1c783b0ce55b373e548
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="creating-native-packages"></a>ネイティブ パッケージを作成する

ネイティブ パッケージには、マネージ コードの代わりに、C++ プロジェクト内で使用することを可能にするネイティブ C++ コードが含まれます。 (「使用」セクションの「[ネイティブ C++ パッケージ](../consume-packages/finding-and-choosing-packages.md#native-c-packages)」を参照してください。)

C++ プロジェクトで使用できるようにするには、パッケージが `native` フレームワークを対象にする必要があります。 現時点では、NuGet ですべての C++ プロジェクトが同様に処理されるように、このフレームワークに関連付けられているバージョン番号はありません。

> [!Note]
> 他の開発者がタグを検索して、お客様のパッケージを見つけられるように、必ず `.nuspec` の `<tags>` セクションに *native* を含めてください。

`native` を対象とするネイティブ NuGet パッケージでは、`\build`、`\content`、および `\tools` フォルダーにファイルが提供されます。`\lib` はこの場合、使用されません (NuGet では、直接 C++ プロジェクトに参照を追加することはできません)。 パッケージには、`\build` のターゲットとプロパティ ファイルも含まれる場合があります。このファイルは、NuGet によってパッケージを使用するプロジェクトに自動的にインポートされます。 これらのファイルは、`.targets` や `.props` の拡張子を含むパッケージ ID と同じ名前になります。 たとえば、[cpprestsdk](https://nuget.org/packages/cpprestsdk/) パッケージでは、`\build` フォルダーに `cpprestsdk.targets` ファイルが含まれます。

`\build` フォルダーは、ネイティブ パッケージだけでなく、すべての NuGet パッケージに使用できます。 `\build` フォルダーでは、`\content`、`\lib`、`\tools` フォルダーと同様に、ターゲット フレームワークが尊重されます。 つまり、`\build\net40` フォルダーと `\build\net45` フォルダーを作成でき、NuGet では適切なプロパティ ファイルとターゲット ファイルがプロジェクトにインポートされるということです。 (MSBuild ターゲットをインポートするために、PowerShell スクリプトを使用する必要はありません。)
