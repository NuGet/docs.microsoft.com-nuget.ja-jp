---
title: NuGet 5.3 リリースノート
description: 新機能、バグ修正、および DCRs を含む NuGet 5.3 のリリースノート。
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: f16bfe5481009f7924a61f03233d288d25ac618f
ms.sourcegitcommit: f4bfdbf62302c95f1f39e81ccf998f8bbc6d56b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70774087"
---
# <a name="nuget-53-release-notes"></a>NuGet 5.3 リリースノート

NuGet 配布の種類:

| NuGet のバージョン | 利用可能な Visual Studio バージョン| 利用可能な .NET SDK|
|:---|:---|:---|
| [**5.3.0-preview3**](https://nuget.org/downloads) | [Visual Studio 2019 バージョン 16.3 Preview 3](https://visualstudio.microsoft.com/vs/preview/) | [3.0.100-preview9](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup> |

<sup>1</sup>.NET Core ワークロードを含む Visual Studio 2019 と共にインストールされます。

## <a name="summary-whats-new-in-53-preview-3"></a>概要:5.3 preview 3 の新機能

* パッケージアイコンは、外部 URL を必要とするのではなく、[パッケージに埋め込むことができ](../reference/msbuild-targets.md#packing-an-icon-image-file)ます。 - [#352](https://github.com/NuGet/Home/issues/352)

* パッケージの SHA の追跡と強制によるセキュリティ強化- [#7281](https://github.com/NuGet/Home/issues/7281)

### <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

**バグ**

* VS: アセンブリが完全に ngen されていません。 [#8513](https://github.com/NuGet/Home/issues/8513)

* メモリ使用量の削減 (イベントからのサブスクリプションの解除)- [#8471](https://github.com/NuGet/Home/issues/8471)

* "Error_UnableToFindProjectInfo" メッセージが文法的に正しくありません- [#8441](https://github.com/NuGet/Home/issues/8441)

* NU1403 の改善-すべてのパッケージを検証し、予期される/実際の sha 値を含めます- [#8424](https://github.com/NuGet/Home/issues/8424)

* [#8401](https://github.com/NuGet/Home/issues/8401) NuGetPackageManager 内の複数の列挙型

* PluginProcess の "パブリック > 内部" の変更を元に戻す- [#8390](https://github.com/NuGet/Home/issues/8390)

* IVsPackageSourceProvider (...) の例外動作が正しく定義されていません- [#8383](https://github.com/NuGet/Home/issues/8383)

* PluginManager コンストラクターを再度公開する- [#8379](https://github.com/NuGet/Home/issues/8379)

* PM UI [#8369](https://github.com/NuGet/Home/issues/8369)のリフレッシュレートを追跡するためのメトリック

* パッケージマネージャー UI を使用したインストール時の UI 更新の数を減らす- [#8358](https://github.com/NuGet/Home/issues/8358)

* テレメトリ: datetime 値はカルチャ固有の形式を使用する- [#8351](https://github.com/NuGet/Home/issues/8351)

* パッケージマネージャー UI の [参照] タブで UI の更新を減らす #6570- [#8339](https://github.com/NuGet/Home/issues/8339)

* [テストの失敗]"構成ファイルを解析できません" というメッセージが2回表示され[#8320](https://github.com/NuGet/Home/issues/8320)

* お客様の修正プログラムについて説明する適切なドキュメントページで、NU5037 エラーを発生させます (パッケージに必要な nuspec ファイルがありません)- [#8291](https://github.com/NuGet/Home/issues/8291)

* プロジェクトの RuntimeIdentifier が変更されると、ロックモードの復元が失敗する- [#8260](https://github.com/NuGet/Home/issues/8260)

* VS レイジー [#8156](https://github.com/NuGet/Home/issues/8156)で設定を読み取ります。

* ' Nuget ソースの追加 ' での回帰により、': ' 文字、16進数値0x3A は名前に含めることができません "エラー- [#7948](https://github.com/NuGet/Home/issues/7948)

* NuGet プラグイン資格情報プロバイダー-プロセスウィンドウを非表示にする- [#7511](https://github.com/NuGet/Home/issues/7511)

* 強制 PackagePathResolver は絶対パス[#7349](https://github.com/NuGet/Home/issues/7349)

* パッケージマネージャー UI の [インストール] タブと [更新] タブで UI の更新を減らす- [#6570](https://github.com/NuGet/Home/issues/6570)

**DCR:**

* NetStandard 2.1- [#8368](https://github.com/NuGet/Home/issues/8368)にマップするように Xamarin フレームワークを更新する

* パッケージマネージャーの [プレビューウィンドウ] の内容をインストール/更新用にコピーできるようにします。 [#8324](https://github.com/NuGet/Home/issues/8324)

* [Proj ファイルの復元を有効にする]- [#8212](https://github.com/NuGet/Home/issues/8212)

* 同時に`NUGET_NETCORE_PLUGIN_PATHS`両方の構成をサポートすると共`NUGET_NETFX_PLUGIN_PATHS`に - [#8151](https://github.com/NuGet/Home/issues/8151)

* バージョン属性を使用して PackageDownload の複数のバージョンを有効にする- [#8074](https://github.com/NuGet/Home/issues/8074)

* -SolutionDirectory オプションと-PackageDirectory オプションを nuget.exe pack- [#7163](https://github.com/NuGet/Home/issues/7163)に追加します。

* NuGet パックを決定的[#6229](https://github.com/NuGet/Home/issues/6229)にできるようにします

**[このリリースで修正されるすべての問題の一覧-5.3 preview 3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**
