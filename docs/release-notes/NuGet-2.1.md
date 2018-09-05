---
title: NuGet 2.1 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 2.1 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fd6dadc7968991c77c1b06a6a261415355b2fd73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548598"
---
# <a name="nuget-21-release-notes"></a>NuGet 2.1 リリース ノート

[NuGet 2.0 のリリース ノート](../release-notes/nuget-2.0.md) | [NuGet 2.2 リリース ノート](../release-notes/nuget-2.2.md)

NuGet 2.1 は、2012 年 10 月 4 日にリリースされました。

## <a name="hierarchical-nugetconfig"></a>Nuget.Config の階層

NuGet 2.1 には探してフォルダー構造をウォークを再帰的に使用して NuGet の設定を制御するのには柔軟性が高まります`NuGet.Config`ファイルとし、見つかったすべてのファイルのセットから構成を構築します。  たとえば、チームの他の内部の依存関係の CI ビルド、パッケージの内部リポジトリがあるシナリオを検討してください。 個々 のプロジェクトのフォルダー構造は、次のようになります。

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

さらに、ソリューションのパッケージの復元が有効な場合、次のフォルダーも存在します。

    C:\myteam\solution1\.nuget

チームがいない利用できるようにすべてのプロジェクトのコンピューターの中には、すべてのプロジェクトで使用できるチームの内部のパッケージのリポジトリを確保するために新しい Nuget.Config ファイルを作成し、c:\myteam フォルダーに配置。 方法はありませんに指定し、プロジェクトごとの [パッケージ] フォルダー。

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

次に示すように c:\myteam 下にある任意のフォルダーから 'nuget.exe ソース' コマンドを実行して、ソースが追加されたことことがわかります。

