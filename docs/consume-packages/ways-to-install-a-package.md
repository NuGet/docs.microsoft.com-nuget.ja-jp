---
title: Nuget パッケージのインストール方法
description: ディスクおよび適用可能なプロジェクト ファイルで何が発生するかなど、NuGet パッケージをプロジェクトにインストールするプロセスを説明します。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/12/2018
ms.topic: overview
ms.openlocfilehash: 5f71ce6217071efc3d483cde4cf36c5585808167
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34816931"
---
# <a name="different-ways-to-install-a-nuget-package"></a>NuGet パッケージをインストールするためのさまざまな方法

NuGet パッケージをダウンロードしてインストールするには、次の表に記載された方法のいずれかを使用できます (これらのツールをまだインストールしていない場合は、「[NuGet クライアント ツールのインストール](../install-nuget-client-tools.md)」を参照してください)。 パッケージは、ダウンロードする代わりにキャッシュから取得できる場合があります。

| メソッド | 説明 |
| --- | --- |
| dotnet.exe CLI<br/>`dotnet add package <package_name>` | (すべてのプラットフォーム) \<package_name\> で指定したパッケージを取得して、その内容を現在のディレクトリのフォルダーに展開し、参照をプロジェクト ファイルに追加します。 また、依存関係も取得してインストールします。<ul><li>[パッケージをインストールして使用する (dotnet CLI)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[dotnet add package コマンド](/dotnet/core/tools/dotnet-add-package)</li></ul> |
| パッケージ マネージャー UI (Visual Studio) | (Windows および Mac) 用意された UI を使用して、指定したパッケージ ソースからパッケージとその依存関係を参照して選択し、プロジェクトにインストールできます。 インストールされたプロジェクトへの参照をプロジェクト ファイルに追加します。<ul><li>[パッケージをインストールして使用する (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[パッケージ マネージャー UI のリファレンス (Windows)](../tools/package-manager-ui.md)</li><li>[プロジェクトに NuGet パッケージを含める (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| パッケージ マネージャー コンソール (Visual Studio)<br/>`Install-Package <package_name>` | (Windows のみ) 選択したソースから、\<package_name\> で指定したパッケージを取得して、ソリューションで指定されたプロジェクトにインストールし、参照をプロジェクト ファイルに追加します。 また、依存関係も取得してインストールします。<ul><li>[パッケージをインストールして使用する (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[パッケージ マネージャー コンソールのガイド](../tools/package-manager-console.md)</li></ul> |
| nuget.exe CLI<br/>`nuget install <package_name>` | (すべてのプラットフォーム) \<package_name\> で指定したパッケージを取得して、その内容を現在のディレクトリのフォルダーに展開します。`packages.config` ファイルでリストされたすべてのパッケージも取得できます。 また、依存関係を取得してインストールしますが、プロジェクト ファイルまたは `packages.config` は変更されません。<ul><li>[install コマンド](../tools/cli-ref-install.md)</li></ul> |

## <a name="what-happens-when-a-package-is-installed"></a>パッケージ インストールのしくみ

分かりやすく言うと、さまざまな NuGet ツールは通常、プロジェクト ファイルまたは `packages.config` にパッケージへの参照を作成し、次にパッケージの復元を実行することによって効果的にパッケージをインストールします。 ただし `nuget install` は例外です。この方法では `packages` フォルダーにパッケージを展開するのみで、その他のファイルは変更しません。

一般的なプロセスは次のとおりです。

1. (`nuget.exe` を除くすべてのツール) プロジェクト ファイルまたは `packages.config` に、パッケージ識別子とバージョンを記録します。

2. パッケージを取得します。
   - 「[グローバル パッケージとキャッシュ フォルダーの管理](managing-the-global-packages-and-cache-folders.md)」で説明されているように、パッケージが "*グローバル パッケージ*" フォルダーにインストール済みかどうかを (正確な識別子とバージョン番号によって) チェックします。

   - パッケージが "*グローバル パッケージ*" フォルダーにない場合、[構成ファイル](Configuring-NuGet-Behavior.md)でリストされているソースからパッケージの取得を試みます。 オンライン ソースの場合は、`nuget.exe` コマンドで `-NoCache` を指定するか、`dotnet restore` で `--no-cache` を指定しない限り、最初にキャッシュからパッケージを取得しようと試みます。 (Visual Studio と `dotnet add package` では常にキャッシュが使用されます。)パッケージがキャッシュから使用された場合、出力に "CACHE" と表示されます。 キャッシュには 30 分の有効期限があります。

   - パッケージがキャッシュにない場合、構成にリストされているソースからパッケージのダウンロードを試みます。 パッケージがダウンロードされると、出力に "GET" および "OK" と表示されます。

   - パッケージがいずれのソースからも正常に取得できない場合は、この時点でインストールが失敗し、[NU1103](../reference/errors-and-warnings.md#nu1103) などのエラーが発生します。 `nuget.exe` コマンドのエラーでは最後にチェックされたソースのみが表示されますが、実際にはいずれのソースからもパッケージをダウンロードできなかったことを意味しています。

   パッケージを取得するときに、NuGet の構成でのソースの順序が適用される場合があります。

   - PackageReference 形式を使用するプロジェクトの場合、NuGet では HTTP ソースをチェックする前に、ローカルのフォルダーとネットワーク共有からソースがチェックされます。

   - `packages.config` 管理形式を使用するプロジェクトの場合、NuGet では構成におけるソースの順序が使用されます。 ただし、復元操作の場合は例外的にソースの順序が無視され、最初に応答したソースのパッケージが使用されます。

   - 一般的に、特定の識別子およびバージョン番号を持つ任意のパッケージは、パッケージが見つかったソースにかかわらずまったく同じであるため、NuGet がソースを確認する順序に特定の意味はありません。

3. (`nuget.exe` を除くすべてのツール)「[グローバル パッケージとキャッシュ フォルダーの管理](managing-the-global-packages-and-cache-folders.md)」で説明されているように、パッケージのコピーとその他の情報を "*HTTP キャッシュ*" フォルダーに保存します。

4. ダウンロードが完了したら、ユーザーごとの "*グローバル パッケージ*" フォルダーにパッケージをインストールします。 NuGet では、パッケージの識別子ごとにサブフォルダーが作成され、次にインストールされるパッケージのバージョンごとにサブフォルダーが作成されます。

5. その他のプロジェクト ファイルとフォルダーを更新します。

    - PackageReference を使用するプロジェクトの場合は、`obj/project.assets.json` に格納されているパッケージの依存関係グラフを更新します。 パッケージの内容自体はいずれのプロジェクト フォルダーにもコピーされません。
    - `packages.config` を使用するプロジェクトの場合は、展開されたパッケージのうちプロジェクトのターゲット フレームワークに一致する部分を、プロジェクトの `packages` フォルダーにコピーします。 (`nuget install` を使用する場合は、展開されたパッケージの全体がコピーされます。`nuget.exe` ではターゲット フレームワークを識別するためのプロジェクト ファイルの調査が行われないためです。)
    - パッケージで[ソースと構成ファイルの変換](../create-packages/source-and-config-file-transformations.md)が使用されている場合は、`app.config` や `web.config` を更新します。

6. プロジェクトにまだインストールされていない下位レベルの依存関係がある場合は、インストールします。 このプロセスでは、[依存関係の解決](../consume-packages/dependency-resolution.md)に関するページで説明されているように、パッケージのバージョンが更新される可能性があります。

7. (Visual Studio のみ) Visual Studio のウィンドウにパッケージの readme ファイルが表示されます (利用可能な場合)。

## <a name="related-articles"></a>関連記事

- [パッケージ使用の概要とワークフロー](../consume-packages/overview-and-workflow.md)
- [パッケージの検索と選択](../consume-packages/finding-and-choosing-packages.md)
- [NuGet キャッシュおよびグローバル パッケージ フォルダーの管理](managing-the-global-packages-and-cache-folders.md)
- [NuGet の動作を構成する](../consume-packages/configuring-nuget-behavior.md)
