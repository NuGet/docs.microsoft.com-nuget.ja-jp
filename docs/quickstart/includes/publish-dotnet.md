1. `.nupkg` ファイルを含むフォルダーに変更します。

1. 次のコマンドでパッケージ名を指定し、キーを API キーに置き換えて、コマンドを実行します。

    ```cli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. dotnet により、公開プロセスの結果が表示されます。

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

「[dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push)」を参照してください。