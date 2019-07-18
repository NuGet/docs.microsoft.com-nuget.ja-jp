---
title: パッケージ インストールのしくみ
description: パッケージ インストール プロセスに関する詳細
author: karann-msft
ms.author: karann
ms.date: 0/20/2019
ms.topic: conceptual
ms.openlocfilehash: 9ea0e6d28fa7af6e4061f762ea9af06c3028c247
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427457"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a>NuGet パッケージのインストールのしくみ

分かりやすく言うと、さまざまな NuGet ツールは通常、プロジェクト ファイルまたは `packages.config` にパッケージへの参照を作成し、次にパッケージの復元を実行することによって効果的にパッケージをインストールします。 ただし `nuget install` は例外です。この方法では `packages` フォルダーにパッケージを展開するのみで、その他のファイルは変更しません。

一般的なプロセスは次のとおりです。

1. (`nuget.exe` を除くすべてのツール) プロジェクト ファイルまたは `packages.config` に、パッケージ識別子とバージョンを記録します。

   インストール ツールが Visual Studio か dotnet CLI の場合は、このツールは最初にパッケージをインストールしようとします。 互換性がない場合、パッケージはプロジェクト ファイルにも `packages.config` にも追加されません。

2. パッケージを取得します。
   - 「[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)」で説明されているように、パッケージが "*グローバル パッケージ*" フォルダーにインストール済みかどうかを (正確な識別子とバージョン番号によって) チェックします。

   - パッケージが "*グローバル パッケージ*" フォルダーにない場合、[構成ファイル](../consume-packages/Configuring-NuGet-Behavior.md)でリストされているソースからパッケージの取得を試みます。 オンライン ソースの場合は、`nuget.exe` コマンドで `-NoCache` を指定するか、`dotnet restore` で `--no-cache` を指定しない限り、最初に HTTP キャッシュからパッケージを取得しようと試みます。 (Visual Studio と `dotnet add package` では常にキャッシュが使用されます。)パッケージがキャッシュから使用された場合、出力に "CACHE" と表示されます。 キャッシュには 30 分の有効期限があります。

   - パッケージが HTTP キャッシュにない場合、構成にリストされているソースからパッケージのダウンロードを試みます。 パッケージがダウンロードされると、出力に "GET" および "OK" と表示されます。 NuGet では、通常の詳細度で http トラフィックが記録されます。

   - パッケージがいずれのソースからも正常に取得できない場合は、この時点でインストールが失敗し、[NU1103](../reference/errors-and-warnings/NU1103.md) などのエラーが発生します。 `nuget.exe` コマンドのエラーでは最後にチェックされたソースのみが表示されますが、実際にはいずれのソースからもパッケージをダウンロードできなかったことを意味しています。

   パッケージを取得するときに、NuGet の構成でのソースの順序が適用される場合があります。

   - NuGet では HTTP ソースをチェックする前に、ローカルのフォルダーとネットワーク共有からソースがチェックされます。

3. 「[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)」で説明されているように、パッケージのコピーとその他の情報を "*HTTP キャッシュ*" フォルダーに保存します。

4. ダウンロードが完了したら、ユーザーごとの "*グローバル パッケージ*" フォルダーにパッケージをインストールします。 NuGet では、パッケージの識別子ごとにサブフォルダーが作成され、次にインストールされるパッケージのバージョンごとにサブフォルダーが作成されます。

5. NuGet では、必要に応じて、パッケージの依存関係がインストールされます。 このプロセスでは、[依存関係の解決](../consume-packages/dependency-resolution.md)に関するページで説明されているように、パッケージのバージョンが更新される可能性があります。

6. その他のプロジェクト ファイルとフォルダーを更新します。

    - PackageReference を使用するプロジェクトの場合は、`obj/project.assets.json` に格納されているパッケージの依存関係グラフを更新します。 パッケージの内容自体はいずれのプロジェクト フォルダーにもコピーされません。
    - パッケージで[ソースと構成ファイルの変換](../create-packages/source-and-config-file-transformations.md)が使用されている場合は、`app.config` や `web.config` を更新します。

7. (Visual Studio のみ) Visual Studio のウィンドウにパッケージの readme ファイルが表示されます (利用可能な場合)。

それでは NuGet パッケージでの生産性の高いコーディングをお楽しみください。
