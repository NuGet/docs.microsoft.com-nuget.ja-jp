#### <a name="windows"></a>Windows
1. 参照してください[nuget.org/downloads](https://nuget.org/downloads) NuGet 3.3 以降を選択し、(2.8.6 はモノラルと互換性がありません)。 最新バージョンは常に推奨される、おり、nuget.org をパッケージを公開する 4.1.0+ が不要です。
2. 各ダウンロード、`nuget.exe`ファイルを直接です。 任意のフォルダーにファイルを保存するのには、ブラウザーに指示します。 ファイルが*いない*インストーラーは、ブラウザーから直接実行する場合は、何も表示されません。
3. 追加するフォルダーを配置した`nuget.exe`ツールを使用して、CLI どこからでも、PATH 環境変数にします。

#### <a name="macoslinux"></a>macOS/Linux
動作は、OS の配布によって若干異なります。

1. インストール[モノラル 4.4.2 以降](http://www.mono-project.com/docs/getting-started/install/)です。
2. シェル プロンプトで次のコマンドを実行します。
    
    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```
3. OS の適切なファイルに次のスクリプトを追加することによって別名を作成 (通常`~/.bash_aliases`または`~/.bash_profile`)。
    
    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```
4. シェルを再読み込みされます。  入力することで、インストールをテスト`nuget`パラメーターなしでします。 NuGet CLI ヘルプを表示する必要があります。