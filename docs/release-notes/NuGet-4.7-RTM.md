---
title: NuGet 4.7 RTM リリース ノート
description: NuGet 4.7.0 のリリース ノートです。既知の問題、バグ修正、追加機能、および DCR を含みます。
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: 2290025d42dcd5704b6b019c17346201fe6a990d
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813794"
---
# <a name="nuget-47-release-notes"></a>NuGet 4.7 リリース ノート

[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) には、[NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe) が付属しています。

## <a name="summary-whats-new-in-470"></a>概要:4.7.0 の新機能

* パッケージの署名が拡張され、[リポジトリの署名付きパッケージ](https://github.com/NuGet/Home/wiki/Repository-Signatures)が有効になりました。

* Visual Studio Version 15.7 では、[packages.config 形式を使用する既存のプロジェクトを移行して、代わりに PackageReference を使用する](../consume-packages/migrate-packages-config-to-package-reference.md)機能が導入されました。

## <a name="summary-whats-new-in-472"></a>概要:4.7.2 の新機能

* セキュリティ修正プログラム: ~/.nuget 内で作成されたファイルに対するアクセス許可の範囲が広すぎる [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-473"></a>概要:4.7.3 の新機能

* セキュリティ修正プログラム: NUPKG ディレクトリより上の NUPKG 内のファイルに相対パスが含まれる場合がある [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>既知の問題

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>右クリックのコンテキスト メニューで `Migrate packages.config to PackageReference...` オプションを使用できない

#### <a name="issue"></a>懸案事項

プロジェクトを最初に開いたとき、NuGet 操作を行うまで NuGet が初期化されていない場合があります。 これにより、`packages.config` または `References` 上の右クリックのコンテキスト メニューで、移行オプションが表示されません。

#### <a name="workaround"></a>回避策

次の NuGet アクションのいずれかを実行します。
* パッケージ マネージャー UI を開く - `References` を右クリックし、`Manage NuGet Packages...` を選択する
* パッケージ マネージャー コンソールを開く - `Tools > NuGet Package Manager` から、`Package Manager Console` を選択する
* NuGet 復元を実行する - ソリューション エクスプローラーのソリューション ノードを右クリックし、`Restore NuGet Packages` を選択する
* NuGet 復元もトリガーするプロジェクトをビルドする

これで、移行オプションを表示できるようになりました。 このオプションは ASP.NET と C++ のプロジェクト タイプではサポートされておらず、表示されません。

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>.NET Framework と NuGet での .NET Standard 2.0 の問題

.NET Standard とそのツールは、.NET Framework 4.6.1 をターゲットとするプロジェクトが、.NET Standard 2.0 以前をターゲットとする NuGet パッケージおよびプロジェクトを使用できるように設計されています。 [このドキュメント](https://github.com/dotnet/standard/issues/481)では、そのシナリオに関連する問題の概要、それらの問題を解決する計画、そのツールの今日の状態で展開できる解決策について説明します。

## <a name="top-issues-fixed-in-this-release"></a>このリリースで修正された主な問題

### <a name="bugs"></a>バグ

* .Net Core プロジェクト システムで、NuGet がデッドロック状態になる (新しい回帰)。 - [#6733](https://github.com/NuGet/Home/issues/6733)
* パック: TfmSpecificPackageFile をグロビング パスと共に使用すると、PackagePath が正しく構成されない - [#6726](https://github.com/NuGet/Home/issues/6726)
* パック: ispackable が明示的に設定されていない限り、Web API プロジェクトでパッケージを作成できない。 - [#6156](https://github.com/NuGet/Home/issues/6156)
* VS UI と PMC で、新しいパッケージを表示するのに 30 分かかる (nuget.exe ではすぐに表示される) - [#6657](https://github.com/NuGet/Home/issues/6657)
* 署名: SignatureUtility.GetCertificateChain(...) ですべてのチェーンの状態がチェックされない - [#6565](https://github.com/NuGet/Home/issues/6565)
* 署名: DER GeneralizedTime 処理を向上させる - [#6564](https://github.com/NuGet/Home/issues/6564)
* 署名: 改ざんされたパッケージをインストールするときに、VS で NU3002 エラーが表示されない - [#6337](https://github.com/NuGet/Home/issues/6337)
* lockFile.GetLibrary では大文字と小文字が区別される - [#6500](https://github.com/NuGet/Home/issues/6500)
* インストール/更新の復元コードと復元コードのパスが一致しない - [#3471](https://github.com/NuGet/Home/issues/3471)
* ソリューション PackageManager バージョン ComboBox で、キーボードを使用して区切りを選択できる - [#2606](https://github.com/NuGet/Home/issues/2606)
* ソースのサービス インデックスを読み込めない `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException:応答状態コードが成功を示さない: 403 (禁止) - [#2530](https://github.com/NuGet/Home/issues/2530)

### <a name="dcrs"></a>DCR

* X-NuGet-Session-Id ヘッダーを生成し、要求全体で関連付ける [機能提案] - [#5330](https://github.com/NuGet/Home/issues/5330)
* IV の API を使用して、Visual Studio 上で実行される復元操作の実行を待機するための方法を公開する。 - [#6029](https://github.com/NuGet/Home/issues/6029)
* NuGet.exe -NoServiceEndpoint でサービス URL のサフィックスの追加を回避する - [#6586](https://github.com/NuGet/Home/issues/6586)
* 補足バージョンにコミット ハッシュを追加する - [#6492](https://github.com/NuGet/Home/issues/6492)
* 署名: リポジトリの署名/副署名の削除を可能にする - [#6646](https://github.com/NuGet/Home/issues/6646)
* 署名: リポジトリの署名/副署名を削除するための API - [#6589](https://github.com/NuGet/Home/issues/6589)
* VS でソース情報をログに記録する - [#6527](https://github.com/NuGet/Home/issues/6527)
* /tools を TFM および RID でのみフィルター処理して、設定の XML を /tools フォルダーに配置できるようにする - [#6197](https://github.com/NuGet/Home/issues/6197)
* パック コマンドが . で始まるファイルを除外した場合、警告する  - [#3308](https://github.com/NuGet/Home/issues/3308)

[このリリースで修正されたすべての問題一覧](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
