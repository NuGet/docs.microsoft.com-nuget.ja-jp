nuget.org のプロファイルから、**[パッケージの管理]** を選択して、公開したパッケージを確認します。 確認メールも送信されます。 パッケージがインデックス作成され、他のユーザーが検索して検索結果に表示されるようになるまでには、時間がかかる場合があることに注意してください。 この間、パッケージのページに次のメッセージが表示されます。

    ![This package has not been indexed yet. It will appear in search results and will be available for install/restore after indexing is complete.](../media/QS_Create-03-NotIndexed.png)

以上です。 最初の NuGet パッケージが nuget.org に公開され、他の開発者はそれを自身のプロジェクトで使用することができます。

このチュートリアルで作成したパッケージが、実際に有用ではない場合 (空のクラス ライブラリを使用して作成されたパッケージなど)、そのパッケージを*一覧から削除*して、検索結果に表示されないようにする必要があります。

1. nuget.org で、ユーザー名 (ページの右上) を選択し、**[パッケージの管理]** を選択します。

1. **[公開済み]** の一覧から削除するパッケージを見つけて、右側のごみ箱のアイコンを選択します。

    ![nuget.org のパッケージの一覧に表示されたごみ箱のアイコン](../media/qs_create-vs-03-trash-can.png)

1. 後続のページで、**[List (package-name) in search results]\(検索結果に (パッケージ名) をリストする\)** というラベルの付いたボックスをオフにし、**[保存]** を選択します。

    ![nuget.org でパッケージの [リストする] チェックボックスをクリア](../media/qs_create-vs-04-unlist.png)