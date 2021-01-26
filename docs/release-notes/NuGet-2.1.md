---
title: NuGet 2.1 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.1 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777028"
---
# <a name="nuget-21-release-notes"></a>NuGet 2.1 リリースノート

[NuGet 2.0 リリースノート](../release-notes/nuget-2.0.md)  | [NuGet 2.2 リリースノート](../release-notes/nuget-2.2.md)

NuGet 2.1 は、2012年10月4日にリリースされました。

## <a name="hierarchical-nugetconfig"></a>階層 Nuget.Config

NuGet 2.1 では、ファイルを検索するフォルダー構造を再帰的に調べ、検出され `NuGet.Config` たすべてのファイルのセットから構成を構築することで、nuget 設定をより柔軟に制御できます。  例として、チームが他の内部依存関係の CI ビルドの内部パッケージリポジトリを持っている場合を考えてみます。 個々のプロジェクトのフォルダー構造は、次のようになります。

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

また、ソリューションに対してパッケージの復元が有効になっている場合は、次のフォルダーも存在します。

```
C:\myteam\solution1\.nuget
```

チームが作業するすべてのプロジェクトでチームの内部パッケージリポジトリを使用できるようにするために、コンピューター上のすべてのプロジェクトで使用できるようにするのではなく、新しい Nuget.Config ファイルを作成し、c:\myteam フォルダーに配置することができます。 プロジェクトごとにパッケージフォルダーを指定しすることはできません。

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

次に示すように、c:\myteam の下にある任意のフォルダーから ' nuget.exe sources ' コマンドを実行して、ソースが追加されたことを確認できます。

