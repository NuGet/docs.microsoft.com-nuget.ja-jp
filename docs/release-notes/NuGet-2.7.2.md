---
title: NuGet 2.7.2 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.7.2 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7643bf930bca39684eb626fe737001bc3e3ea769
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776784"
---
# <a name="nuget-272-release-notes"></a>NuGet 2.7.2 のリリースノート

[NuGet 2.7.1 のリリースノート](../release-notes/nuget-2.7.1.md)  | [NuGet 2.8 リリースノート](../release-notes/nuget-2.8.md)

NuGet 2.7.2 は、2013年11月11日にリリースされました。

## <a name="noteworthy-bug-fixes-and-features"></a>注目すべきバグの修正と機能

### <a name="license-text"></a>ライセンスのテキスト
多くの場合、Microsoft では、Visual Studio の Web アプリケーションプロジェクトの既定のテンプレートの一部として、いくつかの一般的なオープンソースライブラリの NuGet パッケージが含まれています。 jQuery は、このタイプのライブラリの最もよく知られている例です。 製品と共に配信されるコンポーネントに関連付けられたサポート契約により、パッケージのスクリプトファイルには、パブリック nuget.org ギャラリーの同じパッケージにあるスクリプトファイルとは異なるライセンステキストが含まれています。 このテキストの違いにより、異なるライセンステキストブロックの結果としてパッケージの更新が続行されないようにして、スクリプトファイルのコンテンツハッシュ値が異なる (したがって、プロジェクト内で変更として扱われる) ようにすることができます。

この問題を軽減するために、NuGet 2.7.2 は、スクリプト作成者が、次のような特別にマークされたセクション内にライセンステキストブロックを含めることを許可します。

```
/************** NUGET: BEGIN LICENSE TEXT **************
    * The following code is licensed under the MIT license
    * Additional license information below is informational
    * only.
    ************** NUGET: END LICENSE TEXT ***************/
```

このブロックを含むコンテンツファイルを使用してパッケージを更新する場合、NuGet では、ブロックの内容が NuGet ギャラリーのバージョンと比較されることはありません。そのため、コンテンツファイルが元のコピーと一致しているかのように削除および更新できます。

このブロックは、開始行と終了行の任意の場所で発生する "NUGET: BEGIN LICENSE TEXT" と "NUGET: END LICENSE TEXT" というテキストで識別されます。  他の書式設定の要件は存在しないため、言語に関係なく、任意の種類のテキストファイルでこの機能を使用できます。

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>非フレームワークアセンブリのバインドリダイレクトを追加する
.NET Framework の一部であるアセンブリの場合、NuGet は、パッケージの更新時に、アプリケーションの構成ファイルへのバインドリダイレクトの追加をスキップします。 この修正は、アセンブリが .NET Framework の一部と見なされない場合でも、一部のアセンブリにバインドリダイレクトが追加されていない NuGet 2.7 の回帰に対処します。 NuGet 2.7.2 は、以前の NuGet 2.5 と2.6 の動作を復元し、バインドリダイレクトを追加します。

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Xamarin ツールがインストールされたポータブルライブラリのインストール
Xamarin の開発ツールがコンピューターにインストールされている場合、サポートされているフレームワーク構成データを変更して、既存のターゲットフレームワークの組み合わせと Xamarin フレームワークとの互換性を指定します。 バージョン2.7.2 では、NuGet はこれらの暗黙的な互換性規則を認識するようになりました。そのため、Xamarin プラットフォームを対象とする開発者は、Xamarin と互換性のあるものの、パッケージメタデータ自体に明示的にマークされていないポータブルライブラリを簡単にインストールできます。

### <a name="machine-wide-configuration-settings-honored"></a>コンピューター全体の構成設定が受け入れられる
階層 Nuget.Config ファイルを使用する場合、ソリューションルートに最も近い Nuget.Config ファイルに対して repositoryPath キーが受け入れられませんでした。 Visual Studio 2013 では、NuGet によって、"Microsoft と .NET" パッケージソースを追加するために、カスタムの Nuget.Config ファイルが% ProgramData% \NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config にインストールされます。 そのため、ソリューションでカスタム repositoryPath を使用するための回避策は、マシンレベルの Nuget.Config を削除することでした。これは、"Microsoft と .NET" パッケージソースを削除することを意味します。 2.7.2 では、階層的な Nuget.Config ファイルを使用する場合、repositoryPath の優先順位規則が使用されるようになりました。

## <a name="all-changes"></a>すべての変更
NuGet 2.7.2 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)を参照してください。
