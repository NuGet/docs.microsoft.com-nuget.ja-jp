---
title: NuGet 2.5 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 2.5 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 29d0b33714a574281680e110b967269699afbaf1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550484"
---
# <a name="nuget-25-release-notes"></a>NuGet 2.5 リリース ノート

[NuGet 2.2.1 リリース ノート](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 リリース ノート](../release-notes/nuget-2.6.md)

NuGet 2.5 は、2013 年 4 月 25 日にリリースされました。 このリリースがそれほど、バージョン 2.3、2.4 をスキップする感じました。 これまで、これは、最大のリリースで、NuGet のあった経由で[160 作業項目](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all)のリリースでします。

## <a name="acknowledgements"></a>謝辞

今回は外部の共同作成者、次の NuGet 2.5 に、多大な貢献に感謝します。

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) -追加 MonoAndroid、MonoTouch、および既知のターゲット フレームワーク識別子の一覧に MonoMac します。
2. [Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -のスペルの修正`NuGet.targets`大文字の os
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Mono 上でビルドするソリューションを作成します。
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Mono で失敗した単体テストを修正します。
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe パック コマンドに msbuild プロパティが伝達されません
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) - 変更 XML 処理コードを書式設定を保持します。
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - 認識された単語を成功させる build.cmd を許可するカスタム辞書に追加されます。
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - ローカライズされた VS で実行する場合は、単体テストを修正します。
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - PackageService から抽出されたインターフェイス
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936)にパックするときに、プロジェクトの依存関係を処理
11. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991)、 [#3164](https://nuget.codeplex.com/workitem/3164) -サポート クリア テキスト パスワード nuget.cofig ファイルにパッケージ ソースの資格情報を格納する場合
12. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190)、 [#3191](http://nuget.codeplex.com/workitem/3191) -修正 Get-package ヘルプの説明

次のユーザーを魅力的に NuGet 2.5 Beta/RC が承認され、最終リリースの前に修正されたバグを見つけるため。

1. [Tony 壁](https://www.codeplex.com/site/users/view/CodeChief)([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) - 最新の NuGet 2.4、2.5 ビルドで MSTest

## <a name="notable-features-in-the-release"></a>リリースで注目すべき機能

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>ユーザーが既に存在するコンテンツ ファイルの上書きを許可します。

NuGet パッケージに含まれるときにディスクに既に存在するコンテンツのファイルを上書きする機能をすべての時間の最も多く要求された機能の 1 つされました。 NuGet 2.5 以降では、これらの競合が識別され、これらのファイルがスキップされた常に以前は、ファイルを上書きするように求められます。

![コンテンツ ファイルを上書きします。](./media/NuGet-2.5/overwrite-file.png)

'nuget.exe update' および 'Install-package' 両方が、新しいオプション '-FileConflictAction' コマンド ライン シナリオのいくつかの既定値を設定します。

対象のプロジェクトにパッケージからのファイルが既に存在する場合は、既定のアクションを設定します。 「上書き」に設定すると、常にファイルを上書きします。 ファイルをスキップする '無視' に設定します。 指定しない場合、競合するファイルごとに求められます。

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>MSBuild ターゲットおよびプロパティ ファイルの自動インポート

NuGet パッケージの最上位レベルでは、従来の新しいフォルダーが用意されています。  ピアとして`\lib`、 `\content`、および`\tools`、できるようになりました、`\build`パッケージ内のフォルダー。  このフォルダーの下には、固定の名前を持つ 2 つのファイルを配置することができます`{packageid}.targets`または`{packageid}.props`します。 これら 2 つのファイルがあるか直接`build`またはその他のフォルダーと同じようフレームワークに固有のフォルダーの下。 一致する最適なフレームワーク フォルダーを選択するための規則ではものと同じです。

NuGet は \build ファイルでパッケージをインストールと、は、MSBuild が追加されます`<Import>`を指すプロジェクト ファイル内の要素、`.targets`と`.props`ファイル。 `.props`は、上部にあるファイルが追加された、`.targets`ファイル下部に追加されます。

### <a name="specify-different-references-per-platform-using-references-element"></a>使用するプラットフォームごとに異なる参照を指定`<References/>`要素

2.5 では前に、の`.nuspec`ファイル、ユーザーはすべてのフレームワーク用に追加する、参照ファイルを指定してできますのみです。 2.5 ではこの新しい機能では、ユーザーを作成できるので、`<reference/>`要素ごとの例では、サポートされているプラットフォーム。

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

NuGet がに基づいてプロジェクトへの参照を追加する方法のフローを次に示します、`.nuspec`ファイル。

1. 検索、`lib`フォルダー ターゲット フレームワークの適切なは、そのフォルダーからアセンブリの一覧を取得します。
1. 個別にターゲット フレームワークの適切な参照グループを検索し、そのグループからのアセンブリの一覧を取得します。 ターゲット フレームワークを指定せず、参照グループは、フォールバックのグループです。
1. 2 つのリストの積集合を検索し、追加する参照として使用します。

参照機能を使用して、それ以外の場合、複数の重複するアセンブリを実行するために必要なはときに、さまざまなフレームワークをアセンブリのサブセットを適用するパッケージの作成者により、この新しい機能`lib`フォルダー。

メモ: する必要があります現在を使用する nuget.exe パック。 この機能を使用するにはNuGet パッケージ エクスプ ローラーはまだサポートしていません。

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>すべてのパッケージを一度に更新できるようにするすべてのボタンを更新します。

皆さんの多くはすべてのパッケージ; を更新する「更新プログラム パッケージ」PowerShell コマンドレットについて知っておくこれは、UI もで実行する簡単な方法があるようになりました。

この機能を試す。

1. 新しい ASP.NET MVC アプリケーションを作成します。
1. NuGet パッケージの管理 ダイアログを起動します。
1. 「更新プログラム」を選択します。
1. [すべて更新] ボタンをクリックします

![更新 ダイアログ ボックスすべて ボタン](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Nuget.exe パックの強化されたプロジェクト参照のサポート

Nuget.exe パック コマンド プロセスが、次の規則を使用したプロジェクトを参照しているようになりました。

1. 対応する参照先のプロジェクトに含まれる場合`.nuspec`ファイルなどという名前のファイルがある`proj1.nuspec`と同じフォルダーに`proj1.csproj`、このプロジェクトは、id を使用して、パッケージに依存関係として追加は、およびバージョンを読み取ったり、`.nuspec`ファイル。
1. それ以外の場合、参照先のプロジェクトのファイルがパッケージにバンドルされています。 このプロジェクトで参照されているプロジェクトは、そのままルールを再帰的を使用して処理されます。
1. すべての DLL `.pdb`、および`.exe`ファイルが追加されます。
1. その他のすべてのコンテンツ ファイルが追加されます。
1. すべての依存関係がマージされます。

これにより、参照先のプロジェクトがある場合は、依存関係として扱う場合に、`.nuspec`ファイルで、それ以外の場合、パッケージの一部となります。

詳細についてはこちら: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>パッケージに ' 最小 NuGet の Version' プロパティを追加します。

'MinClientVersion' と呼ばれる新しいメタデータ属性は、パッケージを使用するために必要な最小の NuGet クライアント バージョンを示すようになりましたことができます。

この機能には、特定のバージョンの NuGet の後にのみ、パッケージが動作するかを指定するパッケージの作成者が役立ちます。 新しい`.nuspec`パッケージは NuGet の最小バージョンを要求できる NuGet 2.5 では、後に機能が追加されました。

```xml
<metadata minClientVersion="2.6">
```

ユーザーがインストールされている NuGet 2.5、2.6 を必要とすると、パッケージが識別される場合は、パッケージがインストールできないようにすることを示す視覚的な手掛かりを与えられます。 ユーザーは、NuGet のバージョンを更新する、ガイド付きされます。

これは、パッケージのインストールが失敗するように、認識できないスキーマ バージョンの識別を示す開始位置、既存のエクスペリエンスに向上します。

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>依存関係がパッケージのインストール中に更新される不必要に不要になった

NuGet 2.5 では、前に、プロジェクトに既にインストールされているパッケージに依存するパッケージのインストール時に、依存関係が更新されます、新しいインストールの一部として既存のバージョンには、依存関係が満たされている場合でも。

以降、NuGet 2.5 では依存関係のバージョンが既に満たされている場合、依存関係は更新されません他のパッケージのインストール中にします。

**シナリオ:**

1. ソース リポジトリには、バージョン 1.0.0 と 1.0.2 でパッケージ B が含まれています。 B に依存しているパッケージ A も含まれています (> = 1.0.0)。
1. 現在のプロジェクトが既にパッケージ B のバージョン 1.0.0 がインストールされていることを想定しています。 A. のパッケージをインストールするようになりました

**Nuget 2.2 と古い。**

* パッケージ A をインストールするときに NuGet は自動更新 B 1.0.2、既存のバージョン 1.0.0 が既にには依存関係のバージョンの制約を満たす場合でも > 1.0.0 を = です。

**Nuget 2.5 以降。**

* NuGet、既存のバージョン 1.0.0 が依存関係のバージョン制約を満たすことが検出されたため、B が不要になった更新されます。

この変更の詳細については、読み取り、詳細な[作業項目](http://nuget.codeplex.com/workitem/1681)と関連する[ディスカッション スレッド](http://nuget.codeplex.com/discussions/436712)します。

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>nuget.exe 詳細な http 要求を出力します。

Nuget.exe のトラブルシューティングを行うか、単どのような HTTP 要求が、処理中に行われた興味がある、'-詳細度の詳細な ' スイッチが行われたすべての HTTP 要求を出力するようになりました。

![Nuget.exe からの HTTP 出力](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>nuget.exe プッシュでは、UNC およびフォルダーのソースをサポートします。

NuGet 2.5 では、前に、UNC パスまたはローカルのフォルダーに基づくパッケージのソースに 'nuget.exe push' を実行しようとしました、プッシュは失敗します。 階層的な構成を最近追加された機能を使用には、UNC/フォルダーのソース、または HTTP ベースの NuGet ギャラリーのいずれかを指定する必要する nuget.exe の一般的なの操作になる必要があります。

NuGet 2.5 以降 nuget.exe UNC/フォルダーのソースを指定する場合、ソース ファイルのコピーが実行されます。

次のコマンドは機能ようになりました。

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>nuget.exe が明示的に指定された構成ファイルをサポートしています

('仕様' と"pack"を除くすべて) の構成を今すぐアクセス nuget.exe コマンド サポートを新しい '-ConfigFile' オプションは、%appdata%\nuget\nuget.config で既定の構成ファイルの代わりに使用される固有の構成ファイルを強制します。

例:

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>ネイティブ プロジェクトのサポート

NuGet 2.5 では、NuGet ツールは、Visual Studio でのネイティブ プロジェクトで使用できるようになりました。 予定最もネイティブ パッケージは、MSBuild インポート機能を利用して作成ツールを使用して、 [CoApp プロジェクト](http://coapp.org)します。 詳細については、読み取る[ツールに関する詳細](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html)coapp.org web サイト。

"Native"のターゲット フレームワークの名前には、ネイティブ プロジェクトに、パッケージをインストールするときに、\build、\content、および \tools にファイルを含めるパッケージが導入されました。  \`Lib' ネイティブ プロジェクトのフォルダーは使用されません。
