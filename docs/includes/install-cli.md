---
ms.openlocfilehash: 1f65939493cf423a76c024607264acee6c7e9050
ms.sourcegitcommit: ef08f376688f0191a8d3d873b6a4386afd799373
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2019
ms.locfileid: "66271548"
---
#### <a name="windows"></a>Windows

> [!Note]
> NuGet.exe 5.0 以降には、実行するために .NET Framework 4.7.2 以降が必要です。

1. [nuget.org/downloads](https://nuget.org/downloads) にアクセスして、NuGet 3.3 以降を選択します (2.8.6 は Mono と互換性がありません)。 常に最新バージョンが推奨され、パッケージを nuget.org に公開するには 4.1.0 以降が必要です。
1. 各ダウンロードは、直接 `nuget.exe` ファイルです。 ブラウザーで任意のフォルダーにファイルを保存します。 ファイルがインストーラーで*ない*場合、ブラウザーから直接実行しても何も表示されません。
1. `nuget.exe` をPATH 環境変数に配置したフォルダーを追加し、任意の場所の CLI ツールを使用します。

#### <a name="macoslinux"></a>macOS/Linux

動作は、OS のディストリビューションによって微妙に異なる場合があります。

1. [Mono 4.4.2 以降](http://www.mono-project.com/docs/getting-started/install/)をインストールします。

1. シェル プロンプトで次のコマンドを実行します。

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. 次のスクリプトを OS の適切なファイルに追加してエイリアスを作成します (通常、`~/.bash_aliases` または `~/.bash_profile`)。

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. シェルを再度読み込みます。  パラメーターなしで `nuget` を入力してインストールをテストします。 NuGet CLI ヘルプが表示されます。
