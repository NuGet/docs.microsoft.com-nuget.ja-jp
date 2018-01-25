---
title: "NuGet 1.2 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 1.2 の既知の問題、バグの修正、追加された機能は、Dcr などのリリース ノートです。"
keywords: "NuGet 1.2 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cb9eb1cb8fc3a77fc297e04ce73aaf8e24fc557a
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-12-release-notes"></a>NuGet 1.2 リリース ノート

[NuGet 1.0 および 1.1 のリリース ノート](../release-notes/nuget-1.1.md) | [NuGet 1.3 リリース ノート](../release-notes/nuget-1.3.md)

NuGet 1.2 は、2011 年 3 月 30 日にリリースされました。

## <a name="new-features"></a>新機能

### <a name="framework-profile-support"></a>フレームワークのプロファイルのサポート

開始日から NuGet サポートされているを持つライブラリは、さまざまなフレームワークを対象します。 今すぐパッケージが Windows Phone のプロファイルなどの特定のプロファイルを対象とするアセンブリを含む可能性があります。 フレームワークの特定のプロファイルを対象とするには、プロファイルの省略形の後にダッシュを追加します。 たとえば、Windows Phone (Windows Phone 7 とも呼ばれます) で実行されている SilverLight を対象とするには、次のスクリーン ショットに示すよう sl3 wp フォルダーにアセンブリを配置ことができます。

![フレームワークのプロファイル フォルダーのレイアウト](./media/framework-profile-support.png)

なぜおだけを選択しなかった、モニカーとして"wp7"を使用するを依頼する場合があります。 一部にする Windows Phone 7 では、Silverlight の新しいバージョンを後で実行可能性があります、対象としている場合、どのフレームワーク プロファイルをに関する詳細を指定する必要がありますを予測しています。

### <a name="automatically-add-binding-redirects"></a>バインド リダイレクトを自動的に追加します。

パッケージを厳密な名前付きアセンブリをインストールするとき NuGet では、プロジェクトが必要なバインド リダイレクトをコンパイルし、それらを自動的に追加するプロジェクトの順序で構成ファイルに追加する場合が検出されます。 NuGet のバージョン管理というタイトルで David Ebbo のブログの投稿シリーズの一部 3"[バインド リダイレクトを使用して統一](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)"の詳細については、この機能の目的について説明します。

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>フレームワーク アセンブリ参照 (GAC) を指定します。

場合によっては、パッケージは、.NET Framework に含まれるアセンブリに依存可能性があります。 厳密には、必要はありません常に、パッケージのコンシューマーが、framework アセンブリを参照します。 場合によっては、ことが重要、開発者がそのアセンブリ内の型に対して、パッケージを使用するためにコードを記述する必要がある場合などです。 新しい`frameworkAssemblies`要素、メタデータ要素の子要素のセットを指定できます。 `frameworkAssembly` 、GAC 内の Framework アセンブリを指す要素。 Framework アセンブリに重点を置いてに注意してください。
これらのアセンブリは、.NET Framework の一部としてすべてのコンピューター上に存在したと見なされます、パッケージに含まれません。 次の表の属性の一覧、`frameworkAssembly`要素。


|属性 |説明|
|----------------|-----------|
|**assemblyName**|*必要な*します。 など、アセンブリの名前`System.Net`です。|
|**targetFramework**|*省略可能な*します。 フレームワークとプロファイル名 (またはエイリアス) を指定することにより、このフレームワーク アセンブリが"net40"または"sl4"などに適用されます。 説明されている同じ形式を使用して[複数のターゲット フレームワークをサポートする](../create-packages/supporting-multiple-target-frameworks.md)です。|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe は今すぐ API キー資格情報を格納することが

Nuget.exe コマンドライン ツールを使用する場合は、API キーを格納するようになりました SetApiKey コマンドを使用できます。 このように、パッケージをプッシュするたびに指定する必要はありません。 Nuget.exe と API キーを保存する方法の詳細については[パッケージを公開する方法、ドキュメントを読んで](../create-packages/publish-a-package.md)です。

### <a name="package-explorer"></a>パッケージ エクスプ ローラー
パッケージ エクスプ ローラーは、サポート NuGet 1.2 に更新されました。 詳細については、チェック アウト、[パッケージ エクスプ ローラーのリリース ノート](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)です。

## <a name="other-featuresfixes"></a>その他の機能/修正

上記の一覧は、多くの機能を実装しましたおよび修正は、バグの中で最も顕著でした。 すべては実装されている/修正[59 作業項目](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)今回のリリースでします。

## <a name="known-issues"></a>既知の問題

* **1.2 の非互換性をパッケージ化**: コマンド ライン ツールの最新バージョンでビルドされたパッケージ、nuget.exe (> 1.2) は、NuGet VS アドイン (1.1) などの古いバージョンでは動作しません。 互換性のないスキーマについて何かを示すエラー メッセージに実行するを実行する場合にこのエラーが発生します。 NuGet を最新バージョンに更新してください。
* **NuGet.Server 非互換性**: フィード NuGet.Server プロジェクトを使用して内部の NuGet をホストしている場合は、NuGet.Server の最新バージョンでそのプロジェクトを更新する必要があります。
* **署名の不一致エラー**: 署名の不一致に関するメッセージがアップグレード中にエラーが発生発生した場合は、NuGet をまずアンインストールしてからインストールする必要があります。 これに記載されて、[既知の問題のページ](../release-notes/Known-Issues.md)詳細を提供します。 問題は Visual Studio 2010 SP1 を実行しているユーザーに影響を与えるおよびバージョンが適切に署名できません NuGet 1.0 がインストールされているのみです。 このバージョンのみ利用可能となった、CodePlex web サイトから、短時間のため、この問題はならないに影響を与えるユーザーが多すぎます。