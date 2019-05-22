---
ms.openlocfilehash: 48306e77a017c11fa7dc0d695e0177edf4e79d1e
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65975836"
---
# <a name="nuget-51-release-notes"></a>NuGet 5.1 リリース ノート

NuGet 配布の種類:

| NuGet のバージョン | 利用可能な Visual Studio バージョン| 利用可能な .NET SDK|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 バージョン 16.1](https://visualstudio.microsoft.com/downloads/) | [2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>.NET Core ワークロードと共に Visual Studio 2019 のインストール 

<sup>2</sup>.NET Core ワークロードと共に Visual Studio 2019 と省略可能なインストールとして利用可能

## <a name="summary-whats-new-in-51"></a>概要:5.1 の新機能新機能

* 適切な統合 CI/CD ワークフロー - 許可するように既に存在する場合は、パッケージのプッシュをスキップするサポート[#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Visual Studio では、便利なリンクを今すぐでは、パッケージの nuget.org ギャラリー ページ - [# から 5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* などの新しいアセットは .NET Core 3.0 のサポート[Targeting Pack](https://github.com/dotnet/cli/issues/10006)と[ランタイム パック](https://github.com/dotnet/cli/issues/10007)
  * NuGet の pack と restore サポートを対象として、ランタイム パッケージ参照を有効にする FrameworkReferences [#7342](https://github.com/NuGet/Home/issues/7342)
  * PackageDownload - でのサポート「ダウンロードのみ」パッケージ シナリオ[#7339](https://github.com/NuGet/Home/issues/7339)
  * Exlcude ランタイムと復元 (&)、検索結果からパックを対象とするグラフを使用して PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

**バグ**

* プラグイン: 例外の詳細は、プラグインの作成 - 中に失われた[#8057](https://github.com/NuGet/Home/issues/8057)

* 排他の下限の PackageReference の範囲では、ソースのいずれかの下限の境界が存在する場合は機能しません。 - [#8054](https://github.com/NuGet/Home/issues/8054)

* 向上 IsPackableFalseError メッセージ - [#8021](https://github.com/NuGet/Home/issues/8021)

* ロック ファイルのロックを再生成ファイル プロジェクト グラフが変更されたときにパッケージ化[#8019](https://github.com/NuGet/Home/issues/8019)

* プロジェクト システムのバグ:自動を取得する Nuget パッケージの削除 - [#8017](https://github.com/NuGet/Home/issues/8017)

* FrameworkReference を返すためのターゲットの追加 CollectPackageDownloads および CollectPackageReferences - と同様に[#8005](https://github.com/NuGet/Home/issues/8005)

* HTTP キャッシュ:RepositoryResources リソースは、バージョン管理された方法でキャッシュされません[#7997](https://github.com/NuGet/Home/issues/7997)

* ログ記録: - 詳細な例外の呼び出し履歴は報告されません[#7955](https://github.com/NuGet/Home/issues/7955)

* -HTTPS を使用するすべての NuGet Docs の Url を変更する[#7950](https://github.com/NuGet/Home/issues/7950)

* NU3024 警告メッセージの改善[#7933](https://github.com/NuGet/Home/issues/7933)

* ロック ファイルが更新されていないときに削除するには、packagereference [#7930](https://github.com/NuGet/Home/issues/7930)

* Nuspec - で licenseurl とライセンスの要素を検証するときに、エラー ケースの処理を向上させる[#7915](https://github.com/NuGet/Home/issues/7915)

* タブ ヘッダーをクリック「ファイルの場所を開く」の結果エラー - PM UI の右クリック[#7913](https://github.com/NuGet/Home/issues/7913)

* プラグイン: ログ - プラグイン プロセスの終了時に[#7907](https://github.com/NuGet/Home/issues/7907)

* プラグイン: ログ記録の datetime 値の高い衝突率[#7899](https://github.com/NuGet/Home/issues/7899)

* LicenseExpression - で、nuspec でが失敗した Manifest.ReadFrom [#7894](https://github.com/NuGet/Home/issues/7894)

* RestoreLockedMode:ProjectReference がカスタム AssemblyName - プロジェクトに参照するときに予期しない NU1004 [#7889](https://github.com/NuGet/Home/issues/7889)

* 例外のプラグインの起動が失敗したときに、適切なエラー メッセージ[#7857](https://github.com/NuGet/Home/issues/7857)

* NoOp 復元を行うときに避ける *. obj ディレクトリ - dgspec.json 書き込み[#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty が大文字と小文字の不一致 - でプロパティを生成に失敗する場合は true を = [#7843](https://github.com/NuGet/Home/issues/7843)

* 設定: パッケージ ソース パスに無効な文字がクラッシュする - VS [#7820](https://github.com/NuGet/Home/issues/7820)

* ロック ファイルが削除された場合の復元は、NoOp にロック ファイルを生成しません[#7807](https://github.com/NuGet/Home/issues/7807)

* ライセンスの URL と読み取り - メタデータ エラー ライセンス原因[#7547](https://github.com/NuGet/Home/issues/7547)

* 未処理の例外で V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)

* nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)

* 更新の署名の関連するシナリオを反映するように、エラーと警告 docs [#6498](https://github.com/NuGet/Home/issues/6498)

* アセット ファイルがプロジェクトの移動をより簡単には、有効にする相対パスを使用する必要があります[#4582](https://github.com/NuGet/Home/issues/4582)

**Dcr**

* プラグイン: - 診断ログの記録を有効にする[#7859](https://github.com/NuGet/Home/issues/7859)

* NetStandard 2.1 - make Tizen 6 マップ[#7773](https://github.com/NuGet/Home/issues/7773)

**[このリリースでは、5.1 RTM で修正されたすべての問題の一覧](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
