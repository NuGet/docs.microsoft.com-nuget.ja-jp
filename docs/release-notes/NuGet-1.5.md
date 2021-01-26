---
title: NuGet 1.5 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 1.5 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c9946f3d8cf545ec14f842c40105743c231b4b72
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777092"
---
# <a name="nuget-15-release-notes"></a>NuGet 1.5 リリースノート

[NuGet 1.4 リリースノート](../release-notes/nuget-1.4.md)  | [NuGet 1.6 リリースノート](../release-notes/nuget-1.6.md)

NuGet 1.5 は、2011年8月30日にリリースされました。

## <a name="features"></a>特徴

### <a name="project-templates-with-preinstalled-nuget-packages"></a>NuGet パッケージがプレインストールされるプロジェクトテンプレート
新しい ASP.NET MVC 3 プロジェクトテンプレートを作成する場合、プロジェクトに含まれる jQuery スクリプトライブラリは、NuGet パッケージをインストールすることによって実際に配置されます。

ASP.NET MVC 3 プロジェクトテンプレートには、プロジェクトテンプレートが呼び出されたときにインストールされる NuGet パッケージのセットが含まれています。 プロジェクトテンプレートを含む NuGet パッケージを追加する機能は、 _すべて_ のプロジェクトテンプレートでを利用できるようになった nuget の機能です。

この機能の詳細については、この [機能の開発者によるこのブログ投稿](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)を参照してください。

### <a name="explicit-assembly-references"></a>明示的なアセンブリ参照

`<references />`パッケージ内のどのアセンブリを参照する必要があるかを明示的に指定するために使用される新しい要素が追加されました。

たとえば、次のコードを追加するとします。

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

`xunit.dll` `xunit.extensions.dll` フォルダー内に他のアセンブリがある場合でも、とは、フォルダーの適切な[フレームワーク/プロファイルサブフォルダー](../reference/nuspec.md#explicit-assembly-references)から参照され `lib` ます。

この要素が省略されている場合は、通常の動作が適用されます。これは、フォルダー内のすべてのアセンブリを参照し `lib` ます。

__この機能はどのように使用されますか。__

この機能は、デザイン時のみのアセンブリをサポートします。 たとえば、コードコントラクトを使用する場合、コントラクトアセンブリは、Visual Studio が検出できるように拡張するランタイムアセンブリの横にある必要がありますが、コントラクトアセンブリは実際にはプロジェクトによって参照されることはなく、フォルダーにコピーされないようにする必要があり `bin` ます。

同様に、この機能は、ツールアセンブリをランタイムアセンブリの横に配置する必要があるが、プロジェクト参照から除外される単体テストフレームワーク (XUnit など) に対しても使用できます。

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Nuspec 内のファイルを除外する機能を追加しました。
`<file>`ファイル内の要素 `.nuspec` を使用して、ワイルドカードを使用して特定のファイルまたは一連のファイルを含めることができます。 ワイルドカードを使用する場合、含まれているファイルの特定のサブセットを除外する方法はありません。 たとえば、特定のファイルを除くフォルダー内のすべてのテキストファイルが必要であるとします。

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


### <a name="get-package-command-improvement"></a>`Get-Package` コマンドの改善
`Get-Package`コマンドでパラメーターがサポートされるようになりました `-ProjectName` 。 コマンド

```
Get-Package –ProjectName A
```

プロジェクト A にインストールされているすべてのパッケージが一覧表示されます。

### <a name="support-for-proxies-that-require-authentication"></a>認証を必要とするプロキシのサポート
認証を必要とするプロキシの背後で NuGet を使用すると、NuGet はプロキシの資格情報の入力を求められるようになります。 資格情報を入力すると、NuGet はリモートリポジトリに接続できます。

### <a name="support-for-repositories-that-require-authentication"></a>認証を必要とするリポジトリのサポート
NuGet では、基本認証または NTLM 認証を必要とする [プライベートリポジトリ](../hosting-packages/local-feeds.md) への接続がサポートされるようになりました。

ダイジェスト認証のサポートは、今後のリリースで追加される予定です。

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Nuget.org リポジトリのパフォーマンスの向上
Nuget.org ギャラリーでは、パッケージの一覧と検索をより迅速に行うために、いくつかのパフォーマンスが向上しました。

### <a name="solution-dialog-project-filtering"></a>ソリューションダイアログプロジェクトのフィルター処理
ソリューションレベルのダイアログでは、インストールするプロジェクトを要求するときに、選択したパッケージと互換性のあるプロジェクトのみが表示されます。

### <a name="package-release-notes"></a>パッケージのリリースノート
NuGet パッケージには、リリースノートのサポートが含まれるようになりました。 リリースノートは、パッケージの _更新_ を表示するときにのみ表示されます。そのため、最初のリリースに追加することは意味がありません。

![[更新] タブ内のリリースノート](./media/manage-nuget-packages-release-notes.png)

リリースノートをパッケージに追加するには、 `<releaseNotes />` NuSpec ファイルで新しい metadata 要素を使用します。

### <a name="nuspec-ltfiles-gt-improvement"></a>. nuspec &ltfiles/ &gt; 向上
`.nuspec`ファイルに空の要素が許可されるようになりました。これにより、 `<files />` パッケージにファイルを含めないように nuget.exe に指示します。

## <a name="bug-fixes"></a>バグの修正
NuGet 1.5 では、合計107個の作業項目が修正済みです。 これらの103はバグとしてマークされています。

NuGet 1.5 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)を参照してください。

## <a name="bug-fixes-worth-noting"></a>バグ修正:

* [問題 1273](http://nuget.codeplex.com/workitem/1273): `packages.config` パッケージをアルファベット順に並べ替え、余分な空白を削除することで、より多くのバージョンコントロールを使いやすくしました。
* [問題 844](http://nuget.codeplex.com/workitem/844): バージョン番号が正規化され `Install-Package 1.0` 、がバージョンのパッケージで動作するようになりました `1.0.0` 。
* [問題 1060](http://nuget.codeplex.com/workitem/1060): nuget.exe を使用してパッケージを作成するときに、フラグによって `-Version` 要素がオーバーライドされ `<version />` ます。
