---
title: dotnet CLI を使用して NuGet パッケージをインストールし、使用する
description: .NET Core プロジェクトで NuGet パッケージをインストールし、使用するプロセスを説明したチュートリアル。
author: JonDouglas
ms.author: jodou
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: adbf8f457d8520e3087e539b91ef932877aec3a0
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775451"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>クイック スタート: dotnet CLI を使用してパッケージをインストールし使用する

NuGet パッケージには、他の開発者がお客様のプロジェクトで使用できるようにした、再利用可能なコードが含まれます。 背景については、[NuGet の紹介](../What-is-NuGet.md)に関するページを参照してください。 一般的な [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) パッケージに関するこの記事で説明するとおり、パッケージを .NET Core プロジェクトにインストールするには、`dotnet add package` コマンドを使用します。

インストール後、`using <namespace>` でコード内のパッケージを参照します。\<namespace\> は、使用しているパッケージに固有です。 その後、パッケージの API を使用できます。

> [!Tip]
> **nuget.org を開始する**: nuget.org を参照するのは、.NET 開発者が自身のアプリケーションで再利用可能なコンポーネントを検索するための一般的な方法です。 この記事で説明するように、nuget.org を直接検索することも、Visual Studio 内でパッケージを見つけてインストールすることもできます。

## <a name="prerequisites"></a>前提条件

- [.NET Core SDK](https://www.microsoft.com/net/download/)。これは、`dotnet`コマンド ライン ツールを提供します。 Visual Studio 2017 以降、dotnet CLI は .NET Core 関連のワークロードで自動的にインストールされます。

## <a name="create-a-project"></a>プロジェクトの作成

NuGet パッケージは、ある種類の .NET プロジェクトにインストールできます。 このチュートリアルでは、次の手順に従って、単純な .NET Core コンソール プロジェクトを作成します。

1. プロジェクトのフォルダーを作成します。

1. コマンド プロンプトを開いて、新しいフォルダーに切り替えます。

1. 次のコマンドを使用して、プロジェクトを作成します。

    ```dotnetcli
    dotnet new console
    ```

1. `dotnet run` を使用して、アプリが正しく作成されたことをテストします。

## <a name="add-the-newtonsoftjson-nuget-package"></a>Newtonsoft.Json NuGet パッケージを追加する

1. 次のコマンドを使用して、`Newtonsoft.json` パッケージをインストールします。

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. コマンドが完了したら、`.csproj` ファイルを開いて、追加された参照を確認します。

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>アプリで Newtonsoft.Json API を使用する

1. `Program.cs`ファイルを開いて、ファイルの上部に次の行を追加します。

    ```cs
    using Newtonsoft.Json;
    ```

1. `class Program` 行の前に次のコードを追加します。

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. `Main` 関数を次のコードに置き換えます。

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. `dotnet run` コマンドを使用して、アプリをビルドして実行します。 出力は、コード内の `Account` オブジェクトの JSON 表現になります。

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a>関連ビデオ

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

他の NuGet ビデオは、[Channel 9](https://channel9.msdn.com/Series/NuGet-101) および [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_) でご覧いただけます。

## <a name="next-steps"></a>次のステップ

無事に、最初の NuGet パッケージをインストールして使用できるようになりました。

> [!div class="nextstepaction"]
> [dotnet CLI を使用してパッケージをインストールし使用する](../consume-packages/install-use-packages-dotnet-cli.md)

NuGet による提供についてさらに詳しく調べるには、下のリンクを選択してください。

- [パッケージ使用の概要とワークフロー](../consume-packages/overview-and-workflow.md)
- [パッケージの検索と選択](../consume-packages/finding-and-choosing-packages.md)
- [プロジェクト ファイルのパッケージ参照](../consume-packages/package-references-in-project-files.md)
