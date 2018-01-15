---
title: "NuGet パッケージ使用の入門ガイド | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: f31f8259-20a8-4617-880e-5819299372d2
description: "プロジェクトで NuGet パッケージをインストールし、使用するプロセスを説明するチュートリアル。"
keywords: "NuGet をインストールする, NuGet パッケージの使用, NuGet パッケージをインストールする, NuGet パッケージ参照, NuGet パッケージを使用する"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 639f4883f5ce904a44d8aa23d76c93ed79ea4b9d
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2018
---
# <a name="install-and-use-a-package"></a>パッケージをインストールして使用する

NuGet パッケージとは、自分のプロジェクトでの使用が他の開発者によって許可されている再利用可能なコードの単位です。 背景については、[NuGet の紹介](../What-is-NuGet.md)に関するページを参照してください。

[!INCLUDE [install-methods](../includes/install-methods.md)]

インストール後、`using <namespace>` でコード内のパッケージを参照します。\<namespace\> は、使用しているパッケージに固有です。 参照が行われたら、その API からパッケージを呼び出すことができます。

このトピックの残りでは、Package Manager UI を使用し、ユニバーサル Windows プラットフォーム (UWP) プロジェクトで人気の [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) パッケージをインストールする方法を段階的に説明します。 その後、パッケージの使用例を紹介します。 プロジェクトで使用するほとんどすべての NuGet パッケージで同様のワークフローを使用します。

- [前提条件をインストールする](#install-pre-requisites)
- [プロジェクトを作成する](#create-a-project)
- [Newtonsoft.Json NuGet パッケージを追加する](#add-the-newtonsoftjson-nuget-package)
- [アプリで Newtonsoft.Json API を使用する](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> **nuget.org を始める**: nuget.org からのパッケージのインストールは、自分のアプリケーションで再利用できるコンポーネントを .NET 開発者が見つけるための一般的ワークフローです。 このトピックで紹介するように、いつでも nuget.org を直接、検索したり、Visual Studio 内でパッケージを見つけ、インストールしたりできます。

## <a name="install-pre-requisites"></a>前提条件をインストールする

このチュートリアルには、Visual Studio 2015 Update 3 とユニバーサル Windows アプリ用ツール、または Visual Studio 2017 とユニバーサル Windows プラットフォーム開発ワークロードが必要です。 Visual Studio を既にインストールしている場合、インストーラーをもう一度実行し、UWP ツールを追加できます。

[visualstudio.com](https://www.visualstudio.com/) から無料の Community Edition をインストールします。Professional Edition と Enterprise Edition も使用できます。 

## <a name="create-a-project"></a>プロジェクトを作成する

NuGet パッケージをインストールするには、Visual Studio で何らかの .NET ベースのプロジェクトが必要です。 このチュートリアルでは、単純な Windows Presentation Foundation (WPF) またはユニバーサル Windows (UWP) アプリを使用できます。

- WPF (Windows 7+) の場合、**[ファイル]、[新規]、[プロジェクト]** の順に選択し、**[Visual C#]** を展開し、**[Windows クラシック デスクトップ]、[WPF アプリ (.NET フレームワーク)]**、**[OK]** の順に選択します。
- UWP (Windows 10) の場合、**[Windows ユニバーサル]、[空のアプリ (ユニバーサル Windows)]** を代わりに使用します。 プロンプトが表示されたら、ターゲット バージョンと最小バージョンの既定値を受け入れます。

## <a name="add-the-newtonsoftjson-nuget-package"></a>Newtonsoft.Json NuGet パッケージを追加する

1. ソリューション エクスプローラーで **[参照]** を右クリックし、**[NuGet パッケージの管理]** をクリックします。

    ![プロジェクト参照の NuGet パッケージ管理コマンド](media/QS_Use-02-ManageNuGetPackages.png)

1. **[パッケージ ソース]** として "nuget.org" を選択し、**[参照]** タブを選択し、「**Newtonsoft.Json**」を検索し、一覧からそのパッケージを選択し、**[インストール]** を選択します。

    ![Newtonsoft.Json パッケージを見つけます](media/QS_Use-03-NewtonsoftJson.png)

1. パッケージ管理形式を選択するように求められた場合、PackageReference (推奨) または `packages.config` を選択します。

    ![パッケージ参照形式を選択する](media/QS_Use-03b-SelectFormat.png)

1. 変更の確認を求められた場合、**[OK]** を選択します。

1. ソリューション エクスプローラーを右クリックし、**[ソリューションのビルド]** を選択します。 これで NuGet パッケージが復元され、**[参照]** の下の一覧に表示されます。 詳細については、「[パッケージの復元](../consume-packages/package-restore.md)」を参照してください。

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>アプリで Newtonsoft.Json API を使用する

プロジェクトに Newtonsoft.Json パッケージがある場合、その `JsonConvert.SerializeObject` メソッドを呼び出し、オブジェクトを人間が読める文字列に変換できます。

1. `MainWindow.xaml` (WPF) または `MainPage.xaml` (UWP) を開き、既存の `Grid` 要素を次のもので置換します。

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. ソリューション エクスプローラーで `MainWindow.xaml` (WPF) または `MainPage.xaml` (UWP) ノードを展開し、`.cs` ファイルを開き、`MainWindow` または `MainPage` クラス内でコンストラクターの後に次のコードを挿入します。

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

1. プロジェクトに Newtonsoft.Json パッケージを追加した後でも、`JsonConvert` の下に赤い波線が表示されます。これは `using` ステートメントが必要であるためです。 下線の付いた `JsonConvert` にカーソルを合わせると電球と**考えられる修正内容を表示する**オプションが表示されます。

    ![電球と考えられる修正内容を表示するコマンド](media/QS_Use-04-ShowPotentialFixes.png)


1. **[考えられる修正内容を表示する]** (電球) をクリックし、最初の修正案である `using Newtonsoft.Json;` を選択します。 これでファイルの一番上に必要な行が追加されます。

    ![using ステートメントを追加するオプションを表示する電球](media/QS_Use-05-AddUsing.png)

1. アプリをビルドして実行します。F5 を押すか、**[デバッグ]、[デバッグの開始]** を選択してください。ここの例では UWP ですが、WPF の場合も同様です。

    ![UWP アプリの最初の出力](media/QS_Use-06-AppStart.png)

1. ボタンを選択し、TextBlock の内容が JSON テキストに置換されたことを確認します。

    ![ボタンを選択した後の UWP アプリの出力](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a>関連トピック

- [パッケージ使用の概要とワークフロー](../consume-packages/overview-and-workflow.md)
- [パッケージの検索と選択](../consume-packages/finding-and-choosing-packages.md)
- [NuGet の動作を構成する](../consume-packages/configuring-nuget-behavior.md)
