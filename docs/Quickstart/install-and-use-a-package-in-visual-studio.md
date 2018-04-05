---
title: Visual Studio 内から NuGet パッケージを使用するための入門ガイド | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: quickstart
ms.prod: nuget
ms.technology: ''
description: Visual Studio プロジェクトで NuGet パッケージをインストールし、使用するプロセスを説明したチュートリアル。
keywords: NuGet をインストールする, NuGet パッケージの使用, NuGet パッケージをインストールする, NuGet パッケージ参照, NuGet パッケージを使用する
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 4205893cc02cffff8926513a555393d10c046f43
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="install-and-use-a-package-in-visual-studio"></a>Visual Studio でパッケージをインストールして使用する

NuGet パッケージには、他の開発者がお客様のプロジェクトで使用できるようにした、再利用可能なコードが含まれます。 背景については、[NuGet の紹介](../What-is-NuGet.md)に関するページを参照してください。 Package Manager UI または Package Manager Console を使用して、パッケージが Visual Studio プロジェクトにインストールされます。 この記事では、よく使用されている [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) パッケージとユニバーサル Windows プラットフォーム (UWP) プロジェクトを使用したプロセスを示します。 同じプロセスは、他の任意の .NET または .NET Core プロジェクトにも適用されます。

インストール後、`using <namespace>` でコード内のパッケージを参照します。\<namespace\> は、使用しているパッケージに固有です。 参照が行われたら、その API からパッケージを呼び出すことができます。

> [!Tip]
> **nuget.org を開始する**: nuget.org を参照するのは、.NET 開発者が自身のアプリケーションで再利用可能なコンポーネントを検索するための一般的な方法です。 この記事で説明するように、nuget.org を直接検索することも、Visual Studio 内でパッケージを見つけてインストールすることもできます。

## <a name="prerequisites"></a>必須コンポーネント

- ユニバーサル Windows プラットフォーム開発ワークロードを含む Visual Studio 2017、または
- ユニバーサル Windows アプリ用ツールを含む Visual Studio 2015 Update 3。

[visualstudio.com](https://www.visualstudio.com/) から無料の 2017 Community Edition をインストールできます。Professional Edition または Enterprise Edition を使用することもできます。

## <a name="create-a-project"></a>プロジェクトを作成する

NuGet パッケージは任意の .NET プロジェクトにインストールできます。ただし、パッケージが同じターゲット フレームワークをプロジェクトとしてサポートしていることが条件です。

このチュートリアルでは、単純なユニバーサル Windows (UWP) アプリを使用します。 **[ファイル]、[新しいプロジェクト]** の順に使用し、**[Windows ユニバーサル]、[空白のアプリ (ユニバーサル Windows)]** の順に選択して、Visual Studio でプロジェクトを作成します。 プロンプトが表示されたら、ターゲット バージョンと最小バージョンの既定値を受け入れます。

## <a name="add-the-newtonsoftjson-nuget-package"></a>Newtonsoft.Json NuGet パッケージを追加する

パッケージをインストールするには、パッケージ マネージャー UI またはパッケージ マネージャー コンソールのいずれかを使用できます。 パッケージをインストールすると、NuGet で依存関係がプロジェクト ファイルまたは `packages.config` ファイルに記録されます。 詳細については、「[パッケージ利用のワークフロー](../consume-packages/Overview-and-Workflow.md)」を参照してください。

### <a name="package-manager-ui"></a>パッケージ マネージャー UI

1. ソリューション エクスプローラーで **[参照]** を右クリックし、**[NuGet パッケージの管理]** をクリックします。

    ![プロジェクト参照の NuGet パッケージ管理コマンド](media/QS_Use-02-ManageNuGetPackages.png)

1. **[パッケージ ソース]** として "nuget.org" を選択し、**[参照]** タブを選択し、「**Newtonsoft.Json**」を検索し、一覧からそのパッケージを選択し、**[インストール]** を選択します。

    ![Newtonsoft.Json パッケージを見つけます](media/QS_Use-03-NewtonsoftJson.png)

1. ラインセンス プロンプトに同意します。

1. (Visual Studio 2017) パッケージ管理形式を選択するように求められたら、**[プロジェクト ファイルの PackageReference]** を選択します。

    ![パッケージ管理形式の選択](media/QS_Use-03b-SelectFormat.png)

1. 変更の確認を求められた場合、**[OK]** を選択します。

### <a name="package-manager-console"></a>パッケージ マネージャー コンソール

1. **[ツール]、[NuGet パッケージ マネージャー]、[パッケージ マネージャー コンソール]** メニュー コマンドの順に選択します。

1. コンソールが開いたら、**[既定のプロジェクト]** ドロップダウン リストに、パッケージをインストールするプロジェクトが表示されていることを確認します。 ソリューション内に単一のプロジェクトがあれば、それは既に選択されています。

    ![Newtonsoft.Json パッケージを見つけます](media/QS_Use-08-Console1.png)

1. コマンド `Install-Package Newtonsoft.json` を入力します (「[Install-Package](../tools/ps-ref-install-package.md)」を参照してください)。 コンソール ウィンドウに、このコマンドの出力が表示されます。 通常、エラーは、パッケージがプロジェクトのターゲット フレームワークと互換性がないことを示します。

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>アプリで Newtonsoft.Json API を使用する

プロジェクトに Newtonsoft.Json パッケージがある場合、その `JsonConvert.SerializeObject` メソッドを呼び出し、オブジェクトを人間が読める文字列に変換できます。

1. `MainPage.xaml`を開いて、既存の `Grid` 要素を次の XAML に置き換えます。

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. `MainPage.xaml.cs` ファイル (ソリューション エクスプローラーの `MainPage.xaml`ノードの下にあります) を開いて、`MainPage`コンストラクター内に次のコードを挿入します。

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
    using Newtonsoft.json;
    ```

1. アプリをビルドして実行します。F5 キーを押すか、**[デバッグ]、[デバッグの開始]** を選択してください。

    ![UWP アプリの最初の出力](media/QS_Use-06-AppStart.png)

1. ボタンを選択し、TextBlock の内容が JSON テキストに置換されたことを確認します。

    ![ボタンを選択した後の UWP アプリの出力](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a>関連記事

- [パッケージ使用の概要とワークフロー](../consume-packages/overview-and-workflow.md)
- [パッケージの検索と選択](../consume-packages/finding-and-choosing-packages.md)
- [パッケージをインストールする方法](../consume-packages/ways-to-install-a-package.md)
- [NuGet の動作を構成する](../consume-packages/configuring-nuget-behavior.md)
