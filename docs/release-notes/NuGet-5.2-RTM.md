---
title: NuGet 5.2 RTM リリースノート
description: 新機能、バグ修正、および DCRs を含む NuGet 5.2 のリリースノート。
author: karann-msft
ms.author: karann
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: f94bd8ddb8fac8bf47c2826bf5b417595b0efa8b
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471185"
---
# <a name="nuget-52-release-notes"></a>NuGet 5.2 リリースノート

NuGet 配布の種類:

| NuGet のバージョン | 利用可能な Visual Studio バージョン| 利用可能な .NET SDK|
|:---|:---|:---|
| [**5.2.0 以降**](https://nuget.org/downloads) | [Visual Studio 2019 バージョン16.2](https://visualstudio.microsoft.com/downloads/) | [2.1.80 X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>、 [2.2.40 X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>.NET Core ワークロードを含む Visual Studio 2019 と共にインストールされます。 

<sup>2</sup>.NET Core ワークロードを含む Visual Studio 2019 を使用したオプションのインストールとして利用可能

## <a name="summary-whats-new-in-52"></a>概要:5.2 の新機能

* Linux & Mac [#7341](https://github.com/NuGet/Home/issues/7341)でのパスの問題により、NuGet 操作エラーが発生する可能性のある重大なバグを修正しました

* Visual Studio の NuGet パッケージマネージャー UI を使用したパッケージの参照時の UI の応答性の向上 (低速なソースの場合は特に顕著)- [#8039](https://github.com/NuGet/Home/issues/8039)

* ロックファイル ([#8187](https://github.com/NuGet/Home/issues/8187)、[#8160](https://github.com/NuGet/Home/issues/8160)、[#8114](https://github.com/NuGet/Home/issues/8114)、[#7840](https://github.com/NuGet/Home/issues/7840)) および認証プラグイン ([#8300](https://github.com/NuGet/Home/issues/8300)、[#8271](https://github.com/NuGet/Home/issues/8271)、[#8269](https://github.com/NuGet/Home/issues/8269)、[#8210](https://github.com/NuGet/Home/issues/8210)、[#8198](https://github.com/NuGet/Home/issues/8198)、[#7845](https://github.com/NuGet/Home/issues/7845)) に対する信頼性の高い修正プログラム

### <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

**バグ**

* Perfパッケージマネージャーコンソール:UI 遅延更新 "Default project" combobox selected value- [#8235](https://github.com/NuGet/Home/issues/8235)

* PerfPM UI [#8039](https://github.com/NuGet/Home/issues/8039)のパフォーマンスの向上

* Perf[#6824](https://github.com/NuGet/Home/issues/6824) PMC で既定のプロジェクトを読み取るときの UI 遅延

* Perf: [vsfeedback] ローカルパッケージソースに対して NuGet 更新タブがフリーズする- [#6470](https://github.com/NuGet/Home/issues/6470)

* 済みプラグインの起動または終了に失敗した場合、NuGet は完全なハンドシェイクのタイムアウトを待機し[#8300](https://github.com/NuGet/Home/issues/8300)

* プラグイン: プラグイン起動エラーの diagnosability の改善- [#8271](https://github.com/NuGet/Home/issues/8271)

* 済み組み込みプラグインの nuget.exe 検出に関する問題- [#8269](https://github.com/NuGet/Home/issues/8269)

* プラグイン: キャッシュファイルが読み取り専用ではない[#8210](https://github.com/NuGet/Home/issues/8210)

* 済み"タスクが取り消されました。" 復元中に認証プラグインでエラーが発生した[#8198](https://github.com/NuGet/Home/issues/8198)

* プラグインキャッシュが linux プラットフォームで断続的に検出されない- [#7845](https://github.com/NuGet/Home/issues/7845)

* LockFile: ATF では、ターゲットフレームワークの等価性の[#8187](https://github.com/NuGet/Home/issues/8187)チェックが無効なため、FALSE の NU1004 があります

* LockFile: '--locked-mode ' 復元フラグは、ロックファイルが空であるか、形式が正しくない場合には尊重されません[#8160](https://github.com/NuGet/Home/issues/8160)

* LockFile:パッケージでカスタムアセンブリ名を持つ小文字のプロジェクトをロックする (ファイル[#8114](https://github.com/NuGet/Home/issues/8114)をロックする)

* LockFile:プロジェクト参照の小文字をロックファイルに使用する- [#7840](https://github.com/NuGet/Home/issues/7840)

* 復元: 改ざんされた署名されたパッケージをインストールすると、複数のインストールが失敗する (出力が繰り返されます)- [#8175](https://github.com/NuGet/Home/issues/8175)

* VS: ソリューションユーザーオプションが NuGet の更新後に逆シリアル化に失敗する- [#8166](https://github.com/NuGet/Home/issues/8166)

* UnitTest プロジェクトの dotnet-package はエラーを返します- [#8154](https://github.com/NuGet/Home/issues/8154)

* VS インストーラーの NuGet パッケージグループを作成する-VSIX セットアップの問題を修正する- [#8033](https://github.com/NuGet/Home/issues/8033)

* GeneratePackageOnBuild で NoBuild を設定することはできません。 - [#7801](https://github.com/NuGet/Home/issues/7801)

* Nuspec ファイルに明示的なアセンブリ参照[#7638](https://github.com/NuGet/Home/issues/7638)要素が含まれている場合、新しいオプション "-packageformat snupkg" によってエラーが生成されます。

* NuGet.targets(498,5): error :パス '/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341)の一部が見つかりませんでした

**DCR:**

* PackageDownload がサポートされていることを示す msbuild プロパティを追加します- [#8106](https://github.com/NuGet/Home/issues/8106)

* FrameworkReference: FrameworkReference による依存関係フローを抑制します。 PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)

* パッケージ[#7351](https://github.com/NuGet/Home/issues/7351)の外部でランタイムを指定するための機構

**[このリリース-5.2 RTM で修正されるすべての問題の一覧](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**


