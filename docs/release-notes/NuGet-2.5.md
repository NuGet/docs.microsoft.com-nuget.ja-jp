---
title: NuGet 2.5 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.5 のリリースノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940582d5173f5a53dcd04cf1258fc02a2439af4e
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825285"
---
# <a name="nuget-25-release-notes"></a>NuGet 2.5 リリースノート

Nuget [2.2.1 リリースノート](../release-notes/nuget-2.2.1.md) | [Nuget 2.6 リリースノート](../release-notes/nuget-2.6.md)

NuGet 2.5 は、2013年4月25日にリリースされました。 このリリースでは、バージョン2.3 と2.4 をスキップすることになりました。 これは、NuGet に関して私たちが経験した最大のリリースであり、 [160 の作業項目](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all)がリリースに含まれています。

## <a name="acknowledgements"></a>謝辞

NuGet 2.5 への重要な貢献について、次の外部の共同作成者に感謝いたします。

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) -モノ Android、monotouch.dialog、およびモノ mac を既知のターゲットフレームワーク識別子の一覧に追加します。
2. [Andres Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -大文字と小文字を区別する OS の `NuGet.targets` のスペルを修正する
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - ソリューションを Mono で構築します。
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Mono で失敗する単体テストを修正します。
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe pack コマンドはプロパティを MSBuild に反映しません
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) -書式設定を保持するために変更された XML 処理コード。
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - ビルド .cmd を成功させるために、認識された単語をカスタム辞書に追加しました。
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - ローカライズされたおよびでの実行時に単体テストを修正する
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - パッケージを展開する
10. 最大活用[e Bridou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) -パッキング時にプロジェクトの依存関係を処理する
11. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991)、 [#3164](https://nuget.codeplex.com/workitem/3164) 、パッケージソースの資格情報を nuget に保存するときにクリアテキストのパスワードをサポートします。 cofig
12. [James manning](http://www.codeplex.com/site/users/view/jmanning) [@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190)、 [#3191](http://nuget.codeplex.com/workitem/3191) -パッケージのヘルプの説明を修正します。

また、次の各担当者は、最終リリースの前に承認および修正された NuGet 2.5 Beta/RC でバグを見つけることにも感謝します。

1. [Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) -MSTest が最新 NuGet 2.4 および2.5 ビルドで破損する

## <a name="notable-features-in-the-release"></a>リリースの注目すべき機能

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>既に存在するコンテンツファイルをユーザーが上書きできるようにする

常に要求される機能の1つは、NuGet パッケージに含まれている場合に、既にディスク上に存在するコンテンツファイルを上書きする機能です。 NuGet 2.5 以降では、これらの競合が特定され、ファイルを上書きするように求められますが、以前はこれらのファイルは常にスキップされていました。

![コンテンツファイルの上書き](./media/NuGet-2.5/overwrite-file.png)

' nuget.exe update ' と ' FileConflictAction ' の両方に、コマンドラインシナリオの既定値を設定するための新しいオプション '-' が追加されました。

ターゲットプロジェクトにパッケージのファイルが既に存在する場合の既定のアクションを設定します。 常にファイルを上書きするには、[上書き] に設定します。 ファイルをスキップするには、[無視] に設定します。 指定しない場合は、競合しているファイルごとにプロンプトが表示されます。

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>MSBuild ターゲットと props ファイルの自動インポート

NuGet パッケージの最上位レベルで、新しい従来のフォルダーが作成されています。  `\lib`、`\content`、`\tools`のピアとして、パッケージに `\build` フォルダーを含めることができるようになりました。  このフォルダーには、固定名、`{packageid}.targets`、または `{packageid}.props`を含む2つのファイルを配置できます。 これらの2つのファイルは、他のフォルダーと同じように、`build` またはフレームワーク固有のフォルダーの下に直接配置できます。 最も一致するフレームワークフォルダーを選択するルールは、これらのフォルダーとまったく同じです。

NuGet が \ ビルドファイルを含むパッケージをインストールすると、`.targets` ファイルと `.props` ファイルを指す MSBuild `<Import>` 要素がプロジェクトファイルに追加されます。 `.props` ファイルが上部に追加され、`.targets` ファイルが一番下に追加されます。

### <a name="specify-different-references-per-platform-using-references-element"></a>`<References/>` 要素を使用してプラットフォームごとに異なる参照を指定する

`.nuspec` ファイルでは、2.5 より前のユーザーは、すべてのフレームワークに追加される参照ファイルのみを指定できます。 2\.5 のこの新機能により、ユーザーはサポートされている各プラットフォームの `<reference/>` 要素を作成できます。次に例を示します。

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

NuGet が `.nuspec` ファイルに基づいてプロジェクトへの参照を追加する方法のフローを次に示します。

1. ターゲットフレームワークに適した `lib` フォルダーを探し、そのフォルダーからアセンブリの一覧を取得します。
1. ターゲットフレームワークに適した参照グループを個別に検索し、そのグループからアセンブリの一覧を取得します。 ターゲットフレームワークが指定されていない参照グループがフォールバックグループです。
1. 2つのリストの交差部分を検索し、それを追加する参照として使用します。

この新機能では、パッケージの作成者が参照機能を使用して、複数の `lib` フォルダー内で重複するアセンブリを実行する必要がある場合に、アセンブリのサブセットを異なるフレームワークに適用できます。

注: 現在、この機能を使用するには、nuget.exe パックを使用する必要があります。NuGet Package Explorer ではまだサポートされていません。

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>すべてのパッケージを一度に更新できるように、すべてのボタンを更新します

すべてのパッケージを更新するための "パッケージの更新" PowerShell コマンドレットについて多くの知識を持っています。UI でも簡単に実行できるようになりました。

この機能を試すには、次のようにします。

1. 新しい ASP.NET MVC アプリケーションを作成する
1. [NuGet パッケージの管理] ダイアログを起動します。
1. [更新プログラム] を選択します。
1. [すべて更新] ボタンをクリックします。

![ダイアログの [すべて更新] ボタン](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Nuget Pack のプロジェクト参照サポートの向上

現在、nuget.exe pack コマンドは、次の規則で参照されるプロジェクトを処理します。

1. 参照先のプロジェクトに対応する `.nuspec` ファイルがある場合 (`proj1.csproj`と同じフォルダーに `proj1.nuspec` という名前のファイルが存在する場合など)、このプロジェクトは、`.nuspec` ファイルから読み取った id とバージョンを使用して、パッケージへの依存関係として追加されます。
1. それ以外の場合は、参照されるプロジェクトのファイルがパッケージにバンドルされます。 その後、このプロジェクトで参照されるプロジェクトは、sames 規則を再帰的に使用して処理されます。
1. すべての DLL、`.pdb`、`.exe` ファイルが追加されます。
1. その他のすべてのコンテンツファイルが追加されます。
1. すべての依存関係がマージされます。

これにより、`.nuspec` ファイルがある場合は参照先のプロジェクトを依存関係として扱うことができます。それ以外の場合は、パッケージの一部になります。

詳細については、 [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>' 最小 NuGet バージョン ' プロパティをパッケージに追加します

"MinClientVersion" という名前の新しいメタデータ属性は、パッケージを使用するために必要な最小限の NuGet クライアントバージョンを示すようになりました。

この機能を使用すると、パッケージの作成者は、特定のバージョンの NuGet の後でのみパッケージを使用するように指定できます。 NuGet 2.5 の後に新しい `.nuspec` 機能が追加されると、パッケージは最小限の NuGet バージョンを要求できるようになります。

```xml
<metadata minClientVersion="2.6">
```

ユーザーに NuGet 2.5 がインストールされており、パッケージが "2.6 が必要" と識別されている場合は、パッケージがインストールできないことを示す視覚的な手掛かりがユーザーに与えられます。 その後、ユーザーは NuGet のバージョンを更新するように指示されます。

これにより、パッケージのインストールが開始されるが、認識できないスキーマバージョンが識別されたことを示すエラーが発生した場合に、機能が向上します。

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>パッケージのインストール中に、依存関係が不必要に更新されなくなりました

NuGet 2.5 より前では、プロジェクトに既にインストールされているパッケージに依存するパッケージがインストールされている場合、既存のバージョンが依存関係を満たしていても、新しいインストールの一部として依存関係が更新されます。

NuGet 2.5 以降では、依存関係のバージョンが既に満たされている場合、他のパッケージのインストール中に依存関係は更新されません。

**シナリオは次のとおりです。**

1. ソースリポジトリには、バージョン1.0.0 と1.0.2 のパッケージ B が含まれています。 また、B (> = 1.0.0) に依存するパッケージ A も含まれています。
1. 現在のプロジェクトにパッケージ B バージョン1.0.0 が既にインストールされているとします。 ここで、パッケージ A をインストールします。

**NuGet 2.2 以前:**

* パッケージ A をインストールすると、既存のバージョン1.0.0 が既に依存関係バージョンの制約 (> = 1.0.0) を満たしていても、NuGet は B を自動的に1.0.2 に更新します。

**NuGet 2.5 以降:**

* 既存のバージョン1.0.0 が依存関係バージョンの制約を満たしていることが検出されるため、NuGet は B を更新しなくなります。

この変更の背景の詳細については、関連する[ディスカッションスレッド](http://nuget.codeplex.com/discussions/436712)だけでなく、詳細な[作業項目](http://nuget.codeplex.com/workitem/1681)も参照してください。

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>nuget.exe は、詳細な詳細情報を含む http 要求を出力します。

Nuget.exe のトラブルシューティングを行う場合や、操作中に HTTP 要求が行われた場合は、'-詳細詳細 ' スイッチによって行われたすべての HTTP 要求が出力されるようになりました。

![Nuget.exe からの HTTP 出力](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>nuget.exe push で UNC およびフォルダーソースがサポートされるようになりました

NuGet 2.5 より前では、UNC パスまたはローカルフォルダーに基づいてパッケージソースに ' nuget.exe push ' を実行しようとすると、プッシュは失敗します。 最近追加された階層構造の構成機能により、nuget.exe は UNC/フォルダーソースまたは HTTP ベースの NuGet ギャラリーをターゲットにする必要がありました。

Nuget 2.5 以降では、nuget.exe が UNC/フォルダーソースを識別する場合、ソースへのファイルのコピーが実行されます。

次のコマンドが機能するようになります。

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>nuget.exe は、明示的に指定された構成ファイルをサポートします。

構成にアクセスする nuget.exe コマンド (' spec ' と ' pack ' を除く) は、新しい '-ConfigFile ' オプションをサポートするようになりました。このオプションを指定すると、既定の構成ファイルの代わりに、特定の構成ファイルが強制的に使用されます。

例:

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>ネイティブプロジェクトのサポート

NuGet 2.5 では、Visual Studio のネイティブプロジェクトで NuGet ツールを使用できるようになりました。 ほとんどのネイティブパッケージは、 [Coapp プロジェクト](http://coapp.org)によって作成されたツールを使用して、上記の MSBuild インポート機能を利用することを想定しています。 詳細については、coapp.org web サイトの[ツールに関する詳細](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html)を参照してください。

パッケージがネイティブプロジェクトにインストールされている場合、パッケージでは、[ビルド]、[コンテンツ]、[ツール] の順に移動して、パッケージにファイルを含めることができます。  \`lib ' フォルダーはネイティブプロジェクトには使用されません。
