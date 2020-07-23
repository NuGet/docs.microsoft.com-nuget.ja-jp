---
title: Visual Studio での NuGet パッケージの復元に関するトラブルシューティング
description: Visual Studio の一般的な NuGet の復元エラーの説明とトラブルシューティングの方法です。
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: b162990eae2160961f560b6c6ee73e47cb4121d6
ms.sourcegitcommit: f29fa9b93fd59e679fab50d7413bbf67da3ea5b3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/17/2020
ms.locfileid: "86451152"
---
# <a name="troubleshooting-package-restore-errors"></a>パッケージの復元エラーのトラブルシューティング

この記事では、パッケージを復元するときの一般的なエラーと、それを解決する手順に重点を置いて説明しています。 

[パッケージの復元] では、プロジェクト ファイル ( *.csproj*) のパッケージ参照か *packages.config* ファイルに一致する正しい状態になるよう、すべてのパッケージの依存関係のインストールを試みます。 (Visual Studio では、参照は **[依存関係] \ [NuGet]** または **[参照]** ノードの下にあるソリューション エクスプローラーに表示されます。)パッケージを復元するために必要な手順に従うには、「[パッケージの復元](../consume-packages/package-restore.md#restore-packages)」をご覧ください。 プロジェクト ファイル ( *.csproj*) のパッケージ参照、または *packages.config* ファイルが正しくない ([パッケージの復元] 後に必要な状態と一致しない) 場合は、パッケージの復元を使う代わりにパッケージをインストールまたは更新する必要があります。

この記事の手順で問題が解決しない場合は、シナリオをより詳しく検討できるように、[GitHub で問題を報告してください](https://github.com/NuGet/docs.microsoft.com-nuget/issues)。 このページに [このページは役に立ちましたか] コントロールが表示されている場合でも使用しないでください。このコントロールでは、お客様に詳細情報を確認することができません。

## <a name="quick-solution-for-visual-studio-users"></a>Visual Studio ユーザー向けの簡単な解決方法

Visual Studio を使用している場合は、まず次のようにパッケージの復元を有効にします。 それ以外の場合は、次のセクションに進みます。

1. **[ツール]、[NuGet パッケージ マネージャー]、[パッケージ マネージャー設定]** メニュー コマンドの順に選択します。
1. **[パッケージの復元]** の両方のオプションをオンにします。
1. **[OK]** を選択します。
1. プロジェクトをもう一度ビルドします。

![[ツール]/[オプション] で NuGet パッケージの復元を有効にする](../consume-packages/media/restore-01-autorestoreoptions.png)

これらの設定は `NuGet.config` ファイルで変更することもできます。[同意](#consent)に関するセクションを参照してください。 ご自身のプロジェクトが、MSBuild に統合されたパッケージの復元を使用する以前のプロジェクトであった場合は、パッケージの自動復元に[移行](package-restore.md#migrate-to-automatic-package-restore-visual-studio)することが必要になる場合があります。

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>このプロジェクトは、このコンピューターにはない NuGet パッケージを参照しています

詳細なエラー メッセージは次のとおりです。

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

このエラーは、ビルドしようとしているプロジェクトに、現在コンピューターまたはプロジェクトにインストールされていない NuGet パッケージへの参照が 1 つ以上含まれている場合に発生します。

- [PackageReference](package-references-in-project-files.md) 管理形式を使用する場合、このエラーは、[グローバル パッケージとキャッシュ フォルダーの管理](managing-the-global-packages-and-cache-folders.md)に関する記事で説明されているように、パッケージが "*グローバル パッケージ*" フォルダーにインストールされていないことを意味します。
- [packages.config](../reference/packages-config.md) を使用する場合、このエラーは、パッケージがソリューション ルートにある `packages` フォルダーにインストールされていないことを意味します。

このような状況は、ソース管理や別のダウンロードからプロジェクトのソース コードを取得する場合によく発生します。 パッケージは、nuget.org のようなパッケージ フィードから復元できるので、通常はソース管理やダウンロードから除外されます ([パッケージとソース管理](Packages-and-Source-Control.md)に関するページを参照してください)。 パッケージを含めると、リポジトリがいっぱいになったり、.zip ファイルが不必要に大きくなったりします。

このエラーは、プロジェクト ファイルにパッケージの場所の絶対パスが含まれているとき、そのプロジェクトを移動した場合にも発生します。

パッケージを復元するには、次のいずれかの方法を使用します。

- プロジェクト ファイルを移動した場合、ファイルを直接編集し、パッケージ参照を更新します。
- [Visual Studio](package-restore.md#restore-using-visual-studio) ([自動復元](package-restore.md#restore-packages-automatically-using-visual-studio)または[手動復元](package-restore.md#restore-packages-manually-using-visual-studio))
- [dotnet CLI](package-restore.md#restore-using-the-dotnet-cli)
- [nuget.exe CLI](package-restore.md#restore-using-the-nugetexe-cli)
- [MSBuild](package-restore.md#restore-using-msbuild)
- [Azure Pipelines](package-restore.md#restore-using-azure-pipelines)
- [Azure DevOps Server](package-restore.md#restore-using-azure-devops-server)

復元に成功したら、"*グローバル パッケージ*" フォルダーにパッケージが表示されます。 PackageReference を使用するプロジェクトの場合、復元によって `obj/project.assets.json` ファイルが再び作成されます。`packages.config` を使用するプロジェクトの場合、プロジェクトの `packages` フォルダーにパッケージが表示されます。 この場合、プロジェクトを正常にビルドできるようになります。 ビルドできない場合は、フォローを受けられるように [GitHub で問題を報告してください](https://github.com/NuGet/docs.microsoft.com-nuget/issues)。

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>資産ファイル project.assets.json が見つかりません

詳細なエラー メッセージは次のとおりです。

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

PackageReference 管理形式を使用する場合、`project.assets.json` ファイルによってプロジェクトの依存関係グラフが保持されます。このグラフを使用して、必要なパッケージがすべてコンピューターにインストールされていることを確認します。 このファイルはパッケージの復元を通じて動的に生成されるため、通常はソース管理に追加されません。 その結果、自動的にパッケージを復元しない `msbuild` などのツールでプロジェクトをビルドすると、このエラーが発生します。

この場合、`msbuild -t:restore` の後に `msbuild` を実行するか、`dotnet build` を使用します (これでパッケージが自動的に復元されます)。 また、[前のセクション](#missing)のいずれかの方法を使用してパッケージを復元することもできます。

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>1 つ以上の NuGet パッケージを復元する必要がありますが、同意が与えられていないため、復元できませんでした

詳細なエラー メッセージは次のとおりです。

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

このエラーは、NuGet の構成でパッケージの復元が無効になっていることを示します。

「[Visual Studio ユーザー向けの簡単な解決方法](#quick-solution-for-visual-studio-users)」で前述したように、Visual Studio で該当する設定を変更できます。

これらの設定は、該当する `nuget.config` ファイル (通常、Windows では `%AppData%\NuGet\NuGet.Config`、Mac/Linux では `~/.nuget/NuGet/NuGet.Config`) で直接編集することもできます。 `packageRestore` の `enabled` キーと `automatic` キーが True に設定されていることを確認します。

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> `nuget.config` の `packageRestore` 設定を直接編集する場合は、オプションのダイアログ ボックスに現在の値が表示されるように Visual Studio を再起動します。

## <a name="other-potential-conditions"></a>その他の考えられる条件

- ファイルが見つからないため、NuGet の復元を使用してダウンロードするというメッセージのビルド エラーが発生することがあります。 ただし、復元を実行すると、"すべてのパッケージは既にインストールされており、復元するものはありません" と表示されることがあります。 この場合は、`packages` フォルダー (`packages.config` の使用時) または `obj/project.assets.json` ファイル (PackageReference の使用時) を削除し、復元を実行し直してください。 エラーが引き続き発生する場合は、コマンドラインから `nuget locals all -clear` または `dotnet nuget locals all --clear` を使用して、「[グローバル パッケージとキャッシュ フォルダーの管理](managing-the-global-packages-and-cache-folders.md)」で説明されているように、"*グローバル パッケージ*" フォルダーとキャッシュ フォルダーをクリアします。

- ソース管理からプロジェクトを取得するときに、プロジェクト フォルダーが読み取り専用に設定されている可能性があります。 フォルダーのアクセス許可を変更し、パッケージの復元を実行し直してください。

- 古いバージョンの NuGet を使用している可能性があります。 最新の推奨バージョンについては、[nuget.org/downloads](https://www.nuget.org/downloads) を確認してください。 Visual Studio 2015 の場合は、3.6.0 をお勧めします。

他の問題が発生している場合、詳細を確認できるように [GitHub で問題を報告してください](https://github.com/NuGet/docs.microsoft.com-nuget/issues)。
