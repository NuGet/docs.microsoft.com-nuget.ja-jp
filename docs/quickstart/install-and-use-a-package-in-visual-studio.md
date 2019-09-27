---
title: Visual Studio に NuGet パッケージをインストールして使用する
description: Visual Studio プロジェクトで NuGet パッケージをインストールし、使用するプロセスを説明したチュートリアル。
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 92fc78a88733d0308dc26e10c5b0bafb86b78045
ms.sourcegitcommit: e4b0ff4460865db6dc7bc9f20e9f644d98493011
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71307229"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a>クイック スタート: Visual Studio にパッケージをインストールして使用する (Windows のみ)

NuGet パッケージには、他の開発者がお客様のプロジェクトで使用できるようにした、再利用可能なコードが含まれます。 背景については、[NuGet の紹介](../What-is-NuGet.md)に関するページを参照してください。 NuGet パッケージ マネージャーまたはパッケージ マネージャー コンソールを使用して、パッケージが Visual Studio プロジェクトにインストールされます。 この記事では、よく使用されている [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) パッケージと Windows Presentation Foundation (WPF) プロジェクトを使用したプロセスを示します。 同じプロセスは、他の任意の .NET または .NET Core プロジェクトにも適用されます。

インストール後、`using <namespace>` でコード内のパッケージを参照します。\<namespace\> は、使用しているパッケージに固有です。 参照が行われたら、その API からパッケージを呼び出すことができます。

> [!Tip]
> **nuget.org を開始する**:*nuget.org* を参照するのは、.NET 開発者が自身のアプリケーションで再利用可能なコンポーネントを検索するための一般的な方法です。 *nuget.org* を直接検索するか、この記事に示すように、パッケージを検索して Visual Studio 内にインストールすることができます。 一般的な情報については、[NuGet パッケージの検索と評価](../consume-packages/finding-and-choosing-packages.md)に関するページをご覧ください。

## <a name="prerequisites"></a>必須コンポーネント

- .NET デスクトップ開発ワークロードを利用する Visual Studio 2019。

