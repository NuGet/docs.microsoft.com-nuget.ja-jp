---
title: NuGet CLI コマンドをソースします。
description: ソースのコマンドを nuget.exe への参照
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7ef856f783c8e11cdb40edb0d1c1458730d87262
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548109"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="b9575-103">ソースのコマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b9575-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="b9575-104">**適用対象:** パッケージの使用、公開&bullet;**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="b9575-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b9575-105">ユーザー スコープの構成ファイルまたは指定した構成ファイル内にあるソースの一覧を管理します。</span><span class="sxs-lookup"><span data-stu-id="b9575-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="b9575-106">ユーザー スコープの構成ファイルは`%appdata%\NuGet\NuGet.Config`(Windows) と`~/.nuget/NuGet/NuGet.Config`(Mac/linux)。</span><span class="sxs-lookup"><span data-stu-id="b9575-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="b9575-107">ここで、nuget.org のソース URL は `https://api.nuget.org/v3/index.json` となります。</span><span class="sxs-lookup"><span data-stu-id="b9575-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="b9575-108">使用法</span><span class="sxs-lookup"><span data-stu-id="b9575-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="b9575-109">場所`<operation>`の 1 つです*を一覧表示、追加、削除、有効にする、無効化、* または*更新*、 `<name>` 、ソースの名前を指定および`<source>`はソースの URL です。</span><span class="sxs-lookup"><span data-stu-id="b9575-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="b9575-110">オプション</span><span class="sxs-lookup"><span data-stu-id="b9575-110">Options</span></span>

| <span data-ttu-id="b9575-111">オプション</span><span class="sxs-lookup"><span data-stu-id="b9575-111">Option</span></span> | <span data-ttu-id="b9575-112">説明</span><span class="sxs-lookup"><span data-stu-id="b9575-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b9575-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b9575-113">ConfigFile</span></span> | <span data-ttu-id="b9575-114">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="b9575-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b9575-115">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="b9575-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b9575-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b9575-116">ForceEnglishOutput</span></span> | <span data-ttu-id="b9575-117">*(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="b9575-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b9575-118">形式</span><span class="sxs-lookup"><span data-stu-id="b9575-118">Format</span></span> | <span data-ttu-id="b9575-119">適用されます、`list`アクションを指定できます`Detailed`(既定値) または`Short`します。</span><span class="sxs-lookup"><span data-stu-id="b9575-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="b9575-120">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="b9575-120">Help</span></span> | <span data-ttu-id="b9575-121">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="b9575-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="b9575-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b9575-122">NonInteractive</span></span> | <span data-ttu-id="b9575-123">ユーザー入力や確認のプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="b9575-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b9575-124">[Password]</span><span class="sxs-lookup"><span data-stu-id="b9575-124">Password</span></span> | <span data-ttu-id="b9575-125">ソースと認証のパスワードを指定します。</span><span class="sxs-lookup"><span data-stu-id="b9575-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="b9575-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="b9575-126">StorePasswordInClearText</span></span> | <span data-ttu-id="b9575-127">暗号化された形式を格納する既定の動作ではなく暗号化されていないテキストでパスワードを保存することを示します。</span><span class="sxs-lookup"><span data-stu-id="b9575-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="b9575-128">UserName</span><span class="sxs-lookup"><span data-stu-id="b9575-128">UserName</span></span> | <span data-ttu-id="b9575-129">ソースと認証のユーザー名を指定します。</span><span class="sxs-lookup"><span data-stu-id="b9575-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="b9575-130">詳細度</span><span class="sxs-lookup"><span data-stu-id="b9575-130">Verbosity</span></span> | <span data-ttu-id="b9575-131">出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。</span><span class="sxs-lookup"><span data-stu-id="b9575-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="b9575-132">必ず、nuget.exe が後でパッケージ ソースへのアクセスに使用されるため、同じユーザー コンテキストでのソースのパスワードを追加してください。</span><span class="sxs-lookup"><span data-stu-id="b9575-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="b9575-133">パスワードは、構成ファイルで暗号化して保存してが暗号化されたために、同じユーザー コンテキストで解除のみできます。</span><span class="sxs-lookup"><span data-stu-id="b9575-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="b9575-134">そのため、たとえば使用する場合、ビルド サーバー、ビルド サーバーのタスクを実行する同じ Windows ユーザーがパスワードを暗号化する必要があります NuGet パッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="b9575-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="b9575-135">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b9575-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b9575-136">使用例</span><span class="sxs-lookup"><span data-stu-id="b9575-136">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