![親 nuget 構成からのパッケージソース](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` ファイルは、次の順序で検索されます。

1. `.nuget\Nuget.Config`
2. プロジェクトフォルダーからルートへの再帰的なウォーク
3. Global `Nuget.Config` ( `%appdata%\NuGet\Nuget.Config` )

これらの構成は *逆順* で適用されます。つまり、上記の順序に基づいて、グローバル Nuget.Config が最初に適用され、その後、[ルートからプロジェクト] フォルダーから検出された Nuget.Config ファイルの後にが続き `.nuget\Nuget.Config` ます。  これは、要素を使用して、 `<clear/>` 構成から一連の項目を削除する場合に特に重要です。

## <a name="specify-packages-folder-location"></a>' パッケージ ' フォルダーの場所を指定します

以前は、NuGet は、ソリューションルートフォルダーの下にある既知の ' パッケージ ' フォルダーからソリューションのパッケージを管理していました。  NuGet パッケージがインストールされているさまざまなソリューションを持つ開発チームにとっては、ファイルシステム上のさまざまな場所に同じパッケージがインストールされる可能性があります。

NuGet 2.1 では、ファイル内の要素を使用して、packages フォルダーの場所をより細かく制御 `repositoryPath` `NuGet.Config` できます。  前の階層 Nuget.Config サポートの例を基にして、C:\myteam\ 下のすべてのプロジェクトで同じ packages フォルダーを共有することを想定しています。  これを実現するには、次のエントリをに追加 `c:\myteam\Nuget.Config` します。

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

この例では、共有 `Nuget.Config` ファイルは、深さに関係なく、C:\myteam の下に作成されるすべてのプロジェクトの [共有パッケージ] フォルダーを指定します。 ソリューションルートの下に既存の packages フォルダーがある場合は、NuGet によって新しい場所にパッケージが配置される前に、削除する必要があることに注意してください。

## <a name="support-for-portable-libraries"></a>ポータブルライブラリのサポート

[ポータブルライブラリ](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) は、.net 4 で初めて導入された機能です。この機能を使用すると、さまざまな Microsoft プラットフォームでの変更なしで動作するアセンブリを構築できます。これにより、the.NET Framework のバージョンから Silverlight へ、および xbox 360 を Windows Phone ことができます (現時点では、NuGet は xbox ポータブルライブラリターゲットをサポートしません)。  フレームワークのバージョンとプロファイルの [パッケージ規則](../create-packages/supporting-multiple-target-frameworks.md) を拡張することで、NuGet 2.1 では、複合フレームワークとプロファイルターゲットフォルダーを持つパッケージを作成できるようになり、ポータブルライブラリがサポートされるようになりました `lib` 。

例として、次のポータブルクラスライブラリの使用可能なターゲットプラットフォームを考えてみます。

![ポータブルライブラリの作成ダイアログ](./media/releasenotes-21-plib.png)

ライブラリをビルドしてコマンドを実行すると `nuget.exe pack MyPortableProject.csproj` 、生成された NuGet パッケージの内容を調べることによって、新しいポータブルライブラリパッケージのフォルダー構造を確認できます。

![ポータブルライブラリパッケージのレイアウト](./media/releasenotes-21-plib-layout.png)

ご覧のように、ポータブルライブラリのフォルダー名の規則は、"ポータブル-{framework 1} + {framework n}" のパターンに従います。この場合、フレームワークの識別子は既存の [フレームワーク名とバージョンの規則](../reference/target-frameworks.md)に従います。 名前とバージョンの規則の1つの例外は、Windows Phone に使用されるフレームワーク識別子にあります。  このモニカーは、フレームワーク名 ' wp ' (wp7、wp71、または wp8) を使用する必要があります。 たとえば、' wp7 ' を使用すると、エラーが発生します。

このフォルダー構造から作成されたパッケージをインストールすると、NuGet によって、フォルダー名に指定されている複数のターゲットに対して、フレームワークとプロファイルルールが適用されるようになります。  NuGet の照合ルールの背後では、"より具体的な" ターゲットが "より具体的な" ものよりも優先されます。  つまり、特定のプラットフォームを対象とするモニカーは、プロジェクトと互換性がある場合は常に移植可能なものよりも優先されます。  さらに、複数のポータブルターゲットがプロジェクトと互換性がある場合、NuGet では、サポートされているプラットフォームのセットが、パッケージを参照しているプロジェクトに "最も近い" ものとして優先されます。

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Windows 8 および Windows Phone 8 プロジェクトを対象とする

NuGet 2.1 では、ポータブルライブラリプロジェクトを対象とするためのサポートを追加するだけでなく、Windows 8 ストアと Windows Phone 8 プロジェクトの新しいフレームワークモニカーに加えて、各プラットフォームの将来のバージョンで簡単に管理できる Windows ストアおよび Windows Phone プロジェクト用の新しい一般的なモニカーが提供されます。

Windows 8 ストアアプリケーションの場合、識別子は次のようになります。

| NuGet 2.0 以前 | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45, .NETCore45 | Windows、Windows8、win、win8 |

<br/>
Windows Phone プロジェクトの場合、識別子は次のようになります。

| 電話 OS | NuGet 2.0 以前 | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3-wp | wp、wp7、Appname.windowsphone、WindowsPhone7 |
| Windows Phone 7.5 (Mango) | silverlight4-wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (サポートされていません) | wp8、WindowsPhone8 |

<br/>
上記のすべての変更では、以前のフレームワーク名は引き続き NuGet 2.1 によって完全にサポートされます。  今後は、新しい名前を使用する必要があります。これらの名前は、各プラットフォームの将来のバージョンでより安定しています。 ただし、2.1 より前のバージョンの NuGet では、新しい名前はサポートされ *ません* 。そのため、スイッチを作成するタイミングに応じて計画を立ててください。

## <a name="improved-search-in-package-manager-dialog"></a>パッケージマネージャーダイアログの検索機能の向上

過去数回のイテレーションでは、パッケージ検索の速度と関連性を大幅に向上させる変更が NuGet ギャラリーに導入されました。  ただし、これらの機能強化は nuget.org の Web サイトに限定されていました。  Nuget 2.1 では、[NuGet パッケージマネージャー] ダイアログボックスで検索エクスペリエンスが向上しています。  例として、Windows Azure キャッシュプレビューパッケージを検索する場合を考えてみます。  このパッケージに対する適切な検索クエリは、"Azure Cache" にすることができます。  以前のバージョンの [パッケージマネージャー] ダイアログでは、必要なパッケージが結果の最初のページに表示されなくなります。  ただし、NuGet 2.1 では、必要なパッケージが検索結果の先頭に表示されるようになりました。

![パッケージマネージャーダイアログ検索](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>パッケージの更新を強制する

NuGet 2.1 より前では、バージョン番号が大きくない場合、NuGet はパッケージの更新をスキップします。  これにより、特に、チームが各ビルドでパッケージのバージョン番号をインクリメントしたくないビルドまたは CI シナリオの場合に、特定のシナリオに対する摩擦が発生しました。  必要な動作は、に関係なく更新を強制することでした。  NuGet 2.1 では、' 再インストール ' フラグを使用してこれに対処します。  たとえば、以前のバージョンの NuGet では、より新しいパッケージバージョンがないパッケージを更新しようとすると、次のようになります。

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

再インストールフラグを使用すると、新しいバージョンがあるかどうかに関係なくパッケージが更新されます。

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

再インストールフラグが役立つもう1つのシナリオとして、フレームワークの再ターゲット設定があります。 プロジェクトのターゲットフレームワーク (たとえば、.NET 4 から .NET 4.5) を変更すると、Update-Package 再インストールによって、プロジェクトにインストールされているすべての NuGet パッケージの正しいアセンブリへの参照を更新できます。

## <a name="edit-package-sources-within-visual-studio"></a>Visual Studio 内でパッケージソースを編集する

以前のバージョンの NuGet では、Visual Studio の [オプション] ダイアログ内からパッケージソースを更新するには、パッケージソースの削除と再追加が必要でした。  NuGet 2.1 は、構成ユーザーインターフェイスの最初のクラス関数として update をサポートすることで、このワークフローを改善します。

![パッケージマネージャーの構成ダイアログ](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>バグの修正

NuGet 2.1 には、多くのバグ修正が含まれています。 NuGet 2.0 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)を参照してください。
