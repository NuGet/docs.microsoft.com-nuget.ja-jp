---
title: NuGet PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールで使用できる PowerShell コマンドの完全なリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 45c8be9956ceaab844bdcd89f1b96adc256f805c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546665"
---
# <a name="powershell-reference"></a>PowerShell リファレンス

パッケージ マネージャー コンソールでは、以下に示す特定のコマンドを使用して、NuGet と対話する Windows 上の Visual Studio 内での PowerShell インターフェイスを提供します。 (コンソールは Visual Studio for mac で現在使用できません)コンソールの使用にガイドについては、次を参照してください。、[パッケージ マネージャー コンソール](../tools/package-manager-console.md)トピック。

> [!Tip]
> すべての PowerShell コマンドは、パッケージの使用にのみ関連します。 作成とパッケージは、他のパッケージのコンシューマーをすることもできますを除くパッケージを公開する PowerShell コマンドが関係ありません。

> [!Important]
> ここに表示するコマンドは、Visual Studio でパッケージ マネージャー コンソールに固有でありとは異なる、[パッケージ管理モジュールのコマンド](/powershell/module/packagemanagement/?view=powershell-6)一般的な PowerShell 環境では使用できます。 具体的には、各環境には、その他では使用できないコマンドと同じ名前のコマンドも特定の引数は、異なる場合があります。 Visual Studio でのパッケージの管理コンソールを使用する場合、コマンドとこのトピックに記載されている引数が適用されます。

| 一般的なコマンド | 説明 | NuGet のバージョン |
| --- | --- | --- |
| [Install-Package](ps-ref-install-package.md) | プロジェクトにパッケージとその依存関係をインストールします。 | すべて |
| [Update-Package](ps-ref-update-package.md) | パッケージとその依存関係、またはプロジェクト内のすべてのパッケージを更新します。 | すべて |
| [Find-Package](ps-ref-find-package.md) | パッケージ ID またはキーワードを使用してパッケージ ソースを検索します。 | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | 、ローカル リポジトリにインストールされているパッケージの一覧を取得またはパッケージのソースから使用可能なパッケージを一覧表示されます。 | すべて |

| セカンダリ コマンド | 説明 | NuGet のバージョン |
| --- | --- | --- |
| [Add-BindingRedirect](ps-ref-add-bindingredirect.md) | プロジェクトの出力パス内のすべてのアセンブリを調べ、バインド リダイレクトを追加、`app.config`または`web.config`必要な場所。 | すべて |
| [Get-Project](ps-ref-get-project.md) | 既定値または指定されたプロジェクトについての情報を表示します。 | 3.0+ |
| [Open-PackagePage](ps-ref-open-packagepage.md) | プロジェクト、ライセンス、またはレポートの指定したパッケージの URL の不正使用の既定のブラウザーを起動します。 | 3.0 + で非推奨とされます。 |
| [Register-TabExpansion](ps-ref-register-tabexpansion.md) | 一般的に使用されるパラメーターの値は、カスタマイズされた展開を作成することができます、コマンドのパラメーターにタブ拡張を登録します。 | すべて |
| [Sync-Package](ps-ref-sync-package.md) | バージョンには、パッケージがインストールされている get では、プロジェクトを指定し、ソリューション内のプロジェクトの他のバージョンが同期します。 | 3.0+ |
| [Uninstall-Package](ps-ref-uninstall-package.md) | 必要に応じてその依存関係を削除する、プロジェクトからパッケージを削除します。 | すべて |

コンソール内でこれらのコマンドのいずれかで完全かつ詳細なヘルプ、のみ対象のコマンド名を持つ、次を実行します。

```ps
Get-Help <command> -full
```

すべてのパッケージ マネージャー コンソール コマンドは、次をサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216):

- デバッグ
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- 詳細
- WarningAction
- WarningVariable

詳細については、 [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) PowerShell ドキュメントにします。
