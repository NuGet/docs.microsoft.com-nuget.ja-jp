---
title: nuget.org でのパッケージの廃止
description: パッケージの廃止プロセスと、クライアントがこの情報を表示する方法の詳細な説明
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 4a6dbd645cb72b0085fd0347def58ade134fc5ee
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726965"
---
# <a name="deprecating-packages"></a>パッケージの廃止

パッケージを維持しなくなった場合、またはパッケージのコンシューマーに別のパッケージへの移動を促したい場合は、パッケージを廃止することができます。 

パッケージの廃止は、以下で説明するように、パッケージを **非公開** にすることとは異なります。
* パッケージを **非公開** にすると、検索結果に表示されなくなるため、検出できません。 
* パッケージを **廃止** すると、パッケージの既存のコンシューマーが、自分のプロジェクトでそれがインストールされているか、使用されているかを調べることができます。 また、廃止の理由や、ユーザー (パッケージの発行元) によって指定された代替の推奨パッケージを知ることもできます。 パッケージを廃止しても、パッケージは非公開になりません。 

発行元は、パッケージを非公開にすることも、廃止することもできます。

## <a name="deprecation-workflow"></a>廃止のワークフロー
1. パッケージを廃止するには、**[パッケージの管理]** に移動して **[廃止]** を選択します。

    ![パッケージの廃止オプションに移動する](media/deprecation-select-option.png)

2. 廃止するバージョンを選択します。 すべてのバージョンを廃止する場合は、**[Select all versions]\(バージョンをすべて選択\)** オプションを選択します。

    ![廃止するパッケージのバージョンを選択する](media/deprecation-select-version.png)

3. 廃止の理由を選択します。 パッケージが維持されなくなった場合は、**[レガシ]** オプションを選択します。 特定のバージョンに重大なバグがある場合は、**[has critical bugs]\(重大なバグあり\)** オプションを選択します。 その他の理由については、**[その他]** を選択します。 代替の推奨パッケージ (およびバージョン) とカスタム メッセージを所有者に対していつでも指定できます。 

    ![理由、代替の推奨パッケージ、カスタム メッセージを選択する](media/deprecation-save.png)

> [!Note]
> カスタム メッセージは nuget.org にのみ表示され、クライアントには表示されません。 現時点では、`dotnet.exe` や NuGet パッケージ マネージャーなどのクライアントにはカスタム メッセージが表示されません。

## <a name="client-experience-for-deprecated-packages"></a>非推奨のパッケージのクライアント エクスペリエンス
パッケージが非推奨になると、そのコンシューマーには次の方法で通知されます (使用しているクライアントによって異なります)。

### <a name="visual-studio"></a>Visual Studio 
*Visual Studio 2019 バージョン 16.3 以降に適用*

