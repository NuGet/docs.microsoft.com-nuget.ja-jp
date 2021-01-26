---
title: NuGet 5.2 RTM リリースノート
description: 新機能、バグ修正、および DCRs を含む NuGet 5.2 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: 25fa1d09046a583fb987b9f3dd51a0099f4331a7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776212"
---
# <a name="nuget-52-release-notes"></a>NuGet 5.2 リリースノート

NuGet 配布の種類:

| NuGet のバージョン | 利用可能な Visual Studio バージョン| 利用可能な .NET SDK|
|:---|:---|:---|
| [**5.2.0 以降**](https://nuget.org/downloads) | [Visual Studio 2019 バージョン 16.2](https://visualstudio.microsoft.com/downloads/) | [2.1.80 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>、 [2.2.40 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>.NET Core ワークロードを含む Visual Studio 2019 と共にインストールされます。 

<sup>2</sup>.NET Core ワークロードを含む Visual Studio 2019 を使用したオプションのインストールとして利用可能

## <a name="summary-whats-new-in-52"></a>概要: 5.2 の新機能

* Linux & Mac [#7341](https://github.com/NuGet/Home/issues/7341)でのパスの問題により、NuGet 操作エラーが発生する可能性のある重大なバグを修正しました

* Visual Studio の NuGet パッケージマネージャー UI を使用したパッケージの参照時の UI の応答性の向上 (低速なソースの場合は特に顕著)- [#8039](https://github.com/NuGet/Home/issues/8039)

* ロックファイル ([#8187](https://github.com/NuGet/Home/issues/8187)、[#8160](https://github.com/NuGet/Home/issues/8160)、[#8114](https://github.com/NuGet/Home/issues/8114)、[#7840](https://github.com/NuGet/Home/issues/7840)) および認証プラグイン ([#8300](https://github.com/NuGet/Home/issues/8300)、[#8271、#8269](https://github.com/NuGet/Home/issues/8271)[、](https://github.com/NuGet/Home/issues/8269)[#8210](https://github.com/NuGet/Home/issues/8210)、[#8198](https://github.com/NuGet/Home/issues/8198)、[#7845](https://github.com/NuGet/Home/issues/7845)) に対する信頼性の高い修正プログラム

### <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

**バグ**

* パフォーマンス: パッケージマネージャーコンソール: UI 遅延更新 "Default project" combobox selected value- [#8235](https://github.com/NuGet/Home/issues/8235)

* パフォーマンス: PM UI [#8039](https://github.com/NuGet/Home/issues/8039)のパフォーマンスが向上しました。

* Perf: [#6824](https://github.com/NuGet/Home/issues/6824) PMC で既定のプロジェクトを読み取るときの UI 遅延

* Perf: [vsfeedback] ローカルパッケージソースに対して NuGet 更新タブがフリーズする- [#6470](https://github.com/NuGet/Home/issues/6470)

* プラグイン: プラグインの起動または終了に失敗した場合、NuGet は完全なハンドシェイクのタイムアウトを待機し [#8300](https://github.com/NuGet/Home/issues/8300)

* プラグイン: プラグイン起動エラーの diagnosability の改善- [#8271](https://github.com/NuGet/Home/issues/8271)

* プラグイン: 組み込みプラグインの nuget.exe 検出に関する問題- [#8269](https://github.com/NuGet/Home/issues/8269)

* プラグイン: キャッシュファイルが読み取り専用ではない [#8210](https://github.com/NuGet/Home/issues/8210)

* プラグイン: "タスクが取り消されました。" 復元中に認証プラグインでエラーが発生した [#8198](https://github.com/NuGet/Home/issues/8198)

* プラグインキャッシュが linux プラットフォームで断続的に検出されない- [#7845](https://github.com/NuGet/Home/issues/7845)

* LockFile: ATF では、ターゲットフレームワークの等価性の[#8187](https://github.com/NuGet/Home/issues/8187)チェックが無効なため、FALSE の NU1004 があります

* LockFile: '--locked-mode ' 復元フラグは、ロックファイルが空であるか、形式が正しくない場合には尊重されません [#8160](https://github.com/NuGet/Home/issues/8160)

* LockFile: パッケージのロックファイル[#8114](https://github.com/NuGet/Home/issues/8114)で、カスタムアセンブリ名を持つ小文字のプロジェクトは使用しないでください

* LockFile: プロジェクト参照の小文字をロックファイルに設定する- [#7840](https://github.com/NuGet/Home/issues/7840)

* 復元: 改ざんされた署名されたパッケージをインストールすると、複数のインストールが失敗する (出力が繰り返されます)- [#8175](https://github.com/NuGet/Home/issues/8175)

* VS: ソリューションユーザーオプションが NuGet の更新後に逆シリアル化に失敗する- [#8166](https://github.com/NuGet/Home/issues/8166)

* UnitTest プロジェクトの dotnet-package はエラーを返します- [#8154](https://github.com/NuGet/Home/issues/8154)

* VS インストーラーの NuGet パッケージグループを作成する-VSIX セットアップの問題を修正する- [#8033](https://github.com/NuGet/Home/issues/8033)

* GeneratePackageOnBuild で NoBuild を設定することはできません。 - [#7801](https://github.com/NuGet/Home/issues/7801)

* Nuspec ファイルに明示的なアセンブリ参照[#7638](https://github.com/NuGet/Home/issues/7638)要素が含まれている場合、新しいオプション "-packageformat snupkg" によってエラーが生成されます。

* Nuget.exe (498, 5): エラー: パス '/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341)の一部が見つかりませんでした

**DCR**

* PackageDownload がサポートされていることを示す msbuild プロパティを追加します- [#8106](https://github.com/NuGet/Home/issues/8106)

* FrameworkReference: FrameworkReference による依存関係フローを抑制します。 PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)

* パッケージ[#7351](https://github.com/NuGet/Home/issues/7351)の外部で runtime.jsを提供するメカニズム

**[このリリース-5.2 RTM で修正されるすべての問題の一覧](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**


