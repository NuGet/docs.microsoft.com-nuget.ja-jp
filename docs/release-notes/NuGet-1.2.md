---
title: NuGet 1.2 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 1.2 のリリースノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5d10d6bf27614980a144c30c3af6f9892a109061
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237188"
---
# <a name="nuget-12-release-notes"></a>NuGet 1.2 リリースノート

[NuGet 1.0 および1.1 のリリースノート](../release-notes/nuget-1.1.md)  | [NuGet 1.3 リリースノート](../release-notes/nuget-1.3.md)

NuGet 1.2 は、2011年3月30日にリリースされました。

## <a name="new-features"></a>新機能

### <a name="framework-profile-support"></a>フレームワークプロファイルのサポート

最初から、NuGet でサポートされているライブラリが異なるフレームワークを対象としています。 ただし、現在、パッケージには、Windows Phone プロファイルなどの特定のプロファイルを対象とするアセンブリを含めることができます。 フレームワークの特定のプロファイルをターゲットにするには、ダッシュの後にプロファイルの省略形を追加します。 たとえば、Windows Phone (Windows Phone 7) で実行されている SilverLight を対象にするには、次のスクリーンショットに示すように、sl3-wp フォルダーにアセンブリを配置します。

![フレームワークプロファイルフォルダーのレイアウト](./media/framework-profile-support.png)

モニカーとして "wp7" を使用することを選択しなかったのはなぜでしょうか。 ここでは、Windows Phone 7 が将来、Silverlight の新しいバージョンを実行する可能性があることを予測しています。その場合は、ターゲットとするフレームワークプロファイルについてより具体的な情報が必要になる場合があります。

### <a name="automatically-add-binding-redirects"></a>バインドリダイレクトを自動的に追加する

厳密な名前を持つアセンブリを含むパッケージをインストールする場合、NuGet では、プロジェクトをコンパイルして自動的に追加するために、バインドリダイレクトが構成ファイルに追加される必要があるケースを検出できるようになりました。 「[バインドリダイレクトを使用](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)した統合」では、David Ebbo のブログ投稿シリーズの第3部で、この機能の目的について詳しく説明しています。

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>フレームワークアセンブリ参照 (GAC) の指定

場合によっては、パッケージが .NET Framework 内のアセンブリに依存していることもあります。 厳密に言うと、パッケージのコンシューマーがフレームワークアセンブリを参照する必要は必ずしも必要ではありません。 ただし、場合によっては、パッケージを使用するために開発者がそのアセンブリ内の型に対してコードを記述する必要がある場合などにも重要です。 `frameworkAssemblies`メタデータ要素の子要素である新しい要素では、 `frameworkAssembly` GAC 内のフレームワークアセンブリを指す一連の要素を指定できます。 フレームワークアセンブリに重点を置いていることに注意してください。
これらのアセンブリは、すべてのコンピューターに .NET Framework の一部と見なされるため、パッケージには含まれません。 要素の属性を次の表に示し `frameworkAssembly` ます。


|属性 |説明|
|----------------|-----------|
|**assemblyName**|*[必須]* 。 などのアセンブリの名前 `System.Net` 。|
|**targetFramework**|*オプション* 。 このフレームワークアセンブリが適用されるフレームワークとプロファイル名 (またはエイリアス) を指定できます ("net40"、"sl4" など)。 では、「複数の [ターゲットフレームワークのサポート](../create-packages/supporting-multiple-target-frameworks.md)」で説明したのと同じ形式が使用されます。|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe が API キーの資格情報を保存できるようになりました

nuget.exe コマンドラインツールを使用する場合は、SetApiKey コマンドを使用して API キーを格納できるようになりました。 このようにして、パッケージをプッシュするたびに指定する必要はありません。 nuget.exe で API キーを保存する方法の詳細については、 [パッケージの公開に関するドキュメントを参照](../nuget-org/publish-a-package.md)してください。

### <a name="package-explorer"></a>パッケージエクスプローラー
NuGet 1.2 をサポートするように、パッケージエクスプローラーが更新されました。 詳細については、「 [Package Explorer のリリースノート](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)」を参照してください。

## <a name="other-featuresfixes"></a>その他の機能/修正

前の一覧は、実装した多くの機能と修正されたバグに最も顕著でした。 すべてについて、このリリースでは [59 作業項目](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) を実装または修正しています。

## <a name="known-issues"></a>既知の問題

* **1.2 パッケージの非互換性** : 最新バージョンのコマンドライン nuget.exe ツールでビルドされたパッケージ (> 1.2) は、以前のバージョンの NuGet VS アドイン (1.1 など) では動作しません。 互換性のないスキーマに関する情報を示すエラーメッセージが表示された場合は、このエラーが発生しています。 NuGet を最新バージョンに更新してください。
* **Nuget. サーバーの非互換性** : Nuget. server プロジェクトを使用して内部の nuget フィードをホストしている場合は、最新バージョンの Nuget. server を使用してそのプロジェクトを更新する必要があります。
* **署名の不一致エラー** : 署名の不一致に関するメッセージを含むアップグレード中にエラーが発生した場合は、まず NuGet をアンインストールしてからインストールする必要があります。 詳細については、 [既知の問題に関するページ](../release-notes/known-issues.md) を参照してください。 この問題は、Visual Studio 2010 SP1 を実行していて、正しく署名されていないバージョンの NuGet 1.0 がインストールされている場合にのみ影響します。 このバージョンは、CodePlex の web サイトから短時間のみ利用できるようになったため、この問題は多くの人間に影響を与えないようにしてください。