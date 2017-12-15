---
title: "WebMatrix のリリース ノートについては、NuGet 2.6.1 |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 119ea65b-b38b-4a8c-a4ed-6ea06f1aad09
description: "WebMatrix の既知の問題、バグの修正、追加された機能は、Dcr などの NuGet 2.6.1 のリリース ノートです。"
keywords: "WebMatrix のリリース ノート、バグの修正プログラム、既知の問題、NuGet 2.6.1 Dcr、機能の追加"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f859fd8ef74f3246d997790e40f70ad25aadeb71
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>WebMatrix のリリース ノートについては、NuGet 2.6.1

[NuGet 2.6 リリース ノート](../release-notes/nuget-2.6.md) | [NuGet 2.7 リリース ノート](../release-notes/nuget-2.7.md)

NuGet チームは、2014 年 3 月 26 日に WebMatrix の最新の NuGet Package Manager 拡張機能をリリースします。  この更新プログラムをインストールすることができます、 [WebMatrix 拡張機能ギャラリー](http://extensions.webmatrix.com/packages/NuGetPackageManager/)次の手順を使用します。

1. WebMatrix 3 を開く
2. [ホーム] リボンの拡張機能のアイコンをクリックします。
3. 更新プログラム タブを選択します。
4. 2.6.1 に NuGet Package Manager を更新する をクリックします。
6. 終了し、WebMatrix 3 の再起動

## <a name="notable-changes"></a>主な変更点

この拡張機能の更新プログラムにより 2 つの問題を最も多く使用には、WebMatrix 内で NuGet パッケージの使用が直面しています。  NuGet スキーマ バージョン エラーが発生しました、最初と 2 つ目が先頭のゼロ バイト Dll へのバグ、`bin`フォルダーです。

### <a name="nuget-schema-version-error"></a>NuGet のスキーマ バージョン エラー

WebMatrix 3 がリリースされた後に、NuGet パッケージを新しいスキーマのバージョンを必要とする NuGet の新機能が導入されました。  Web サイトの NuGet パッケージを管理するとき、これらの新しいパッケージ エラー WebMatrix で表示される可能性があります。

![エラーが発生しました。 スキーマのバージョンに互換性がありません。 最新バージョンには、NuGet をアップグレードしてください。](./media/NuGet-2.8/webmatrix-schema-version.png)

この最新リリースでは、最新の NuGet パッケージは、このエラーが発生していることを妨げてとの互換性を提供します。 Microsoft.AspNet.WebPages を含むパッケージの新しいバージョンは、WebMatrix で今すぐインストールできます。  これらのパッケージの一部を使用していた NuGet 機能など、 [XDT 構成変換](../release-notes/nuget-2.6.md#xdt)、これまで WebMatrix でサポートされていませんでした。

### <a name="zero-byte-dlls-in-bin-folder"></a>Bin フォルダー内の 0 バイト Dll

一部のユーザーが報告される NuGet のインストールをパッケージ化をビン分割にコピーする Dll を含む WebMatrix で Dll スライド ショーにした後、 `bin` 0 バイトのファイルとフォルダー。  これは、実行時にアプリケーションを中断します。

[この問題](https://nuget.codeplex.com/workitem/4060)固定されているようになりました。

## <a name="other-recent-improvements"></a>最近使用したその他の改善

Visual Studio の NuGet パッケージ マネージャー 2.8 のリリース時おもリリース NuGet Package Manager 2.5.0 WebMatrix です。  説明したこの中に、 [NuGet 2.8 のリリース ノート](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)特定の更新プログラムが導入された新機能が記述されていません。

### <a name="update-all"></a>すべて更新します。

すべての 1 つの手順で、web サイトのパッケージを今すぐ更新することができます。  WebMatrix で、NuGet 拡張機能を開くときは、ギャラリー、インストールされている、および利用可能な更新を持つ方すべてのパッケージの一覧を表示します。  以前は、すべてのパッケージが個別に更新する必要がありますが、今すぐは [更新] タブに表示される便利すべて"更新"ボタン。

![利用可能な更新ですべてのパッケージを更新するには、[すべて更新] をクリックします。](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>既存のファイルを上書き

Web サイトに既に存在するファイルを含むパッケージをインストールするときに、NuGet には常に同じサイレント (単独で、既存のファイルのまま)、それらのファイルが無視されました。  これは、パッケージがインストールされているか、ときに実際にはありませんでしたが正しく更新印象に可能性があります。  NuGet が求められますファイルを上書きするようになりました。

![ファイルの競合の解決](./media/NuGet-2.8/webmatrix-overwrite-file.png)
