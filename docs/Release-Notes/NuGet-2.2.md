---
title: "NuGet 2.2 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 25389d8c-e7db-4920-ab5e-cff20cebee7e
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 2.2 リリース ノートです。"
keywords: "NuGet 2.2 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 690e76a0686a5e7bb699410edef4a6e62ccd2a32
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-22-release-notes"></a>NuGet 2.2 リリース ノート

[NuGet 2.1 リリース ノート](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 リリース ノート](../release-notes/nuget-2.2.1.md)

NuGet 2.2 は、2012 年 12 月 12 日にリリースされました。

## <a name="visual-studio-quick-launch"></a>Visual Studio のクイック起動
Visual Studio 2012 で追加された新機能の 1 つが、[クイック起動ダイアログ](http://msdn.microsoft.com/library/hh417697.aspx)です。 NuGet 2.2 は、クイック起動 で入力した検索語句をパッケージ マネージャー ダイアログを初期化できるようにこのダイアログ ボックスを拡張します。 たとえば、'jquery' を今サイド リンク バーに入力するオプションが含まれます 'jquery' と一致する NuGet パッケージを検索する結果にします。

![Visual Studio のクイック起動で NuGet](./media/quick-launch.png)

このオプションを選択すると、という用語は、'jquery' の標準的な NuGet パッケージ マネージャー検索エクスペリエンスが起動します。

![事前設定済みの NuGet パッケージ マネージャー ダイアログ ボックス](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>パッケージの内容をフォルダー全体を指定します。
NuGet 2.2 でフォルダー全体を指定できるようになりました、`<file>`の要素、`.nuspec`ファイルをそのフォルダーの内容のすべてが含まれます。 たとえば、次によりすべてのスクリプトをプロジェクトにパッケージがインストールされている場合、contents\scripts フォルダーに追加するパッケージのスクリプト フォルダーにされます。

```xml
<file src="scripts\" target="content\scripts"/>
```

**6/24/16 を更新します。 パッケージをインストールするときに、"content"フォルダーに空のフォルダーは無視されます。**

## <a name="known-issues"></a>既知の問題

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>パッケージ マネージャー コンソールを使用する場合、f# プロジェクトのパッケージのインストールが失敗します。
パッケージ マネージャー コンソールを使用して、f# プロジェクトに NuGet パッケージをインストールしようとすると、ときに、InvalidOperationException がスローされます。 私たちは積極的に連携し、問題を解決するには、f# チームがその間は、回避策は、コンソールではなく、NuGet のパッケージ マネージャー ダイアログ ボックスを使用して、f# のプロジェクトに NuGet パッケージのインストールします。 [詳細については、codeplex から入手できる](http://nuget.codeplex.com/workitem/2873)です。


## <a name="bug-fixes"></a>バグ修正
NuGet 2.2 には、多くのバグ修正が含まれています。 作業の完全な一覧アイテムを固定 NuGet 2.2 でくださいビュー、[今回のリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)です。
