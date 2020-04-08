---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "68860573"
---
[restore](../../reference/cli-reference/cli-ref-restore.md) コマンドを使用すると、*packages* フォルダーにないすべてのパッケージがダウンロードされ、インストールされます。

PackageReference に移行されたプロジェクトの場合は、代わりに [msbuild -t:restore](../package-restore.md#restore-using-msbuild) を使ってパッケージを復元します。

`restore` ではパッケージがディスクに追加されるだけで、プロジェクトの依存関係は変更されません。 プロジェクトの依存関係を復元するには、`packages.config` を変更し、`restore` コマンドを使用します。

他の `nuget.exe` CLI コマンドと同様に、最初にコマンド ラインが開かれ、使用するプロジェクト ファイルが含まれているディレクトリに切り替えられます。

`restore` を使用してパッケージを復元するには:

```cli
nuget restore MySolution.sln
```