Visual Studio では `Installed` タブに非推奨のパッケージの使用に関する警告が表示されます。パッケージとその非推奨情報 (非推奨とされた理由と代わりに使用する代替パッケージ (存在する場合) など) が表示されます。

   ![Visual Studio のパッケージ マネージャーの [Installed] タブに表示された非推奨のパッケージ](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*.NET SDK 3.0 以降に適用*

dotnet.exe を使用する場合は、ソリューションまたはプロジェクト フォルダーに対して `dotnet list package --deprecated` コマンドを実行すると、非推奨のパッケージの一覧と廃止情報を取得できます。

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```

## <a name="transfer-popularity-to-a-newer-package"></a>新しいパッケージに人気を引き継ぐ

レガシ パッケージを非推奨にしたパッケージ作成者は、その "人気" を新しいパッケージに引き継ぎ、新しいパッケージの検索ランキングを上げることができます。 これは、お客様が非推奨のパッケージではなく、新しいパッケージを見つけるのに役立ちます。

たとえば、次の 2 つのパッケージがあるとします。

* 非推奨のレガシ パッケージ `Contoso.Legacy` (300 万ダウンロードあり)
* 最新のパッケージ `Contoso.Latest` (5 ダウンロードあり)

NuGet.org では、ダウンロード数が多く、人気の高い検索結果が優先されます。 検索クエリ "Contoso" を指定した場合、非推奨のパッケージ `Contoso.Legacy` は検索結果で最新のパッケージ `Contoso.Latest` より上位にランク付けされる可能性があります。

この問題を解決するために、非推奨のレガシ パッケージの人気を最新のパッケージに引き継ぐことができます。 これにより、`Contoso.Latest` は検索結果の上位にランク付けられ、`Contoso.Legacy` のランクは低くなります。 パッケージの内部人気スコアのみが影響を受け、各パッケージの実際のダウンロード数には影響しません。

> [!Note]
> 人気を引き継ぐと、コンシューマーがレガシ パッケージを見つけるのが非常に困難になる可能性があります。

以下の表で、人気を引き継ぐことがクエリ "Contoso" の検索ランキングにどのように影響するかについて具体的に説明します。

| 検索ランキング    | 人気を引き継ぐ前        | 人気を引き継いだ後         |
|----------------   |--------------------------------   |--------------------------------   |
| 1                 | *Contoso.Legacy、3M ダウンロード*    | *Contoso.Latest、5 ダウンロード*     |
| 2                 | Contoso.Scanner、2M ダウンロード     | Contoso.Scanner、2M ダウンロード     |
| 3                 | Contoso.Core、1.5M ダウンロード     | Contoso.Core、1.5M ダウンロード     |
| 4                 | Contoso.UI、1M ダウンロード          | Contoso.UI、1M ダウンロード          |
| ...               | ...                               | ...                               |
| 20                | *Contoso.Latest、5 ダウンロード*     | *Contoso.Legacy、3M ダウンロード*    |

### <a name="popularity-transfer-application-process"></a>人気の引き継ぎを申請するプロセス

1. [人気を引き継ぐ場合の要件](#popularity-transfer-requirements)を確認します。
2. 人気を引き継ぐ必要がある非推奨パッケージと、人気を受け継ぐ必要がある安定したパッケージのリストを、[account@nuget.org](mailto:account@nuget.org) に電子メールで送信します。

申請が送信された後、申請の受理または拒否 (拒否の原因となった条件を含む) が通知されます。 所有者の身元を確認するために、追加の身元確認の質問が必要になることがあります。

#### <a name="popularity-transfer-requirements"></a>人気を引き継ぐ場合の要件

* レガシ パッケージと新しいパッケージでは、すべての所有者を共有する必要があります。
* 新しいパッケージは、名前付けと機能 (つまり、進化または次世代) について、レガシ パッケージに明確に関連している必要があります。
* すべてのバージョンのレガシ パッケージを非推奨にし、人気を受け継ぐ新しいパッケージをポイントするようにする必要があります。
* 人気を引き継ぐことが、NuGet ユーザーの混乱や NuGet 検索エクスペリエンスの悪化を招くことはありません。
* 新しいパッケージには安定したバージョンが必要です。
* レガシ パッケージで別の非推奨パッケージから人気を受け継ぐことはできません。

### <a name="advanced-popularity-transfer-scenarios"></a>高度な人気の引き継ぎシナリオ

#### <a name="package-consolidations"></a>パッケージの統合

1 つの新しいパッケージを優先し、複数の非推奨パッケージの人気を引き継ぐことができます。 たとえば、次の 3 つのパッケージがあるとします。

* 最初の非推奨レガシ パッケージ `Contoso.Legacy1`
* 2 つ目の非推奨レガシ パッケージ `Contoso.Legacy2`
* 新しい統合パッケージ `Contoso.Latest`

`Contoso.Legacy1` と `Contoso.Legacy2` を非推奨にした後で、それらの人気を `Contoso.Latest` に引き継ぐことを申請できます。

#### <a name="package-splits"></a>パッケージの分割

非推奨パッケージの人気を、最大 5 つの新しいパッケージに引き継いで分割することができます。 これは、非推奨パッケージの機能が複数の新しいパッケージに分割されている場合に便利です。 たとえば、次の 3 つのパッケージがあるとします。

* 非推奨レガシ パッケージ `Contoso.Legacy`
* 最初の新しいパッケージ `Contoso.Web`
* 2 つ目の新しいパッケージ `Contoso.Cloud`

`Contoso.Legacy` には、Web とクラウドの両方の機能が含まれていますが、次世代用に、その機能を異なるパッケージに分割することにしました。 `Contoso.Legacy` を非推奨にした後で、その人気を `Contoso.Web` と `Contoso.Cloud` の両方に引き継ぐことを申請できます。

> [!Warning]
> 引き継がれた人気は、すべての新しいパッケージ間で均等に分割されます。 そのため、非推奨パッケージの人気をできるだけ少ないパッケージに引き継ぐことをお勧めします。

#### <a name="popularity-transfer-chains"></a>人気の引き継ぎチェーン

非推奨パッケージでは、別の非推奨パッケージから既に人気を受け継いでいる場合、自身の人気を引き継ぐことはできません。 たとえば、次の 3 つのパッケージがあるとします。

* 非推奨レガシ パッケージ `Contoso.First`
* 非推奨レガシ パッケージ `Contoso.Second`
* 新しいパッケージ `Contoso.Latest`

`Contoso.First` でその人気を `Contoso.Second,` に引き継ぐと、`Contoso.Second` でその人気を `Contoso.Latest` に引き継ぐことはできません。 代わりに、「[パッケージの統合](#package-consolidations)」シナリオに従って、`Contoso.First` と `Contoso.Second` の両方の人気を `Contoso.Latest` に引き継ぐことをお勧めします。
