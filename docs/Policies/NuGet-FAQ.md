---
title: "NuGet に関してよく寄せられる質問 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/11/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "コマンド ラインと Visual Studio での NuGet の使用、および NuGet ギャラリーでの作業に関する一般的な質問と回答。"
keywords: "NuGet に関する Q&A, 質問と回答, 一般的な問題, NuGet のバージョン, パッケージのバージョン"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3782fe5dcf8df002d99446aa7548a6eacc62211c
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2018
---
# <a name="nuget-frequently-asked-questions"></a>NuGet に関してよく寄せられる質問

**NuGet を実行するために必要なものは何ですか?**

UI とコマンド ライン ツールの両方に関するすべての情報は、[インストール ガイド](../install-nuget-client-tools.md)で入手できます。

**NuGet で Mono はサポートされますか?**

コマンド ライン ツール `nuget.exe` は Mono 3.2+ でビルドおよび実行され、Mono でパッケージを作成できます。

`nuget.exe` は Windows では完全に動作しますが、Linux と OS X では既知の問題があります。GitHub の [Mono に関する問題](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono)を参照してください。

[グラフィカル クライアント](https://github.com/mrward/monodevelop-nuget-addin)は、MonoDevelop 用のアドインとして使用できます。

**パッケージの内容と、それが自分のアプリケーションに対して安定したものであり、役立つものであるかどうかはどのように判別すればよいですか?**

パッケージについて学習するための主なソースとして、nuget.org (または別のプライベート フィード) のリスト ページがあります。 nuget.org の各パッケージ ページには、パッケージ、そのバージョン履歴、使用状況の統計の説明が含まれます。 パッケージ ページの **[情報]** セクションには、プロジェクトの Web サイトへのリンクも含まれています。通常はこのサイトで、パッケージの使用方法について学習する際に役立つ多くの例とその他のドキュメントを見つけます。

詳細については、「[パッケージの検索と選択](../consume-packages/finding-and-choosing-packages.md)」を参照してください。

## <a name="nuget-in-visual-studio"></a>Visual Studio の NuGet

**別の Visual Studio 製品では NuGet はどのようにサポートされますか?**

- Windows の Visual Studio では、[パッケージ マネージャー UI](../tools/package-manager-ui.md) と[パッケージ マネージャー コンソール](../tools/package-manager-console.md)がサポートされます。
- 「[プロジェクトに NuGet パッケージを含める](/visualstudio/mac/nuget-walkthrough)」で説明されているように、Visual Studio for Mac には NuGet 機能が組み込まれています。
- Visual Studio Code (すべてのプラットフォーム) には、直接 NuGet は統合されていません。 [NuGet CLI](../tools/nuget-exe-cli-reference.md) または [dotnet CLI](../tools/dotnet-commands.md) を使用してください。
- Visual Studio Team Services では、[NuGet パッケージを復元するためのビルド ステップ](/vsts/build-release/tasks/package/nuget)が提供されます。 [Team Services でプライベート NuGet パッケージ フィードをホストする](https://www.visualstudio.com/docs/package/nuget/publish)こともできます。

**インストールされている NuGet ツールの正確なバージョンはどのように確認すればよいですか?**

Visual Studio で、**[ヘルプ]、[Microsoft Visual Studio のバージョン情報]** コマンドを使用して、**[NuGet パッケージ マネージャー]** の横に表示されるバージョンを確認します。

または、パッケージ マネージャー コンソールを起動 (**[ツール]、[NuGet パッケージ マネージャー]、[パッケージ マネージャー コンソール]** の順に選択) し、「`$host`」と入力して、バージョンを含む NuGet に関する情報を表示します。

**NuGet ではどのようなプログラミング言語がサポートされますか?**

通常、NuGet は .NET 言語に対して動作し、プロジェクトに .NET ライブラリを取り込むように設計されています。 また、いくつかのプロジェクトの種類で MSBuild と Visual Studio オートメーションがサポートされるため、程度の差はありますが他のプロジェクトと言語もサポートされます。

最新バージョンの NuGet では C#、Visual Basic、F#、WiX、C++ がサポートされます。

**NuGet ではどのようなプロジェクト テンプレートがサポートされますか?**

NuGet では、Windows、Web、クラウド、SharePoint、Wix などのさまざまなプロジェクト テンプレートが完全にサポートされます。

**Visual Studio テンプレートの一部であるパッケージはどのように更新すればよいですか?**

パッケージ マネージャー UI の **[更新]** タブに移動して、**[すべて更新]** を選択するか、パッケージ マネージャー コンソールで [`Update-Package` コマンド](../tools/ps-ref-update-package.md)を使用します。

テンプレート自体を更新するには、テンプレート リポジトリを手動で更新する必要があります。 これについては、[Xavier Decoster のブログ](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages)を参照してください。 最新バージョンのすべての依存関係が相互に互換性がない場合、手動で更新するとテンプレートが壊れる可能性があるため、これは自身の責任で行うことに注意してください。

**Visual Studio 外部で NuGet を使用できますか?**

はい。NuGet はコマンド ラインから直接動作します。 [インストール ガイド](../install-nuget-client-tools.md)と [CLI 参照](../tools/nuget-exe-cli-reference.md)に関するページを参照してください。

## <a name="nuget-command-line"></a>NuGet コマンド ライン

**最新バージョンの NuGet コマンド ライン ツールはどのように取得すればよいですか?**

[インストール ガイド](../install-nuget-client-tools.md)を参照してください。

**nuget.exe のライセンスとは何ですか?**

MIT ライセンスの条件に従って、nuget.exe を再配布できます。 再配布を選択した nuget.exe のコピーを更新および修正するのは、お客様の責任です。

**NuGet コマンド ライン ツールを拡張することはできますか?**

はい。[Rob Reynold の投稿](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx)で説明されているように、`nuget.exe` にカスタム コマンドを追加することができます。

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>NuGet パッケージ マネージャー コンソール (Windows の Visual Studio)

**パッケージ マネージャー コンソールでは DTE オブジェクトにどのようにアクセスするのですか?**

Visual Studio オートメーション オブジェクト モデルのトップ レベル オブジェクトは、DTE (開発ツール環境) オブジェクトと呼ばれます。 コンソールでは、`$DTE` という名前の変数を通じてこれが提供されます。 詳細については、Visual Studio 機能拡張ドキュメントの「[オートメーション モデルの概要](/visualstudio/extensibility/internals/automation-model-overview)」を参照してください。

**$DTE 変数を DTE2 型にキャストしようとしましたが、""EnvDTE.DTEClass" 型の "EnvDTE.DTEClass" 値を "EnvDTE80.DTE2" 型に変換できません" という内容のエラーが表示されました。何が問題なのでしょうか?**

これは、PowerShell が COM オブジェクトと対話する方法に関する既知の問題です。 以下を試してみてください。

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface` は、NuGet PowerShell ホストによって追加されたヘルパー関数です。

## <a name="creating-and-publishing-packages"></a>パッケージの作成と発行

**フィードではどのように自分のパッケージをリストするのですか?**

「[パッケージの作成と発行](../quickstart/create-and-publish-a-package.md)」を参照してください。

**異なるバージョンの .NET Framework をターゲットとする複数バージョンのライブラリがあります。これをサポートする 1 つのパッケージをビルドするにはどうすればよいですか?**

[複数の .NET Framework バージョンとプロファイルのサポート](../create-packages/supporting-multiple-target-frameworks.md)に関するページを参照してください。

**独自のリポジトリまたはフィードを設定するにはどうすればよいですか?**

[パッケージのホスティングの概要](../hosting-packages/overview.md)に関するページを参照してください。

**パッケージを自分の NuGet フィードに一括でアップロードするにはどうすればよいですか?**

「[Bulk publishing NuGet packages」](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (NuGet パッケージの一括発行) (jeffhandly.com) を参照してください。

## <a name="working-with-packages"></a>パッケージの操作

**プロジェクト レベルのパッケージとソリューション レベルのパッケージの違いは何ですか?**

ソリューション レベルのパッケージ (NuGet 3.x+) はソリューションに 1 回だけインストールされ、ソリューション内のすべてのプロジェクトで使用可能になります。 プロジェクト レベルのパッケージは、このパッケージを使用するプロジェクトごとにインストールされます。 ソリューション レベルのパッケージでは、パッケージ マネージャー コンソール内から呼び出すことができる新しいコマンドがインストールされる場合もあります。

**インターネットに接続せずに NuGet パッケージをインストールすることはできますか?**

はい。Scott Hanselman のブログ投稿「[How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx)」 (nuget.org がダウンしたとき (または飛行機内で) NuGet にアクセスする方法) (hanselman.com) を参照してください。

**既定のパッケージ フォルダーとは異なる場所にパッケージをインストールするにはどうすればよいですか?**

`nuget config -set repositoryPath=<path>` を使用して、`Nuget.Config` で [`repositoryPath`](../reference/nuget-config-file.md#config-section) を設定します。

**NuGet パッケージ フォルダーがソース管理に追加されないようにするにはどうすればよいですか?**

`Nuget.Config` の [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) を `true` に設定します。 このキーはソリューション レベルで動作するため、`$(Solutiondir)\.nuget\Nuget.Config` ファイルに追加する必要があります。 Visual Studio からのパッケージの復元を有効にすると、このファイルは自動的に作成されます。

**パッケージの復元を無効にするにはどうすればよいですか?**

「[パッケージの復元の有効化と無効化](../consume-packages/package-restore.md#enabling-and-disabling-package-restore)」を参照してください。

**リモートの依存関係があるローカル パッケージをインストールするときに、"依存関係を解決できません" という内容のエラーが表示されるのはなぜですか?**

プロジェクトにローカル パッケージをインストールする場合は、**すべて**のソースを選択する必要があります。 これにより、フィードを 1 つだけ使用するのではなく、すべて集約することになります。 このエラーが表示されるのは、ローカル リポジトリのユーザーは、多くの場合、企業ポリシーにより、リモート パッケージが誤ってインストールされないようにする必要があるためです。

**同じフォルダーに複数のプロジェクトがあります。プロジェクトごとに別個の packages.config ファイルを使用するにはどうすればよいですか?**

別個のプロジェクトが別個のフォルダーに存在するほとんどのプロジェクトでは、NuGet で各プロジェクトの `packages.config` ファイルが特定されるため、これは問題ではありません。 NuGet 3.3+ では、同じフォルダーに複数のプロジェクトがある場合、プロジェクトの名前を `packages.config` ファイル名に挿入できます (パターン `packages.{project-name}.config` を使用)。NuGet はそのファイルを使用します。

各プロジェクト ファイルには独自の依存関係リストが含まれるため、PackageReference を使用する場合、これは問題ではありません。

**自分のリポジトリ リストに nuget.org が表示されません。これを戻すにはどうすればよいですか?**

- 自分のソース リストに `https://api.nuget.org/v3/index.json` を追加します。または、
- `%appdata%\.nuget\NuGet.Config` (Windows) または `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) を削除し、NuGet で自動的に再作成します。

**パッケージで特定のライセンス情報が提供されない場合の既定のライセンス条項は何ですか?**

各パッケージには、パッケージに含まれている条項が適用されます。 パッケージのアクセス、ダウンロード、または取得の前に、適用される条項を確認する必要があります。 nuget.org で、パッケージ ページの **[ライセンス情報]** リンクを使用します。

パッケージでライセンス条項が指定されていない場合は、nuget.org パッケージ ページの **[Contact owners]\(所有者に問い合わせる\)** リンクを使用して、パッケージ所有者に直接問い合わせてください。 Microsoft はサードパーティのパッケージ プロバイダーを通じてユーザーに知的財産ライセンスを付与することはありません。また、サードパーティによって提供される情報について責任を負いません。

## <a name="managing-packages-on-nugetorg"></a>nuget.org でのパッケージの管理

**パッケージ メタデータをアップロードしてから編集することはできますか? nuspec を編集し、新しいパッケージをアップロードしてパッケージ メタデータを変更するように求められるのはなぜですか?**

NuGet では、すべてのパッケージに署名する必要があります。 パッケージ署名の設計原理は、署名付きパッケージ コンテンツ (nuspec を含む) は不変でなければならないということです。 パッケージ メタデータを編集すると、nuspec が変更され、既存の署名が無効になります。 パッケージが作成された後にパッケージ メタデータの編集が必要とならないように、既存のワークフローを変更することをお勧めします。

パッケージに対してリストされる依存関係は、パッケージ自体から自動的に生成されるものであり、編集できないことに注意してください。

また、パッケージを [staging.nuget.org](http://staging.nuget.org) にアップロードすることは、パブリック ギャラリーでパッケージを使用できるようにせずに、パッケージをテストして検証する優れた方法です。

**今後発行されるパッケージの名前を予約することはできますか?**

はい。 ご使用のアカウントのパッケージ ID プレフィックスを要求することで、[nuget.org](https://www.nuget.org/) でパッケージの ID を予約できます。 パッケージ ID プレフィックスを要求するには、[ドキュメント](https://docs.microsoft.com/nuget/reference/id-prefix-reservation)の指示に従ってください。

**パッケージの所有権はどのように要求するのですか?**

「[nuget.org でパッケージ所有者を管理する](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg)」を参照してください。

**ソフトウェア ライセンスに違反しているパッケージ所有者にはどのように対処するのですか?**

NuGet コミュニティと協力して、パッケージ所有者と他のソフトウェアの所有者間で発生する可能性のある紛争を解決することをお勧めします。 [紛争解決プロセス](../policies/dispute-resolution.md)が作成されています。nuget.org 管理者に仲裁を求める前にこのプロセスに従ってください。

**nuget.org に自分のテスト パッケージをアップロードするよう勧めされていますか?**

テスト目的で、[staging.nuget.org](http://staging.nuget.org) を使用することができます。また、[myget.org](https://myget.org) や [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/) などのパブリック NuGet サーバーを代わりに使用することもできます。

staging.nuget.org にアップロードされたパッケージは保持されない場合があることに注意してください。 [preview の終了](http://blog.nuget.org/20130419/goodbye-preview.html)に関するページ参照してください。

**nuget.org にアップロードできるパッケージの最大サイズは何ですか?**

nuget.org では最大 250 MB のパッケージをアップロードできますが、可能な場合はパッケージを 1 MB 未満に保ち、依存関係を使用してパッケージを相互にリンクさせることをお勧めします。 一般に、競合を避けるため、パッケージにはアセンブリを 1 つだけ含めます。

NuGet では HTTP を使用してパッケージをダウンロードするため、パッケージが大きいと、小さいパッケージよりもインストールに失敗する可能性が高くなります。

複数のパッケージ間で依存関係を共有することはできます。これにより、NuGet パッケージのコンシューマーの合計ダウンロード サイズが小さくなります。

依存関係は、ほとんどの場合、静的なものであり、変わることはありません。 コードでバグを修正するときは、依存関係の更新が必要ない場合があります。 依存関係をバンドルする場合、結局は毎回大きなパッケージを再配布することになります。 NuGet パッケージを関連する依存関係に分割することで、パッケージのコンシューマーに応じて、アップグレードをより細かく行うことができます。

## <a name="nugetorg-not-accessible"></a>nuget.org にアクセスできない

**nuget.org でパッケージのダウンロードやアップロードができないのはなぜですか?**

まず、最新バージョンの NuGet を使用していることを確認してください。 そのバージョンでも失敗する場合は、[サポートに問い合わせて](https://www.nuget.org/policies/Contact)、次の内容を含む、追加の接続のトラブルシューティングに関する情報を提供してください。

- 使用している NuGet のバージョン
- 使用しているパッケージ ソース
- 詳細な復元ログ
- MTR または Fiddler のトレース (下記参照)
- 地理的地域
- ご利用のオペレーティング システムのバージョン
- コンピューターの構成 (CPU、ネットワーク、ハード ドライブ)
- コンピューターがプロキシとファイアウォールのどちらの背後にあるのか
- コンピューターにインストールされている .NET のバージョン
- .NET CLI などのクロスプラットフォーム ツール、または使用している DNU のバージョン

*MTR をキャプチャするには:*

- [http://winmtr.net/download/](http://winmtr.net/) から WinMTR をダウンロードします
- ホスト名として「`api.nuget.org`」を入力して、**[開始]** をクリックします。
- **[送信]** 列が 100 以上になるまで待ちます。

    ![MTR のキャプチャ](media/mtr.png)

- クリップボードにテキストをコピーします。

*Fiddler をキャプチャするには:*

- 最新バージョンの [Fiddler](http://www.telerik.com/download/fiddler) をインストールします。
- Fiddler を起動し、**[ファイル]、[Capture Traffic]\(トラフィックのキャプチャ\)** メニューを使用してトラフィックのキャプチャを無効にします。
- すべてのセッションを削除します (リストのすべての項目を選択して、**Delete** キーを押します)。
- **[ツール]、[Fiddler Options...]\(Fiddler オプション...\)** メニューの **[HTTPS]** タブにある **[Decrypt HTTPS traffic]\(HTTPS トラフィックの暗号化解除\)** をオフにして、HTTPS トラフィックをキャプチャするように Fiddler を構成します。
- Visual Studio を閉じます。
- **[ファイル]、[Capture Traffic]\(トラフィックのキャプチャ\)** メニューを有効にします。
- Visual Studio または nuget.exe を起動して、機能していないアクションを実行します。 これらのアクションによって生成されるトラフィックは Fiddler に表示されます。
- アクションが実行されたら、**[ファイル]、[保存]、[すべてのセッション]** を使用して、キャプチャされたセッションを保存します。

注: Fiddler を介して NuGet トラフィックをルーティングするために、`HTTP_PROXY` 環境変数を `http://127.0.0.1:8888` に設定する必要がある場合があります。

これが失敗した場合は、[この StackOverflow の投稿に記載されているヒント](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall)を試してください。

**nuget.org の API エンドポイントは何ですか?**

V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (V2 API は使用されなくなり、NuGet 4+ では機能しないことに注意してください)。
