---
title: Windows の Visual Studio を使用した .NET Framework NuGet パッケージの作成と公開
description: Windows の Visual Studio を使用した、.NET Framework NuGet パッケージの作成と公開に関するチュートリアルです。
author: karann-msft
ms.author: karann
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: e00aac83a710e2f745d5e4bb9aec741ee686e595
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380646"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a>クイック スタート: Visual Studio を使用したパッケージの作成と公開 (.NET Framework、Windows)

.NET Framework クラス ライブラリから NuGet パッケージを作成するには、Windows の Visual Studio で DLL を作成した後、nuget.exe コマンド ライン ツールを使用してパッケージを作成し、公開します。

> [!Note]
> このクイック スタートが適用されるのは、Windows 用の Visual Studio 2017 以降のバージョンのみです。 ここで説明される機能は、Visual Studio for Mac には含まれません。 代わりに [dotnet CLI ツール](create-and-publish-a-package-using-the-dotnet-cli.md)を使用してください。

## <a name="prerequisites"></a>必須コンポーネント

1. [visualstudio.com](https://www.visualstudio.com/) から Visual Studio 2017 以降の任意のエディションと、.NET 関連の任意のワークロードをインストールします。 Visual Studio 2017 では、.NET ワークロードをインストールする際、NuGet 機能は自動的に含まれません。

1. `nuget.exe` CLI をインストールします。[nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)からその `.exe`ファイルをダウンロードし、適切なフォルダーに保存して、そのフォルダーを PATH 環境変数に追加してください。

1. まだ持っていない場合は、[nuget.org で無料アカウントを登録](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)します。 新しいアカウントを作成すると、確認メールが送信されます。 パッケージをアップロードするには、その前にアカウントを確認する必要があります。

## <a name="create-a-class-library-project"></a>クラス ライブラリ プロジェクトを作成する

パッケージ化するコードに既存の .NET Framework クラス ライブラリ プロジェクトを使用することも、次の手順に従って単純なプロジェクトを作成することもできます。

1. Visual Studio で、 **[ファイル]、[新規]、[プロジェクト]** の順に選択し、 **[Visual C#]** ノードを選択し、"クラス ライブラリ (.NET Framework)" テンプレートを選択し、プロジェクトに AppLogger という名前を付け、 **[OK]** をクリックします。

1. 作成されたプロジェクト ファイルを右クリックし、 **[ビルド]** を選択して、プロジェクトが正しく作成されたことを確認します。 DLL は、デバッグ フォルダー (または代わりにその構成をビルドした場合はリリース フォルダー) 内にあります。

実際の NuGet パッケージ内ではもちろん、多くの便利な機能を実装し、他のユーザーはそれを使用してアプリケーションをビルドできます。 また、目的のターゲット フレームワークに設定することもできます。 例については、[UWP](../guides/create-uwp-packages.md) と [Xamarin](../guides/create-packages-for-xamarin.md) のガイドを参照してください。

しかし、このチュートリアルでは、パッケージを作成するには、テンプレートのクラス ライブラリで十分なため、追加のコードを記述することはありません。 それでも、パッケージの一部の機能コードが必要な場合は、次のように使用します。

```cs
using System;

namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> それ以外を選択する理由がない限り、.NET Standard は最も広い範囲の使用プロジェクトとの互換性を提供するため、NuGet パッケージの優先ターゲットです。 「[Visual Studio を使用したパッケージの作成と公開 (.NET Standard)](create-and-publish-a-package-using-visual-studio.md)」を参照してください。

## <a name="configure-project-properties-for-the-package"></a>パッケージのプロジェクト プロパティを構成する

NuGet パッケージには、パッケージ識別子、バージョン番号、説明などの関連するメタデータを含むマニフェスト (`.nuspec` ファイル) が含まれています。 これらの一部は、プロジェクトのプロパティから直接引き出すことができるので、プロジェクトとマニフェストの両方で個別に更新する必要はありません。 このセクションでは、適用可能なプロパティを設定する場所について説明します。

1. **[プロジェクト]、[プロパティ]** メニュー コマンドの順に選択し、 **[アプリケーション]** タブを選択します。

1. **[アセンブリ名]** フィールドで、パッケージに一意の識別子を付けます。

    > [!Important]
    > パッケージには、nuget.org または使用しているホスト全体で一意の識別子を付ける必要があります。 このチュートリアルでは、以降の公開手順でパッケージを一般公開するので (ただし、誰かが実際に使用する可能性はありません)、名前に "Sample" または "Test" を含めることをお勧めします。
    >
    > 既に存在する名前のパッケージを公開しようとすると、エラーが表示されます。

1. **[アセンブリ情報]** ボタンを選択すると、マニフェストに含める他のプロパティを入力するためのダイアログ ボックスが表示されます ([.nuspec ファイル リファレンスの置換トークン](../reference/nuspec.md#replacement-tokens)に関するセクションを参照してください)。 最もよく使用されるフィールドは、 **[タイトル]** 、 **[説明]** 、 **[会社名]** 、 **[著作権]** 、 **[アセンブリ バージョン]** です。 これらのプロパティは、最終的に nuget.org のようなホスト上でパッケージと共に表示されるので、わかりやすい値を設定してください。

    ![Visual Studio の .NET Framework プロジェクトのアセンブリ情報](media/qs_create-vs-01b-project-properties.png)

1. 省略可能: プロパティを直接表示および編集するには、プロジェクトの `Properties/AssemblyInfo.cs` ファイルを開きます。

1. プロパティが設定されたら、プロジェクトの構成を**リリース**に設定し、プロジェクトをリビルドして、更新された DLL を生成します。

## <a name="generate-the-initial-manifest"></a>初期マニフェストを生成する

DLL を入手し、プロジェクトのプロパティを設定したら、`nuget spec` コマンドを使用してプロジェクトから最初の `.nuspec` ファイルを生成します。 この手順には、プロジェクト ファイルから情報を引き出すための関連する置換トークンが含まれています。

`nuget spec` を 1 回のみ実行して最初のマニフェストを生成します。 パッケージを更新するときは、プロジェクトの値を変更するか、マニフェストを直接編集します。

1. コマンド プロンプトを開き、`AppLogger.csproj` ファイルが格納されているプロジェクト フォルダーに移動します。

1. 次のコマンドを実行します: `nuget spec AppLogger.csproj` プロジェクトを指定すると、NuGet でプロジェクトの名前 (この場合は `AppLogger.nuspec`) と一致するマニフェストが作成されます。 マニフェストには置換トークンも含まれます。

1. テキスト エディターで `AppLogger.nuspec` を開き、内容を確認します。内容は次のようになります。

    ```xml
    <?xml version="1.0"?>
    <package >
      <metadata>
        <id>Package</id>
        <version>1.0.0</version>
        <authors>YourUsername</authors>
        <owners>YourUsername</owners>
        <license type="expression">MIT</license>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Package description</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2019</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a>マニフェストを編集する

1. `.nuspec` ファイルで既定値のパッケージを作成しようとすると NuGet でエラーが発生するため、次のフィールドを編集して続行する必要があります。 これらの使用方法については、[.nuspec ファイル リファレンスのオプションのメタデータ要素](../reference/nuspec.md#optional-metadata-elements)に関するセクションを参照してください。

    - licenseUrl
    - projectUrl
    - iconUrl
    - releaseNotes
    - tags

1. 公開用にビルドされたパッケージの場合は、**Tags** プロパティに特に注意してください。これらのタグは nuget.org などのソースで他のユーザーがパッケージを検索して、パッケージの動作を理解する場合に役立ちます。

1. [.nuspec ファイル リファレンス](../reference/nuspec.md)で説明されているように、この時点で他の要素をマニフェストに追加することもできます。

1. 続行する前にファイルを保存してください。

## <a name="run-the-pack-command"></a>pack コマンドを実行する

1. `.nuspec` ファイルを含むフォルダーのコマンド プロンプトから、コマンド `nuget pack` を実行します。

1. NuGet で、現在のフォルダー内に *identifier-version.nupkg* の形式で `.nupkg` ファイルが生成されます。

## <a name="publish-the-package"></a>パッケージを公開する

`.nupkg` ファイルを作成したら、`nuget.exe` と、nuget.org から取得した API キーを使用して、そのファイルを nuget.org に公開します。nuget.org の場合は、`nuget.exe` 4.1.0 以降を使用する必要があります。

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>API キーを取得する

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>nuget push を使用して公開する

1. コマンド ラインを開き、`.nupkg` ファイルを含むフォルダーに変更します。

1. 次のコマンドでパッケージ名を指定し、キーを API キーに置き換えて、コマンドを実行します。

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe によって公開プロセスの結果が表示されます。

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

[nuget push](../reference/cli-reference/cli-ref-push.md)に関するページを参照してください。

### <a name="publish-errors"></a>公開エラー

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>公開済みパッケージを管理する

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a>次の手順

無事に、最初の NuGet パッケージを作成できました。

> [!div class="nextstepaction"]
> [パッケージの作成](../create-packages/creating-a-package.md)

NuGet による提供についてさらに詳しく調べるには、下のリンクを選択してください。

- [パッケージの公開](../nuget-org/publish-a-package.md)
- [プレリリース パッケージ](../create-packages/Prerelease-Packages.md)
- [複数のターゲット フレームワークのサポート](../create-packages/supporting-multiple-target-frameworks.md)
- [パッケージのバージョン管理](../concepts/package-versioning.md)
- [ローカライズされたパッケージを作成する](../create-packages/creating-localized-packages.md)
