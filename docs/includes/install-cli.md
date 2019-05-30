---
ms.openlocfilehash: 1f65939493cf423a76c024607264acee6c7e9050
ms.sourcegitcommit: ef08f376688f0191a8d3d873b6a4386afd799373
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2019
ms.locfileid: "66271548"
---
#### <a name="windows"></a><span data-ttu-id="41910-101">Windows</span><span class="sxs-lookup"><span data-stu-id="41910-101">Windows</span></span>

> [!Note]
> <span data-ttu-id="41910-102">NuGet.exe 5.0 以降には、実行するために .NET Framework 4.7.2 以降が必要です。</span><span class="sxs-lookup"><span data-stu-id="41910-102">NuGet.exe 5.0 and later require .NET Framework 4.7.2 or later to execute.</span></span>

1. <span data-ttu-id="41910-103">[nuget.org/downloads](https://nuget.org/downloads) にアクセスして、NuGet 3.3 以降を選択します (2.8.6 は Mono と互換性がありません)。</span><span class="sxs-lookup"><span data-stu-id="41910-103">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="41910-104">常に最新バージョンが推奨され、パッケージを nuget.org に公開するには 4.1.0 以降が必要です。</span><span class="sxs-lookup"><span data-stu-id="41910-104">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="41910-105">各ダウンロードは、直接 `nuget.exe` ファイルです。</span><span class="sxs-lookup"><span data-stu-id="41910-105">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="41910-106">ブラウザーで任意のフォルダーにファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="41910-106">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="41910-107">ファイルがインストーラーで*ない*場合、ブラウザーから直接実行しても何も表示されません。</span><span class="sxs-lookup"><span data-stu-id="41910-107">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="41910-108">`nuget.exe` をPATH 環境変数に配置したフォルダーを追加し、任意の場所の CLI ツールを使用します。</span><span class="sxs-lookup"><span data-stu-id="41910-108">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="41910-109">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="41910-109">macOS/Linux</span></span>

<span data-ttu-id="41910-110">動作は、OS のディストリビューションによって微妙に異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="41910-110">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="41910-111">[Mono 4.4.2 以降](http://www.mono-project.com/docs/getting-started/install/)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="41910-111">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="41910-112">シェル プロンプトで次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="41910-112">Execute the following command at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. <span data-ttu-id="41910-113">次のスクリプトを OS の適切なファイルに追加してエイリアスを作成します (通常、`~/.bash_aliases` または `~/.bash_profile`)。</span><span class="sxs-lookup"><span data-stu-id="41910-113">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="41910-114">シェルを再度読み込みます。</span><span class="sxs-lookup"><span data-stu-id="41910-114">Reload the shell.</span></span>  <span data-ttu-id="41910-115">パラメーターなしで `nuget` を入力してインストールをテストします。</span><span class="sxs-lookup"><span data-stu-id="41910-115">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="41910-116">NuGet CLI ヘルプが表示されます。</span><span class="sxs-lookup"><span data-stu-id="41910-116">NuGet CLI help should display.</span></span>
