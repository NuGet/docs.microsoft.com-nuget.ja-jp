---
title: "NuGet パッケージを作成して公開するための入門ガイド | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/3/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 91781ed6-da5c-49f0-b973-16dd8ad84229
description: "nuget.exe コマンドライン インターフェイスと Visual Studio の両方を使用して、NuGet パッケージを作成して公開するチュートリアル。"
keywords: "NuGet パッケージの作成、NuGet パッケージの公開、NuGet チュートリアル"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 36a7c2b1d056dddf07a59737de1c3e94294689ac
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="create-and-publish-a-package"></a>パッケージの作成と公開

.NET クラス ライブラリから NuGet パッケージを作成して、nuget.org に公開する簡単なプロセスです。次の手順では、NuGet コマンド ライン インターフェイス (CLI) と Visual Studio を使用して、このプロセスについて説明します。

- [前提条件](#install-pre-requisites)
- [.nuspec パッケージ マニフェスト ファイルを作成する](#create-the-nuspec-package-manifest-file)
- [pack コマンドを実行する](#run-the-pack-command)
- [パッケージを公開する](#publish-the-package)

## <a name="pre-requisites"></a>前提条件

1. [visualstudio.com](https://www.visualstudio.com/) から Visual Studio 2017 の任意のエディションをインストールします。

1. [nuget.org/downloads](https://nuget.org/downloads) から `nuget.exe` の最新バージョンをダウンロードし、`.exe` を自分の PATH 内の場所に保存することで、NuGet CLI ツール `nuget.exe` をインストールします。 ダウンロードされるのは、インストーラーではなく、ツール*そのもの*であることに注意してください。

1. パッケージ化するコードに適した .NET クラス ライブラリ プロジェクトを作成します。 プロジェクトがまだない場合は、次の手順で単純なものを作成できます。
    1. Visual Studio で、**[ファイル]、[新規]、[プロジェクト]** の順に選択し、**[Visual C#]、[Windows]** ノードの順に展開して "クラス ライブラリ" テンプレートを選択し、プロジェクトに AppLogger という名前を付け、**[OK]** をクリックします。
    1. 作成されたプロジェクト ファイルを右クリックし、**[ビルド]** を選択して、プロジェクトが正しく作成されたことを確認します。 DLL は、デバッグ フォルダー (または代わりにその構成をビルドした場合はリリース フォルダー) 内にあります。

    実際の NuGet パッケージ内ではもちろん、多くの便利な機能を実装して、他の人がその上にアプリケーションをビルドできます。 しかし、このチュートリアルでは、パッケージを作成するには、テンプレートのクラス ライブラリで十分なため、追加のコードを記述することはありません。

## <a name="create-the-nuspec-package-manifest-file"></a>.nuspec パッケージ マニフェスト ファイルを作成する

すべての NuGet パッケージには、その内容と依存関係を説明するマニフェスト &mdash;`.nuspec` ファイル&mdash; が必要です。 `nuget spec` コマンドを使用してこのファイルを作成し、カスタマイズすることができます。 この例では、プロジェクト ファイルから `.nuspec` を作成します。マニフェストは、[パッケージの作成](../create-packages/creating-a-package.md)ページで説明されているような他の方法でも作成できます。

1. コマンド プロンプトを開き、プロジェクト ファイル (`.csproj`) が格納されているフォルダーに移動します。

1. NuGet CLI `spec` コマンドを実行してマニフェストを生成すると、プロジェクトにちなんだ名前 (`AppLogger.nuspec` など) が付けられます。

    ```
    nuget spec
    ```

1. テキスト エディターでファイルを開きます。 マニフェストは次のコードのようになります。*$`<token>`$* の形式のトークンは、パッケージ化プロセス中にプロジェクトの Properties/AssemblyInfo.cs ファイルからの値に置き換えられます。 トークンの詳細については、「[Creating the .nuspec file](../create-packages/creating-a-package.md#creating-the-nuspec-file)」 (.nuspec ファイルの作成) を参照してください。

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. nuget.org 全体で一意のパッケージ ID を選択します。[パッケージの作成](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)ページに記載されている名前付け規則を使用することをお勧めします。 必ず作成者と説明のタグを更新してください。そうしないと、次の手順でエラーが発生します。 例として更新された `.nuspec` ファイルを以下に示します。

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> 公開用にビルドされたパッケージの場合は、`<tags>` 要素に特に注意してください。これらのタグは他のユーザーがパッケージを検索して、パッケージの動作を理解するのに役立ちます。

## <a name="run-the-pack-command"></a>pack コマンドを実行する

プロジェクトから NuGet パッケージ (`.nupkg` ファイル) を作成するには、`pack` コマンドを実行します。

```
nuget pack AppLogger.csproj
```

このコマンドは、`.nuspec` ファイルからパッケージの名前とバージョン番号を使用して、`AppLogger.1.0.0.0.nupkg` を作成します。 `.nuspec` ファイルのさまざまなフィールドを既定値から変更していない場合は、コマンドにより警告が発行されます。

## <a name="publish-the-package"></a>パッケージを公開する

`.nupkg` ファイルを作成したら、`push` コマンドを使用してそれを nuget.org に公開します。 または、[nuget.org の公開ワークフロー](../create-packages/publish-a-package.md#publish-to-nugetorg)を使用できます。

> [!Warning]
> nuget.org に公開するパッケージは、他の開発者に公開されます。 パッケージを非公開でホストするには、[パッケージのホスティング](../hosting-packages/overview.md)に関するページを参照してください。


1. [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) に無料のアカウントを作成するか、既にある場合はログインします。 新しいアカウントを作成すると、確認メールが送信されます。 パッケージをアップロードするには、その前にアカウントを確認する必要があります。

1. ログイン後、(右上で) ユーザー名を選択し、**[API キー]** を選択します。

1. **[作成]** を選択し、キーの名前を入力し、**[API キー]** の下で **[スコープの選択]、[プッシュ]** の順に選択し、**[Glob pattern]\(glob パターン\)** に「*」を入力し、**[作成]** を選択します。

1. キーが作成されたら、**[コピー]** を選択して、CLI で必要となるアクセス キーを取得します。

    ![API キーをクリップボードにコピーする](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > 安全な場所にキーを保存して秘密にします。 キーが誤って流出した場合は、いつでも再生成することができます。 CLI を通じてパッケージをプッシュする必要がなくなった場合は、API キーを削除することもできます。

1. コマンド プロンプトで、次のコマンドでパッケージ名を指定し、キーを手順 4 でコピーした値に置き換えて、コマンドを実行します。

    ```
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```
    
1. nuget.exe によって公開プロセスの結果が表示されます。

    ```
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. nuget.org のプロファイルから、**[パッケージの管理]** を選択して、公開したパッケージを確認します。 確認メールも送信されます。 パッケージがインデックス作成され、他のユーザーが検索して検索結果に表示されるようになるまでには、時間がかかる場合があることに注意してください。 この間、パッケージのページに次のメッセージが表示されます。

    ![このパッケージはまだインデックスされていません。 インデックス作成が完了すると、検索結果に表示され、インストール/復元に使用できるようになります。](media/QS_Create-03-NotIndexed.png)

> [!Note]
> **ウイルス スキャン**: nuget.org にアップロードされたすべてのパッケージはウイルス スキャンが行われ、ウイルスが見つかった場合には拒否されます。 nuget.org の一覧にあるすべてのパッケージも定期的にスキャンされます。

以上です。 最初の NuGet パッケージが [nuget.org](https://www.nuget.org/) に公開され、他の開発者がそれを自身のプロジェクトで使用することができます。

## <a name="related-topics"></a>関連トピック

- [パッケージの作成](../create-packages/creating-a-package.md)
- [パッケージの公開](../create-packages/publish-a-package.md)
- [複数のターゲット フレームワークのサポート](../create-packages/supporting-multiple-target-frameworks.md)
- [パッケージのバージョン管理](../reference/package-versioning.md)
- [ローカライズされたパッケージを作成する](../create-packages/creating-localized-packages.md)
