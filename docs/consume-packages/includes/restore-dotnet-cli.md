---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825170"
---
[dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) コマンドを使用すると、プロジェクト ファイルに一覧表示されているパッケージが復元されます ([PackageReference](../../consume-packages/package-references-in-project-files.md) 参照)。 .NET Core 2.0 以降では、復元は、`dotnet build` と `dotnet run` で自動的に実行されます。 NuGet 4.0 以降、`nuget restore` と同じコードが実行されます。

他の `dotnet` CLI コマンドと同様に、最初にコマンド ラインが開かれ、使用するプロジェクト ファイルが含まれているディレクトリに切り替えられます。

`dotnet restore` を使用してパッケージを復元するには:

```dotnetcli
dotnet restore 
```