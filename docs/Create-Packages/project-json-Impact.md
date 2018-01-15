---
title: "project.json の NuGet パッケージの作成者に与える影響 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 983485df-9375-4827-b58b-70065320ee37
description: "NuGet 3.x での project.json の実装が、サポートされていない機能、コンテンツ、パッケージ形式などのパッケージの作成者にどのように影響するかの詳細です。"
keywords: "NuGet と project.json、project.json の影響、パッケージの作成に関する考慮事項、project.json の機能"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 69a6bbbe1c96b06dbba7ac787b836b8b62c438ec
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2018
---
# <a name="impact-of-projectjson-when-creating-packages"></a>パッケージを作成するときの project.json の影響

NuGet 3 以降で使用される `project.json` システムは、次のセクションで示されるように、いくつかの方法でパッケージの作成者に影響します。

## <a name="changes-affecting-existing-packages-usage"></a>既存のパッケージの使用方法に影響する変更

従来の NuGet パッケージでは、推移的な世界に引き継がれていない一連の機能がサポートされています。

### <a name="install-and-uninstall-scripts-are-ignored"></a>スクリプトのインストールとアンインストールが無視される

[依存関係の解決](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference-and-projectjson)に関するページで説明されている推移的な復元モデルには、"パッケージのインストール時刻" の概念はありません。 パッケージは存在するか、存在しないかのいずれかですが、パッケージのインストール時に発生する一貫性のあるプロセスはありません。

また、インストール スクリプトは、Visual Studio でのみサポートされていました。 他の IDE では、このようなスクリプトをサポートするには、Visual Studio 拡張 API を模擬表示する必要があり、一般的なエディターやコマンドライン ツールではサポートされていませんでした。

### <a name="content-transforms-are-not-supported"></a>コンテンツの変換がサポートされない

インストール スクリプトと同様に、変換はパッケージのインストールで実行され、通常はべき等ではありません。 インストール時刻は存在しなくなったため、XDT 変換と同様の機能はサポートされません。また、このようなパッケージが推移的なシナリオで使用される場合は無視されます。


### <a name="content"></a>Content

従来の NuGet パッケージでは、ソース コードや構成ファイルなどのコンテンツ ファイルを配布しています。 通常、次の 2 つのシナリオで使用されます。

1. 初期ファイルはプロジェクトにドロップされるため、ユーザーは後で編集することができます。 一般的な例は、既定の構成ファイルです。

2. コンテンツ ファイルはプロジェクトにインストールされているアセンブリの補完として使用されます。 こちらの例は、アセンブリによって使用されるロゴ イメージになります。

現在、コンテンツのサポートは、スクリプトや変換と同じような理由で無効にされていますが、Microsoft ではコンテンツのサポートの設計を進めています。

コンテンツ ファイルはパッケージ内で引き続き実行することができ、現在は無視されますが、エンド ユーザーは引き続き適切な位置にコピーできます。

コンテンツ ファイルを戻す提案のいずれかを表示でき、その進行状況はこちらで見守ることができます: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)。

## <a name="impact-for-package-authors"></a>パッケージの作成者への影響

上記の機能を使用するパッケージでは、別のメカニズムを使用する必要があります。 このために一般的に最も便利なメカニズムは、引き続き完全にサポートされる MSBuild ターゲット/プロパティになります。 ビルド システムでは、パッケージでその他の規則を選ぶことができます。 このようにして、MSBuild ターゲットが Roslyn アナライザーと同様にサポートされます。 `packages.config` と `project.json` シナリオ用にターゲットとアナライザーをサポートするパッケージをビルドできます。

スタートアップが簡単になるように、プロジェクトを変更しようとするパッケージは、通常、ごく限られたシナリオのセットで動作するため、代わりに readme、またはパッケージの使用方法に関するガイダンスを提供する必要があります。

以下に示すパッケージ形式を使用するには、既存のパッケージはほとんど必要ありません。

この形式では、最も重要視されるシナリオとしてネイティブ コンテンツを有効にします。 つまり、マネージ アセンブリは、ターゲット プラットフォームに基づいたマネージ アセンブリと一緒にバイナリの実装を配布する、ハードウェアの実装に近いかによって異なるということです。 たとえば、System.IO.Compression パッケージでは、このテクノロジを使用しています。 [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

要約すると、上記の機能が絶対に必要というわけではない場合、ここで説明されている形式は NuGet 3.x 以降によってのみサポートされるので、既存のパッケージ形式と一緒にしておくことをお勧めします。

shim を使用して `packages.config` と `project.json` の両方のシナリオに機能するように、パッケージをビルドすることはできますが、上述の使用されていない機能ではなく、従来の方法でパッケージを構築すると簡単なことが多いです。


## <a name="3x-package-format"></a>3.x のパッケージ形式  ##

3.x のパッケージ形式は、NuGet 2.x を超える次のいくつかの追加機能を許可します。

1. コンパイルに使用される参照アセンブリとさまざまなプラットフォーム/デバイス上のランタイムに使用される実装アセンブリのセットを定義する。 この機能では、コンシューマーに一般的なセキュリティを提供しながら、プラットフォーム固有の API を利用できるようにします。 特に、中間ポータブル ライブラリの記述が簡単になります。

2. パッケージがプラットフォーム (例: オペレーティング システム、CPU アーキテクチャ) でピボットすることを許可する。

3. コンパニオン パッケージに対してプラットフォーム固有の実装の分離を許可する。

4. 最も重要視される依存関係として、ネイティブの依存関係をサポートする。