---
title: "NuGet 1.5 のリリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 1.5 のリリース ノートします。"
keywords: "NuGet 1.5 のリリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 261cfbbd262bad28f142b0c3dff8a541641d9fda
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-15-release-notes"></a>NuGet 1.5 のリリース ノート

[NuGet 1.4 のリリース ノート](../release-notes/nuget-1.4.md) | [NuGet 1.6 リリース ノート](../release-notes/nuget-1.6.md)

NuGet 1.5 は、2011 年 8 月 30 日にリリースされました。

## <a name="features"></a>フィーチャー

### <a name="project-templates-with-preinstalled-nuget-packages"></a>プレインストールされた NuGet パッケージとプロジェクト テンプレート
新しい ASP.NET MVC 3 プロジェクト テンプレートを作成するときにプロジェクトに含まれる jQuery スクリプト ライブラリが実際にによって配置された NuGet パッケージをインストールします。

ASP.NET MVC 3 プロジェクト テンプレートには、一連プロジェクト テンプレートが呼び出されたときにインストールされる NuGet パッケージにはが含まれています。 プロジェクト テンプレートを使用して NuGet パッケージを含めるには、この機能は、NuGet の機能では今すぐを_任意_プロジェクト テンプレートに得られる利点がようになりました。

この機能の詳細については、このテキストを読み取る[、機能の開発者がブログの投稿](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)です。

### <a name="explicit-assembly-references"></a>明示的にアセンブリ参照

追加された新しい`<references />`内で対象のアセンブリを明示的に指定するための要素、パッケージを参照してください。

たとえば、次のコードを追加するとします。

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

のみ、`xunit.dll`と`xunit.extensions.dll`適切な参照される[framework/プロファイル サブフォルダー](../schema/nuspec.md#explicit-assembly-references)の`lib`フォルダー、フォルダー内に他のアセンブリがある場合でもです。

この要素を省略したかどうかは、内のすべてのアセンブリを参照しているので、通常の動作が適用されます、`lib`フォルダーです。

__この機能で使用されますか。__

この機能は、デザイン時アセンブリのみをサポートします。 たとえば、コード コントラクトを使用する場合、コントラクト アセンブリしなければなりません Visual Studio は、それらを見つけることができますが、コントラクト アセンブリは実際には参照できません、プロジェクトにコピーしてはならないように、補強ランタイム アセンブリの横にあります。`bin`フォルダーです。

同様に、機能は、ランタイムのアセンブリの横にあるが、プロジェクト参照から除外するには、そのツール アセンブリが必要になる XUnit などのユニット テスト フレームワークに使用できます。

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>追加の機能で、.nuspec ファイルを除外するには
`<file>`内の要素、`.nuspec`ファイルを使用して、特定のファイルまたはワイルドカードを使用してファイルのセットが含まれます。 ワイルドカードを使用する場合、含まれているファイルの特定のサブセットを除外する方法はありません。 たとえば、特定の 1 つを除く、フォルダー内のすべてのテキスト ファイルを必要とします。

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

セミコロンを使用すると、複数のファイルを指定します。

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

または、ワイルドカードを使用して、すべてのバックアップ ファイルなどのファイルのセットを除外するには

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>ダイアログ ボックスを使用してパッケージを削除する依存関係を削除するメッセージが表示されます。
NuGet が表示されたら、依存関係を使用してパッケージをアンインストールする場合は、パッケージとパッケージの依存関係の削除を許可します。

![依存パッケージの削除](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package`コマンドの向上
`Get-Package`コマンドをサポートするようになりました、`-ProjectName`パラメーター。 したがって、コマンド

    Get-Package –ProjectName A

A. をプロジェクトにインストールされているすべてのパッケージが一覧表示します。

### <a name="support-for-proxies-that-require-authentication"></a>認証を必要とするプロキシのサポート
NuGet を使用して認証を必要とするプロキシの背後にある、NuGet では、プロキシの資格情報を求められますようになりました。 リモート リポジトリへの接続に NuGet を使用する資格情報を入力できます。

### <a name="support-for-repositories-that-require-authentication"></a>認証を必要とするリポジトリのサポート
NuGet への接続を今すぐサポート[プライベート リポジトリ](../hosting-packages/local-feeds.md)基本認証または NTLM 認証を必要とします。

ダイジェスト認証のサポートは、将来のリリースで追加されます。

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Nuget.org リポジトリにパフォーマンスの向上
Nuget.org ギャラリー パッケージを一覧表示して、検索を高速化にいくつかのパフォーマンスが向上をしました。

### <a name="solution-dialog-project-filtering"></a>ソリューション ダイアログのプロジェクトがフィルター処理
ソリューション レベル ダイアログ ボックスでどのようなプロジェクトをインストールする指示されたときに、選択したパッケージと互換性があるプロジェクトだけ表示されます。

### <a name="package-release-notes"></a>パッケージのリリース ノート
NuGet パッケージの管理には、リリース ノートのサポートが追加されました。 このリリース ノートにのみ表示を表示するときに_更新_パッケージのため、意味がないため、最初のリリースに追加します。

![更新プログラム タブ内のリリース ノート](./media/manage-nuget-packages-release-notes.png)

リリース ノートをパッケージに追加するには、新しい使用`<releaseNotes />`NuSpec ファイル内のメタデータの要素。

### <a name="nuspec-ltfiles-gt-improvement"></a>.nuspec & ltfiles/&gt;向上
`.nuspec`ファイルできるようになりました空`<files />`要素は、パッケージのすべてのファイルを含めない nuget.exe が示されます。

## <a name="bug-fixes"></a>バグ修正
NuGet 1.5 では、作業項目の固定 107 の合計がありました。 これらの 103 はバグとしてマークされています。

作業の完全な一覧の項目で修正 NuGet 1.5 では、くださいビュー、[今回のリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)です。

## <a name="bug-fixes-worth-noting"></a>注目すべきバグ修正:

* [問題 1273](http://nuget.codeplex.com/workitem/1273): 行われた`packages.config`パッケージをアルファベット順に並べ替え、余分な空白を削除してわかりやすい複数のバージョン管理します。
* [問題 844](http://nuget.codeplex.com/workitem/844): バージョン番号を今すぐ正規化ように`Install-Package 1.0`バージョンのパッケージで動作`1.0.0`です。
* [問題 1060](http://nuget.codeplex.com/workitem/1060): nuget.exe を使用してパッケージを作成するときに、`-Version`上書きフラグ、`<version />`要素。
