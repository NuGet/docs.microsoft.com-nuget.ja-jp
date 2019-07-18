---
title: インストールして、Visual Studio で NuGet パッケージの管理
description: Visual Studio で NuGet パッケージ マネージャー UI を使用して NuGet パッケージを操作するための手順です。
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 97e5de3f07199cd3c6a645749c8f2f1603ca630e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426247"
---
# <a name="install-and-manage-packages-in-visual-studio"></a>インストールして、Visual Studio でパッケージの管理

Windows 上の Visual Studio で NuGet パッケージ マネージャー UI を使用すると、簡単にインストール、アンインストール、およびプロジェクトとソリューションの NuGet パッケージを更新できます。 Visual studio for Mac のエクスペリエンスを参照してください。[を含む NuGet パッケージをプロジェクトに](/visualstudio/mac/nuget-walkthrough)します。 パッケージ マネージャー UI では、Visual Studio のコードに含まれません。

> [!NOTE]
> Visual Studio 2015 での NuGet パッケージ マネージャーは不足しているが、場合**ツール > 拡張機能と更新しています.** を検索し、 *NuGet パッケージ マネージャー*拡張機能。 Visual Studio の拡張機能インストーラーを使用する場合は、ダウンロード、拡張機能から直接[ https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)します。
>
> Visual Studio 2017 以降、NuGet、NuGet パッケージ マネージャーが自動的にインストールのいずれか。NET に関連するワークロード。 個別に選択してインストール、**個々 のコンポーネント > コード ツール > NuGet パッケージ マネージャー** Visual Studio インストーラーでオプションです。

## <a name="finding-and-installing-a-package"></a>検索して、パッケージをインストールします。

1. **ソリューション エクスプ ローラー**、いずれかを右クリックして**参照**プロジェクトや選択**NuGet パッケージの管理.** .

    ![NuGet パッケージのメニュー オプションを管理します。](media/ManagePackagesUICommand.png)

