---
title: nuget.org でのパッケージの廃止
description: パッケージの廃止プロセスと、クライアントがこの情報を表示する方法の詳細な説明
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "74096880"
---
# <a name="deprecating-packages"></a>パッケージの廃止

パッケージを維持しなくなった場合、またはパッケージのコンシューマーに別のパッケージへの移動を促したい場合は、パッケージを廃止することができます。 

パッケージの廃止は、以下で説明するように、パッケージを**非公開**にすることとは異なります。
* パッケージを**非公開**にすると、検索結果に表示されなくなるため、検出できません。 
* パッケージを**廃止**すると、パッケージの既存のコンシューマーが、自分のプロジェクトでそれがインストールされているか、使用されているかを調べることができます。 また、廃止の理由や、ユーザー (パッケージの発行元) によって指定された代替の推奨パッケージを知ることもできます。 パッケージを廃止しても、パッケージは非公開になりません。 

発行元は、パッケージを非公開にすることも、廃止することもできます。

## <a name="deprecation-workflow"></a>廃止のワークフロー
1. パッケージを廃止するには、 **[パッケージの管理]** に移動して **[廃止]** を選択します。

    ![パッケージの廃止オプションに移動する](media/deprecation-select-option.png)

2. 廃止するバージョンを選択します。 すべてのバージョンを廃止する場合は、 **[Select all versions]\(バージョンをすべて選択\)** オプションを選択します。

    ![廃止するパッケージのバージョンを選択する](media/deprecation-select-version.png)

3. 廃止の理由を選択します。 パッケージが維持されなくなった場合は、 **[レガシ]** オプションを選択します。 特定のバージョンに重大なバグがある場合は、 **[has critical bugs]\(重大なバグあり\)** オプションを選択します。 その他の理由については、 **[その他]** を選択します。 代替の推奨パッケージ (およびバージョン) とカスタム メッセージを所有者に対していつでも指定できます。 

    ![理由、代替の推奨パッケージ、カスタム メッセージを選択する](media/deprecation-save.png)

> [!Note]
> カスタム メッセージは nuget.org にのみ表示され、クライアントには表示されません。 現時点では、`dotnet.exe` や NuGet パッケージ マネージャーなどのクライアントにはカスタム メッセージが表示されません。

## <a name="client-experience-for-deprecated-packages"></a>非推奨のパッケージのクライアント エクスペリエンス
パッケージが非推奨になると、そのコンシューマーには次の方法で通知されます (使用しているクライアントによって異なります)。

### <a name="visual-studio"></a>Visual Studio 
*Visual Studio 2019 バージョン 16.3 以降に適用*

Visual Studio では `Installed` タブに非推奨のパッケージの使用に関する警告が表示されます。その後、パッケージとその廃止情報 (非推奨とされた理由、代わりに使用する代替パッケージ (存在する場合)) に関する警告が表示されます。

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
