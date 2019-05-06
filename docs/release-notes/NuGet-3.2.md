---
title: NuGet 3.2 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 3.2 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5bdd2aa5621eead9ce79794052663cc2f8a63d45
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549523"
---
# <a name="nuget-32-release-notes"></a>NuGet 3.2 リリース ノート

[NuGet 3.2 RC リリース ノート](../release-notes/nuget-3.2-RC.md) | [NuGet 3.2.1 のリリース ノート](../release-notes/nuget-3.2.1.md)

NuGet 3.2 がリリースされた、2015 年 9 月 16日の機能強化と修正、3.1.1 のコレクションとしてリリースされ、両方からは[dist.nuget.org](http://dist.nuget.org/index.html)と[Visual Studio ギャラリー](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015)します。

## <a name="new-features"></a>新機能

* 同じフォルダーに置かれているプロジェクトを異なるようになりましたが`project.json`各プロジェクトに固有フォルダー内のファイル。  プロジェクトごとに、名前、`project.json`ファイル`{ProjectName}.project.json`と NuGet では、プロジェクトごとにその構成に優先順位を適切に指定されます。  これは Windows 10 のツール v1.1 がインストールされているのではサポートされてのみ[1102](https://github.com/NuGet/Home/issues/1102)
* NuGet クライアントをサポートで使用される共有のグローバル パッケージ フォルダーの場所を指定するグローバル NUGET_PACKAGES 環境変数を指定する`project.json`ツール v1.1 の Windows 10 を使用したプロジェクトを管理します。

## <a name="command-line-updates"></a>更新プログラムのコマンドライン

これは、NuGet v3 のサーバーをサポートする nuget.exe のクライアントの最初のバージョンで管理されているプロジェクトのパッケージを復元する`project.json`ファイル。

さまざまなクライアントとのやり取りを向上させるためには、このリリースで対処された認証済みフィードの問題が発生しました。

* インストール/復元の相互作用 - 認証済みフィードには、最初の要求の資格情報の送信だけ[1300](https://github.com/NuGet/Home/issues/1300)、 [456](https://github.com/NuGet/Home/issues/456)
* プッシュ コマンドで資格情報の構成 - からが解決しない[1248](https://github.com/NuGet/Home/issues/1248)
* ユーザー エージェントとヘッダーが統計情報の追跡のための NuGet リポジトリに送信されるようになりました[929](https://github.com/NuGet/Home/issues/929)

さまざまな NuGet リポジトリをリモートで作業しようとしています。 ネットワーク障害を処理しやすくする機能強化を行いました。

* -リモートのフィードに接続できない場合に、エラー メッセージが改善[1238](https://github.com/NuGet/Home/issues/1238)
* NuGet の復元コマンドを正しく - エラーが発生したときに、1 を返すを修正[1186](https://github.com/NuGet/Home/issues/1186)
* ネットワーク接続を今すぐ再試行すべての 200 の HTTP 5xx エラーの場合は 5 回の試行の最大[1120](https://github.com/NuGet/Home/issues/1120)
* プッシュ コマンドの中にサーバーのリダイレクト応答の処理を改善[1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` 引数として Nuget.Config から URL またはリポジトリのいずれかの名前になりました[1046](https://github.com/NuGet/Home/issues/1046)
* 復元中に、リポジトリに配置されていない不足しているパッケージが警告ではなくエラーとしてレポートされるようになりました[1038](https://github.com/NuGet/Home/issues/1038)
* Unix または Linux のシナリオに \r\n の multipartwebrequest 処理を修正[776](https://github.com/NuGet/Home/issues/776)

さまざまなコマンドを使用して問題の修正を数多くあります。

* プッシュ コマンドは、パッケージのソース - に対して put コマンドの前に GET を不要になったは[1237](https://github.com/NuGet/Home/issues/1237)
* 一覧のコマンドは、バージョン番号を不要になった繰り返されます[1185](https://github.com/NuGet/Home/issues/1185)
* パック-ビルド引数を持つようになりました正しく C# 6.0 のサポート[1107](https://github.com/NuGet/Home/issues/1107)
* F# プロジェクトをパックしようとしています修正された問題は、Visual Studio 2015 - で構築された[1048。](https://github.com/NuGet/Home/issues/1048)
* パッケージが既に存在 - ときに、ここでは機能を復元する[1040](https://github.com/NuGet/Home/issues/1040)
* 強化されたエラー メッセージ`packages.config`ファイル形式が正しくありません - [1034](https://github.com/NuGet/Home/issues/1034)
* -の相対パスを使用する - SolutionDirectory スイッチを使用して、復元コマンドを修正[992](https://github.com/NuGet/Home/issues/992)
* -ソリューション全体の更新をサポートする更新コマンドを改善[924](https://github.com/NuGet/Home/issues/924)

このリリースで対処された問題の完全な一覧は NuGet GitHub で見つかる[コマンド ライン マイルス トーン](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)します。

## <a name="visual-studio-extension-updates"></a>Visual Studio 拡張機能の更新

### <a name="new-features-in-visual-studio"></a>Visual Studio の新機能

* ソリューションを構築することがなく復元するパッケージは、ソリューション ノードをソリューション エクスプ ローラーに追加された新しいコンテキスト メニュー項目 ([1274](https://github.com/NuGet/Home/issues/1274))。

![新しいパッケージを復元する' コンテキスト メニュー項目](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>更新し、Visual Studio での修正

認証されたフィードの修正プログラム ロール アップされも、拡張機能で対処します。  拡張機能では、以下の認証がアドレス指定も。

* これで、認証済みフィードを適切に正しく NuGet v3 を扱う方法の代わりに v2 に認証済みフィード - と[1216](https://github.com/NuGet/Home/issues/1216)
* 認証の資格情報を使用してプロジェクトの修正要求`project.json`v2 フィード - との通信と[1082](https://github.com/NuGet/Home/issues/1082)

ネットワーク接続には、Visual Studio で、ユーザー インターフェイスが影響を受ける必要があるし、これを次の修正に対処しました。

* パッケージのバージョンのローカル キャッシュの保守性の向上[1096](https://github.com/NuGet/Home/issues/1096)
* V2 フィード - として扱うことを示す試行できなくにフィード v3 への接続時にエラーの動作を変更[1253](https://github.com/NuGet/Home/issues/1253)
* 複数のパッケージ ソースのパッケージをインストールするときに、インストールの失敗を防ぐようになりました[1183](https://github.com/NuGet/Home/issues/1183)

ビルド操作との対話の処理を改善しました。

* 1 つのプロジェクトが失敗する - のパッケージを復元する場合は、プロジェクトをビルドし続けるようになりました[1169](https://github.com/NuGet/Home/issues/1169)
* ソリューションの再構築 - を強制的にソリューション内の別のプロジェクトでの依存関係がプロジェクトにパッケージをインストールする[981](https://github.com/NuGet/Home/issues/981)
* -プロジェクトへの変更を正しくロールバックに失敗したパッケージのインストールを修正[1265](https://github.com/NuGet/Home/issues/1265)
* 不注意で削除の修正、`developmentDependency`属性でパッケージを`packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* 呼び出す`install.ps1`ある適切な`$package.AssemblyReferences`オブジェクトの成功 - [1245](https://github.com/NuGet/Home/issues/1245)
* プロジェクトが正常な状態で、UWP プロジェクトでパッケージのアンインストール妨げなく[1128](https://github.com/NuGet/Home/issues/1128)
* ソリューションの組み合わせを含む`packages.config`と`project.json`プロジェクトが正しく秒を必要とせずに組み込まれましたビルド操作 - [1122](https://github.com/NuGet/Home/issues/1122)
* リンクまたは別のフォルダーに配置された場合、app.config ファイルを正しく検索[1111](https://github.com/NuGet/Home/issues/1111)、 [894](https://github.com/NuGet/Home/issues/894)
* UWP プロジェクトが一覧にないパッケージをインストールできます[1109](https://github.com/NuGet/Home/issues/1109)
* ソリューションは、保存された状態ではありません、パッケージの復元が許可されるようになりました[1081](https://github.com/NuGet/Home/issues/1081)

ファイルが修正された構成の更新を処理するには。

* 以降のビルドのパッケージから配信される、ターゲット ファイルを削除できなく、`project.json`マネージ プロジェクト - [1288](https://github.com/NuGet/Home/issues/1288)
* ASP.NET 5 ソリューションのビルドの中に Nuget.Config ファイルを変更できなく[1201](https://github.com/NuGet/Home/issues/1201)
* パッケージの更新プログラムの中にバージョン制約を許可される変更できなく[1130](https://github.com/NuGet/Home/issues/1130)
* ロック ファイル今すぐロックされたままのビルド中に[1127](https://github.com/NuGet/Home/issues/1127)
* 今すぐ変更`packages.config`しない更新プログラムの中に書き直すことと[585](https://github.com/NuGet/Home/issues/585)

TFS ソース管理との相互作用が向上します。

* -TFS にバインドされているパッケージのインストールを不要になった失敗[番号 1164](https://github.com/NuGet/Home/issues/1164)、 [980](https://github.com/NuGet/Home/issues/980)
* 修正済みの NuGet ユーザー インターフェイスを TFS 2013 の統合 - [1071](https://github.com/NuGet/Home/issues/1071)
* パッケージ フォルダーから来るよう適切に復元されたパッケージへの参照を修正[1004](https://github.com/NuGet/Home/issues/1004)

最後に、これらの項目も改善されました。

* ログ メッセージの詳細度が小さくなります`project.json`マネージ プロジェクト - [1163。](https://github.com/NuGet/Home/issues/1163)
* ユーザー インターフェイス - に正しくインストールされているバージョンのパッケージを表示するようになりました[1061](https://github.com/NuGet/Home/issues/1061)
* 今すぐその nuspec で指定された依存関係の範囲を使用してパッケージの安定したパッケージのバージョンでは、インストールされているこれらの依存関係のプレリリース版がある[1304](https://github.com/NuGet/Home/issues/1304)

Visual Studio 拡張機能は、NuGet GitHub で見つかるの対処された問題の完全な一覧[3.2 マイルス トーン](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>既知の問題

GitHub の問題一覧上の問題を追跡するために引き続き。 [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)