1. **参照** タブには、現在選択されているソースからの人気度でパッケージが表示されます (を参照してください[パッケージ ソース](#package-sources))。 検索ボックスを使用して、左上の特定のパッケージを検索します。 パッケージを実現する、その情報を表示するには、一覧から選択、**インストール**と共にバージョン選択ドロップダウン ボタンをクリックします。

    ![NuGet パッケージのダイアログの参照 タブを管理します。](media/Search.png)

1. ドロップダウン リストから目的のバージョンを選択し、選択**インストール**します。 Visual Studio では、パッケージとその依存関係をプロジェクトにインストールします。 ライセンス条項に同意を求められる場合があります。 インストールが完了したら、追加されたパッケージが表示されます、**インストール済み**タブ。パッケージが記載されても、**参照**のソリューション エクスプ ローラーでプロジェクトに参照できますを示すノード`using`ステートメント。

    ![ソリューション エクスプ ローラー内の参照](media/References.png)

> [!Tip]
> プレリリース版を検索に含めるし、プレリリース版で使用できるように、バージョン ドロップダウンの選択、**プレリリースを含める**オプション。

## <a name="uninstalling-a-package"></a>パッケージをアンインストールします。

1. **ソリューション エクスプ ローラー**、いずれかを右クリックして**参照**または目的のプロジェクトと選択**NuGet パッケージの管理.** .
1. 選択、**インストール済み**タブ。
1. (必要な場合は、リストをフィルター処理する検索を使用) をアンインストールするパッケージを選択し、選択**アンインストール**します。

    ![パッケージをアンインストールします。](media/UninstallPackage.png)

1. なお、**プレリリースを含める**と**パッケージ ソース**コントロールがある影響しないパッケージをアンインストールするときにします。

## <a name="updating-a-package"></a>パッケージの更新

1. **ソリューション エクスプ ローラー**、いずれかを右クリックして**参照**または目的のプロジェクトと選択**NuGet パッケージの管理.** .(Web サイト プロジェクトを右クリックし、 **Bin**フォルダー)。
1. 選択、**更新**タブを選択したパッケージ ソースから使用可能な更新プログラムのあるパッケージを参照してください。 選択**プレリリースを含める**更新リストにプレリリース パッケージを含めます。
1. パッケージを更新し、右側のドロップダウン リストから目的のバージョンを選択し、選択選択**更新**します。

    ![パッケージの更新](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>一部のパッケージ、 **Update**ボタンが無効になり、参照されている"暗黙的に、SDK によって"というメッセージが表示されます (または"AutoReferenced")。 このメッセージは、パッケージが大規模なフレームワークまたは SDK の一部であるとは別には更新されないことを示します。 (このようなパッケージが内部的に付いて`<IsImplicitlyDefined>True</IsImplicitlyDefined>`)。たとえば、 `Microsoft.NETCore.App` .NET Core SDK の一部であり、パッケージのバージョンでないアプリケーションで使用されるランタイム フレームワークのバージョンと同じです。 必要がある[、.NET Core のインストールを更新する](https://aka.ms/dotnet-download)を新しいバージョンの ASP.NET Core と .NET Core ランタイムを取得します。 [.NET Core メタパッケージとバージョン管理の詳細については、このドキュメントを参照してください](/dotnet/core/packages)します。 これは、次の一般的に使用されるパッケージに適用されます。
    * Microsoft.AspNetCore.All
    * Microsoft.AspNetCore.App
    * Microsoft.NETCore.App
    * NETStandard.Library

    ![参照または AutoReferenced として暗黙的にマークされているパッケージの例](media/PackageManagerUIAutoReferenced.png)

1. 最新バージョンに更新プログラムには、複数のパッケージをクリックし、一覧でそれを選択、**更新**リストの上ボタン。
1. 個々 のパッケージを更新することも、**インストール済み**タブ。パッケージの詳細がここでは、バージョン セレクターを含める (対象に、**プレリリースを含める**オプション)、 **Update**ボタンをクリックします。

## <a name="managing-packages-for-the-solution"></a>ソリューションのパッケージを管理します。

ソリューションのパッケージの管理は、複数のプロジェクトを同時に操作する便利な手段です。

1. 選択、**ツール > NuGet パッケージ マネージャー > ソリューションの NuGet パッケージを管理しています.** メニュー コマンド、またはソリューションを右クリックし  **NuGet パッケージの管理.** :

    ![ソリューションの NuGet パッケージを管理します。](media/ManagePackagesSolutionUICommand.png)

1. ソリューションのパッケージを管理する場合、UI を使用して、操作によって影響を受けるプロジェクトを選択できます。

    ![ソリューションのパッケージを管理するときに、プロジェクト セレクター](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>タブを統合します。

開発者と同じソリューション内の別のプロジェクト間で同じ NuGet パッケージの異なるバージョンを使用することを不適切な通常見なします。 パッケージ マネージャー UI は、ソリューションのパッケージを管理することを選択すると、**統合**を簡単に確認できます個別のバージョン番号を持つパッケージがソリューション内の異なるプロジェクトで使用されているタブ。

![[パッケージ マネージャー UI の統合] タブ](media/ConsolidateTab.png)

この例で、ClassLibrary1 プロジェクトで使用して EntityFramework 6.2.0、ConsoleApp1 で EntityFramework 6.1.0 を使用している一方です。 パッケージのバージョンを統合するには、次の操作を行います。

- プロジェクトの一覧で更新するプロジェクトを選択します。
- これらすべてのプロジェクトで使用するバージョンを選択、**バージョン**EntityFramework 6.2.0 などのコントロール。
- 選択、**インストール**ボタンをクリックします。

パッケージ マネージャーは、選択したすべてのプロジェクト、その後、パッケージに表示されなくに選択したパッケージのバージョンをインストール、**統合**タブ。

## <a name="package-sources"></a>パッケージ ソース

Visual Studio のパッケージの取得元のソースを変更するには、ソース セレクターから 1 つを選択します。

![パッケージ マネージャー UI でのパッケージ ソース セレクター](media/PackageSourceDropDown.png)

パッケージ ソースを管理するには。

1. 選択、**設定**パッケージ マネージャー UI のアイコンは、以下に示すまたはを使用して、**ツール > オプション**コマンドをスクロールして**NuGet パッケージ マネージャー**:

    ![パッケージ マネージャー UI の [設定] アイコン](media/PackageSourceSettings.png)

1. 選択、**パッケージ ソース**ノード。

    ![パッケージのソース オプション](media/options.png)

1. ソースを追加するには、次のように選択します。 **+** 、名前を編集、URL またはパスを入力、**ソース**制御、および選択**Update**します。 ソースは、セレクターのドロップダウン リストに表示されます。
1. パッケージ ソースを変更するには、選択しでの編集を行う、**名前**と**ソース**ボックス、および選択**Update**します。
1. パッケージ ソースを無効にするには、一覧内の名前の左側にあるボックスをオフにします。
1. パッケージ ソースを削除することを選択し、、 **X**ボタンをクリックします。
1. 使用し、下矢印ボタンは変わりませんパッケージ ソースの優先順位。 Visual Studio は、パッケージ ソースの順序を無視し、要求に応答する最初のソースからパッケージを使用します。 詳細については、次を参照してください。[パッケージの復元](../consume-packages/package-restore.md)します。

> [!Tip]
> コンピューター レベルまたはユーザー レベルで表示する場合がありますパッケージ ソースを削除した後再表示され場合、`NuGet.Config`ファイル。 参照してください[一般的な NuGet 構成](../consume-packages/configuring-nuget-behavior.md)これらのファイルの場所、ファイルを手動で編集するかを使用して、ソースを削除、 [nuget ソース コマンド](../tools/nuget-exe-CLI-reference.md)します。

## <a name="package-manager-options-control"></a>パッケージ マネージャーのオプションを制御します。

パッケージ マネージャー UI が、小規模なを表示、パッケージを選択すると、展開可能な**オプション**(ここで両方とも、折りたたみし、展開) バージョン セレクターで、次のコントロール。 一部のプロジェクトの型だけを**プレビュー ウィンドウの表示**オプションが提供されます。

![パッケージ マネージャーのオプション](media/PackageManagerUIOptions.png)

次のセクションでは、これらのオプションについて説明します。

### <a name="show-preview-window"></a>プレビュー ウィンドウを表示します。

選択した場合、モーダル ウィンドウが表示されますが、選択したパッケージの依存関係パッケージをインストールする前に。

![プレビュー ダイアログ ボックスの例](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>インストールと更新プログラムのオプション

(使用できませんのすべてのプロジェクトの種類。)

**依存関係の動作**NuGet がインストールする依存パッケージのバージョンを決定する方法を構成します。

- *依存関係を無視する*おり、インストールされているパッケージを通常それがすべての依存関係のインストールをスキップします。
- *最も低い*[Default] では、プライマリの選択したパッケージの要件を満たす最低限のバージョン番号と共に、依存関係がインストールされます。
- *最上位の修正プログラム*でも、同じメジャーおよびマイナー バージョン番号が、パッチ番号の最も高いバージョンをインストールします。 たとえば、バージョン 1.2.2 が指定されている場合、最も高いバージョン 1.2 で始まるがインストールされます。
- *最上位のマイナー*同じメジャー バージョン番号が最も高いマイナー番号と修正プログラム番号を使用のバージョンをインストールします。 バージョン 1.2.2 が指定されている場合、最上位のバージョン 1 で始まるはインストールします。
- *最も高い*最高の使用可能なバージョンのパッケージをインストールします。

**競合のアクションをファイル**NuGet を使用して、プロジェクトまたはローカル コンピューターに既に存在するパッケージを処理する方法を指定します。

- *プロンプト*NuGet 維持するか既存のパッケージを上書きするかどうかを確認するように指示します。
- *すべて無視*NuGet 既存のパッケージの上書きをスキップするように指示します。
- *すべて上書き*NuGet 既存のパッケージを上書きするように指示します。

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>アンインストール オプション

(使用できませんのすべてのプロジェクトの種類。)

**依存関係を削除**: 選択した場合、プロジェクトの他の場所で参照していない場合、依存パッケージを削除します。

**強制アンインストールの依存関係がある場合でも**: 選択すると、引き続きプロジェクトで参照されている場合でも、パッケージをアンインストールします。 これは通常と組み合わせて使用**依存関係を削除**パッケージをあらゆる要素を削除する依存関係がインストールされていること。 このオプションを使用するおそれがあります、ただし、プロジェクトに壊れた参照。 このような場合は、する必要があります[これら他のパッケージを再インストール](../consume-packages/reinstalling-and-updating-packages.md)します。
