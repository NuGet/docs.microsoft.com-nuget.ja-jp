---
title: NuGet 2.7.2 リリース ノート
description: NuGet 2.7.2 などのリリース ノートには、問題、バグの修正、追加機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3e63944a05f66d5dadf17c5d4b91d3bc4478bb33
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550071"
---
# <a name="nuget-272-release-notes"></a>NuGet 2.7.2 リリース ノート

[NuGet 2.7.1 リリース ノート](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 のリリース ノート](../release-notes/nuget-2.8.md)

NuGet 2.7.2 は、2013 年 11 月 11 日にリリースされました。

## <a name="noteworthy-bug-fixes-and-features"></a>注目に値するバグ修正と機能

### <a name="license-text"></a>ライセンスのテキスト
はかなり時間、Microsoft は、Visual Studio で Web アプリケーション プロジェクトの既定のテンプレートの一部としていくつかの一般的なオープン ソース ライブラリの NuGet パッケージを含めるが。 jQuery は、ライブラリのこの種類の例では、最もよく知られている可能性があります。 サポート契約は、製品と共に配信されるコンポーネントに関連付けられている、ため、パッケージのスクリプト ファイルには、パブリック nuget.org ギャラリーで、同じパッケージにあるスクリプト ファイルよりもテキスト別のライセンスにはが含まれています。 このテキストの違いは、パッケージの更新を防ぐためさまざまなコンテンツのハッシュ値を持つスクリプト ファイルを原因別のライセンスのテキスト ブロックの結果として処理 (およびためとして扱う場合に、プロジェクト内で変更)。

この問題を軽減するには、NuGet 2.7.2 は、スクリプトの作成者には、次のように特別にマークされたセクション内にあるライセンスのテキスト ブロックを含めるを許可します。

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

コンテンツを含むパッケージを更新するときに、このブロックを含むファイル NuGet はいないブロックの内容の要因と、NuGet ギャラリー上のバージョンと比較した結果ことができますしたがって削除し、元のコピーと一致する場合と同様に、コンテンツ ファイルを更新します。

このブロックは、テキスト"NUGET:: 開始ライセンス TEXT"と"NUGET:: 終了ライセンス TEXT"、先頭に任意の場所で発生して、最終行によって識別されます。  その他の書式設定の要件が存在しない任意の種類の言語に関係なく、テキスト ファイルで使用するには、この機能を許可します。

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Framework アセンブリ以外の追加のバインド リダイレクト
.NET Framework の一部であるアセンブリでは、NuGet はパッケージを更新するときに、アプリケーションの構成ファイルに追加のバインド リダイレクトをスキップします。 この修正プログラム アドレスというバインド リダイレクトが追加されない一部のアセンブリのそれらのアセンブリでない場合でも、NuGet 2.7 の回帰には、.NET Framework の一部と見なされます。 2.7.2 NuGet では、前の NuGet 2.5 と 2.6 の動作を復元し、バインド リダイレクトを追加します。

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>インストールされている Xamarin ツールでポータブル ライブラリをインストールします。
コンピューターでは、Xamarin の開発ツールがインストールされている、ときに、既存のターゲット フレームワークの組み合わせと Xamarin フレームワーク間の互換性を指定する構成データをサポートされているフレームワークを変更します。 2.7.2 のバージョンでは、NuGet はこれらの暗黙の互換性規則に注意してください。 今すぐとため簡単で、パッケージのポータブル ライブラリを Xamarin と互換性がありますが、明示的にマークをようインストール Xamarin プラットフォームを対象とする開発者向けメタデータ自体です。

### <a name="machine-wide-configuration-settings-honored"></a>コンピューター全体の構成設定が受け入れられます
階層の Nuget.Config ファイルを使用する場合、ソリューションのルートに最も近い Nuget.Config ファイルの repositoryPath キーが受け付けられませんでしたされています。 Visual Studio 2013 では、NuGet は、"Microsoft および .NET"のパッケージ ソースを追加するには、%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config でカスタム Nuget.Config ファイルをインストールします。 結果として、ソリューションでカスタム repositoryPath の使用に関する解決策 -"Microsoft および .NET"のパッケージ ソースを削除することにもコンピューター レベル Nuget.Config を削除することでした。 階層の Nuget.Config ファイルを使用して NuGet 2.7.2 で今すぐ repositoryPath の優先順位の規則はします。

## <a name="all-changes"></a>すべての変更
作業の完全な一覧の項目で修正された NuGet 2.7.2、くださいビュー、[このリリースの NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)します。
