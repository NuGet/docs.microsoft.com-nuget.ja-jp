---
title: NuGet 1.5 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 1.5 のリリースノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940a19cdc485d611d03b52ee3102bc95a78a36bb
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383350"
---
# <a name="nuget-15-release-notes"></a>NuGet 1.5 リリースノート

Nuget [1.4 リリースノート](../release-notes/nuget-1.4.md) | [Nuget 1.6 リリースノート](../release-notes/nuget-1.6.md)

NuGet 1.5 は、2011年8月30日にリリースされました。

## <a name="features"></a>フィーチャー

### <a name="project-templates-with-preinstalled-nuget-packages"></a>NuGet パッケージがプレインストールされるプロジェクトテンプレート
新しい ASP.NET MVC 3 プロジェクトテンプレートを作成する場合、プロジェクトに含まれる jQuery スクリプトライブラリは、NuGet パッケージをインストールすることによって実際に配置されます。

ASP.NET MVC 3 プロジェクトテンプレートには、プロジェクトテンプレートが呼び出されたときにインストールされる NuGet パッケージのセットが含まれています。 プロジェクトテンプレートを含む NuGet パッケージを追加する機能は、_すべて_のプロジェクトテンプレートでを利用できるようになった nuget の機能です。

この機能の詳細については、この[機能の開発者によるこのブログ投稿](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)を参照してください。

### <a name="explicit-assembly-references"></a>明示的なアセンブリ参照

パッケージ内のどのアセンブリを参照する必要があるかを明示的に指定するために使用される新しい `<references />` 要素が追加されました。

たとえば、次のコードを追加するとします。

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

その後、フォルダー内に他のアセンブリがある場合でも、`lib` フォルダーの適切な[フレームワーク/プロファイルサブフォルダー](../reference/nuspec.md#explicit-assembly-references)からは、`xunit.dll` と `xunit.extensions.dll` のみが参照されます。

この要素が省略されている場合は、通常の動作が適用されます。これは、`lib` フォルダー内のすべてのアセンブリを参照します。

__この機能はどのように使用されますか。__

この機能は、デザイン時のみのアセンブリをサポートします。 たとえば、コードコントラクトを使用する場合、コントラクトアセンブリは、Visual Studio が検出できるように拡張するランタイムアセンブリの横にある必要がありますが、コントラクトアセンブリは実際にはプロジェクトによって参照されていないため、`bin` フォルダーにコピーしないでください。

同様に、この機能は、ツールアセンブリをランタイムアセンブリの横に配置する必要があるが、プロジェクト参照から除外される単体テストフレームワーク (XUnit など) に対しても使用できます。

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Nuspec 内のファイルを除外する機能を追加しました。
`.nuspec` ファイル内の `<file>` 要素を使用して、ワイルドカードを使用して特定のファイルまたは一連のファイルを含めることができます。 ワイルドカードを使用する場合、含まれているファイルの特定のサブセットを除外する方法はありません。 たとえば、特定のファイルを除くフォルダー内のすべてのテキストファイルが必要であるとします。

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

複数のファイルを指定するには、セミコロンを使用します。

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

または、ワイルドカードを使用して、すべてのバックアップファイルなどの一連のファイルを除外します。

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>ダイアログボックスを使用してパッケージを削除し、依存関係を削除する
依存関係を含むパッケージをアンインストールすると、NuGet プロンプトが表示され、パッケージと共にパッケージの依存関係を削除できます。

![依存パッケージの削除](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` コマンドの機能強化
`Get-Package` コマンドで `-ProjectName` パラメーターがサポートされるようになりました。 コマンド

    Get-Package –ProjectName A

プロジェクト A にインストールされているすべてのパッケージが一覧表示されます。

### <a name="support-for-proxies-that-require-authentication"></a>認証を必要とするプロキシのサポート
認証を必要とするプロキシの背後で NuGet を使用すると、NuGet はプロキシの資格情報の入力を求められるようになります。 資格情報を入力すると、NuGet はリモートリポジトリに接続できます。

### <a name="support-for-repositories-that-require-authentication"></a>認証を必要とするリポジトリのサポート
NuGet では、基本認証または NTLM 認証を必要とする[プライベートリポジトリ](../hosting-packages/local-feeds.md)への接続がサポートされるようになりました。

ダイジェスト認証のサポートは、今後のリリースで追加される予定です。

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Nuget.org リポジトリのパフォーマンスの向上
Nuget.org ギャラリーでは、パッケージの一覧と検索をより迅速に行うために、いくつかのパフォーマンスが向上しました。

### <a name="solution-dialog-project-filtering"></a>ソリューションダイアログプロジェクトのフィルター処理
ソリューションレベルのダイアログでは、インストールするプロジェクトを要求するときに、選択したパッケージと互換性のあるプロジェクトのみが表示されます。

### <a name="package-release-notes"></a>パッケージのリリースノート
NuGet パッケージには、リリースノートのサポートが含まれるようになりました。 リリースノートは、パッケージの_更新_を表示するときにのみ表示されます。そのため、最初のリリースに追加することは意味がありません。

![[更新] タブ内のリリースノート](./media/manage-nuget-packages-release-notes.png)

リリースノートをパッケージに追加するには、NuSpec ファイルで新しい `<releaseNotes />` メタデータ要素を使用します。

### <a name="nuspec-ltfiles-gt-improvement"></a>. nuspec & ltfiles/&gt; の改善
`.nuspec` ファイルでは、空の `<files />` 要素が許可されるようになりました。これにより、パッケージにファイルを含めないように nuget.exe に指示します。

## <a name="bug-fixes"></a>バグ修正
NuGet 1.5 では、合計107個の作業項目が修正済みです。 これらの103はバグとしてマークされています。

NuGet 1.5 で修正された作業項目の完全な一覧については、[このリリースの Nuget Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)を参照してください。

## <a name="bug-fixes-worth-noting"></a>バグ修正:

* [問題 1273](http://nuget.codeplex.com/workitem/1273): パッケージをアルファベット順に並べ替え、余分な空白を削除することで、より多くのバージョンコントロール `packages.config` しました。
* [問題 844](http://nuget.codeplex.com/workitem/844): バージョン番号が正規化され、`1.0.0`バージョンのパッケージで `Install-Package 1.0` が機能するようになりました。
* [問題 1060](http://nuget.codeplex.com/workitem/1060): nuget.exe を使用してパッケージを作成するときに、`-Version` フラグが `<version />` 要素よりも優先されます。
