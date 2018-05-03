---
title: NuGet 2.5 のリリース ノート
description: 既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 2.5 のリリース ノートします。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: accea5033e44927259537b5047a4a821babc6146
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-25-release-notes"></a>NuGet 2.5 のリリース ノート

[NuGet 2.2.1 リリース ノート](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 リリース ノート](../release-notes/nuget-2.6.md)

NuGet 2.5 は、2013 年 4 月 25 日にリリースされました。 このリリースが大きすぎて、バージョン 2.3 および 2.4 をスキップする感じました。 までに、これは、最大のリリースと、NuGet のきました経由で[160 作業項目](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all)リリースします。

## <a name="acknowledgements"></a>謝辞

NuGet 2.5 に大幅な貢献の次の外部共同作成者いただき、ありがとうたいと思います。

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) -追加 MonoAndroid、MonoTouch、および既知のターゲット フレームワーク識別子の一覧に MonoMac です。
2. [Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -のスペル修正`NuGet.targets`大文字小文字を区別 os
3. [David ファウラー](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - ソリューションの Mono でビルドを確認します。
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - モノラルで失敗する単体テストを修正します。
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe パック コマンドは、msbuild プロパティを反映しません
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) - 変更された XML 処理コードの書式設定を保持するためにします。
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Build.cmd を正常に使用できるようにカスタム辞書に認識された単語を追加します。
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - ローカライズされた VS で実行されている場合は、単体テストを修正します。
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - PackageService から抽出されたインターフェイス
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) -梱包する場合のプロジェクトの依存関係の処理
11. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991)、 [#3164](https://nuget.codeplex.com/workitem/3164) -サポート クリア テキスト パスワード nuget.cofig ファイルにパッケージ ソースの資格情報を格納する場合
12. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190)、 [#3191](http://nuget.codeplex.com/workitem/3191) -修正 Get-package ヘルプの説明

次の個人用を認めるように NuGet 2.5 ベータ/RC が承認され、最終リリース前に修正されたバグを見つけるため。

1. [Tony 壁](https://www.codeplex.com/site/users/view/CodeChief)([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) - MSTest 最新 NuGet 2.4 と 2.5 ビルド分割

## <a name="notable-features-in-the-release"></a>リリースで注目に値する機能

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>ユーザーが既に存在するコンテンツのファイルの上書きを許可します。

NuGet パッケージに含まれるときにディスクに既に存在するコンテンツのファイルを上書きする権限をすべての時間の多かった機能の 1 つされました。 NuGet 2.5 以降では、これらの競合識別され、これらのファイルがスキップされた常に以前は、ファイルを上書きするように求められます。

![コンテンツ ファイルを上書き](./media/NuGet-2.5/overwrite-file.png)

'nuget.exe update' および 'Install-package' これで、新しいオプションがあります両方 '-FileConflictAction' コマンド ライン シナリオのいくつかの既定値に設定します。

対象のプロジェクトにパッケージからファイルが既に存在する場合は、既定のアクションを設定します。 常にファイルを上書きする「上書き」に設定します。 'Ignore' に設定すると、ファイルをスキップします。 指定しない場合、競合している各ファイルが求められます。

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>MSBuild のターゲットと props ファイルの自動インポート

NuGet パッケージの最上位レベルには、従来の新しいフォルダーが用意されています。  ピアとして`\lib`、 `\content`、および`\tools`、するできるようになりました、`\build`パッケージ内のフォルダーです。  このフォルダーの下には、固定名は、2 つのファイルを配置することができます`{packageid}.targets`または`{packageid}.props`です。 これら 2 つのファイルがあるか直接`build`またはフレームワーク固有のフォルダーに、他のフォルダーと同じようにします。 最も一致するフレームワーク フォルダーを選択するためのルールは、ものと同じではまったくです。

NuGet \build ファイルとパッケージのインストール時に、MSBuild が追加`<Import>`要素を指すプロジェクト ファイルで、`.targets`と`.props`ファイル。 `.props`一方、上部にあるファイルが追加、`.targets`ファイルが下部に追加します。

### <a name="specify-different-references-per-platform-using-references-element"></a>プラットフォームごとの別の参照を指定`<References/>`要素

2.5 では前に、の`.nuspec`ファイル、ユーザーがすべてのフレームワーク用に追加する、参照ファイルを指定できますのみです。 これで、この新しい機能により 2.5 では、ユーザーを作成できます、`<reference/>`例については、サポートされているプラットフォームごとの要素。

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

ここでは、NuGet がに基づいてプロジェクトへの参照を追加する方法のフロー、`.nuspec`ファイル。

1. 検索、`lib`フォルダー ターゲット フレームワークの適切なは、そのフォルダーからアセンブリの一覧を取得します。
1. 別に、ターゲット フレームワークを適切な参照グループを検索し、そのグループからのアセンブリの一覧を取得します。 指定されたターゲット フレームワークなしの参照グループは、フォールバックのグループです。
1. 2 つのリストの積集合を検索し、追加する参照として使用します。

この新機能によって、それ以外の場合は複数の重複するアセンブリを実行する必要がある場合は、さまざまなフレームワークにアセンブリのサブセットを適用する参照機能を使用するパッケージ作成者`lib`フォルダーです。

メモ: する必要があります現在を使用する nuget.exe パック。 この機能を使用するにはNuGet パッケージ エクスプ ローラーはまだサポートしていません。

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>すべてのパッケージを一度に更新を許可するすべてのボタンを更新します。

多くは次のトピック、「更新プログラム パッケージ」PowerShell コマンドレットを更新するすべてのパッケージです。も、UI を使用する簡単な方法があるようになりました。

この機能を試してみてください。

1. 新しい ASP.NET MVC アプリケーションを作成します。
1. NuGet パッケージの管理 ダイアログを起動します。
1. '更新' を選択します。
1. [すべて更新] ボタンをクリックします。

![ダイアログ ボックスで [すべて] ボタンを更新します。](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Nuget.exe パックの強化されたプロジェクト参照のサポート

Nuget.exe パック コマンド、プロセスが次の規則にプロジェクトを参照しているようになりました。

1. 場合は、参照先プロジェクトに対応する`.nuspec`ファイル、たとえばという名前のファイルがある`proj1.nuspec`と同じフォルダーに`proj1.csproj`し、このプロジェクトが追加の依存関係として、id を使用して、パッケージ、およびバージョンからの読み取り、`.nuspec`ファイル。
1. それ以外の場合、参照先のプロジェクトのファイルは、パッケージにまとめられます。 このプロジェクトによって参照されるプロジェクトは、sames ルールを再帰的を使用して処理されます。
1. すべての DLL `.pdb`、および`.exe`ファイルが追加されます。
1. その他のすべてのコンテンツ ファイルが追加されます。
1. すべての依存関係がマージされます。

これにより、参照先のプロジェクトがある場合、依存関係として扱われる、`.nuspec`ファイルで、それ以外の場合、パッケージの一部になります。

詳細については、ここは: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>パッケージに '最低限の NuGet バージョン' プロパティを追加します。

という新しいメタデータの属性 'minClientVersion' は、パッケージを使用するために必要な最小の NuGet クライアント バージョンを示すようになりましたことができます。

この機能を使用すると、パッケージの作成者を特定のバージョンの NuGet の後にパッケージが動作するを指定します。 新しい`.nuspec`機能後に追加された NuGet 2.5 では、パッケージは NuGet の最小バージョンを要求することができます。

```xml
<metadata minClientVersion="2.6">
```

ユーザーがインストールされている NuGet 2.5 2.6 を必要とすると、パッケージが識別される場合は、パッケージをインストール可能にすることはできませんを示すユーザーへ視覚的な手掛かりが与えられます。 ユーザーは、NuGet のバージョンを更新するガイドします。

これは、パッケージをインストールし、失敗する可能性が認識されていないスキーマ バージョンが識別されたことを示すに開始する位置を示す既存のエクスペリエンスに向上します。

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>依存関係がパッケージのインストール中に更新されなく不必要に

NuGet 2.5 では、前に、プロジェクトに既にインストールされているパッケージに依存していたパッケージのインストール時に、依存関係が更新されます、新しいインストールの一部として、既存のバージョンには、依存関係が満たされる場合でもです。

NuGet 2.5 から始めて、依存関係のバージョンを既に満たしている場合、依存関係は更新されません他のパッケージのインストール中にします。

**シナリオ:**

1. ソース リポジトリには、バージョン 1.0.0 1.0.2 パッケージ B が含まれています。 パッケージ A が B に依存しているも含まれています (> = 1.0.0)。
1. 現在のプロジェクトは既にパッケージ B のバージョン 1.0.0 がインストールされていることを想定しています。 A. のパッケージをインストールするようになりました

**NuGet 2.2 と古い: で**

* パッケージ A をインストールするときに NuGet が自動更新 B 1.0.2、既存のバージョン 1.0.0 が既にこれは依存関係のバージョンの制約を満たす場合でも > 1.0.0 を = です。

**NuGet 2.5 と新しい: で**

* 既存のバージョン 1.0.0 が依存関係のバージョンの制約を満たすことが検出されたために、NuGet は B を不要になった更新されます。

この変更の詳細については、読み取り、詳細な[作業項目](http://nuget.codeplex.com/workitem/1681)、関連するだけでなく[ディスカッション スレッド](http://nuget.codeplex.com/discussions/436712)です。

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>nuget.exe 詳細な詳細レベルでの http 要求を出力します。

Nuget.exe のトラブルシューティングを行うか、単興味があるどの HTTP 要求が行われる操作中に、'-詳細な詳細度 ' スイッチが行われるすべての HTTP 要求を出力するようになりました。

![Nuget.exe から HTTP 出力](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>nuget.exe プッシュに今すぐ UNC とフォルダーのソースがサポートしています

NuGet 2.5 では、前に、UNC パスまたはローカル フォルダーに基づくパッケージ ソース 'nuget.exe プッシュ' を実行する試行する場合は、プッシュは失敗します。 階層構造の構成を最近追加された機能を使用して、UNC/フォルダーのソース、または HTTP ベース NuGet ギャラリーのいずれかを対象とする必要がある nuget.exe の一般的なになる必要があります。

NuGet 2.5 から始めて nuget.exe UNC/フォルダーのソースを識別する場合、ソース ファイルのコピーを実行します。

次のコマンドが動作します。

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>nuget.exe が明示的に指定された構成ファイルをサポートしています

('仕様' と 'pack' を除くすべて) の構成を今すぐアクセスする nuget.exe のコマンドは、新しいサポート '-ConfigFile' オプションは、%appdata%\nuget\nuget.config で既定の構成ファイルの代わりに使用する固有の構成ファイルを強制します。

例:

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>ネイティブ プロジェクトのサポート

NuGet 2.5 で NuGet ツールは Visual Studio でのネイティブ プロジェクトで使用できるようになりました。 予定最もネイティブ パッケージは、上記の MSBuild のインポート機能を利用して作成ツールを使用して、 [CoApp プロジェクト](http://coapp.org)です。 詳細については、「[詳細についてはツール、](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) coapp.org web サイトです。

"Native"のターゲット フレームワークの名前には、ファイルを含める \build、\content、および \tools でネイティブ プロジェクトにパッケージがインストールされているときにパッケージが導入されました。  \`Lib' フォルダーは、ネイティブ プロジェクトには使用されません。
