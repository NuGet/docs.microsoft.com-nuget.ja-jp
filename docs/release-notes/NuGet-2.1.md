---
title: NuGet 2.1 リリース ノート
description: 既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 2.1 リリース ノートです。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3b7a000098a7362f4b1c2c4072c6cd1468baf9b5
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2018
ms.locfileid: "32044809"
---
# <a name="nuget-21-release-notes"></a>NuGet 2.1 リリース ノート

[NuGet 2.0 リリース ノート](../release-notes/nuget-2.0.md) | [NuGet 2.2 リリース ノート](../release-notes/nuget-2.2.md)

NuGet 2.1 は、2012 年 10 月 4 日にリリースされました。

## <a name="hierarchical-nugetconfig"></a>Nuget.Config の階層

NuGet 2.1 では、再帰的に探して、フォルダー構造のウォークを使用して NuGet 設定の制御をより柔軟`NuGet.Config`ファイルとし、見つかったすべてのファイルのセットから構成をビルドします。  たとえば、チームが、内部のパッケージ リポジトリの他の内部の依存関係の CI ビルドを持つシナリオを考えます。 個々 のプロジェクトのフォルダー構造は、次のようになります。

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

さらに、パッケージの復元がソリューションの有効な場合、次のフォルダーも存在されます。

    C:\myteam\solution1\.nuget

が使用できるようにすべてのプロジェクトのマシンで、中に、チームが機能するすべてのプロジェクトで使用できるチームの内部のパッケージ リポジトリを利用するには、新しい Nuget.Config ファイルを作成し、c:\myteam フォルダーに配置することおことができません。 方法がないを指定し、プロジェクトごとの [パッケージ] フォルダーです。

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