![親の nuget 構成からパッケージ ソース](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` 次の順序でのファイルが検索されます。

1. `.nuget\Nuget.Config`
2. ルート プロジェクト フォルダーから再帰がについて説明します
3. グローバル`Nuget.Config`(`%appdata%\NuGet\Nuget.Config`)

この構成は、適用により、*の逆順*、上記の順序に基づくことを意味するには、全体の Nuget.Config が最初に適用される検出された Nuget.Config ファイル ルートからプロジェクト フォルダーに、後にによって`.nuget\Nuget.Config`します。  これは、使用する場合に特に重要な`<clear/>`構成から一連の項目を削除する要素。

## <a name="specify-packages-folder-location"></a>'パッケージ' フォルダーの場所を指定します。

以前は、NuGet がソリューションのルート フォルダーの下の既知の 'パッケージ' フォルダーからソリューションのパッケージを管理します。  NuGet パッケージをインストールしているが、さまざまなソリューションが開発チームが、その結果、ファイル システム上のさまざまな場所にインストールされる同じパッケージで。

NuGet 2.1 を使用して、[パッケージ] フォルダーの場所をより細かく制御を提供する、`repositoryPath`内の要素、`NuGet.Config`ファイル。  Nuget.Config の階層のサポートの前の例でのビルドでは、C:\myteam\ 共有と同じパッケージ フォルダーの下のすべてのプロジェクトがあるすることを前提としています。  これを実現するには、次のエントリを追加だけ`c:\myteam\Nuget.Config`です。

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

この例で、共有`Nuget.Config`ファイルは、深さに関係なく C:\myteam の下に作成されるすべてのプロジェクトの共有パッケージ フォルダーを指定します。 既存のパッケージ フォルダーをソリューションのルートの下にある場合は場合、NuGet は、新しい場所にパッケージを配置前に削除する必要がありますに注意してください。

## <a name="support-for-portable-libraries"></a>ポータブル ライブラリのサポート

[ポータブル ライブラリ](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library)は Windows Phone、Xbox の偶数を Silverlight に.net Framework のバージョンからのさまざまな Microsoft プラットフォームで変更せずに作業できるアセンブリをビルドすることができます .NET 4 で初めて導入された機能です360 (ただし、現時点では、NuGet は Xbox のポータブル ライブラリのターゲットをサポートしていません)。  拡張することによって、[パッケージ規則](../create-packages/supporting-multiple-target-frameworks.md)framework のバージョンとプロファイルは、NuGet 2.1 ようになりましたポータブル ライブラリを複合フレームワークとプロファイルのターゲットを持つパッケージの作成を有効にして`lib`フォルダー。

たとえば、次のポータブル クラス ライブラリの使用可能なターゲット プラットフォームを検討してください。

![ポータブル ライブラリの作成ダイアログ](./media/releasenotes-21-plib.png)

ライブラリをビルドした後と、コマンド`nuget.exe pack MyPortableProject.csproj`実行は、新しいポータブル ライブラリのパッケージ フォルダーの構造を表示するには、生成された NuGet パッケージの内容が検査をします。

![ポータブル ライブラリ パッケージのレイアウト](./media/releasenotes-21-plib-layout.png)

ご覧のように、ポータブル ライブラリ フォルダーの名前規則のパターンに従います 'ポータブル {フレームワーク 1} + framework {n}' フレームワーク識別子が既存をに従って[フレームワークの名前とバージョンの規約](../reference/target-frameworks.md)します。 名前とバージョンの規則に 1 つの例外には、Windows Phone のために使用するフレームワークの識別子が記載されています。  このモニカーでは、フレームワーク名 'wp' (wp7、wp71 または wp8) を使用する必要があります。 ' Silverlight-wp7' を使用してなどのエラーが発生します。

このフォルダー構造から作成されたパッケージをインストールするときに NuGet が、フォルダー名で指定されている複数の対象に、フレームワークやプロファイルの規則を適用できますようになりました。  NuGet の照合ルールの背後にある、「特定性の低い」の「詳細」のターゲットが優先原則です。  意味、特定のプラットフォームを対象とするモニカーが常に優先移植可能なはどちらもプロジェクトと互換性がある場合。  さらに、複数の移植可能なターゲットがプロジェクトと互換性のある場合は、NuGet はサポートされているプラットフォームのセットは、パッケージを参照するプロジェクトに「最も近い」場所の 1 つを優先します。

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>ターゲットの Windows 8 および Windows Phone 8 プロジェクト

ポータブル ライブラリ プロジェクトを対象とするためのサポートを追加するだけでなく、NuGet 2.1 は Windows 8 のストアと Windows Phone 8 の両方のプロジェクトと Windows ストアとなる Windows Phone プロジェクトの新しい一般的なモニカーをいくつかの新しいフレームワークのモニカーを提供しますそれぞれのプラットフォームの将来のバージョン間での管理が容易です。

Windows 8 ストア アプリケーションでは、識別子は次のようです。

| 2.0 およびそれ以前の NuGet | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45、します。NETCore45 | Windows、windows 8 を win、win8 |

<br/>
Windows Phone プロジェクトでは、識別子は次のようです。

| Phone OS | 2.0 およびそれ以前の NuGet | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3-wp | wp、wp7、WindowsPhone、WindowsPhone7 |
| Windows Phone 7.5 (Mango) | silverlight4 wp71 | wp71、WindowsPhone71 |
| Windows Phone 8 | (サポートされていません) | wp8、WindowsPhone8 |

<br/>
上記の変更は、すべての NuGet 2.1 で完全にサポートするフレームワークの古い名前が引き続き。  今後は、新しい名前は、使用してください、それぞれのプラットフォームの将来のバージョン間でより安定したになります。 新しい名前は*いない*する 2.1 より前のバージョンの NuGet ではサポートされて、ただし、適切に計画スイッチを作成します。

## <a name="improved-search-in-package-manager-dialog"></a>パッケージ マネージャー ダイアログ ボックスで検索機能の向上

過去のいくつかのイテレーションにおける速度とパッケージの検索の妥当性を大幅に向上する NuGet ギャラリーに変更が導入されました。  ただし、これらの機能強化は、nuget.org の Web サイトに限定されていました。  NuGet 2.1 により、検索エクスペリエンスの機能の向上が NuGet パッケージ マネージャー ダイアログを利用します。  たとえば、Windows Azure キャッシュ プレビュー パッケージを必要とすることを想像してください。  このパッケージの適切な検索クエリには、"Azure Cache"可能性があります。  パッケージ マネージャー ダイアログの以前のバージョンで、目的のパッケージはさらには表示されない結果の最初のページ。  ただし、NuGet の 2.1 では、目的のパッケージに表示されます、検索結果の上部にあります。

![パッケージ マネージャー ダイアログの検索](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>パッケージを強制的に更新

パッケージの更新がない NuGet 2.1 では、前に NuGet をスキップは高いバージョン番号。  これには、ビルド CI シナリオ場合や、チームがない場合にパッケージ バージョンをビルドするたびに番号をインクリメントする場合は特に – 特定のシナリオの摩擦が導入されました。  目的の動作を強制的に更新に関係なくでした。  NuGet 2.1 では、'再インストール' フラグを使用してこれを説明します。  たとえば、以前のバージョンの NuGet になります次最新パッケージのバージョンがないパッケージを更新しようとしています。

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

かどうかに関係なく、パッケージを更新、再インストール フラグの新しいバージョンがあります。

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

もう 1 つのシナリオを再インストール フラグが便利では、フレームワークの再ターゲットのです。 (たとえば、.NET 4 から .NET 4.5)、プロジェクトのターゲット フレームワークを変更するときに更新プログラム パッケージの再インストール、プロジェクトにインストールされているすべての NuGet パッケージの適切なアセンブリへの参照を更新することができます。

## <a name="edit-package-sources-within-visual-studio"></a>Visual Studio 内でパッケージ ソースを編集します。

NuGet の以前のバージョンでは、削除および再パッケージ ソースを追加するために必要な Visual Studio のオプション ダイアログ内からパッケージ ソースを更新しています。  NuGet 2.1 では、構成用ユーザー インターフェイスのファースト クラスの関数として更新をサポートすることでこのワークフローが向上します。

![パッケージ マネージャーの構成 ダイアログ](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>バグ修正

NuGet 2.1 には、多くのバグ修正が含まれています。 作業の完全な一覧の項目で修正された NuGet 2.0 では、くださいビュー、[このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)します。
