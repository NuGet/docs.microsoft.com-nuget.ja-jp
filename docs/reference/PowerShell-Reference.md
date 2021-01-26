---
title: NuGet PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールで使用できる PowerShell コマンドの完全なリファレンスです。
author: JonDouglas
ms.author: jodou
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 98bea8a225f4864953f898ef57b26e9093f7c2e9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779366"
---
# <a name="powershell-reference"></a>PowerShell リファレンス

パッケージマネージャーコンソールでは、Windows 上の Visual Studio 内で PowerShell インターフェイスを使用して、以下に示す特定のコマンドを使用して NuGet と対話します。 (コンソールは現在 Visual Studio for Mac では使用できません)。コンソールの使用ガイドについては、「 [パッケージマネージャーコンソールを使用したパッケージのインストールと管理](../consume-packages/install-use-packages-powershell.md) 」を参照してください。

> [!Tip]
> すべての PowerShell コマンドは、パッケージの使用のみに関連しています。 パッケージが他のパッケージのコンシューマーでもある場合を除き、パッケージの作成と公開に関連する PowerShell コマンドはありません。

> [!Important]
> ここに記載トされているコマンドは、Visual Studio のパッケージ マネージャー コンソールに固有のものであり、一般的な PowerShell 環境で使用できる[Package Management モジュール コマンド](/powershell/module/packagemanagement/?view=powershell-6)とは異なります。 具体的には、各環境には他の環境では使用できないコマンドがあり、同じ名前のコマンドでも特定の引数が異なる場合があります。 Visual Studio で Package Management コンソールを使用する場合、このトピックに記載されているコマンドと引数が適用されます。

| 一般的なコマンド | 説明 | NuGet のバージョン |
| --- | --- | --- |
| [Install-Package](ps-reference/ps-ref-install-package.md) | パッケージとその依存関係をプロジェクトにインストールします。 | すべて |
| [Update-Package](ps-reference/ps-ref-update-package.md) | パッケージとその依存関係、またはプロジェクト内のすべてのパッケージを更新します。 | すべて |
| [Find-Package](ps-reference/ps-ref-find-package.md) | パッケージ ID またはキーワードを使用してパッケージソースを検索します。 | 3.0 以上 |
| [Get-Package](ps-reference/ps-ref-get-package.md) | ローカルリポジトリにインストールされているパッケージの一覧を取得するか、パッケージソースから使用可能なパッケージを一覧表示します。 | すべて |

| セカンダリコマンド | 説明 | NuGet のバージョン |
| --- | --- | --- |
| [Add-BindingRedirect](ps-reference/ps-ref-add-bindingredirect.md) | プロジェクトの出力パス内のすべてのアセンブリを調べ、バインドリダイレクトをまたはに追加し `app.config` `web.config` ます (必要な場合)。 | すべて |
| [Get-Project](ps-reference/ps-ref-get-project.md) | 既定のプロジェクトまたは指定されたプロジェクトに関する情報を表示します。 | 3.0 以上 |
| [Open-PackagePage](ps-reference/ps-ref-open-packagepage.md) | 指定されたパッケージのプロジェクト、ライセンス、またはレポート不正使用の URL を使用して、既定のブラウザーを起動します。 | 3.0 以降では非推奨 |
| [登録/タブ拡張](ps-reference/ps-ref-register-tabexpansion.md) | コマンドのパラメーターにタブ拡張を登録します。これにより、よく使用されるパラメーター値用にカスタマイズされた展開を作成できます。 | すべて |
| [Sync-Package](ps-reference/ps-ref-sync-package.md) | 指定したプロジェクトからインストールされているパッケージのバージョンを取得し、そのバージョンをソリューション内の残りのプロジェクトと同期します。 | 3.0 以上 |
| [Uninstall-Package](ps-reference/ps-ref-uninstall-package.md) | プロジェクトからパッケージを削除し、必要に応じて依存関係を削除します。 | すべて |

コンソール内のこれらのコマンドの詳細なヘルプを表示するには、次のコマンドを実行します。

```ps
Get-Help <command> -full
```

すべてのパッケージマネージャーコンソールコマンドは、次の [一般的な PowerShell パラメーター](/powershell/module/microsoft.powershell.core/about/about_commonparameters)をサポートしています。

- デバッグ
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- "詳細"
- WarningAction
- WarningVariable

詳細については、PowerShell のドキュメントの [about_CommonParameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters) を参照してください。