---
ms.openlocfilehash: 9764479d88cc8d87a9f455e64bd46ae8de15055d
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860600"
---
[dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) コマンドを使用すると、プロジェクト ファイルに一覧表示されているパッケージが復元されます ([PackageReference](../../consume-packages/package-references-in-project-files.md) 参照)。 .NET Core 2.0 以降では、復元は、`dotnet build` と `dotnet run` で自動的に実行されます。 NuGet 4.0 以降、`nuget restore` と同じコードが実行されます。

他の `dotnet` CLI コマンドと同様に、最初にコマンド ラインが開かれ、使用するプロジェクト ファイルが含まれているディレクトリに切り替えられます。

`dotnet restore` を使用してパッケージを復元するには:

```cli
dotnet restore 
```