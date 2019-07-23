---
title: NuGet パッケージの種類を設定する
description: パッケージの使用目的を示すパッケージの種類について説明します。
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 8a3ba6af19125b75af17cab8c093e89485e20324
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843494"
---
# <a name="set-a-nuget-package-type"></a>NuGet パッケージの種類を設定する

NuGet 3.5+ では、パッケージに特定の*パッケージの種類*の印を付け、その用途を示すことができます。 種類の印が付いていないパッケージ (初期のバージョンの NuGet で作成されたすべてのパッケージが相当) は種類が `Dependency` に初期設定されます。

- 種類が `Dependency` のパッケージでは、ビルド時または実行時アセットがライブラリとアプリケーションに追加されます。(互換性があれば) あらゆる種類のプロジェクトにインストールできます。

- 種類が `DotnetCliTool` であるパッケージは [dotnet CLI](/dotnet/articles/core/tools/index) の拡張であり、コマンド ラインから呼び出されます。 このようなパッケージは .NET Core プロジェクトにのみインストールできます。復元操作には影響を与えません。 このようなプロジェクト別の拡張機能に関する詳細は、[.NET Core 拡張性](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility)ドキュメントにあります。

- カスタム タイプのパッケージでは、パッケージ ID と同じ形式ルールに準拠する任意の種類識別子が使用されます。 ただし、`Dependency` と `DotnetCliTool` 以外の種類は、Visual Studio の NuGet パッケージ マネージャーには認識されません。

パッケージの種類は `.nuspec` ファイルで設定されます。 下位互換性を維持するには、種類 `Dependency` を明示的に設定*しない*で、NuGet に依存するのが最適な方法です。NuGet は、種類が指定されない場合、この種類を想定します。

- `.nuspec`:`<metadata>` 要素の下の `packageTypes\packageType` ノード内のパッケージの種類を示します。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
