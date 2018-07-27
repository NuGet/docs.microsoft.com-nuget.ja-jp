`push` コマンドのエラーは、通常、問題があることを示します。 たとえば、プロジェクトのバージョン番号の更新を忘れて、既に存在するパッケージを公開しようとした場合などがあります。

また、ホストに既に存在する識別子を使用してパッケージを公開しようとするとエラーが表示されます。 たとえば、"AppLogger" という名前は既に存在します。 その場合、`push` コマンドを実行すると、次のエラーが表示されます。

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

作成したばかりの有効な API キーを使用している場合、エラーの "アクセス許可" 部分では完全には明白ではありませんが、このメッセージは名前の競合を示します。 パッケージ識別子を変更し、プロジェクトをリビルドして、 `.nupkg` ファイルを再作成した後、`push` コマンドを再試行します。