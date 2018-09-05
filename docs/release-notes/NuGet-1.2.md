---
title: NuGet 1.2 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 1.2 リリース ノートです。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b47f73c1c225540226d3780e17053427b8ea4a8a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545688"
---
# <a name="nuget-12-release-notes"></a>NuGet 1.2 リリース ノート

[NuGet 1.0 および 1.1 のリリース ノート](../release-notes/nuget-1.1.md) | [NuGet 1.3 のリリース ノート](../release-notes/nuget-1.3.md)

NuGet 1.2 は、2011 年 3 月 30 日にリリースされました。

## <a name="new-features"></a>新機能

### <a name="framework-profile-support"></a>Framework のプロファイルのサポート

しなくては NuGet、最初からサポート ライブラリは、さまざまなフレームワークを対象します。 今すぐパッケージは、Windows Phone プロファイルなどの特定のプロファイルを対象とするアセンブリを含めることができます。 ターゲット フレームワークの特定のプロファイルをするには、プロファイルの省略形の後にダッシュを追加します。 たとえば、Windows Phone (Windows Phone 7 とも呼ばれます) で実行されている SilverLight を対象と、次のスクリーン ショットに示すように、sl3 wp フォルダーにアセンブリを配置できます。

![フレームワーク プロファイル フォルダーのレイアウト](./media/framework-profile-support.png)

なぜ"wp7"をモニカーとして使用する選択しなかっただけを要求する可能性があります。 Windows Phone 7 が Silverlight の新しいバージョンを後で実行、対象としたフレームワーク プロファイルについて詳細を指定する必要がありますにしていることを予測しています。

### <a name="automatically-add-binding-redirects"></a>バインド リダイレクトを自動的に追加します。

厳密な名前付きアセンブリを使用したパッケージをインストールするときに NuGet では、プロジェクトが必要なバインド リダイレクトは、プロジェクトをコンパイルして、自動的に追加するために、構成ファイルに追加する場合が検出されます。 NuGet のバージョン管理というタイトルの David Ebbo のブログ投稿のパート 3"[バインド リダイレクトを使用して統一](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)"の詳細については、この機能の目的について説明します。

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>フレームワーク アセンブリ参照 (GAC) の指定

場合によっては、パッケージは、.NET Framework に含まれるアセンブリに依存可能性があります。 厳密に言う必要はありません常に、パッケージのコンシューマーがフレームワーク アセンブリを参照します。 場合によっては、開発者が、パッケージを使用するためにコード アセンブリ内の型を記述する必要がある場合など、重要です。 新しい`frameworkAssemblies`要素であるメタデータの要素の子要素のセットを指定できます。`frameworkAssembly`要素は、GAC 内のフレームワーク アセンブリをポイントします。 Framework アセンブリに重点を置いたに注意してください。
これらのアセンブリは、.NET Framework の一部としてすべてのコンピューター上に存在したと見なされます、パッケージには含まれません。 次の表の属性の一覧、`frameworkAssembly`要素。


|属性 |説明|
|----------------|-----------|
|**assemblyName**|*必要な*します。 など、アセンブリの名前`System.Net`します。|
|**targetFramework**|*省略可能な*します。 フレームワークとプロファイル名 (またはエイリアス) を指定することにより、このフレームワーク アセンブリが"net40"または"sl4"などに適用されます。 説明されている同じ形式を使用して[複数のターゲット フレームワークをサポートしている](../create-packages/supporting-multiple-target-frameworks.md)します。|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe はこれで API キーの資格情報を格納することが

Nuget.exe コマンドライン ツールを使用する場合は、API キーを格納するようになりました SetApiKey コマンドを使用できます。 これにより、パッケージをプッシュするたびに、これを指定する必要はありません。 Nuget.exe を使用して、API キーを保存の詳細については[パッケージを公開する方法のドキュメントを読む](../create-packages/publish-a-package.md)します。

### <a name="package-explorer"></a>パッケージ エクスプ ローラー
NuGet 1.2 をサポートするパッケージ エクスプ ローラーが更新されました。 詳細については、チェック アウト、[パッケージ エクスプ ローラーのリリース ノート](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)します。

## <a name="other-featuresfixes"></a>その他の機能/修正

上記の一覧が、最も顕著な多くの機能を実装しましたとバグを修正しました。 すべてを実装/修正[59 作業項目](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)このリリースでします。

## <a name="known-issues"></a>既知の問題

* **1.2 パッケージの非互換性の**: パッケージは、コマンド ライン ツールの最新バージョンで構築された、nuget.exe (1.2 >) は、NuGet VS アドイン (1.1) などの以前のバージョンでは機能しません。 互換性のないスキーマについて何かを示すエラー メッセージに実行する場合にこのエラーが発生しています。 NuGet を最新バージョンに更新してください。
* **NuGet.Server の非互換性**: フィード、NuGet.Server プロジェクトを使用して内部の NuGet をホストしている場合は、最新バージョンの NuGet.Server でそのプロジェクトを更新する必要があります。
* **署名の不一致エラー**: 署名の不一致に関するメッセージが、アップグレード中にエラーを実行する場合、最初に NuGet をアンインストールし、インストールする必要があります。 これが記載されています、[既知の問題ページ](../release-notes/known-issues.md)の詳細を提供します。 のみ、問題は、Visual Studio 2010 SP1 を実行しているに影響し、インストールが正しく署名されていない NuGet 1.0 のバージョンします。 このバージョンのみしました CodePlex web サイトから使用可能な短時間のため、この問題は多数のユーザーに影響しません。