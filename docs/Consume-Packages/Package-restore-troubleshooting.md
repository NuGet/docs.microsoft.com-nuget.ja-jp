---
title: "Visual Studio での NuGet パッケージの復元に関するトラブルシューティング | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Visual Studio の一般的な NuGet の復元エラーの説明とトラブルシューティングの方法です。"
keywords: "NuGet パッケージの復元、パッケージの復元、トラブルシューティング、問題解決"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8efaed497a596921af3c73ab919831c73bf598e0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2018
---
# <a name="troubleshooting-package-restore-errors"></a>パッケージの復元エラーのトラブルシューティング

この記事では、パッケージを復元するときの一般的なエラーと、それを解決する手順に重点を置いて説明しています。 パッケージの復元の詳細については、[パッケージの復元](../consume-packages/package-restore.md#enabling-and-disabling-package-restore)に関するセクションを参照してください。

この記事の手順で問題が解決しない場合は、シナリオをより詳しく検討できるように、[GitHub で問題を報告してください](https://github.com/NuGet/docs.microsoft.com-nuget/issues)。 このページに [このページは役に立ちましたか] コントロールが表示されている場合でも使用しないでください。このコントロールでは、お客様に詳細情報を確認することができません。

## <a name="quick-solution-for-visual-studio-users"></a>Visual Studio ユーザー向けの簡単な解決方法

Visual Studio を使用している場合は、まず次のようにパッケージの復元を有効にします。 それ以外の場合は、次のセクションに進みます。

1. **[ツール]、[NuGet パッケージ マネージャー]、[パッケージ マネージャー設定]** メニュー コマンドの順に選択します。
1. **[パッケージの復元]** の両方のオプションをオンにします。
1. **[OK]** を選択します。
1. プロジェクトをもう一度ビルドします。

![[ツール]/[オプション] で NuGet パッケージの復元を有効にする](../consume-packages/media/restore-01-autorestoreoptions.png)

これらの設定は `NuGet.config` ファイルで変更することもできます。[同意](#consent)に関するセクションを参照してください。

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>このプロジェクトは、このコンピューターにはない NuGet パッケージを参照しています

詳細なエラー メッセージは次のとおりです。

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

このエラーは、1 つ以上の NuGet パッケージの参照を含むプロジェクトをビルドしようとしましたが、それらのパッケージが現在プロジェクトにキャッシュされていないことを示します (パッケージは、プロジェクトが `packages.config` を使用する場合はソリューション ルートの `packages` フォルダーにキャッシュされ、プロジェクトが PackageReference 形式を使用する場合は `obj/project.assets.json` ファイルにキャッシュされます)。

このような状況は、ソース管理や別のダウンロードからプロジェクトのソース コードを取得する場合によく発生します。 パッケージは、nuget.org のようなパッケージ フィードから復元できるので、通常はソース管理やダウンロードから除外されます ([パッケージとソース管理](Packages-and-Source-Control.md)に関するページを参照してください)。 パッケージを含めると、リポジトリがいっぱいになったり、.zip ファイルが不必要に大きくなったりします。

パッケージを復元するには、次のいずれかの方法を使用します。

- Visual Studio で、**[ツール] > [NuGet パッケージ マネージャー] > [パッケージ マネージャー設定]** メニュー コマンドを選択し、**[パッケージの復元]** の両方のオプションをオンにして、**[OK]** を選択します。 ソリューションをもう一度ビルドします。
- .NET Core プロジェクトの場合は、`dotnet restore` または `dotnet build` (自動的に復元が実行されます) を実行します。
- コマンド ラインで `nuget restore` を実行します (ただし、`dotnet restore` を使用する `dotnet` で作成されたプロジェクトは例外です)。
- PackageReference 形式を使用するプロジェクトのコマンド ラインで、`msbuild /t:restore` を実行します。

復元が成功すると、`packages` フォルダー (`packages.config` の使用時) または `obj/project.assets.json` ファイル (PackageReference の使用時) のいずれかが表示されます。 この場合、プロジェクトを正常にビルドできるようになります。 ビルドできない場合は、フォローを受けられるように [GitHub で問題を報告してください](https://github.com/NuGet/docs.microsoft.com-nuget/issues)。

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>資産ファイル project.assets.json が見つかりません

詳細なエラー メッセージは次のとおりです。

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

このエラーは、[前のセクション](#missing)で説明したエラーと同じ理由で発生し、同じ救済手段を利用できます。 たとえば、ソース管理から取得した .NET Core プロジェクトで `msbuild` を実行しても、パッケージは自動的に復元されません。 この場合、`msbuild /t:restore` の後に `msbuild` を実行するか、`dotnet build` を使用します (これでパッケージが自動的に復元されます)。

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

`nuget.config` の `packageRestore` 設定を直接編集する場合は、オプションのダイアログ ボックスに現在の値が表示されるように Visual Studio を再起動します。

## <a name="other-potential-conditions"></a>その他の考えられる条件

- ファイルが見つからないため、NuGet の復元を使用してダウンロードするというメッセージのビルド エラーが発生することがあります。 ただし、復元を実行すると、"すべてのパッケージは既にインストールされており、復元するものはありません" と表示されることがあります。 この場合は、`packages` フォルダー (`packages.config` の使用時) または `obj/project.assets.json` ファイル (PackageReference の使用時) を削除し、復元を実行し直してください。

- ソース管理からプロジェクトを取得するときに、プロジェクト フォルダーが読み取り専用に設定されている可能性があります。 フォルダーのアクセス許可を変更し、パッケージの復元を実行し直してください。

- 古いバージョンの NuGet を使用している可能性があります。 最新の推奨バージョンについては、[nuget.org/downloads](https://www.nuget.org/downloads) を確認してください。 Visual Studio 2015 の場合は、3.6.0 をお勧めします。

他の問題が発生している場合、詳細を確認できるように [GitHub で問題を報告してください](https://github.com/NuGet/docs.microsoft.com-nuget/issues)。