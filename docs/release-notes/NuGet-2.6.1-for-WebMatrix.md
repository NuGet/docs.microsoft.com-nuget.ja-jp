---
title: NuGet 2.6.1 for WebMatrix のリリース ノート
description: NuGet 2.6.1 の既知の問題、バグの修正、追加機能、および Dcr を含む WebMatrix のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 10d80a921cbc34b537f91644da97efc44530fa75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550318"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>NuGet 2.6.1 for WebMatrix のリリース ノート

[NuGet 2.6 リリース ノート](../release-notes/nuget-2.6.md) | [NuGet 2.7 リリース ノート](../release-notes/nuget-2.7.md)

NuGet チームでは、2014 年 3 月 26日に WebMatrix の最新の NuGet パッケージ マネージャー拡張機能をリリースします。  この更新プログラムをインストールすることができます、 [WebMatrix 拡張機能ギャラリー](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery)次の手順を使用します。

1. WebMatrix 3 を開く
1. [ホーム] リボンの拡張機能アイコンをクリックします
1. [更新] タブを選択します。
1. 2.6.1 に NuGet パッケージ マネージャーを更新する をクリックします。
1. 閉じて再起動 WebMatrix 3

## <a name="notable-changes"></a>主な変更点

この拡張機能の更新プログラムにより 2 つの問題を最も多く使用には、WebMatrix 内で NuGet パッケージの使用が直面しています。  最初は、NuGet のスキーマ バージョンのエラーと、もう 1 つは、先頭のゼロ バイトの Dll にバグは、`bin`フォルダー。

### <a name="nuget-schema-version-error"></a>NuGet のスキーマ バージョン エラー

WebMatrix 3 がリリースされてから新機能は NuGet パッケージを新しいスキーマ バージョンを必要とする NuGet に導入されています。  Web サイトの NuGet パッケージを管理するときに、これらの新しいパッケージは WebMatrix に表示されるエラーにつながります。

![エラーが発生しました。 スキーマのバージョンに互換性がありません。 NuGet を最新バージョンにアップグレードしてください。](./media/NuGet-2.8/webmatrix-schema-version.png)

この最新リリースでは、最新の NuGet パッケージは、このエラーが発生していることを防止との互換性を提供します。 Microsoft.AspNet.WebPages を含むパッケージの新しいバージョンは、WebMatrix で今すぐインストールできます。  などに、NuGet の機能を使用してこれらのパッケージの一部が[XDT 構成変換の](../release-notes/nuget-2.6.md#xdt)、これまで WebMatrix でサポートされていませんでした。

### <a name="zero-byte-dlls-in-bin-folder"></a>Bin フォルダーで 0 バイトの Dll

一部のユーザーが報告する NuGet のインストールをパッケージ化を含む Dll を bin にコピーを WebMatrix で Dll の表示にした後、 `bin` 0 バイトのファイルとフォルダー。  これにより、アプリケーションは、実行時に中断します。

[この問題](https://nuget.codeplex.com/workitem/4060)が修正されました。

## <a name="other-recent-improvements"></a>その他の最新の機能強化

Visual Studio の NuGet パッケージ マネージャー 2.8 のリリース時もリリースされました。 NuGet パッケージ マネージャー 2.5.0 WebMatrix の。  説明したこの中に、 [NuGet 2.8 リリース ノート](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)特定の更新プログラムが導入された新機能をお伝えします。

### <a name="update-all"></a>すべてを更新します。

すべての 1 つの手順で web サイトのパッケージを更新できます。  NuGet 拡張機能を開くには、WebMatrix で、ギャラリー、インストールされている、および、使用可能な更新プログラムのあるものすべてのパッケージの一覧を表示します。  以前は、すべてのパッケージが個別に更新する必要がありますが、[更新] タブに表示される便利な [すべて更新] ボタンがあるようになりました。

![利用可能な更新ですべてのパッケージを更新するには、[すべて更新] をクリックします。](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>既存のファイルを上書きします。

Web サイトに既に存在するファイルが含まれているパッケージをインストールするときに、NuGet には常にサイレント モードでそれらのファイル (単独で、既存のファイルを離れること) が無視されました。  これは、パッケージがインストールされているか、ときに実際にはありませんでしたが正しく更新という印象につながりますでした。  ファイルを上書きするには、NuGet は求められますようになりました。

![ファイルの競合の解決](./media/NuGet-2.8/webmatrix-overwrite-file.png)
