---
title: "NuGet PowerShell リファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/2/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: cd08b869-44c6-480e-90f7-494a6d08e6d0
description: "Visual Studio で NuGet パッケージ マネージャー コンソールで利用できる PowerShell コマンドの完全な参照です。"
keywords: "NuGet パッケージ マネージャー コンソールで、NuGet Powershell コマンドでは、NuGet Powershell リファレンス"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c0da5c88447784fdd49d824bbd03b11f73c22ebc
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="powershell-reference"></a>PowerShell リファレンス

パッケージ マネージャー コンソールは、以下に示す特定のコマンドを使用して NuGet を使って操作する Windows 上の Visual Studio 内での PowerShell インターフェイスを提供します。 (コンソールは Visual Studio for mac で現在使用できません)コンソールの使用にについては、次を参照してください。、 [Package Manager Console](../tools/package-manager-console.md)トピックです。

> [!Tip]
> すべての PowerShell コマンドは、パッケージの消費量にのみ関連します。 PowerShell コマンドは、作成、およびパッケージには、他のパッケージのコンシューマーことができます。 その範囲内に以外のパッケージを公開には関連ありません。

> [!Important]
> ここに示すコマンドは、Visual Studio で、パッケージ マネージャー コンソールに固有とは異なる、[パッケージ管理モジュールのコマンド](https://msdn.microsoft.com/powershell/reference/6/packagemanagement/packagemanagement)一般的な PowerShell 環境で使用可能なことです。 具体的には、各環境には、他のでは使用できないコマンドと同じ名前のコマンドは特定の引数も異なる場合があります。 Visual Studio でパッケージの管理コンソールを使用すると、コマンドと引数のこのトピックに記載されていますが適用されます。

| 一般的なコマンド | 説明 | NuGet のバージョン |
| --- | --- | --- |
| [インストール パッケージ](ps-ref-install-package.md) | プロジェクトにパッケージとその依存関係をインストールします。 | すべて |
| [更新プログラム パッケージ](ps-ref-update-package.md) | パッケージとその依存関係またはプロジェクト内のすべてのパッケージを更新します。 | すべて |
| [Find-package](ps-ref-find-package.md) | パッケージ ID またはキーワードを使用して、パッケージ ソースを検索します。 | 3.0+ |
| [Get-package](ps-ref-get-package.md) | ローカル リポジトリにインストールされているパッケージの一覧を取得またはパッケージ ソースから使用可能なパッケージを一覧表示します。 | すべて |

| セカンダリ コマンド | 説明 | NuGet のバージョン |
| --- | --- | --- |
| [追加 BindingRedirect](ps-ref-add-bindingredirect.md) | プロジェクトの出力パス内のすべてのアセンブリを調べ、バインド リダイレクトを追加、`app.config`または`web.config`必要な場合です。 | すべて |
| [Get プロジェクト](ps-ref-get-project.md) | 既定値または指定したプロジェクトについての情報を表示します。 | 3.0+ |
| [開く PackagePage](ps-ref-open-packagepage.md) | プロジェクト、ライセンス、または指定したパッケージの不正使用を URL のレポートで既定のブラウザーを起動します。 | 3.0 以降で廃止されました |
| [レジスタ TabExpansion](ps-ref-register-tabexpansion.md) | 一般的に使用されるパラメーター値では、カスタマイズされた展開を作成することができます、コマンドのパラメーターにタブ拡張を登録します。 | すべて |
| [Sync パッケージ](ps-ref-sync-package.md) | バージョンがインストール パッケージから取得では、プロジェクトを指定し、ソリューション内のプロジェクトの残りの部分のバージョンを同期します。 | 3.0+ |
| [アンインストール パッケージ](ps-ref-uninstall-package.md) | 必要に応じてその依存関係を削除する、プロジェクトからパッケージを削除します。 | すべて |

コンソール内でこれらのコマンドのいずれかを完全かつ詳細なヘルプ、だけ対象のコマンド名を持つ、次を実行します。

```ps
Get-Help <command> -full
```

パッケージ マネージャー コンソールのすべてのコマンドは、次をサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216):

- デバッグ
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- 詳細
- WarningAction
- WarningVariable

詳細についてを参照してください[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) PowerShell ドキュメントにします。
