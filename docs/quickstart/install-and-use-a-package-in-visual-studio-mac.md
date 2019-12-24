---
title: Visual Studio for Mac に NuGet パッケージをインストールして使用する
description: Visual Studio for Mac プロジェクトに NuGet パッケージをインストールして使用するプロセスを説明したチュートリアル。
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2019
ms.locfileid: "70238478"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a>クイック スタート: Visual Studio for Mac にパッケージをインストールして使用する

NuGet パッケージには、他の開発者がお客様のプロジェクトで使用できるようにした、再利用可能なコードが含まれます。 背景については、[NuGet の紹介](../What-is-NuGet.md)に関するページを参照してください。 パッケージは、NuGet パッケージ マネージャーを使って Visual Studio for Mac プロジェクトにインストールします。 この記事では、人気のある [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) パッケージと .NET Core コンソール プロジェクトを使ってそのプロセスを説明します。 他の任意の Xamarin または .NET Core プロジェクトにも同じプロセスを適用できます。

インストール後、`using <namespace>` でコード内のパッケージを参照します。\<namespace\> は、使用しているパッケージに固有です。 参照が行われたら、その API からパッケージを呼び出すことができます。

> [!Tip]
> **nuget.org を開始する**:*nuget.org* を参照するのは、.NET 開発者が自身のアプリケーションで再利用可能なコンポーネントを検索するための一般的な方法です。 *nuget.org* を直接検索するか、この記事に示すように、パッケージを検索して Visual Studio 内にインストールすることができます。 一般的な情報については、[NuGet パッケージの検索と評価](../consume-packages/finding-and-choosing-packages.md)に関するページをご覧ください。

## <a name="prerequisites"></a>必須コンポーネント

- Visual Studio 2019 for Mac。

[visualstudio.com](https://www.visualstudio.com/) から無料の 2019 Community Edition をインストールするか、Professional または Enterprise Edition を使用できます。

Windows 上の Visual Studio を使用している場合は、[Visual Studio でのパッケージのインストールと使用 (Windows のみ)](install-and-use-a-package-in-visual-studio.md) に関するページをご覧ください。

## <a name="create-a-project"></a>プロジェクトを作成する

NuGet パッケージは任意の .NET プロジェクトにインストールできます。ただし、パッケージが同じターゲット フレームワークをプロジェクトとしてサポートしていることが条件です。

このチュートリアルでは、シンプルな .NET Core コンソール アプリを使用します。 Visual Studio for Mac で、 **[ファイル] > [新しいソリューション...]** を使用し、 **[.NET Core] > [アプリ] > [コンソールアプリケーション]** テンプレートを選択して、プロジェクトを作成します。 **[次へ]** をクリックします。 プロンプトが表示されたら、 **[ターゲット フレームワーク]** の既定値をそのまま受け入れます。

Visual Studio によってプロジェクトが作成され、ソリューション エクスプローラーに開かれます。

## <a name="add-the-newtonsoftjson-nuget-package"></a>Newtonsoft.Json NuGet パッケージを追加する

パッケージをインストールするには、NuGet パッケージ マネージャーを使用します。 パッケージをインストールすると、NuGet によって、プロジェクト ファイルまたは `packages.config` ファイルのどちらか (プロジェクトの形式によって異なります) に依存関係が記録されます。 詳細については、「[パッケージ利用のワークフロー](../consume-packages/Overview-and-Workflow.md)」を参照してください。

### <a name="nuget-package-manager"></a>NuGet パッケージ マネージャー

1. ソリューション エクスプローラーで、 **[依存関係]** を右クリックして、 **[パッケージの追加...]** を選択します。

    ![プロジェクト参照の NuGet パッケージ管理コマンド](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. ダイアログの左上隅で **[パッケージ ソース]** として "nuget.org" を選択し、「**Newtonsoft.Json**」を検索します。一覧からそのパッケージを選択して **[パッケージの追加...]** を選択します。

    ![Newtonsoft.Json パッケージを見つけます](media/QS_Use_Mac-03-NewtonsoftJson.png)

    NuGet パッケージ マネージャーに関する詳細が必要な場合は、[Visual Studio for Mac を使用したパッケージのインストールおよび管理](../consume-packages/install-use-packages-visual-studio.md)に関するページをご覧ください。

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>アプリで Newtonsoft.Json API を使用する

プロジェクトに Newtonsoft.Json パッケージがある場合、その `JsonConvert.SerializeObject` メソッドを呼び出し、オブジェクトを人間が読める文字列に変換できます。

1. `Program.cs` ファイルを開き (Solution Pad にあります)、ファイルの内容を次のコードに置き換えます。

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. **[実行] > [デバッグの開始]** を選択して、アプリをビルドして実行します。

1. アプリを実行すると、コンソールにシリアル化された JSON 出力が表示されます。

  ![コンソール アプリの出力](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a>次の手順
無事に、最初の NuGet パッケージをインストールして使用できるようになりました。

> [!div class="nextstepaction"]
> [Visual Studio for Mac を使用してパッケージをインストールして管理する](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

NuGet による提供についてさらに詳しく調べるには、下のリンクを選択してください。

- [パッケージ使用の概要とワークフロー](../consume-packages/overview-and-workflow.md)
- [プロジェクト ファイルのパッケージ参照](../consume-packages/package-references-in-project-files.md)
