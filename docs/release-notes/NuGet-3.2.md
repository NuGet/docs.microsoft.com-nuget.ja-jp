---
title: NuGet 3.2 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.2 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 38a56b1572770b02ff09135a3b0290742ca80f41
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780307"
---
# <a name="nuget-32-release-notes"></a>NuGet 3.2 リリースノート

[NuGet 3.2-RC リリースノート](../release-notes/nuget-3.2-RC.md)  | [NuGet 3.2.1 のリリースノート](../release-notes/nuget-3.2.1.md)

NuGet 3.2 は、3.1.1 リリースの改善と修正のコレクションとして2015年9月16日にリリースされ、 [dist.nuget.org](http://dist.nuget.org/index.html) と [Visual Studio ギャラリー](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015)の両方から入手できます。

## <a name="new-features"></a>新機能

* 同じフォルダーに存在するプロジェクトは `project.json` 、各プロジェクトに固有のフォルダー内に異なるファイルを持つことができるようになりました。  各プロジェクトについて、ファイルに名前を `project.json` `{ProjectName}.project.json` 付けます。 NuGet によって、各プロジェクトの構成が適切に設定されます。  これは、Windows 10 Tools v1.1 がインストールされている場合にのみサポートされます-  [1102](https://github.com/NuGet/Home/issues/1102)
* NuGet クライアントは、グローバル NUGET_PACKAGES 環境変数の指定をサポートしており、 `project.json` Windows 10 tools v1.1 でマネージプロジェクトで使用される共有グローバルパッケージフォルダーの場所を指定します。

## <a name="command-line-updates"></a>コマンドラインの更新

これは、NuGet v3 サーバーをサポートし、ファイルで管理されているプロジェクトのパッケージを復元する、nuget.exe クライアントの最初のバージョンです `project.json` 。

このリリースでは、クライアントとのやり取りを向上させるために、いくつかの認証済みフィードの問題が解決されました。

* インストール/復元の相互作用は、最初の要求の資格情報のみを認証されたフィードに送信する- [1300](https://github.com/NuGet/Home/issues/1300)、 [456](https://github.com/NuGet/Home/issues/456)
* プッシュコマンドでは、構成からの資格情報は解決されません- [1248](https://github.com/NuGet/Home/issues/1248)
* ユーザーエージェントとヘッダーが、統計の追跡に役立つように NuGet リポジトリに送信されるようになりました- [929](https://github.com/NuGet/Home/issues/929)

リモート NuGet リポジトリを操作しているときに、ネットワークエラーの処理を改善するために、いくつかの機能強化が行われています。

* リモートフィードに接続できない場合のエラーメッセージの改善- [1238](https://github.com/NuGet/Home/issues/1238)
* エラー状態が発生したときに正常に1を返すように NuGet restore コマンドを修正しました- [1186](https://github.com/NuGet/Home/issues/1186)
* 200ミリ秒ごとにネットワーク接続を再試行しています。 HTTP 5xx エラーが発生した場合、最大5回試行します。 [1120](https://github.com/NuGet/Home/issues/1120)
* プッシュコマンド中のサーバーリダイレクト応答の処理の改善- [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` では、引数として Nuget.Config の URL またはリポジトリ名がサポートされるようになりました- [1046](https://github.com/NuGet/Home/issues/1046)
* 復元中にリポジトリに見つからなかったパッケージは、警告[1038](https://github.com/NuGet/Home/issues/1038)ではなくエラーとして報告されるようになりました。
* Unix/Linux シナリオ用に \r\n の multipartwebrequest の処理を修正しました- [776](https://github.com/NuGet/Home/issues/776)

さまざまなコマンドに関して、いくつかの修正があります。

* プッシュコマンドでは、パッケージソースに対して PUT を実行する前に GET が実行されなくなりました- [1237](https://github.com/NuGet/Home/issues/1237)
* List コマンドはバージョン番号を繰り返しません- [1185](https://github.com/NuGet/Home/issues/1185)
* -Build 引数を使用したパックは、C# 6.0- [1107](https://github.com/NuGet/Home/issues/1107)を正しくサポートするようになりました
* Visual Studio 2015- [1048](https://github.com/NuGet/Home/issues/1048)でビルドされた F # プロジェクトをパックしようとした問題を修正しました
* パッケージが既に存在する場合は、今すぐ復元する- [1040](https://github.com/NuGet/Home/issues/1040)
* `packages.config`ファイルの形式が正しくない場合のエラーメッセージの改善- [1034](https://github.com/NuGet/Home/issues/1034)
* -SolutionDirectory スイッチで相対パスを使用して復元コマンドを修正しました- [992](https://github.com/NuGet/Home/issues/992)
* ソリューション全体の更新プログラムをサポートするための更新されたコマンドの改善- [924](https://github.com/NuGet/Home/issues/924)

このリリースで解決される問題の完全な一覧については、NuGet GitHub の [コマンドラインマイルストーン](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)を参照してください。

## <a name="visual-studio-extension-updates"></a>Visual Studio 拡張機能の更新

### <a name="new-features-in-visual-studio"></a>Visual Studio の新機能

* ソリューションをビルドしないでパッケージを復元できるようにする、ソリューションノードのソリューションエクスプローラーに新しいコンテキストメニュー項目が追加されました ([1274](https://github.com/NuGet/Home/issues/1274))。

![新しい [パッケージの復元] コンテキストメニュー項目](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Visual Studio の更新プログラムと修正プログラム

認証されたフィードの修正は、拡張機能でもロールアップおよびアドレス指定されました。  拡張機能では、次の認証項目もアドレス指定されています。

* V2 で認証されたフィードではなく、NuGet v3 で認証されたフィードを正しく正しく処理するようになりました- [1216](https://github.com/NuGet/Home/issues/1216)
* を使用 `project.json` し、v2 フィードと通信するプロジェクトの認証資格情報の要求を修正しました- [1082](https://github.com/NuGet/Home/issues/1082)

ネットワーク接続が Visual Studio のユーザーインターフェイスに影響を与え、次の修正によって解決されました。

* パッケージバージョンのローカルキャッシュのメンテナンスの向上- [1096](https://github.com/NuGet/Home/issues/1096)
* V3 フィードに接続するときのエラー動作が変更され、v2 フィードとして扱わないようになりました- [1253](https://github.com/NuGet/Home/issues/1253)
* 複数のパッケージソースを含むパッケージをインストールするときにインストールエラーが発生しないようにする- [1183](https://github.com/NuGet/Home/issues/1183)

ビルド操作との対話処理を改善しました。

* 1つのプロジェクトのパッケージの復元に失敗した場合にプロジェクトのビルドを続行する- [1169](https://github.com/NuGet/Home/issues/1169)
* ソリューション内の別のプロジェクトに依存しているプロジェクトにパッケージをインストールすると、ソリューションが強制的に再構築されます。 [981](https://github.com/NuGet/Home/issues/981)
* 失敗したパッケージのインストールを修正して、プロジェクトへの変更を適切にロールバックする- [1265](https://github.com/NuGet/Home/issues/1265)
* `developmentDependency`1263 でパッケージの属性の誤った削除を修正しました `packages.config`  -  [](https://github.com/NuGet/Home/issues/1263)
* への呼び出しで、 `install.ps1` 適切なオブジェクトが渡されました `$package.AssemblyReferences` - [1245](https://github.com/NuGet/Home/issues/1245)
* プロジェクトが正しくない状態にあるときに UWP プロジェクトのパッケージのアンインストールを妨げなくなりました- [1128](https://github.com/NuGet/Home/issues/1128)
* とプロジェクトの組み合わせを含むソリューション `packages.config` `project.json` が正しくビルドされるようになりました。2つ目のビルド操作は必要ありません- [1122](https://github.com/NuGet/Home/issues/1122)
* app.config ファイルがリンクされているか、別のフォルダーに配置されている場合に適切に検索する- [1111](https://github.com/NuGet/Home/issues/1111)、 [894](https://github.com/NuGet/Home/issues/894)
* UWP プロジェクトで、一覧にないパッケージをインストールできるようになりました- [1109](https://github.com/NuGet/Home/issues/1109)
* ソリューションが保存された状態ではないときに、パッケージの復元が許可されるようになりました- [1081](https://github.com/NuGet/Home/issues/1081)

構成ファイルの更新の処理が修正されました。

* マネージプロジェクトの後続のビルドでパッケージから配信されたターゲットファイルを削除しないよう `project.json` にする- [1288](https://github.com/NuGet/Home/issues/1288)
* ASP.NET 5 ソリューションビルド中に Nuget.Config ファイルを変更できなくなりました- [1201](https://github.com/NuGet/Home/issues/1201)
* パッケージの更新中に許可されているバージョンの制約を変更しなくなりました- [1130](https://github.com/NuGet/Home/issues/1130)
* ロックファイルは、ビルド中にロックされたままになります。 [1127](https://github.com/NuGet/Home/issues/1127)
* `packages.config`更新中に変更し、書き換えないようにする- [585](https://github.com/NuGet/Home/issues/585)

TFS ソース管理との相互作用が改善されました。

* TFS- [1164](https://github.com/NuGet/Home/issues/1164)、 [980](https://github.com/NuGet/Home/issues/980)にバインドされているパッケージのインストールに失敗しなくなりました
* TFS 2013 統合を許可するように NuGet ユーザーインターフェイスを修正しました- [1071](https://github.com/NuGet/Home/issues/1071)
* 正常に復元されたパッケージへの参照を、パッケージフォルダーから正しく取得しました- [1004](https://github.com/NuGet/Home/issues/1004)

最後に、これらの項目も改善されました。

* マネージプロジェクトのログメッセージの詳細度の詳細 `project.json` - [1163](https://github.com/NuGet/Home/issues/1163)
* インストールされているパッケージのバージョンがユーザーインターフェイスに正しく表示されるようになりました- [1061](https://github.com/NuGet/Home/issues/1061)
* Nuspec で指定された依存関係の範囲を持つパッケージは、安定したパッケージバージョンに対してインストール済みの依存関係のプレリリースバージョンを持つようになりました- [1304](https://github.com/NuGet/Home/issues/1304)

Visual Studio 拡張機能で解決される問題の完全な一覧については、「NuGet GitHub [3.2 マイルストーン](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)」を参照してください。

## <a name="known-issues"></a>既知の問題

GitHub の問題の一覧に関する問題は、引き続き次の場所にあります。 [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)