---
title: NuGet 5.1 RTM リリースノート
description: 新機能、バグ修正、および DCRs を含む NuGet 5.1 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: d6f6bffc6b5fda9ee1b9d9830f6d7d3c0f5be654
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780132"
---
# <a name="nuget-51-release-notes"></a>NuGet 5.1 リリースノート

NuGet 配布の種類:

| NuGet のバージョン | 利用可能な Visual Studio バージョン| 利用可能な .NET SDK|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 バージョン 16.1](https://visualstudio.microsoft.com/downloads/) | [2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>、 [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>.NET Core ワークロードを含む Visual Studio 2019 と共にインストールされます。 

<sup>2</sup>.NET Core ワークロードを含む Visual Studio 2019 を使用したオプションのインストールとして利用可能

## <a name="summary-whats-new-in-51"></a>概要: 5.1 の新機能

* CI/CD ワークフローとの統合を強化するために既に存在する場合は、パッケージプッシュをスキップできるようになります。 [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Visual Studio で、パッケージの nuget.org ギャラリーページへの便利なリンクが提供されるようになりました [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* [ターゲットパック](https://github.com/dotnet/cli/issues/10006)や[ランタイムパック](https://github.com/dotnet/cli/issues/10007)など、新しい .net Core 3.0 資産のサポート
  * ターゲットおよびランタイムパッケージの参照を有効にするための FrameworkReferences の NuGet パックと復元のサポート- [#7342](https://github.com/NuGet/Home/issues/7342)
  * PackageDownload を使用した "ダウンロードのみ" パッケージのシナリオをサポートする- [#7339](https://github.com/NuGet/Home/issues/7339)
  * 検索結果からランタイムとターゲットパックを除外し & PackageType- [#7337](https://github.com/NuGet/Home/issues/7337)を使用してグラフを復元する

### <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

**バグ**

* プラグイン: プラグインの作成中に例外の詳細が失われました- [#8057](https://github.com/NuGet/Home/issues/8057)

* 排他的下限を持つ PackageReference range は、いずれかのソースに下限が存在する場合は機能しません。 - [#8054](https://github.com/NuGet/Home/issues/8054)

* Ispackablefalse エラーメッセージの改善- [#8021](https://github.com/NuGet/Home/issues/8021)

* パッケージロックファイル-プロジェクトグラフが変更したときにロックファイルを再生成する- [#8019](https://github.com/NuGet/Home/issues/8019)

* ProjectSystem のバグ: Nuget パッケージの自動削除の取得- [#8017](https://github.com/NuGet/Home/issues/8017)

* CollectPackageDownloads および[#8005](https://github.com/NuGet/Home/issues/8005) CollectPackageReferences と同様の frameworkreference を返すターゲットを追加します。

* HTTP キャッシュ: RepositoryResources リソースはバージョン管理された方法でキャッシュされていません- [#7997](https://github.com/NuGet/Home/issues/7997)

* ログ: 例外呼び出し履歴は詳細な詳細度で報告されません- [#7955](https://github.com/NuGet/Home/issues/7955)

* HTTPS を使用するようにすべての NuGet Docs Url を変更する [#7950](https://github.com/NuGet/Home/issues/7950)

* NU3024 の警告メッセージの改善- [#7933](https://github.com/NuGet/Home/issues/7933)

* packagereference が削除されたときにロックファイルが更新されない- [#7930](https://github.com/NuGet/Home/issues/7930)

* [#7915](https://github.com/NuGet/Home/issues/7915) nuspec で licenseurl と license 要素を検証するときのエラーケースの処理を改善する

* PM UI-タブヘッダーを右クリックし、[ファイルの場所を開く] をクリックすると、エラー [#7913](https://github.com/NuGet/Home/issues/7913)

* プラグイン: プラグインプロセスが終了したときにログを記録する- [#7907](https://github.com/NuGet/Home/issues/7907)

* プラグイン: ログに記録される datetime 値の競合率が高い- [#7899](https://github.com/NuGet/Home/issues/7899)

* LicenseExpression Expression で nuspec を使用すると、すべての[](https://github.com/NuGet/Home/issues/7894)で失敗します。

* RestoreLockedMode: ProjectReference がカスタム AssemblyName [#7889](https://github.com/NuGet/Home/issues/7889)を持つプロジェクトを参照しているときに、予期しない NU1004 があります

* プラグインの起動が例外で失敗した場合のエラーメッセージの改善- [#7857](https://github.com/NuGet/Home/issues/7857)

* NoOp 復元を実行する場合は、obj ディレクトリへの書き込み時に * .dgspec.jsを避ける- [#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty = true は、ケースが一致しない場合にプロパティを生成できません- [#7843](https://github.com/NuGet/Home/issues/7843)

* 設定: パッケージソースパスに無効な文字があると、VS- [#7820](https://github.com/NuGet/Home/issues/7820)がクラッシュする可能性があります

* ロックファイルが削除された場合、restore では、NoOp でロックファイルが生成されません- [#7807](https://github.com/NuGet/Home/issues/7807)

* ライセンス URL とライセンスにより、メタデータで読み取りエラーが発生する- [#7547](https://github.com/NuGet/Home/issues/7547)

* [#7523](https://github.com/NuGet/Home/issues/7523) V2FeedParser でのハンドルされない例外

* 無効な引数の終了コード0が返さ nuget.exe- [#7178](https://github.com/NuGet/Home/issues/7178)

* 署名関連のシナリオを反映するようにエラーと警告ドキュメントを更新する- [#6498](https://github.com/NuGet/Home/issues/6498)

* アセットファイルは、相対パスを使用して、より簡単にプロジェクトを移動できるようにする必要があり [#4582](https://github.com/NuGet/Home/issues/4582)

**DCR**

* プラグイン: 診断ログを有効にする- [#7859](https://github.com/NuGet/Home/issues/7859)

* Tizen 6 を NetStandard 2.1 にマップする- [#7773](https://github.com/NuGet/Home/issues/7773)

**[このリリース-5.1 RTM で修正されるすべての問題の一覧](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
