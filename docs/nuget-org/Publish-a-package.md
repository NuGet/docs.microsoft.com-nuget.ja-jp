---
title: NuGet パッケージの公開方法
description: NuGet パッケージを nuget.org やプライベート フィードに公開する方法と nuget.org でパッケージ所有権を管理する方法に関する詳細。
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 02c6c8f3018bfd063c2d16a10381f88b54cac840
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231345"
---
# <a name="publishing-packages"></a>パッケージを公開する

パッケージを作成し、`.nupkg` ファイルを入手している場合は、このプロセスにより、他の開発者がパッケージを簡単に利用できるようにすることができます。公開または非公開のいずれかを選択できます。

- 公開パッケージの場合、この記事で説明するように、[nuget.org](https://www.nuget.org/packages/manage/upload) 経由で世界中の開発者が利用できます (NuGet 4.1.0 以降が必要です)。
- 非公開パッケージは、特定のチームまたは組織だけが利用できます。このようにするには、パッケージをファイル共有、プライベート NuGet サーバー、[Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish)、またはサードパーティのリポジトリ (たとえば myget、ProGet、Nexus Repository、Artifactory) でホストします。 詳細については、「[Hosting Packages Overview](../hosting-packages/overview.md)」 (パッケージ ホストの概要) を参照してください。

この記事では、nuget.org に公開する方法を取り上げます。Azure Artifacts に公開する方法については、「[Package Management](https://www.visualstudio.com/docs/package/nuget/publish)」(パッケージ管理) をご覧ください。

## <a name="publish-to-nugetorg"></a>nuget.org に公開する

Nuget.org の場合、Microsoft アカウントでサインインする必要があります。このアカウントで、nuget.org でのアカウント登録を行うよう求められます。また、古いバージョンのポータルを使用して作成された nuget.org アカウントで、サインインすることも可能です。

![NuGet サインインの場所](media/publish_NuGetSignIn.png)

次に、パッケージを nuget.org Web ポータルからアップロードするか、コマンド ラインから nuget.org にプッシュするか (`nuget.exe` 4.1.0 以上が必要です)、CI/CD プロセスの一部として Azure DevOps Services を通して公開します。これらの方法について、以降のセクションで説明します。

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Web ポータル: nuget.org の [パッケージのアップロード] を使用

1. nuget.org の上部メニューで **[アップロード]** を選択して、パッケージの場所を参照します。

    ![nuget.org 上でパッケージをアップロードする](media/publish_UploadYourPackage.PNG)

1. nuget.org では、パッケージ名が使用可能かどうかが示されます。 使用できない場合、お使いのプロジェクトのパッケージ ID を変更し、リビルドしてから、アップロードをもう一度やり直してください。

1. パッケージ名が使用可能な場合、nuget.org では、パッケージ マニフェストからメタデータを確認できる **[確認]** セクションを開きます。 いずれかのメタデータを変更するには、お使いのプロジェクト (プロジェクト ファイルまたは `.nuspec` ファイル) を編集し、リビルドし、パッケージを再作成して、もう一度アップロードします。

1. **[Import Documentation]\(ドキュメントのインポート\)** では、マークダウンを貼り付けて、URL でドキュメントを参照したり、ドキュメント ファイルをアップロードしたりできます。

1. すべての情報が準備できたら、 **[送信]** ボタンを選択します。

### <a name="command-line"></a>コマンド ライン

nuget.org にパッケージをプッシュするには、[nuget.exe v4.1.0 以降](https://www.nuget.org/downloads)を使用する必要があります。これは必須の [NuGet プロトコル](../api/nuget-protocols.md)を実装します。 また、nuget.org 上で作成される API キーも必要です。

#### <a name="create-api-keys"></a>API キーの作成

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>dotnet nuget push を使用して公開する

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>nuget push を使用して公開する

1. コマンド プロンプトで次のコマンドを実行して、`<your_API_key>` を nuget.org から取得したキーに置き換えます。

    ```cli
    nuget setApiKey <your_API_key>
    ```

    このコマンドでは、ご利用の API キーがご利用の NuGet 構成に格納されます。そのため、同じコンピューター上でこの手順をもう一度繰り返す必要はありません。

    > [!NOTE]
    > API キーは、プライベート フィードでの認証には使用されません。 ソースで認証するための資格情報を管理するには、[`nuget sources` コマンド](../reference/cli-reference/cli-ref-sources.md)を参照してください。
    > API キーは、個々の NuGet サーバーから取得できます。 nuget.org の APIKeys を作成して管理するには、[publish-api-key](../quickstart/includes/publish-api-key.md) を参照してください。

1. 以下のコマンドを使用して、NuGet ギャラリーにパッケージをプッシュします。

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a>署名付きパッケージの公開

署名付きパッケージを送信するには、最初にパッケージの署名に使用する[証明書を登録する](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg)必要があります。 

> [!Warning]
> [署名付きパッケージの要件](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg)を満たしていないパッケージは、nuget.org に拒否されます。

### <a name="package-validation-and-indexing"></a>パッケージの検証とインデックスの作成

nuget.org にプッシュされたパッケージは、ウィルス チェックなど、いくつかの検証を受けます。 (Nuget.org 上のすべてのパッケージが定期的にスキャンされます。)

パッケージがすべての検証に合格すると、インデックスが作成され、検索結果に表示されるようになりますが、それには時間がかかることがあります。 インデックスの作成が完了すると、パッケージが正常に公開されたことを示す確認の電子メールが届きます。 パッケージが検証で不合格になった場合、パッケージの詳細ページが更新され、関連するエラーが表示されます。それに関する電子メールも届きます。

パッケージの検証とインデックスの作成は、通常、15 以内で完了します。 パッケージ公開に予想以上の時間がかかる場合、[status.nuget.org](https://status.nuget.org/) にアクセスし、nuget.org に中断が発生していないか確認してください。 すべてのシステムが動作しているとき、1 時間以内にパッケージが正常に公開されない場合、nuget.org にログインし、パッケージ ページの [Contact Support] リンクからお問い合わせください。

パッケージのステータスを表示するには、nuget.org でアカウント名の下にある **[パッケージの管理]** を選択します。検証が完了すると、確認の電子メールを受信します。

パッケージにインデックスが付けられ、検索結果に表示されるようになり、他のユーザーが検索可能になるまで時間がかかることがあります。その間、パッケージ ページには次のメッセージが表示されます。

![パッケージがまだ公開されていないことを示すメッセージ](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a>Azure DevOps Services (CI/CD)

Azure DevOps Services を使用して、継続的インテグレーション/配置プロセスの一部としてパッケージを nuget.org にプッシュする場合は、`nuget.exe` 4.1 以上を NuGet タスクの中で使用する必要があります。 詳細は、Microsoft DevOps ブログの「[Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/)」 (ビルドで最新の NuGet を利用する) にあります。

## <a name="managing-package-owners-on-nugetorg"></a>nuget.org でパッケージ所有者を管理する

各 NuGet パッケージの `.nuspec` はパッケージの作成者を定義するものですが、nuget.org ギャラリーでは、所有権の定義にそのメタデータは使用されません。 nuget.org では、パッケージを公開した人に最初の所有権が割り当てられます。 これは nuget.org UI からパッケージをアップロードしたログイン ユーザーになるか、`nuget SetApiKey` または `nuget push` と共に API キーが使用されたユーザーになります。

パッケージ所有者にはすべて、パッケージの完全アクセス許可が与えられます。他の所有者を追加したり、削除したり、更新内容を公開したりできます。

パッケージの所有権は次のように変更します。

1. パッケージの現在の所有者になっているアカウントで nuget.org にサインインします。
1. 自分のアカウント名を選択し、 **[パッケージの管理]** を選択し、 **[Published Packages]\(公開されたパッケージ\)** を展開します。
1. 管理するパッケージを選択し、右側にある **[Manage owners]\(所有者を管理する\)** を選択します。

ここにはいくつかのオプションがあります。

1. **[Current Owners]\(現在の所有者\)** に一覧表示されたいずれかの所有者を削除します。
1. ユーザー名、メッセージを入力して **[追加]** を選択し、 **[所有者の追加]** に所有者を追加します。 この動作でその新しい共同所有者に確認リンクを含む電子メールが送信されます。 確認後、その人に所有者を追加したり、削除したりできる完全アクセス許可が与えられます。 (確認されるまで、 **[Current Owners]\(現在の所有者\)** セクションにはその人が承認待ちとして表示されます。)
1. 所有権を譲渡するには (所有権が変更された場合や間違ったアカウントでパッケージが公開された場合)、新しい所有者を追加します。新しい所有者は所有権を確認したら、一覧から他の所有者を削除できます。

会社またはグループに所有権を割り当てるには、適切なチーム メンバーに転送される電子メール エイリアスを利用して nuget.org アカウントを作成します。 たとえば、そのようなエイリアスである [microsoft](https://nuget.org/profiles/microsoft) アカウントや [aspnet](https://nuget.org/profiles/aspnet) アカウントでさまざまな Microsoft ASP.NET パッケージが共同所有されています。

### <a name="recovering-package-ownership"></a>パッケージ所有権を回復する

パッケージにアクティブな所有者が与えられていないことがあります。 たとえば、パッケージを作る会社を元々の所有者が去った場合、nuget.org 資格情報をなくした場合、ギャラリーの早期のバグが原因でパッケージが所有者なしになった場合などです。

自分がパッケージの正当な所有者であり、所有権を取り戻す必要がある場合、nuget.org の[問い合わせフォーム](https://www.nuget.org/policies/Contact)を利用し、NuGet チームに状況を説明してください。 その後、パッケージの所有権を検証するプロセスが開始します。パッケージのプロジェクト URL、Twitter、電子メール、その他の手段で既存の所有者が確認されます。 いずれの方法でも確認できない場合、所有者になるための新しい招待を送信します。
