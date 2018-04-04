#### <a name="windows"></a><span data-ttu-id="eb48f-101">Windows</span><span class="sxs-lookup"><span data-stu-id="eb48f-101">Windows</span></span>
1. <span data-ttu-id="eb48f-102">参照してください[nuget.org/downloads](https://nuget.org/downloads) NuGet 3.3 以降を選択し、(2.8.6 はモノラルと互換性がありません)。</span><span class="sxs-lookup"><span data-stu-id="eb48f-102">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="eb48f-103">最新バージョンは常に推奨される、おり、nuget.org をパッケージを公開する 4.1.0+ が不要です。</span><span class="sxs-lookup"><span data-stu-id="eb48f-103">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
2. <span data-ttu-id="eb48f-104">各ダウンロード、`nuget.exe`ファイルを直接です。</span><span class="sxs-lookup"><span data-stu-id="eb48f-104">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="eb48f-105">任意のフォルダーにファイルを保存するのには、ブラウザーに指示します。</span><span class="sxs-lookup"><span data-stu-id="eb48f-105">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="eb48f-106">ファイルが*いない*インストーラーは、ブラウザーから直接実行する場合は、何も表示されません。</span><span class="sxs-lookup"><span data-stu-id="eb48f-106">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
3. <span data-ttu-id="eb48f-107">追加するフォルダーを配置した`nuget.exe`ツールを使用して、CLI どこからでも、PATH 環境変数にします。</span><span class="sxs-lookup"><span data-stu-id="eb48f-107">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="eb48f-108">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="eb48f-108">macOS/Linux</span></span>
<span data-ttu-id="eb48f-109">動作は、OS の配布によって若干異なります。</span><span class="sxs-lookup"><span data-stu-id="eb48f-109">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="eb48f-110">インストール[モノラル 4.4.2 以降](http://www.mono-project.com/docs/getting-started/install/)です。</span><span class="sxs-lookup"><span data-stu-id="eb48f-110">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>
2. <span data-ttu-id="eb48f-111">シェル プロンプトで次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="eb48f-111">Execute the following commands at a shell prompt:</span></span>
    
    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```
3. <span data-ttu-id="eb48f-112">OS の適切なファイルに次のスクリプトを追加することによって別名を作成 (通常`~/.bash_aliases`または`~/.bash_profile`)。</span><span class="sxs-lookup"><span data-stu-id="eb48f-112">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>
    
    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```
4. <span data-ttu-id="eb48f-113">シェルを再読み込みされます。</span><span class="sxs-lookup"><span data-stu-id="eb48f-113">Reload the shell.</span></span>  <span data-ttu-id="eb48f-114">入力することで、インストールをテスト`nuget`パラメーターなしでします。</span><span class="sxs-lookup"><span data-stu-id="eb48f-114">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="eb48f-115">NuGet CLI ヘルプを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="eb48f-115">NuGet CLI help should display.</span></span>