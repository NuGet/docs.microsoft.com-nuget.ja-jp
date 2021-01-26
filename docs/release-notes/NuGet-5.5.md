---
title: NuGet 5.5 リリースノート
description: 新機能、バグ修正、および DCRs を含む NuGet 5.5 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0fde67dd03c31e986ed89f2f8627608e279ef908
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780114"
---
# <a name="nuget-55-release-notes"></a>NuGet 5.5 リリースノート

NuGet 配布の種類:

| NuGet のバージョン | 利用可能な Visual Studio バージョン| 利用可能な .NET SDK|
|:---|:---|:---|
| [**5.5.0**](https://nuget.org/downloads) | [Visual Studio 2019 バージョン 16.5](https://visualstudio.microsoft.com/downloads/) | [3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup>.NET Core ワークロードを含む Visual Studio 2019 と共にインストールされます。

## <a name="summary-whats-new-in-55"></a>概要: 5.5 の新機能

* Visual Studio の NuGet パッケージマネージャー UI のアクセシビリティとスクリーンリーダーエクスペリエンスが向上しました。
    * スクリーンリーダーエクスペリエンスでのアクセシビリティの問題、ショートカットテキストがない、インストールされたテキストボックスのアクセス可能な名前などが含まれている、- [#9059](https://github.com/NuGet/Home/issues/9059)
    * パッケージ一覧のスクリーンリーダーエクスペリエンスに関するアクセシビリティの問題- [#9077](https://github.com/NuGet/Home/issues/9077)
    * "参照"、"インストール"、"更新" タブに関連するスクリーンリーダーエクスペリエンスのアクセシビリティに関する問題- [#9078](https://github.com/NuGet/Home/issues/9078)
    * ナレーターは、"Blank"、"No Dependencies" "、" nuget.exe "、" MIT "のリンクラベルを発表しません [#9157](https://github.com/NuGet/Home/issues/9157)

* ローカルフィードでホストされているパッケージのための、Visual Studio パッケージマネージャー UI での自己完結型アイコンの表示のサポート- [#8189](https://github.com/NuGet/Home/issues/8189)

* `RestoreUseStaticGraphEvaluation`MSBuild スタティック Graph api を呼び出して評価を高速化する、を使用した非 op 復元パフォーマンスの大幅な向上- [8791](https://github.com/NuGet/Home/issues/8791)

* クロスプラットフォーム認証プラグインでの dotnet.exe の信頼性の向上
    * [#7842](https://github.com/NuGet/Home/issues/7842) TaskCanceledException で失敗 dotnet restore
    * プラグイン: "タスクが取り消されました"-これにより、ADO 認証に問題があります。 - [#8528](https://github.com/NuGet/Home/issues/8528)

* `dotnet nuget <add|remove|update|disable|enable|list> source`コマンド[#4126](https://github.com/NuGet/Home/issues/4126)の追加

* `--skip-duplicate`Dotnet nuget プッシュ[#8778](https://github.com/NuGet/Home/issues/8778)の使用に関するサポート

* `packages.config`Msbuild/restore を使用したサポート- [#8506](https://github.com/NuGet/Home/issues/8506)

### <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

**バグ**

* V3 Api を使用した Self-Updater の再作業- [#4197](https://github.com/NuGet/Home/issues/4197)

* パッケージの依存関係のバージョンが ' * ' に設定されている場合、パッケージの依存関係のバージョンが正しくありません- [#6697](https://github.com/NuGet/Home/issues/6697)

* ErrorUnsafePackageEntry エラーメッセージが問題の原因を指していません- [#7505](https://github.com/NuGet/Home/issues/7505)

* "*" シナリオでは、ロックファイルは受け入れられません- [#8073](https://github.com/NuGet/Home/issues/8073)

* PackageReference (MSBuild/Dotnet/VS restore do) を使用している場合、NuGet.exe はパッケージの最新バージョンに解決されません。- [#8432](https://github.com/NuGet/Home/issues/8432)

* dotnet list パッケージとマルチターゲット化 WPF プロジェクト- [#8463](https://github.com/NuGet/Home/issues/8463)

* ConcurrencyUtilities の向上 (CPU 使用率の削減)- [#8653](https://github.com/NuGet/Home/issues/8653)

* アンロードされたプロジェクトシナリオの DG 仕様は、プレビュー復元では記述できません- [#8793](https://github.com/NuGet/Home/issues/8793)

* Visual Studio NuGet パッケージ (RestoreManagerPackage) は、ソリューションビルドイベントに対して自動読み込みを行う必要があります- [#8796](https://github.com/NuGet/Home/issues/8796)

* .Vssettings 初期化- [#8842](https://github.com/NuGet/Home/issues/8842)のデッドロック

* プロジェクトがソリューションフォルダーに配置されている場合、VisualStudio ツールボックスは NuGet パッケージから設定されません- [#8868](https://github.com/NuGet/Home/issues/8868)

* VS: ソリューションの復元永続的が競合状態によって失敗する- [#8881](https://github.com/NuGet/Home/issues/8881)

* [インストール済み] タブおよび [検索] の定数 "読み込み中" <term>[更新] タブの [ [#8890](https://github.com/NuGet/Home/issues/8890)

* キャッシュの有効期限が切れた後、VS PM UI に埋め込みアイコンがない- [#9069](https://github.com/NuGet/Home/issues/9069)

* アドイン UI の起動 [#9112](https://github.com/NuGet/Home/issues/9112)

* Restore: IncludeExcludeFiles. Equals (...) の実装が正しくありません- [#9167](https://github.com/NuGet/Home/issues/9167)

* 復元: PackageSpec () は、等しくない複製を作成し [#9211](https://github.com/NuGet/Home/issues/9211)

* [ビルドがエラーで終了した場合は常にエラー一覧を表示する] がオンになっていない場合に表示されるエラー一覧 [#8190](https://github.com/NuGet/Home/issues/8190)

* 静的なグラフの復元では、空の SolutionPath を渡すことはできません- [#9061](https://github.com/NuGet/Home/issues/9061)

* 復元: 各プロジェクトのクロージャが4回[#9042](https://github.com/NuGet/Home/issues/9042)に計算されます。

* 復元: DependencyGraphSpec. Load (...) は JObject- [#9040](https://github.com/NuGet/Home/issues/9040)を必要としません

* 復元: 大きなオブジェクトヒープ (LOH) で作成された大きな文字列- [#9031](https://github.com/NuGet/Home/issues/9031)

* 新しい mono のカスタム nuget.exe が MSBuild SDK リゾルバー- [8848](https://github.com/NuGet/Home/issues/8848)のために壊れている可能性があります

* で nuget.dgspec.jsが "別のプロセスで使用されています"- [8692](https://github.com/NuGet/Home/issues/8692)の場合に復元が失敗する

**DCR**

* _GetRestoreProjectStyle のロジックはタスクの[#8804](https://github.com/NuGet/Home/issues/8804)である必要があります。

* [インストールされているタブに既定で非推奨情報を追加する]- [#8541](https://github.com/NuGet/Home/issues/8541)

**[このリリースで修正されるすべての問題の一覧-5.5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**
