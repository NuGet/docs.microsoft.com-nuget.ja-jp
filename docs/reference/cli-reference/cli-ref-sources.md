---
title: source コマンド (NuGet CLI)
description: Nuget.exe の source コマンドリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327599"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="ef83b-103">source コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ef83b-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="ef83b-104">**適用対象:** パッケージの使用、 &bullet; **サポートされるバージョン**の発行: すべて</span><span class="sxs-lookup"><span data-stu-id="ef83b-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ef83b-105">ユーザースコープ構成ファイルまたは指定された構成ファイルにあるソースの一覧を管理します。</span><span class="sxs-lookup"><span data-stu-id="ef83b-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="ef83b-106">ユーザースコープ構成ファイルは、(Windows `%appdata%\NuGet\NuGet.Config` ) と`~/.nuget/NuGet/NuGet.Config` (Mac/Linux) にあります。</span><span class="sxs-lookup"><span data-stu-id="ef83b-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="ef83b-107">ここで、nuget.org のソース URL は `https://api.nuget.org/v3/index.json` となります。</span><span class="sxs-lookup"><span data-stu-id="ef83b-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="ef83b-108">使用法</span><span class="sxs-lookup"><span data-stu-id="ef83b-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="ef83b-109">ここ`<operation>`で、は*List、Add、Remove、Enable、Disable、* または Update `<name>`のいずれかで、はソース`<source>`の名前、はソースの URL です。</span><span class="sxs-lookup"><span data-stu-id="ef83b-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="ef83b-110">操作できるソースは一度に1つだけです。</span><span class="sxs-lookup"><span data-stu-id="ef83b-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="ef83b-111">オプション</span><span class="sxs-lookup"><span data-stu-id="ef83b-111">Options</span></span>

| <span data-ttu-id="ef83b-112">オプション</span><span class="sxs-lookup"><span data-stu-id="ef83b-112">Option</span></span> | <span data-ttu-id="ef83b-113">説明</span><span class="sxs-lookup"><span data-stu-id="ef83b-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ef83b-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ef83b-114">ConfigFile</span></span> | <span data-ttu-id="ef83b-115">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="ef83b-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ef83b-116">指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="ef83b-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ef83b-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ef83b-117">ForceEnglishOutput</span></span> | <span data-ttu-id="ef83b-118">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="ef83b-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ef83b-119">Format</span><span class="sxs-lookup"><span data-stu-id="ef83b-119">Format</span></span> | <span data-ttu-id="ef83b-120">`list`アクションに適用され、 `Detailed` (既定値) または`Short`にすることができます。</span><span class="sxs-lookup"><span data-stu-id="ef83b-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="ef83b-121">Help</span><span class="sxs-lookup"><span data-stu-id="ef83b-121">Help</span></span> | <span data-ttu-id="ef83b-122">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="ef83b-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="ef83b-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="ef83b-123">NonInteractive</span></span> | <span data-ttu-id="ef83b-124">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="ef83b-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ef83b-125">Password</span><span class="sxs-lookup"><span data-stu-id="ef83b-125">Password</span></span> | <span data-ttu-id="ef83b-126">ソースでの認証に使用するパスワードを指定します。</span><span class="sxs-lookup"><span data-stu-id="ef83b-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="ef83b-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="ef83b-127">StorePasswordInClearText</span></span> | <span data-ttu-id="ef83b-128">暗号化されたフォームを格納する既定の動作ではなく、暗号化されていないテキストにパスワードを格納することを示します。</span><span class="sxs-lookup"><span data-stu-id="ef83b-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="ef83b-129">UserName</span><span class="sxs-lookup"><span data-stu-id="ef83b-129">UserName</span></span> | <span data-ttu-id="ef83b-130">ソースでの認証に使用するユーザー名を指定します。</span><span class="sxs-lookup"><span data-stu-id="ef83b-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="ef83b-131">Verbosity</span><span class="sxs-lookup"><span data-stu-id="ef83b-131">Verbosity</span></span> | <span data-ttu-id="ef83b-132">出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*</span><span class="sxs-lookup"><span data-stu-id="ef83b-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="ef83b-133">Nuget を後で使用してパッケージソースにアクセスするのと同じユーザーコンテキストで、ソースのパスワードを追加してください。</span><span class="sxs-lookup"><span data-stu-id="ef83b-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="ef83b-134">パスワードは暗号化されて構成ファイルに格納され、暗号化されたときと同じユーザーコンテキストでのみ暗号化を解除できます。</span><span class="sxs-lookup"><span data-stu-id="ef83b-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="ef83b-135">たとえば、ビルドサーバーを使用して NuGet パッケージを復元する場合、ビルドサーバータスクを実行するのと同じ Windows ユーザーでパスワードを暗号化する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef83b-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="ef83b-136">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="ef83b-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ef83b-137">使用例</span><span class="sxs-lookup"><span data-stu-id="ef83b-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
