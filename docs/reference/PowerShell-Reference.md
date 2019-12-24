---
title: NuGet PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールで使用できる PowerShell コマンドの完全なリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 142af9c4f7d25c3b0d986524313851cceb1e4c60
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327929"
---
# <a name="powershell-reference"></a>PowerShell 参照

パッケージマネージャーコンソールでは、Windows 上の Visual Studio 内で PowerShell インターフェイスを使用して、以下に示す特定のコマンドを使用して NuGet と対話します。 (コンソールは現在 Visual Studio for Mac では使用できません)。コンソールの使用ガイドについては、「[パッケージマネージャーコンソールを使用したパッケージのインストールと管理](../consume-packages/install-use-packages-powershell.md)」を参照してください。

> [!Tip]
> すべての PowerShell コマンドは、パッケージの使用のみに関連しています。 パッケージが他のパッケージのコンシューマーでもある場合を除き、パッケージの作成と公開に関連する PowerShell コマンドはありません。

> [!Important]
> ここに記載されているコマンドは、Visual Studio のパッケージマネージャーコンソールに固有のものであり、一般的な PowerShell 環境で使用できる[Package Management モジュールコマンド](/powershell/module/packagemanagement/?view=powershell-6)とは異なります。 具体的には、各環境には、他の環境では使用できないコマンドがあり、同じ名前のコマンドが特定の引数で異なる場合もあります。 Visual Studio で Package Management コンソールを使用する場合は、このトピックに記載されているコマンドと引数が適用されます。

| 一般的なコマンド | 説明 | NuGet のバージョン |
| --- | --- | --- |
| [Install-Package](ps-reference/ps-ref-install-package.md) | パッケージとその依存関係をプロジェクトにインストールします。 | すべて |
| [Update-Package](ps-reference/ps-ref-update-package.md) | パッケージとその依存関係、またはプロジェクト内のすべてのパッケージを更新します。 | すべて |
| [Find-Package](ps-reference/ps-ref-find-package.md) | パッケージ ID またはキーワードを使用してパッケージソースを検索します。 | 3.0+ |
| [Get-Package](ps-reference/ps-ref-get-package.md) | ローカルリポジトリにインストールされているパッケージの一覧を取得するか、パッケージソースから使用可能なパッケージを一覧表示します。 | すべて |

| セカンダリコマンド | 説明 | NuGet のバージョン |
| --- | --- | --- |
| [Add-BindingRedirect](ps-reference/ps-ref-add-bindingredirect.md) | プロジェクトの出力パス内のすべてのアセンブリを調べ、バインドリダイレクト`app.config`をまたはに追加します ( `web.config`必要な場合)。 | すべて |
| [Get-Project](ps-reference/ps-ref-get-project.md) | 既定のプロジェクトまたは指定されたプロジェクトに関する情報を表示します。 | 3.0+ |
| [Open-PackagePage](ps-reference/ps-ref-open-packagepage.md) | 指定されたパッケージのプロジェクト、ライセンス、またはレポート不正使用の URL を使用して、既定のブラウザーを起動します。 | 3\.0 以降では非推奨 |
| [Register-TabExpansion](ps-reference/ps-ref-register-tabexpansion.md) | コマンドのパラメーターにタブ拡張を登録します。これにより、よく使用されるパラメーター値用にカスタマイズされた展開を作成できます。 | すべて |
| [Sync-Package](ps-reference/ps-ref-sync-package.md) | 指定したプロジェクトからインストールされているパッケージのバージョンを取得し、そのバージョンをソリューション内の残りのプロジェクトと同期します。 | 3.0+ |
| [Uninstall-Package](ps-reference/ps-ref-uninstall-package.md) | プロジェクトからパッケージを削除し、必要に応じて依存関係を削除します。 | すべて |

コンソール内のこれらのコマンドの詳細なヘルプを表示するには、次のコマンドを実行します。

```ps
Get-Help <command> -full
```

すべてのパッケージマネージャーコンソールコマンドは、次の[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216)をサポートしています。

- Debug
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Verbose
- WarningAction
- WarningVariable

詳細については、PowerShell のドキュメントの[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216)を参照してください。