![親の nuget 構成からのパッケージ ソース](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` 次の順序でのファイルが検索されます。

1. `.nuget\Nuget.Config`
2. 再帰がルート プロジェクト フォルダーからウォークします。
3. グローバル`Nuget.Config`(`%appdata%\NuGet\Nuget.Config`)

この構成は、適用により、*の逆順*、上記の順序に基づくことを意味するには、グローバル Nuget.Config はするが最初に適用、後に、検出された Nuget.Config ファイルのルートからプロジェクトのフォルダーに、その後によって`.nuget\Nuget.Config`です。  これは、使用する場合に特に重要な`<clear/>`構成から一連の項目を削除する要素。

## <a name="specify-packages-folder-location"></a>'Packages' フォルダーの場所を指定します。

以前は、NuGet は、ソリューションのルート フォルダーの下に見つかった既知 'packages' フォルダーからソリューションのパッケージを管理するがします。  インストールされている NuGet パッケージである必要が多くのさまざまなソリューションを持っている開発チームの場合は、ファイル システム上のさまざまな場所にインストールされる同じパッケージになります。

NuGet 2.1 を使用して、[パッケージ] フォルダーの場所をより細かく制御を提供する、`repositoryPath`内の要素、`NuGet.Config`ファイル。  Nuget.Config の階層のサポートの前の例でのビルドでは、C:\myteam\ 共有、同じパッケージ フォルダーの下のすべてのプロジェクトがあるたいことを前提としています。  これを行うには、単に次のエントリを追加`c:\myteam\Nuget.Config`です。

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

この例では、共有で`Nuget.Config`ファイルの深さに関係なく C:\myteam の下に作成されるすべてのプロジェクトの共有のパッケージ フォルダーを指定します。 場合は、ソリューションのルートの下の既存のパッケージ フォルダーにある場合は、NuGet は、新しい場所にパッケージを配置前に削除する必要がありますに注意してください。

## <a name="support-for-portable-libraries"></a>ポータブル ライブラリのサポート

[ポータブル ライブラリ](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library)Silverlight は、Windows Phone およびでも Xbox に.net Framework のバージョンからのさまざまな Microsoft プラットフォームでの変更なしで使用できるようにアセンブリをビルドすることができます .NET 4 で初めて導入された機能です360 (ただし、現時点では、NuGet は、Xbox ポータブル ライブラリのターゲットをサポートしていません)。  拡張することによって、[規則をパッケージ化](../create-packages/supporting-multiple-target-frameworks.md)framework のバージョンとプロファイルは、NuGet 2.1 では、ポータブル ライブラリを複合フレームワークとプロファイルのターゲットを持つパッケージを作成することによって`lib`フォルダーです。

たとえば、次のポータブル クラス ライブラリの使用可能なターゲット プラットフォームを検討してください。

![ポータブル ライブラリの作成 ダイアログ ボックス](./media/releasenotes-21-plib.png)

ライブラリをビルドした後とコマンド`nuget.exe pack MyPortableProject.csproj`実行すると、新しい、移植可能なライブラリのパッケージ フォルダーの構造を表示するには、生成された NuGet パッケージの内容が検査をします。

![ポータブル ライブラリ パッケージのレイアウト](./media/releasenotes-21-plib-layout.png)

ご覧のように、ポータブル ライブラリ フォルダーの名前規則、パターンに従う 'ポータブル {フレームワーク 1} + framework {n}' フレームワーク識別子は、既存に従う、[フレームワークの名前とバージョン規則](../reference/target-frameworks.md)です。 Windows Phone を使用するフレームワーク識別子の名前とバージョンの規則に 1 つの例外はあります。  このモニカーは、フレームワーク名 'wp' (wp7、wp71 または wp8) を使用してください。 ' Silverlight-wp7' を使用してなどのエラーが発生します。

このフォルダー構造から作成されたパッケージをインストールするときに NuGet がフォルダー名で指定されている複数の対象にそのフレームワークとプロファイルのルールを適用できますようになりました。  NuGet の照合ルールの背後にある、「特定」のターゲットが優先される「汎用性」の原則です。  つまり、こと、特定のプラットフォームを対象とするモニカーは常によりも優先されるポータブルのどちらもプロジェクトに互換性がある場合。  さらに、複数のターゲットをポータブル プロジェクトと互換性のある場合は、NuGet をここでサポートされているプラットフォームの設定は、パッケージを参照しているプロジェクトに「最も近い」のいずれかを選びます。

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>ターゲットの Windows 8 および Windows Phone 8 プロジェクト

ポータブル ライブラリ プロジェクトを対象とするサポートを追加するだけでなく NuGet 2.1 では、新しいフレームワーク モニカー Windows 8 ストアおよび Windows Phone 8 の両方のプロジェクトと Windows ストアおよび Windows Phone プロジェクトとなる新しいによって一般的なモニカーそれぞれのプラットフォームの将来のバージョン間での管理が容易です。

Windows 8 ストア アプリケーションの場合は、識別子は次のようになります。

| NuGet 2.0 およびそれ以前 | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45、します。NETCore45 | Windows、windows 8、win、win8 |

<br/>
Windows Phone プロジェクトの場合は、識別子は次のようになります。

| 電話の OS | NuGet 2.0 およびそれ以前 | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3-wp | wp、wp7、WindowsPhone、WindowsPhone7 |
| Windows Phone 7.5 (Mango) | silverlight4 wp71 | wp71、WindowsPhone71 |
| Windows Phone 8 | (サポートされていません) | wp8、WindowsPhone8 |

<br/>
上記の変更は、すべての framework の古い名前は引き続き NuGet 2.1 によって完全にサポートします。  さらに、新しい名前を付けるなるのでより安定したそれぞれのプラットフォームの将来のバージョン間でします。 新しい名前は*いない*する NuGet の 2.1 以前のバージョンでサポートされている、ただし、適切に計画、スイッチを作成する際のです。

## <a name="improved-search-in-package-manager-dialog"></a>パッケージ マネージャー ダイアログ ボックスに検索機能の向上

過去のいくつかのイテレーションにおける速度とパッケージの検索の妥当性が大幅に向上 NuGet ギャラリーへの変更が導入されました。  ただし、これらの機能強化は、nuget.org の Web サイトに限られていました。  NuGet 2.1 では、エクスペリエンスの強化された検索を NuGet パッケージ マネージャー ダイアログ ボックスを通じて利用できます。  たとえば、Windows Azure キャッシュ プレビュー パッケージを検索するようにしたい想像してください。  このパッケージの適切な検索クエリには、"Azure Cache"可能性があります。  以前のバージョンのパッケージ マネージャー ダイアログでは、目的のパッケージもリストされません結果の最初のページにします。  ただし、NuGet 2.1 で目的のパッケージに表示されます、検索結果の上部にあります。

![パッケージ マネージャー ダイアログの検索](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>パッケージの更新を強制します。

NuGet NuGet 2.1 では、前に、not があったときに、パッケージの更新をスキップは指定された高いバージョン番号。  これには、ここで、チームを必要としないパッケージのバージョンをビルドするたびに数値をインクリメント ビルドまたは CI シナリオの場合は特に – 特定のシナリオの摩擦が導入されました。  目的の動作を強制的に更新に関係なくでした。  NuGet 2.1 は、これを 'を再インストール' フラグに対処します。  たとえば、以前のバージョンの NuGet 結果は、次にパッケージのより新しいバージョンがないパッケージを更新しようとするとき。

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

かどうかに関係なく、再インストール フラグで、パッケージが更新されて新しいバージョンが存在します。

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

もう 1 つのシナリオを再インストール フラグが便利では、フレームワークが再ターゲットのされます。 (たとえば、.NET 4 から .NET 4.5)、プロジェクトのターゲット フレームワークを変更するときに更新プログラム パッケージの再インストールするプロジェクトにインストールされているすべての NuGet パッケージの正しいアセンブリへの参照を更新できます。

## <a name="edit-package-sources-within-visual-studio"></a>Visual Studio 内でのパッケージ ソースを編集します。

NuGet の以前のバージョンで削除して、パッケージ ソースを再追加するために必要な Visual Studio のオプション ダイアログ内からパッケージ ソースを更新しています。  NuGet 2.1 では、構成のユーザー インターフェイスのファースト クラスの関数として更新をサポートすることによりこのワークフローが向上します。

![パッケージ マネージャーの構成 ダイアログ](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>バグ修正

NuGet 2.1 には、多くのバグ修正が含まれています。 作業の完全な一覧の項目で修正 NuGet 2.0 では、くださいビュー、[今回のリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)です。
