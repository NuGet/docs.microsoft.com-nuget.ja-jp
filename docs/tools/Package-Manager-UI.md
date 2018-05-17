---
title: NuGet パッケージ マネージャーの UI リファレンス
description: Visual Studio で NuGet パッケージ マネージャーの UI を使用して NuGet パッケージを操作するための手順です。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 1d8cb8186b9cedb29918d48539bdf45b130030c0
ms.sourcegitcommit: 00c4c809c69c16fcf4d81012eb53ea22f0691d0b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2018
---
# <a name="nuget-package-manager-ui"></a>NuGet パッケージ マネージャーの UI

Windows 上の Visual Studio で NuGet パッケージ マネージャー UI を使用すると、インストール、アンインストール、およびプロジェクトおよびソリューションの NuGet パッケージの更新を簡単にできます。 Mac のエクスペリエンスを Visual Studio で、次を参照してください。[などの NuGet パッケージ、プロジェクトの](/visualstudio/mac/nuget-walkthrough)します。 パッケージ マネージャーの UI は、Visual Studio のコードに含まれていません。

このトピックの内容:

- [検索とインストール パッケージ ([参照] タブ)](#finding-and-installing-a-package)
- [パッケージ (インストール済み タブ) をアンインストールします。](#uninstalling-a-package)
- [パッケージ (インストールおよび更新 タブ) の更新](#updating-a-package)(が含まれています、 [「SDK によって暗黙的に参照される」または"AutoReferenced"メッセージ](#implicit_reference))
- [ソリューションのパッケージを管理する](#managing-packages-for-the-solution)(同時に複数のプロジェクトの操作)。
- [パッケージ ソース](#package-sources)
- [パッケージ マネージャーのオプションを制御します。](#package-manager-options-control)

> [!Note]
> Visual Studio 2015 内の NuGet パッケージ マネージャー、欠落している場合は確認**ツール > 拡張機能と更新しています.** を検索し、 *NuGet Package Manager*拡張機能です。 Visual Studio での拡張機能インストーラーを使用することがない場合は、ダウンロードから直接、拡張機能[ https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)です。
>
> Visual Studio 2017 のいずれかと NuGet と NuGet パッケージ マネージャーが自動的にインストールします。NET に関連するワークロードです。 個別に選択してインストール、**個々 のコンポーネント > コード ツール > の NuGet package manager** Visual Studio 2017 インストーラー オプション。

## <a name="finding-and-installing-a-package"></a>検索して、パッケージをインストールします。

1. **ソリューション エクスプ ローラー**、いずれかを右クリックして**参照**またはプロジェクトと選択**NuGet パッケージを管理しています.**.

    ![NuGet パッケージのメニュー オプションを管理します。](media/ManagePackagesUICommand.png)

1. **参照** タブでは、現在選択されているソースから人気度によってパッケージが表示されます (を参照してください[ソースをパッケージ化](#package-sources))。 検索ボックスを使用して、左上の特定のパッケージを検索します。 パッケージ一覧から選択できるよう、情報を表示する、**インストール**バージョン選択ドロップダウン リストとボタンをクリックします。

    ![[管理] タブの NuGet パッケージ ダイアログの参照](media/Search.png)

1. ドロップダウン リストから、必要なバージョンを選択し、選択**インストール**です。 Visual Studio は、プロジェクトにパッケージとその依存関係をインストールします。 ライセンス条項に同意するように求められます。 インストールが完了したらに追加されたパッケージが表示されます。、**インストール**タブです。パッケージが記載されても、**参照**のソリューション エクスプ ローラーで、プロジェクト内に参照できることを示すノード`using`ステートメントです。

    ![ソリューション エクスプ ローラー内の参照](media/References.png)

> [!Tip]
> プレリリース バージョンを検索に含めるし、プレリリース版で利用できるように、バージョン ドロップダウンの選択、**プレリリースを含める**オプション。

## <a name="uninstalling-a-package"></a>パッケージをアンインストールします。

1. **ソリューション エクスプ ローラー**、いずれかを右クリックして**参照**または目的のプロジェクトをクリックし、 **NuGet パッケージを管理しています.**.
1. 選択、**インストール**タブです。
1. (必要な場合は、リストをフィルター処理する検索を使用) をアンインストールするパッケージを選択し、選択**アンインストール**です。

    ![パッケージをアンインストールします。](media/UninstallPackage.png)

1. 注意してください、 **Include prerelease**と**パッケージ ソース**コントロールがある影響しないパッケージをアンインストールするとします。

## <a name="updating-a-package"></a>パッケージの更新

1. **ソリューション エクスプ ローラー**、いずれかを右クリックして**参照**または目的のプロジェクトをクリックし、 **NuGet パッケージを管理しています.**.(Web サイト プロジェクトを右クリックし、 **Bin**フォルダーです)。
1. 選択、**更新**タブを選択したパッケージ ソースから使用可能な更新プログラムのあるパッケージを参照してください。 選択**プレリリースを含める**プレリリースのパッケージの一覧に含める、更新します。
1. パッケージを更新し、右側のドロップダウン リストから、必要なバージョンを選択して、選択を選択して**更新**です。

    ![パッケージの更新](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>一部のパッケージ、**更新**ボタンが無効になり、メッセージが参照されている"暗黙的に、SDK によって"というメッセージが表示されます (または"AutoReferenced") です。 メッセージは、Microsoft.NETCore.App または Microsoft.NETStandard.Library など、パッケージが、大規模なフレームワークまたは SDK の一部であるとは別に更新してはならないことを示します。 (このようなパッケージが付いている内部的に`<IsImplicitlyDefined>True</IsImplicitlyDefined>`)。パッケージを更新するには、パッケージ名を含んでいる SDK の推論が属する、SDK を更新します。 たとえば、Microsoft.NETCore.App と同様に、パッケージは、.NET Core SDK の一部、したがって、.NET Core SDK のインストールを更新する必要があります。

    ![参照または AutoReferenced として暗黙的にマークされているパッケージの例](media/PackageManagerUIAutoReferenced.png)

1. 更新するには複数のパッケージを最新のバージョンでそれを選択リストと選択、**更新**一覧の上のボタンをクリックします。
1. 個々 のパッケージを更新することも、**インストール**タブです。ここでは、パッケージの詳細がバージョン セレクターを含める (対象に、 **Include prerelease**オプション) と**更新**ボタンをクリックします。

## <a name="managing-packages-for-the-solution"></a>ソリューションのパッケージを管理します。

ソリューションのパッケージの管理は、同時に複数のプロジェクトを操作する便利な手段です。

1. 選択、**ツール > NuGet Package Manager > ソリューションの NuGet パッケージを管理しています.** メニュー コマンド、またはソリューションを右クリックし  **NuGet パッケージを管理しています.**:

    ![ソリューションの NuGet パッケージを管理します。](media/ManagePackagesSolutionUICommand.png)

1. ソリューションのパッケージを管理する場合、UI 操作によって影響を受けるプロジェクトを選択できます。

    ![ソリューションのパッケージを管理するときに、プロジェクト セレクター](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>タブを統合します。

開発者と同じソリューション内の別のプロジェクトにわたって、同じの NuGet パッケージの異なるバージョンを使用することを不適切な通常解釈します。 ソリューションのパッケージを管理することを選択すると、パッケージ マネージャーの UI を提供する**Consolidate**を簡単にわかるソリューション内の別のプロジェクトで個別のバージョン番号を持つパッケージを使用する場所 タブ。

![[パッケージ マネージャー UI の統合] タブ](media/ConsolidateTab.png)

この例では、ClassLibrary1 プロジェクトは EntityFramework を使用した 6.2.0、EntityFramework 6.1.0 ConsoleApp1 が使用されている一方です。 パッケージのバージョンを統合するには、次の操作を行います。

- プロジェクトの一覧で更新するプロジェクトを選択します。
- 内のそれらのすべてのプロジェクトで使用するバージョンを選択して、**バージョン**EntityFramework 6.2.0 などのコントロールです。
- 選択、**インストール**ボタンをクリックします。

パッケージ マネージャーでは、選択したパッケージのバージョンをインストールするまで、パッケージは表示されなくなりますで、選択したすべてのプロジェクトに、 **Consolidate**タブです。

## <a name="package-sources"></a>パッケージ ソース

Visual Studio のパッケージの取得元のソースを変更するには、ソース セレクターから 1 つを選択します。

![パッケージ マネージャー UI でパッケージ ソースの選択](media/PackageSourceDropDown.png)

パッケージ ソースを管理します。

1. 選択、**設定**パッケージ マネージャー UI のアイコンが以下に示すか、使用して、**ツール > オプション**コマンドをスクロールして**NuGet Package Manager**:

    ![パッケージ マネージャー UI の [設定] アイコン](media/PackageSourceSettings.png)

1. 選択、**パッケージ ソース**ノード。

    ![パッケージ ソースのオプション](media/options.png)

1. ソースを追加するには、次のように選択します。 **+**、名前を編集、URL またはパスを入力、**ソース**制御、および選択**更新**です。 ソースは、セレクターのドロップダウンに表示されます。
1. パッケージ ソースを変更するには、選択しでの編集を行う、**名前**と**ソース**ボックス、および選択**更新**です。
1. パッケージ ソースを無効にするには、一覧内の名前の左側のボックスをオフにします。
1. 削除するには、パッケージ ソースを選択し、、 **X**ボタンをクリックします。
1. 上矢印を使用し、下向きの矢印ボタンをパッケージ ソースの優先順位を変更します。 Visual Studio は、プロジェクトのパッケージを復元するときに、優先順位の順序でこれらのソースを検索します。 詳細については、次を参照してください。[パッケージの復元](../consume-packages/package-restore.md)です。

> [!Tip]
> 場合は、パッケージ ソースでは、削除した後再表示され、コンピューター レベルまたはユーザー レベルで表示場合があります`NuGet.Config`ファイル。 参照してください[構成 NuGet 動作](../consume-packages/configuring-nuget-behavior.md)これらのファイルの場所を削除して、ソース ファイルを手動で編集するかを使用して、 [nuget コマンドをソース](../tools/nuget-exe-CLI-reference.md)です。

## <a name="package-manager-options-control"></a>パッケージ マネージャーのオプションを制御します。

パッケージを選択すると、パッケージ マネージャーの UI 表示の小さな展開可能な**オプション**コントロール (この図で折りたたまれているし、展開された両方) のバージョンのセレクターの下。 一部のプロジェクトの型だけを**ショー プレビュー ウィンドウ**オプションが用意されてです。

![パッケージ マネージャーのオプション](media/PackageManagerUIOptions.png)

次のセクションでは、これらのオプションについて説明します。

### <a name="show-preview-window"></a>プレビュー ウィンドウを表示します。

選択した場合、モーダル ウィンドウが表示されますが、選択したパッケージの依存関係パッケージをインストールする前に。

![プレビュー ダイアログ ボックスの例](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>インストールと更新プログラムのオプション

(使用できませんのすべてのプロジェクトの種類)。

**依存関係の動作**NuGet がインストールする依存パッケージのバージョンを決定する方法を構成します。

- *依存関係を無視する*がインストールされているパッケージを通常破損の依存関係のインストールをスキップします。
- *最小*[既定値] は、プライマリの選択したパッケージの要件を満たしている最小バージョン番号を持つ依存関係をインストールします。
- *最上位の修正プログラム*同じメジャーおよびマイナー バージョン番号が最新の修正プログラム番号とバージョンをインストールします。 たとえば、バージョン 1.2.2 が指定されている場合、最高バージョン 1.2 で始まるがインストールされます。
- *最高のマイナー*バージョンが同じメジャー バージョン番号が、最高のマイナー番号と修正プログラム番号をインストールします。 1.2.2 のバージョンが指定されている場合、1 で始まる最高のバージョンがインストールされます。
- *最も高い*パッケージの利用可能な最高のバージョンがインストールされます。

**競合のアクションをファイル**NuGet を使用して、プロジェクトまたはローカル コンピューターに既に存在するパッケージを処理する方法を指定します。

- *プロンプト*を NuGet に維持するか既存のパッケージを上書きするかどうかを確認するように指示します。
- *すべて無視*を NuGet に既存のパッケージの上書きをスキップするように指示します。
- *すべて上書きする*を NuGet に既存のパッケージを上書きするように指示します。

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>アンインストール オプション

(使用できませんのすべてのプロジェクトの種類)。

**依存関係を削除**: 選択した場合、プロジェクトの他の場所で参照していない場合、依存パッケージを削除します。

**強制アンインストールに依存している場合でも**: 選択した場合、プロジェクトにまだ参照されている場合でも、パッケージをアンインストールします。 これは通常と組み合わせて使用**依存関係を削除**パッケージとその内容を削除する依存関係がインストールされています。 このオプションを使用するおそれがあります、ただし、プロジェクトに壊れた参照。 このような場合にする必要があります[これら他のパッケージを再インストール](../consume-packages/reinstalling-and-updating-packages.md)です。
