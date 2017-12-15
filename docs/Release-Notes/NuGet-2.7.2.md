---
title: "NuGet 2.7.2 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: c775d1d7-de26-476c-bf9e-0cf95986a22f
description: "NuGet 2.7.2 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。"
keywords: "NuGet 2.7.2 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5bb1eb346666c5d5ee790fcdcd7d844bfd37b22e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-272-release-notes"></a>NuGet 2.7.2 リリース ノート

[NuGet 2.7.1 リリース ノート](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 リリース ノート](../release-notes/nuget-2.8.md)

NuGet 2.7.2 は、2013 年 11 月 11 日にリリースされました。

## <a name="noteworthy-bug-fixes-and-features"></a>注目すべきことのバグ修正と機能

### <a name="license-text"></a>ライセンスのテキスト
はかなりの時間は、Visual Studio で Web アプリケーション プロジェクトの既定のテンプレートの一部としていくつかの一般的なオープン ソース ライブラリ用の NuGet パッケージが Microsoft に含まれているがします。 jQuery は、ライブラリのこの型の最も一般的な例を示します可能性があります。 サポート契約を製品と共に配信されるコンポーネントに関連付けられているため、パッケージのスクリプト ファイルには、パブリック nuget.org ギャラリーで同じパッケージで見つかったスクリプト ファイルよりも別のライセンスのテキストが含まれています。 テキストの違いは、パッケージの更新を防ぐためさまざまなコンテンツのハッシュ値を含むスクリプト ファイルを原因別のライセンスのテキスト ブロックの結果として処理 (およびためとして扱われる、プロジェクト内で変更)。

この問題を軽減するのには、NuGet 2.7.2 は、スクリプトの作成者には、次のように特別にマークされたセクション内にあるライセンスのテキスト ブロックを含めるを許可します。

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

コンテンツを含むパッケージを更新するときにこのブロックを含むファイル NuGet はいない NuGet ギャラリーのバージョンと比較した結果に、ブロックの内容を考慮できます削除され元のコピーと一致する場合と同様に、コンテンツ ファイルを更新します。

このブロックは、テキスト"NUGET:: 開始ライセンス TEXT"と"NUGET:: 終了ライセンス TEXT"の先頭で任意の場所に発生した行と最終行で識別されます。  その他の書式設定の要件が存在していない言語に関係なく、テキスト ファイルの種類で使用するには、この機能を許可します。

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>アセンブリ以外のフレームワークをバインド リダイレクトを追加します。
.NET Framework の一部であるアセンブリの場合は、NuGet はパッケージを更新するときにアプリケーションの構成ファイルに追加のバインド リダイレクトをスキップします。 この修正プログラムのアドレス、バインド リダイレクト追加されませんでした中、一部のアセンブリでは、それらのアセンブリがない場合でも NuGet 2.7 の回帰には、.NET Framework の一部と見なされます。 NuGet 2.7.2 は、以前の NuGet 2.5 および 2.6 の動作を復元し、バインド リダイレクトを追加します。

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Xamarin ツールがインストールされているポータブル ライブラリをインストールします。
マシンには、Xamarin の開発ツールがインストールされている、ときに、既存のターゲット フレームワークの組み合わせ、および Xamarin フレームワークの間の互換性を指定する、サポートされているフレームワークの構成データを変更します。 バージョン 2.7.2、NuGet は、これらの暗黙的な互換性規則の対応するようになりましたしたがって簡単で、パッケージのようなをする Xamarin と互換性のあるが、明示的にマークされているポータブル ライブラリをインストールする Xamarin プラットフォームを対象とする開発者向けメタデータ自体です。

### <a name="machine-wide-configuration-settings-honored"></a>コンピューター全体の構成設定の受け入れ
Nuget.Config ファイルの階層を使用する場合、ソリューションのルートに最も近い Nuget.Config ファイルの repositoryPath キーが受け付けられませんでしたされています。 Visual Studio 2013 では、NuGet は、"Microsoft および .NET"のパッケージ ソースを追加するために %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config でカスタム Nuget.Config ファイルをインストールします。 その結果、回避ソリューションでカスタム repositoryPath を使用するためも、"Microsoft および .NET"のパッケージ ソースを削除するためのもののコンピューター レベル。 Nuget.Config を削除することでした。 NuGet 2.7.2 では、repositoryPath の優先順位規則 Nuget.Config ファイルの階層を使用する場合。

## <a name="all-changes"></a>すべての変更
作業の完全な一覧の項目で修正 NuGet 2.7.2、くださいビュー、[今回のリリースの NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)です。
