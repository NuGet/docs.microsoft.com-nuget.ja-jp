---
title: dotnet CLI を使用して NuGet パッケージをインストールし、管理する
description: dotnet CLI を使用して NuGet パッケージを操作する方法。
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: a796c7a7537c3052259c7cf3f17d60981a495442
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317717"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>dotnet CLI を使用してパッケージをインストールして管理する

CLI ツールを使用すると、プロジェクトやソリューションで NuGet パッケージを簡単にインストール、アンインストール、更新できます。 Windows、Mac OS X、Linux で実行されます。

dotnet CLI は .NET Core や .NET Standard のプロジェクト (SDK スタイルのプロジェクト タイプ) で使用され、また、その他の SDK スタイル プロジェクト (.NET Framework を対象とする SDK スタイルのプロジェクト) で使用されます。 詳細については、「[SDK 属性](/dotnet/core/tools/csproj#additions)」を参照してください。

この記事では、最も一般的ないくつかの dotnet CLI コマンドの基本的な使用方法を説明します。 これらのコマンドの多くでは、コマンドにプロジェクト ファイルが指定されていない限り、CLI ツールは現在のディレクトリでプロジェクト ファイルを探します (プロジェクト ファイルはオプションのスイッチです)。 コマンドと使用できる引数の完全一覧については、[.NET Core コマンドライン インターフェイス (CLI) ツール](../reference/dotnet-commands.md)に関するページを参照してください。

## <a name="prerequisites"></a>必須コンポーネント

- [.NET Core SDK](https://www.microsoft.com/net/download/)。これは、`dotnet`コマンド ライン ツールを提供します。 Visual Studio 2017 以降、dotnet CLI は .NET Core 関連のワークロードで自動的にインストールされます。

## <a name="install-a-package"></a>パッケージをインストールします

[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) では、パッケージ参照がプロジェクト ファイルに追加され、`dotnet restore` が実行されてパッケージがインストールされます。

1. コマンド ラインを開き、プロジェクト ファイルが含まれるディレクトリに切り替えます。

2. 次のコマンドを使用して、NuGet パッケージをインストールします。

    ```cli
    dotnet add package <PACKAGE_NAME>
    ```

    たとえば、`Newtonsoft.Json` パッケージをインストールするには、次のコマンドを使用します。

    ```cli
    dotnet add package Newtonsoft.Json
    ```

3. コマンドが完了したら、プロジェクト ファイルを見て、パッケージがインストールされたことを確認します。

   `.csproj` ファイルを開くと、追加された参照を確認できます。

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>パッケージの特定のバージョンをインストールする

バージョンが指定されていない場合、NuGet では最新版のパッケージがインストールされまする [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) コマンドを使用し、特定のバージョンの NuGet パッケージをインストールすることもできます。

```cli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

たとえば、`Newtonsoft.Json` パッケージのバージョン 12.0.1 を追加するには、このコマンドを使用します。

```cli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a>パッケージ参照の一覧表示

[dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) コマンドを使用し、プロジェクトのパッケージ参照を一覧表示できます。

```cli
dotnet list package
```

## <a name="remove-a-package"></a>パッケージを削除する

プロジェクト ファイルからパッケージ参照を削除するには、[dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) コマンドを使用します。

```cli
dotnet remove package <PACKAGE_NAME>
```

たとえば、`Newtonsoft.Json` パッケージを削除するには、次のコマンドを使用します。

```cli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>パッケージを更新する

NuGet では、パッケージ バージョンを指定しない限り (`-v` スイッチ)、`dotnet add package` コマンドの使用時、最新版のパッケージがインストールされます。

## <a name="restore-packages"></a>パッケージの復元

[dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) コマンドを使用すると、プロジェクト ファイルに一覧表示されているパッケージが復元されます ([PackageReference](../consume-packages/package-references-in-project-files.md) 参照)。 .NET Core 2.0 以降では、復元は、`dotnet build` と `dotnet run` で自動的に実行されます。 NuGet 4.0 以降、`nuget restore` と同じコードが実行されます。

他の `dotnet` CLI コマンドと同様に、最初にコマンド ラインが開かれ、使用するプロジェクト ファイルが含まれているディレクトリに切り替えられます。

`dotnet restore` を使用してパッケージを復元するには:

```cli
dotnet restore 
```
