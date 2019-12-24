---
title: NuGet 3.3 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.3 のリリースノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 482c03a4f6ca39edf317b6ef8d535e79b53d5d16
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317038"
---
# <a name="nuget-33-release-notes"></a>NuGet 3.3 リリースノート

[Nuget 3.2.1 リリースノート](../release-notes/nuget-3.2.1.md) | [nuget 3.4-RC リリースノート](../release-notes/nuget-3.4-RC.md)

NuGet 3.3 は、2015年11月30日にリリースされました。これには、ユーザーインターフェイスの更新とコマンドライン機能が多数あり、NuGet クライアントに対する有用な修正プログラムが集められています。

## <a name="new-features"></a>新機能

* 認証済みフィードで NuGet コマンドラインクライアントがシームレスに動作できるようにする資格情報プロバイダーが導入されました。 [Visual Studio Team Services 資格情報プロバイダーをインストール](../api/nuget-exe-credential-providers.md)し、それを使用するように nuget クライアントを構成する手順については、Nuget のドキュメントを参照してください。

## <a name="new-user-interface-features"></a>新しいユーザーインターフェイスの機能

* 使用可能なタブを個別に参照、インストール、および更新する
* 利用可能な更新プログラムが含まれているパッケージの数を示す更新可能なバッジ
* パッケージがインストールされているか、更新プログラムが利用可能かどうかを示すパッケージバッジ
* ダウンロード数と作成者がパッケージリストに追加されました
* パッケージ一覧に表示可能な最大バージョン番号と現在インストールされているバージョン番号
* パッケージリストからのクイックインストール、更新、およびアンインストールを可能にするアクションボタン
* パッケージ詳細パネルのより明確なアクションボタン
* パッケージの詳細パネルでのパッケージの更新日
* ソリューションビューの統合パネル
* ソリューションビューでのプロジェクトとインストールされているバージョン番号の並べ替え可能なグリッド

## <a name="new-command-line-features"></a>新しいコマンドライン機能

このバージョンでは、 `add` [nuget.exe リファレンス](../reference/nuget-exe-cli-reference.md)で説明されているように、フォルダーベースのリポジトリを初期化するコマンドと`init`コマンドを導入しました。 このフォルダー構造を使用して構築および管理されるリポジトリは、このブログで説明されているように、大幅なパフォーマンス上の[利点を提供](http://blog.nuget.org/20150922/Accelerate-Package-Source.html)します。

## <a name="contentfiles"></a>ContentFiles

新しい`project.json` フォルダー`contentFiles`と要素の表記`contentFiles`によって、マネージプロジェクトでコンテンツがサポートされるようになりました。 `.nuspec`  このコンテンツは、プロジェクトシステムとのやり取りのためにパッケージ作成者が直接指定できます。  `.nuspec`ドキュメントで contentfiles を構成する方法の詳細については、 [nuspec のリファレンスを参照](../reference/nuspec.md)してください。

## <a name="nuget-locals-cache-management"></a>NuGet ローカルキャッシュ管理

NuGet コマンドラインが更新され、ワークステーションでローカルキャッシュを管理する方法に関する情報が追加されました。  ローカルコマンドの詳細については、「 [NuGet コマンドラインリファレンス](../reference/cli-reference/cli-ref-locals.md)」を参照してください。

## <a name="fixed-issues"></a>修正済みの問題

**注目すべき問題**

* Mono- [1543](https://github.com/NuGet/Home/issues/1543)でソリューションファイルを使用してパッケージを復元するための NuGet コマンドラインによる復元

3\.3 リリースで解決された問題の完全な一覧については、「 [3.3 マイルストーン](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)」の GitHub を参照してください。

3\.3 コマンドラインリリースで修正された問題の一覧は、 [3.3 コマンドラインマイルストーン](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)に記録されます。

## <a name="known-issues"></a>既知の問題

GitHub の問題の一覧に関する問題は、引き続き次の場所にあります。[http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)