---
title: NuGet 2.2 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 2.2 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545993"
---
# <a name="nuget-22-release-notes"></a>NuGet 2.2 リリース ノート

[NuGet 2.1 リリース ノート](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 リリース ノート](../release-notes/nuget-2.2.1.md)

NuGet 2.2 は、2012 年 12 月 12 日にリリースされました。

## <a name="visual-studio-quick-launch"></a>Visual Studio のクイック起動
Visual Studio 2012 で追加された新機能の 1 つが、[クイック起動ダイアログ](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box)します。 NuGet 2.2 では、クイック起動で入力した検索語句でパッケージ マネージャー ダイアログを初期化することができます、このダイアログ ボックスを拡張します。 クイック起動で"jquery"を入力すると、今すぐなどには、"jquery"に一致する NuGet パッケージの検索結果でオプションを含まれます。

![Visual Studio のクイック起動の NuGet](./media/quick-launch.png)

このオプションを選択すると、"jquery"という用語の標準的な NuGet パッケージ マネージャー検索エクスペリエンスが起動します。

![あらかじめ設定されている NuGet パッケージ マネージャー ダイアログ ボックス](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>パッケージのコンテンツのフォルダー全体を指定します。
NuGet 2.2 のフォルダー全体を指定できるようになりました、`<file>`の要素、`.nuspec`ファイルをそのフォルダーの内容のすべてが含まれます。 たとえば、次によりすべてのスクリプト パッケージのスクリプト フォルダーをプロジェクトにパッケージがインストールされている場合、contents\scripts フォルダーに追加します。

```xml
<file src="scripts\" target="content\scripts"/>
```

**6/24/16 の更新: パッケージをインストールするときに、"content"フォルダー内の空のフォルダーは無視されます。**

## <a name="known-issues"></a>既知の問題

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>パッケージ マネージャー コンソールを使用する場合、f# プロジェクトのパッケージのインストールが失敗しました。
パッケージ マネージャー コンソールを使用して、f# プロジェクトに NuGet パッケージをインストールしようとすると、InvalidOperationException がスローされます。 問題を解決するには、f# チームと協力して積極的にいますが、それまでは、回避は、コンソールではなく、NuGet のパッケージ マネージャー ダイアログ ボックスを使用して、f# のプロジェクトに NuGet パッケージをインストールするには。 [詳細については、codeplex から入手できる](http://nuget.codeplex.com/workitem/2873)します。


## <a name="bug-fixes"></a>バグ修正
NuGet 2.2 には、多くのバグ修正が含まれています。 作業の完全な一覧の項目で修正された NuGet 2.2、くださいビュー、[このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)します。
