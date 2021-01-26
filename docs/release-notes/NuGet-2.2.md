---
title: NuGet 2.2 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.2 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780434"
---
# <a name="nuget-22-release-notes"></a>NuGet 2.2 リリースノート

[NuGet 2.1 リリースノート](../release-notes/nuget-2.1.md)  | [NuGet 2.2.1 リリースノート](../release-notes/nuget-2.2.1.md)

NuGet 2.2 は、2012年12月12日にリリースされました。

## <a name="visual-studio-quick-launch"></a>Visual Studio のクイック起動
Visual Studio 2012 で追加された新機能の1つに、[ [クイック起動] ダイアログ](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box)がありました。 NuGet 2.2 では、このダイアログボックスが拡張され、クイック起動に入力された検索語句を使用してパッケージマネージャーダイアログを初期化できるようになりました。 たとえば、クイック起動で「jquery」と入力すると、' jquery ' に一致する NuGet パッケージを検索するためのオプションが結果に含まれるようになります。

![Visual Studio の NuGet のクイック起動](./media/quick-launch.png)

このオプションを選択すると、"jquery" という用語に対して標準の NuGet パッケージマネージャーの検索エクスペリエンスが起動します。

![事前設定された NuGet パッケージマネージャーダイアログ](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>パッケージコンテンツのフォルダー全体を指定する
NuGet 2.2 では、ファイルの要素にフォルダー全体を指定し `<file>` `.nuspec` て、そのフォルダーのすべての内容を含めることができるようになりました。 たとえば、次のようにすると、パッケージがプロジェクトにインストールされるときに、パッケージの scripts フォルダー内のすべてのスクリプトが content\ scripts フォルダーに追加されます。

```xml
<file src="scripts\" target="content\scripts"/>
```

**更新プログラム 6/24/16: パッケージのインストール時に、"content" フォルダー内の空のフォルダーは無視されます。**

## <a name="known-issues"></a>既知の問題

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>パッケージマネージャーコンソールを使用すると、F # プロジェクトのパッケージのインストールが失敗する
パッケージマネージャーコンソールを使用して NuGet パッケージを F # プロジェクトにインストールしようとすると、InvalidOperationException がスローされます。 私たちは問題を解決するために F # チームと積極的に連携していますが、その間は、コンソールではなく NuGet の [パッケージマネージャー] ダイアログを使用して、NuGet パッケージを F # プロジェクトにインストールすることをお勧めします。 [詳細については、CodePlex を](http://nuget.codeplex.com/workitem/2873)参照してください。


## <a name="bug-fixes"></a>バグの修正
NuGet 2.2 には、多くのバグ修正が含まれています。 NuGet 2.2 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)を参照してください。
