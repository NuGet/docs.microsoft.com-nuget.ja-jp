---
title: nuget.exe CLI を使用して NuGet パッケージを管理する
description: nuget.exe CLI を使用して NuGet パッケージを操作する方法。
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 7039dd27f2dddebc3c84e5ad35d5efec59547792
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428415"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>nuget.exe CLI を使用してパッケージを管理する

CLI ツールを使用すると、プロジェクトやソリューションで NuGet パッケージを簡単に更新し、復元できます。 このツールからは、Windows のすべての NuGet 機能が提供され、Mono で実行される場合の Mac と Linux のほとんどの機能も提供されます。

`nuget.exe` CLI は、.NET Framework プロジェクトと非 SDK スタイルのプロジェクト (例: .NET Standard ライブラリを対象とする非 SDK スタイルのプロジェクト) 用です。 `PackageReference` に移行された非 SDK スタイルのプロジェクトを使用している場合、代わりに `dotnet` CLI を使用してください。 `nuget.exe` CLI には、パッケージ参照のために [packages.config](../reference/packages-config.md) ファイルが必要になります。

> [!NOTE]
> ほとんどのシナリオでは、PackageReference に `packages.config` を使用する [非 SDK スタイルのプロジェクトを移行する](../consume-packages/migrate-packages-config-to-package-reference.md)ことをお勧めします。そうすることで、`nuget.exe` CLI の代わりに `dotnet` CLI を使用できます。 C++ プロジェクトと ASP.NET プロジェクトについては、現在のところ、移行を利用できません。

この記事では、最も一般的ないくつかの `nuget.exe` CLI コマンドの基本的な使用方法を説明します。 これらのコマンドの多くでは、コマンドにプロジェクト ファイルが指定されていない限り、CLI ツールは現在のディレクトリでプロジェクト ファイルを探します。 コマンドと使用できる引数の完全一覧については、「[nuget.exe CLI reference](../reference/nuget-exe-cli-reference.md)」(nuget.exe CLI リファレンス) を参照してください。

## <a name="prerequisites"></a>必須コンポーネント

- `nuget.exe` CLI をインストールします。[nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)からその `.exe`ファイルをダウンロードし、適切なフォルダーに保存して、そのフォルダーを PATH 環境変数に追加してください。

## <a name="install-a-package"></a>パッケージをインストールします

[install](../reference/cli-reference/cli-ref-install.md) コマンドでは、指定されたパッケージ ソースを利用し、パッケージがダウンロードされ、プロジェクトにインストールされます。既定では、現在のフォルダーにインストールされます。 プロジェクトのルート ディレクトリの *packages* フォルダーに新しいパッケージをインストールします。

> [!IMPORTANT]
> `install` コマンドではプロジェクト ファイルや *packages.config* が変更されることはありません。そのため、パッケージがディスクに追加されるだけであり、プロジェクトの依存関係が変更されないという点で `restore` と似ています。 依存関係を追加するには、Visual Studio でパッケージ マネージャー UI かコンソールを利用してパッケージ復元を追加するか、*packages.config* を変更し、`install` か `restore` を実行します。

1. コマンド ラインを開き、プロジェクト ファイルが含まれるディレクトリに切り替えます。

2. 次のコマンドを使用し、NuGet パッケージを *packages* フォルダーにインストールします。

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    `Newtonsoft.json` パッケージを *packages* フォルダーにインストールするには、次のコマンドを使用します。

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

あるいは、次のコマンドを使用すれば、既存の `packages.config` ファイルを使用する NuGet パッケージを *packages* フォルダーにインストールできます。 その場合、パッケージはプロジェクトの依存関係に追加されず、ローカルでインストールされます。

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>パッケージの特定のバージョンをインストールする

[install](../reference/cli-reference/cli-ref-install.md) コマンドを使用するとき、バージョンが指定されていない場合、NuGet では最新版のパッケージがインストールされまする 特定のバージョンの NuGet パッケージをインストールすることもできます。

```cli
nuget install <packageID | configFilePath> -Version <version>
```

たとえば、`Newtonsoft.json` パッケージのバージョン 12.0.1 を追加するには、このコマンドを使用します。

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

`install` の制限や動作については、「[Install a package](#install-a-package)」(パッケージのインストール) を参照してください。

## <a name="remove-a-package"></a>パッケージを削除する

1 つまたは複数のパッケージを削除するには、削除するパッケージを *packages* フォルダーから削除します。

パッケージを再インストールする場合、`restore` または `install` コマンドを使用します。

## <a name="list-packages"></a>パッケージを一覧表示する

[list](../reference/cli-reference/cli-ref-list.md) コマンドを使用し、特定のソースからパッケージの一覧を表示できます。 `-Source` オプションを使用し、検索を制限します。

```cli
nuget list -Source <source>
```

たとえば、*packages* フォルダーのパッケージを一覧表示します。

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

検索語句を使用する場合、検索には、パッケージの名前、タグ、パッケージの説明が含まれます。

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a>個別パッケージを更新する

NuGet では、パッケージ バージョンを指定しない限り、`install` コマンドを使用すると、最新版のパッケージがインストールされます。

## <a name="update-all-packages"></a>すべてのパッケージを更新する

すべてのパッケージを更新するには、[update](../reference/cli-reference/cli-ref-update.md) コマンドを使用します。 利用できる最も新しいバージョンに (`packages.config` を使用する) プロジェクトのすべてのパッケージを更新します。 `restore` は `update` を実行する前に実行することをお勧めします。

```cli
nuget update
```

## <a name="restore-packages"></a>パッケージの復元

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

## <a name="get-the-cli-version"></a>CLI バージョンを取得する

次のコマンドを実行します。

```cli
nuget help
```

ヘルプ出力の最初の行は、バージョンを示しています。 上へのスクロールを回避するには、代わりに `nuget help | more` を使用します。