[visualstudio.com](https://www.visualstudio.com/) から無料の 2019 Community Edition をインストールするか、Professional または Enterprise Edition を使用できます。

Visual Studio for Mac を使用している場合は、[Visual Studio for Mac でのパッケージのインストールと使用](install-and-use-a-package-in-visual-studio-mac.md)に関するページをご覧ください。

## <a name="create-a-project"></a>プロジェクトを作成する

NuGet パッケージは任意の .NET プロジェクトにインストールできます。ただし、パッケージが同じターゲット フレームワークをプロジェクトとしてサポートしていることが条件です。

このチュートリアルでは、単純な WPF アプリを使用します。 **[ファイル]**  >  **[新しいプロジェクト]** を使用し、検索ボックスに「 **.NET**」と入力して、 **[WPF アプリ (.NET Framework)]** を選択し、Visual Studio にプロジェクトを作成します。 **[次へ]** をクリックします。 プロンプトが表示されたら、 **[フレームワーク]** の既定値をそのまま受け入れます。

Visual Studio によってプロジェクトが作成され、ソリューション エクスプローラーに開かれます。

## <a name="add-the-newtonsoftjson-nuget-package"></a>Newtonsoft.Json NuGet パッケージを追加する

パッケージをインストールするには、NuGet パッケージ マネージャーまたはパッケージ マネージャー コンソールのいずれかを使用できます。 パッケージをインストールすると、NuGet では、プロジェクト ファイルまたは `packages.config` ファイルのどちらかに依存関係が記録されます (プロジェクトの形式に依存します)。 詳細については、「[パッケージ利用のワークフロー](../consume-packages/Overview-and-Workflow.md)」を参照してください。

### <a name="nuget-package-manager"></a>NuGet パッケージ マネージャー

1. ソリューション エクスプローラーで **[参照]** を右クリックし、 **[NuGet パッケージの管理]** をクリックします。

    ![プロジェクト参照の NuGet パッケージ管理コマンド](media/QS_Use-02-ManageNuGetPackages.png)

1. **[パッケージ ソース]** として "nuget.org" を選択し、 **[参照]** タブを選択し、「**Newtonsoft.Json**」を検索し、一覧からそのパッケージを選択し、 **[インストール]** を選択します。

    ![Newtonsoft.Json パッケージを見つけます](media/QS_Use-03-NewtonsoftJson.png)

    NuGet パッケージ マネージャーについて詳しくは、[Visual Studio を使用したパッケージのインストールおよび管理](../consume-packages/install-use-packages-visual-studio.md)に関するページをご覧ください。

1. ラインセンス プロンプトに同意します。

1. (Visual Studio 2017 のみ) パッケージ管理の形式を選択するように求められたら、 **[プロジェクト ファイルの PackageReference]** を選択します。

    ![パッケージ管理形式の選択](media/QS_Use-03b-SelectFormat.png)

1. 変更の確認を求められた場合、 **[OK]** を選択します。

### <a name="package-manager-console"></a>パッケージ マネージャー コンソール

1. **[ツール]**  >  **[NuGet パッケージ マネージャー]**  >  **[パッケージ マネージャー コンソール]** メニュー コマンドの順に選択します。

1. コンソールが開いたら、 **[既定のプロジェクト]** ドロップダウン リストに、パッケージをインストールするプロジェクトが表示されていることを確認します。 ソリューション内に単一のプロジェクトがあれば、それは既に選択されています。

    ![Newtonsoft.Json パッケージを見つけます](media/QS_Use-08-Console1.png)

1. コマンド `Install-Package Newtonsoft.Json` を入力します (「[Install-Package](../reference/ps-reference/ps-ref-install-package.md)」を参照してください)。 コンソール ウィンドウに、このコマンドの出力が表示されます。 通常、エラーは、パッケージがプロジェクトのターゲット フレームワークと互換性がないことを示します。

   パッケージ マネージャー コンソールについて詳しくは、[パッケージ マネージャー コンソールを使用したパッケージのインストールおよび管理](../consume-packages/install-use-packages-powershell.md)に関するページをご覧ください。

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>アプリで Newtonsoft.Json API を使用する

プロジェクトに Newtonsoft.Json パッケージがある場合、その `JsonConvert.SerializeObject` メソッドを呼び出し、オブジェクトを人間が読める文字列に変換できます。

1. `MainWindow.xaml`を開いて、既存の `Grid` 要素を次の XAML に置き換えます。

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. `MainWindow.xaml.cs` ファイル (ソリューション エクスプローラーの `MainWindow.xaml` ノード下にあります) を開いて、`MainWindow` クラス内に次のコードを挿入します。

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. プロジェクトに Newtonsoft.Json パッケージを追加した後でも、`JsonConvert` の下に赤い波線が表示されます。これは、コード ファイルの上部に `using` ステートメントが必要であるためです。

    ```cs
    using Newtonsoft.Json;
    ```

1. アプリをビルドして実行します。F5 キーを押すか、 **[デバッグ]**  >  **[デバッグの開始]** を選択してください。

    ![WPF アプリの最初の出力](media/QS_Use-06-AppStart.png)

1. ボタンを選択し、TextBlock の内容が JSON テキストに置換されたことを確認します。

    ![ボタンを選択した後の WPF アプリの出力](media/QS_Use-07-AppEnd.png)

## <a name="next-steps"></a>次の手順

無事に、最初の NuGet パッケージをインストールして使用できるようになりました。

> [!div class="nextstepaction"]
> [Visual Studio を使用してパッケージをインストールして管理する](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [パッケージ マネージャー コンソールを使用してパッケージをインストールして管理する](../consume-packages/install-use-packages-powershell.md)

NuGet による提供についてさらに詳しく調べるには、下のリンクを選択してください。

- [パッケージ使用の概要とワークフロー](../consume-packages/overview-and-workflow.md)
- [パッケージの検索と選択](../consume-packages/finding-and-choosing-packages.md)
- [プロジェクト ファイルのパッケージ参照](../consume-packages/package-references-in-project-files.md)
