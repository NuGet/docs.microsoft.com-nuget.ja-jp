---
title: NuGet 4.0 RC リリース ノート
description: NuGet 4.0 RC のリリース ノートであり、既知の問題、バグ修正、追加機能、および DCR が含まれています。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 8124b11d0489a2c72ffcfdde28e8528c1da1f677
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-40-rc-release-notes"></a>NuGet 4.0 RC リリース ノート

[NuGet 3.5 RTM リリース ノート](../release-notes/nuget-3.5-RTM.md)

[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) の焦点は .NET Core シナリオのサポートを追加することです。顧客からの重要なフィードバックに対処し、さまざまなシナリオにおけるパフォーマンスを改善します。 このリリースでは、PackageReference のサポート、MSBuild ターゲットとしての NuGet コマンド、バックグラウンド パッケージの復元など、いくつかの改善点があります。

## <a name="bug-fixes"></a>バグ修正

- `dotnet pack --version-suffix foo` の動作変更  -  [#3838](https://github.com/NuGet/Home/issues/3838)

- vs "15" コンピューターでのみ、nuget.exe 復元が失敗する - [#3834](https://github.com/NuGet/Home/issues/3834)

- .NETCore ファイルの新しいプロジェクトが復元中ビルドを阻む - [#3780](https://github.com/NuGet/Home/issues/3780)

- VS2015 から VS "15" へ移行した ASP.NET Core Web アプリを復元できない。 - [#3773](https://github.com/NuGet/Home/issues/3773)

- [テスト不合格] パッケージ ‘jQuery 検証’ を PM UI でアンインストールできない - [#3755](https://github.com/NuGet/Home/issues/3755)

- パッケージを UWP `project.json` にインストールするとき、親プロジェクトも復元されなければならない - [#3731](https://github.com/NuGet/Home/issues/3731)

- 詳細度を通常ではなく高にしてパッケージ ソースをログに記録するように NuGet ターゲットを変更する - [#3719](https://github.com/NuGet/Home/issues/3719)

- dotnet
  - dotnetcore pack3 には既定で XML ドキュメントを含める必要がある - [#3698](https://github.com/NuGet/Home/issues/3698)

- パッケージなしのソースが最初で、すべてのソースが選択されているとき、UI から一括更新できない - [#3696](https://github.com/NuGet/Home/issues/3696)

- Nuget パック コマンドにすべてのファイルが含まれない - [#3678](https://github.com/NuGet/Home/issues/3678)

- OOM 問題 - [#3661](https://github.com/NuGet/Home/issues/3661)

- アセット ファイルの ProjectFileDependencyGroups セクションでプロジェクトにライブラリ名を使用する必要がある - [#3611](https://github.com/NuGet/Home/issues/3611)

- "dotnet restore" と再帰するディレクトリ - [#3517](https://github.com/NuGet/Home/issues/3517)

- Restore3 の問題がエラーではなく警告としてログに記録される - [#3503](https://github.com/NuGet/Home/issues/3503)

- TFS 問題: "ワークスペースで [ファイル] が見つからないか、それにアクセスする許可がない" - [#2805](https://github.com/NuGet/Home/issues/2805)

- vs クイック起動検索ボックスに "nuget <packagename>" と入力すると、"nuget " プレフィックスが維持される - [#2719](https://github.com/NuGet/Home/issues/2719)

- System.Xml.XmlException: Core Properties パートのルート要素を認識できない。 ライン 2、位置 2。 - [#2718](https://github.com/NuGet/Home/issues/2718)

- テキスト フィールドの &lt; または &gt; をエスケープ処理すると、`.nuspec` がビルドされなくなる - [#2651](https://github.com/NuGet/Home/issues/2651)

- nuget.exe 削除で資格情報が求められない (非対話モードで) - [#2626](https://github.com/NuGet/Home/issues/2626)

- nuget.exe 削除でローカル ソースの API キーに関して、意味がない場合にも警告される - [#2625](https://github.com/NuGet/Home/issues/2625)

- EF プリパッケージのインストール時、エラー処理が望ましくない - [#2566](https://github.com/NuGet/Home/issues/2566)

- パッケージ マネージャーで選択を変更後、Visual Studio がクラッシュ - [#2551](https://github.com/NuGet/Home/issues/2551)

- dotnet
  - 浮動バージョンが使用されているとき、フラット リストのローカル リポジトリで、dotnetcore 復元が小文字と大文字を区別して ID を参照する - [#2516](https://github.com/NuGet/Home/issues/2516)

- V2 フィードで nuget.exe 削除が壊れる - [#2509](https://github.com/NuGet/Home/issues/2509)

- nuget.exe プッシュのタイムアウトでエラー メッセージの改善が必要 - [#2503](https://github.com/NuGet/Home/issues/2503)

- 適切なインポートなしのツール復元が警告なく失敗する。 - [#2462](https://github.com/NuGet/Home/issues/2462)

- nuget.org からインストールするときでも、プライベート フィードがあると、NuGet が資格情報の入力を求める - [#2346](https://github.com/NuGet/Home/issues/2346)

- ApplicationInsights 2.0 パッケージが一覧にあるが、存在しない - [#2317](https://github.com/NuGet/Home/issues/2317)

- VS "15" プレビュー 5 ブランチの UIDelay - [#3500](https://github.com/NuGet/Home/issues/3500)

- UWP のビルド中、復元に対して最初の OnBuild イベントがない - [#3489](https://github.com/NuGet/Home/issues/3489)

- PowerShell 5 で EntityFramework のインストールが中断される - [#3312](https://github.com/NuGet/Home/issues/3312)

- 詳細なログ記録にソースを追加 (3.5 で考慮) - [#3294](https://github.com/NuGet/Home/issues/3294)

- NoCache パラメーターが nuget クライアント バージョン 3.4+ で無視される - [#3074](https://github.com/NuGet/Home/issues/3074)

- 資格情報プロバイダーが VS に読み込まれないとき、NuGet が中断されない - [#2422](https://github.com/NuGet/Home/issues/2422)

## <a name="features"></a>フィーチャー

- x86 を実行するように CI を設定する - [#3868](https://github.com/NuGet/Home/issues/3868)

- 自動復元 3/3: 非ブロッキング UI - [#3658](https://github.com/NuGet/Home/issues/3658)

- 自動復元 2/3: 指名時のバックグラウンド復元 - [#3657](https://github.com/NuGet/Home/issues/3657)

- ビルド動作に一致するようにプロジェクト参照を復元 (再帰) - [#3615](https://github.com/NuGet/Home/issues/3615)

- VS "15" で DPL サポート - ミニバー - [#3614](https://github.com/NuGet/Home/issues/3614)

- 設定ファイルをプログラム ファイルに移動 - [#3613](https://github.com/NuGet/Home/issues/3613)

- 生成された復元 props と targets に複数のバージョン対応が必要 - [#3496](https://github.com/NuGet/Home/issues/3496)

- PackageTargetFallback の NuGet 復元サポート (以前のインポート) - [#3494](https://github.com/NuGet/Home/issues/3494)

- ToolsRef 実装 - [#3472](https://github.com/NuGet/Home/issues/3472)

- RID の Restore3 - [#3465](https://github.com/NuGet/Home/issues/3465)

- NuGet UI で PackageRefs の追加、削除、更新に対応 - [#3457](https://github.com/NuGet/Home/issues/3457)

- 自動復元 1/3: プロジェクト復元情報のキャッシュによる指定 API の実装 - [#3456](https://github.com/NuGet/Home/issues/3456)

- [0] NuGet 復元タスクとターゲット - [#2994](https://github.com/NuGet/Home/issues/2994)

- [1] MSBuild のソリューションレベル復元を有効にする - [#2993](https://github.com/NuGet/Home/issues/2993)

- Visual Studio で資格情報プロバイダーのパブリック拡張をサポート - [#2909](https://github.com/NuGet/Home/issues/2909)

- 再帰的 nuget 復元 - [#2533](https://github.com/NuGet/Home/issues/2533)

- dev15 で Microsoft.TeamFoundation.Client を読み込めず、VS "15" プレビューに関して、Microsoft.TeamFoundation.Client バージョンを 15.0 に更新する必要がある - [#2392](https://github.com/NuGet/Home/issues/2392)

- VS "15" プレビューで C++ UWP プロジェクトに C++ パッケージをインストールできない - [#2369](https://github.com/NuGet/Home/issues/2369)

- Nupkg で \buildCrossTargeting\ フォルダーをサポートする必要あり - また、"複数バージョン対応の" MSBuild スコープに `.targets` / `.props` をインポートする必要あり。 - [#3499](https://github.com/NuGet/Home/issues/3499)

- ToolsReference デザイン - [#3462](https://github.com/NuGet/Home/issues/3462)

- `.csproj` で復元と PackageReferences をサポートするように NuGet UI を修正  -  [#3455](https://github.com/NuGet/Home/issues/3455)

- VS パッケージ マネージャー設定にキャッシュ消去ボタンを追加 - [#3289](https://github.com/NuGet/Home/issues/3289)

## <a name="dcrs"></a>DCR

- 自動復元中、ソリューション復元を防ぐ必要あり。 - [#3797](https://github.com/NuGet/Home/issues/3797)

- NuGet パッケージ マネージャー UI からの NetCore インストールで、パッケージがサポートしているものではなく、すべての TFM にインストールされる - [#3721](https://github.com/NuGet/Home/issues/3721)

- 復元を指定する API で DotNetCliToolsReferences もサポートする必要あり。 - [#3702](https://github.com/NuGet/Home/issues/3702)

- VS "15" vsix をシステム コンポーネントとしてマークする - [#3700](https://github.com/NuGet/Home/issues/3700)

- 参照元 MS.VS.Services.Client から MS.VS.Services.Client.Interactive に移行する - [#3670](https://github.com/NuGet/Home/issues/3670)

- $(RestoreLegacyPackagesDirectory) は復元時、プロジェクト レベルで適用される必要あり - [#3618](https://github.com/NuGet/Home/issues/3618)

- シングル TargetFramework のプロジェクトに復元するとき、props を条件にするべきではない - [#3588](https://github.com/NuGet/Home/issues/3588)

- dotnet
  - dotnetcore restore3 foo.csproj は projectref 依存関係に従い、それらも復元する必要あり。 ビルドのように。 - [#3577](https://github.com/NuGet/Home/issues/3577)

- "type": "platform" 依存関係が "type" として表現される: ロック ファイルの "package" - [#2695](https://github.com/NuGet/Home/issues/2695)

- nuget.exe 詳細モードでダウンロード URL を表示する必要がある - [#2629](https://github.com/NuGet/Home/issues/2629)

- NuGet xplat を Microsoft.NetCore.App と netcoreapp1.0 に移動する - [#2483](https://github.com/NuGet/Home/issues/2483)

- プッシュ - コマンド ラインからプッシュするとき、シンボル サーバーを上書きできなければならない - [#2348](https://github.com/NuGet/Home/issues/2348)

- グローバル パッケージ パスを見つけるためにコードを連結する - [#2296](https://github.com/NuGet/Home/issues/2296)

- suppressParent よりもよい名前が必要 - [#2196](https://github.com/NuGet/Home/issues/2196)

- MSBuild プロジェクトに使用する `project.json` 依存関係名を決定する - [#1914](https://github.com/NuGet/Home/issues/1914)

- SemVer 2.0.0 サポートを NuGet.Core に追加 - [#3383](https://github.com/NuGet/Home/issues/3383)

- 推移的依存関係 NuPkgs と `.targets` を MSBuild で利用できるようにする - [#3342](https://github.com/NuGet/Home/issues/3342)

- コマンドラインからの NuGet 復元が VS より大幅に遅い - [#3330](https://github.com/NuGet/Home/issues/3330)

- パッケージ ID とバージョン比較で大文字と小文字を区別するようにする - [#2522](https://github.com/NuGet/Home/issues/2522)

- NoCache オプションが `packages.config` ベースの復元/インストールで機能しない (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)

- FindPackageByIdResource リソースに既定のキャッシュ コンテキストとロガーが必要 - [#1357](https://github.com/NuGet/Home/issues/1357)
