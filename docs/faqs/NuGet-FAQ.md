---
title: NuGet に関してよく寄せられる質問
description: コマンド ラインと Visual Studio での NuGet の使用に関する一般的な質問と回答。
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9094d6b4a2dbd6ea1899b4470624948ce7c21f43
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317620"
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

- Windows の Visual Studio では、[パッケージ マネージャー UI](../consume-packages/install-use-packages-visual-studio.md) と[パッケージ マネージャー コンソール](../consume-packages/install-use-packages-powershell.md)がサポートされます。
- 「[プロジェクトに NuGet パッケージを含める](/visualstudio/mac/nuget-walkthrough)」で説明されているように、Visual Studio for Mac には NuGet 機能が組み込まれています。
- Visual Studio Code (すべてのプラットフォーム) には、直接 NuGet は統合されていません。 [NuGet CLI](../reference/nuget-exe-cli-reference.md) または [dotnet CLI](../reference/dotnet-commands.md) を使用してください。
- Azure DevOps には、[NuGet パッケージを復元するためのビルド ステップ](/vsts/build-release/tasks/package/nuget)があります。 [Azure DevOps でプライベート NuGet パッケージ フィードをホストする](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish)こともできます。

**インストールされている NuGet ツールの正確なバージョンはどのように確認すればよいですか?**

Visual Studio で、 **[ヘルプ]、[Microsoft Visual Studio のバージョン情報]** コマンドを使用して、 **[NuGet パッケージ マネージャー]** の横に表示されるバージョンを確認します。

または、パッケージ マネージャー コンソールを起動 ( **[ツール]、[NuGet パッケージ マネージャー]、[パッケージ マネージャー コンソール]** の順に選択) し、「`$host`」と入力して、バージョンを含む NuGet に関する情報を表示します。

**NuGet ではどのようなプログラミング言語がサポートされますか?**

通常、NuGet は .NET 言語に対して動作し、プロジェクトに .NET ライブラリを取り込むように設計されています。 また、いくつかのプロジェクトの種類で MSBuild と Visual Studio オートメーションがサポートされるため、程度の差はありますが他のプロジェクトと言語もサポートされます。

最新バージョンの NuGet では C#、Visual Basic、F#、WiX、C++ がサポートされます。

**NuGet ではどのようなプロジェクト テンプレートがサポートされますか?**

NuGet では、Windows、Web、クラウド、SharePoint、Wix などのさまざまなプロジェクト テンプレートが完全にサポートされます。

**Visual Studio テンプレートの一部であるパッケージはどのように更新すればよいですか?**

パッケージ マネージャー UI の **[更新]** タブに移動して、 **[すべて更新]** を選択するか、パッケージ マネージャー コンソールで [`Update-Package` コマンド](../reference/ps-reference/ps-ref-update-package.md)を使用します。

テンプレート自体を更新するには、テンプレート リポジトリを手動で更新する必要があります。 これについては、[Xavier Decoster のブログ](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages)を参照してください。 最新バージョンのすべての依存関係が相互に互換性がない場合、手動で更新するとテンプレートが壊れる可能性があるため、これは自身の責任で行うことに注意してください。

**Visual Studio 外部で NuGet を使用できますか?**

はい。NuGet はコマンド ラインから直接動作します。 [インストール ガイド](../install-nuget-client-tools.md)と [CLI 参照](../reference/nuget-exe-cli-reference.md)に関するページを参照してください。

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

「[パッケージの復元の有効化と無効化](../consume-packages/package-restore.md#enable-and-disable-package-restore-visual-studio)」を参照してください。

**リモートの依存関係があるローカル パッケージをインストールするときに、"依存関係を解決できません" という内容のエラーが表示されるのはなぜですか?**

プロジェクトにローカル パッケージをインストールする場合は、**すべて**のソースを選択する必要があります。 これにより、フィードを 1 つだけ使用するのではなく、すべて集約することになります。 このエラーが表示されるのは、ローカル リポジトリのユーザーは、多くの場合、企業ポリシーにより、リモート パッケージが誤ってインストールされないようにする必要があるためです。

**同じフォルダーに複数のプロジェクトがあります。プロジェクトごとに別個の packages.config ファイルを使用するにはどうすればよいですか?**

別個のプロジェクトが別個のフォルダーに存在するほとんどのプロジェクトでは、NuGet で各プロジェクトの `packages.config` ファイルが特定されるため、これは問題ではありません。 NuGet 3.3+ では、同じフォルダーに複数のプロジェクトがある場合、プロジェクトの名前を `packages.config` ファイル名に挿入できます (パターン `packages.{project-name}.config` を使用)。NuGet はそのファイルを使用します。

各プロジェクト ファイルには独自の依存関係リストが含まれるため、PackageReference を使用する場合、これは問題ではありません。

**自分のリポジトリ リストに nuget.org が表示されません。これを戻すにはどうすればよいですか?**

- 自分のソース リストに `https://api.nuget.org/v3/index.json` を追加します。または、
- `%appdata%\.nuget\NuGet.Config` (Windows) または `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) を削除し、NuGet で自動的に再作成します。
