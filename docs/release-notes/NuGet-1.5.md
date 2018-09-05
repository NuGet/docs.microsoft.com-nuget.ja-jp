---
title: NuGet 1.5 のリリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 1.5 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c2b549f65e675e5fde9ae1dfea3f44f7d691a86b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548726"
---
# <a name="nuget-15-release-notes"></a>NuGet 1.5 のリリース ノート

[NuGet 1.4 のリリース ノート](../release-notes/nuget-1.4.md) | [NuGet 1.6 リリース ノート](../release-notes/nuget-1.6.md)

NuGet 1.5 は、2011 年 8 月 30 日にリリースされました。

## <a name="features"></a>フィーチャー

### <a name="project-templates-with-preinstalled-nuget-packages"></a>プレインストールされている NuGet パッケージを使用したプロジェクト テンプレート
新しい ASP.NET MVC 3 プロジェクト テンプレートを作成するときに、プロジェクトに含まれる jQuery スクリプト ライブラリが NuGet パッケージをインストールすることでがあります配置実際にされます。

ASP.NET MVC 3 プロジェクト テンプレートには、プロジェクト テンプレートが呼び出されたときにインストールされる NuGet パッケージのセットが含まれています。 プロジェクト テンプレートを使用した NuGet パッケージを含めるには、この機能は、NuGet の機能であるようになりましたが_任意_プロジェクト テンプレートのメリットを得ることができます。

この機能の詳細については、「この[機能の開発者によるブログの投稿](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)します。

### <a name="explicit-assembly-references"></a>明示的なアセンブリ参照

新しい追加`<references />`要素内でアセンブリを明示的に指定するために使用、パッケージを参照してください。

たとえば、次のコードを追加するとします。

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

後のみ、`xunit.dll`と`xunit.extensions.dll`から適切な参照は[フレームワーク/プロファイル サブフォルダー](../reference/nuspec.md#explicit-assembly-references)の`lib`フォルダー、フォルダー内の他のアセンブリがある場合でもです。

この要素を省略したかどうかでのすべてのアセンブリを参照しているので、通常の動作が適用されます、`lib`フォルダー。

__この機能のを使用目的は?__

この機能は、デザイン時アセンブリのみをサポートします。 たとえば、コード コントラクトを使用する場合、コントラクト アセンブリは Visual Studio は、それらを見つけることができますが、コントラクト アセンブリを選択し、実際に参照しないで、プロジェクトでにコピーしてはならないように拡張するランタイム アセンブリの隣にあるが必要`bin`フォルダー。

同様に、機能は、そのツールのアセンブリはランタイム アセンブリの横にあるが、プロジェクト参照から除外する必要がある XUnit などの単体テスト フレームワークに使用できます。

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>.Nuspec ファイルを除外する機能を追加しました
`<file>`内の要素を`.nuspec`ファイルを使用して、特定のファイルまたはワイルドカードを使用してファイルのセットが含まれます。 ワイルドカードを使用する場合、含まれているファイルの特定のサブセットを除外する方法はありません。 たとえば、特定の 1 つを除く、フォルダー内のすべてのテキスト ファイルを必要とします。

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

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>ダイアログ ボックスを使用してパッケージを削除する依存関係を削除するように求められます
NuGet が表示されたら、依存関係を使用してパッケージをアンインストールするときに、パッケージとパッケージの依存関係の削除を許可します。

![依存パッケージを削除します。](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` コマンドの向上
`Get-Package`コマンドがサポートされています、`-ProjectName`パラメーター。 したがって、コマンド

    Get-Package –ProjectName A

A. をプロジェクトにインストールされているすべてのパッケージが一覧表示します。

### <a name="support-for-proxies-that-require-authentication"></a>認証が必要なプロキシのサポート
NuGet を使用して、認証が必要なプロキシの背後にある、NuGet では、プロキシの資格情報が求めるされますようになりました。 NuGet リモート リポジトリに接続するのには、資格情報を入力できます。

### <a name="support-for-repositories-that-require-authentication"></a>認証を必要とするリポジトリのサポート
NuGet への接続を今すぐサポート[プライベート リポジトリ](../hosting-packages/local-feeds.md)基本認証または NTLM 認証を必要とします。

ダイジェスト認証のサポートは、将来のリリースで追加されます。

### <a name="performance-improvements-to-the-nugetorg-repository"></a>リポジトリ nuget.org をパフォーマンスの向上
Nuget.org ギャラリー パッケージを一覧表示して、高速検索をいくつかのパフォーマンス強化を行いました。

### <a name="solution-dialog-project-filtering"></a>ソリューション ダイアログ プロジェクトのフィルタ リング
ソリューション レベル ダイアログ ボックスで、インストールするには、どのようなプロジェクトのプロンプト時に、選択したパッケージと互換性があるプロジェクトだけを示します。

### <a name="package-release-notes"></a>パッケージのリリース ノート
NuGet パッケージには、リリース ノートのサポートが追加されました。 リリース ノートにのみ表示を表示するときに_更新_パッケージのため意味をなさない、最初のリリースに追加します。

![[更新] タブ内のリリース ノート](./media/manage-nuget-packages-release-notes.png)

にパッケージをリリース ノートを追加する、新しい使用`<releaseNotes />`NuSpec ファイル内のメタデータ要素。

### <a name="nuspec-ltfiles-gt-improvement"></a>.nuspec & ltfiles/&gt;向上
`.nuspec`ファイルは現在空により`<files />`要素は、すべてのファイルをパッケージに含めない nuget.exe が示されます。

## <a name="bug-fixes"></a>バグ修正
NuGet 1.5 では、作業項目の固定 107 の合計がありました。 これらの 103 はバグとしてマークされています。

作業の完全な一覧の項目で修正された NuGet 1.5 では、くださいビュー、[このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)します。

## <a name="bug-fixes-worth-noting"></a>注目すべきバグ修正:

* [問題 1273](http://nuget.codeplex.com/workitem/1273): 行った`packages.config`パッケージをアルファベット順に並べ替え、余分な空白を削除してわかりやすい複数のバージョン管理します。
* [問題 844](http://nuget.codeplex.com/workitem/844): バージョン番号を正規化するようになりましたように`Install-Package 1.0`バージョンを使用してパッケージで動作`1.0.0`します。
* [問題 1060](http://nuget.codeplex.com/workitem/1060)。 nuget.exe を使用してパッケージを作成するときに、`-Version`上書きフラグ、`<version />`要素。
