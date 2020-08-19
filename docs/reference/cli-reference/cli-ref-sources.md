---
title: NuGet CLI ソースコマンド
description: nuget.exe sources コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 73c9cea8200a1ab1937d25a9a611ae7f2a943dba
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622591"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="8bf6a-103">sources コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8bf6a-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="8bf6a-104">**適用対象:** パッケージの使用、 &bullet; **サポートされるバージョン** の発行: すべて</span><span class="sxs-lookup"><span data-stu-id="8bf6a-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8bf6a-105">ユーザースコープ構成ファイルまたは指定された構成ファイルにあるソースの一覧を管理します。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="8bf6a-106">ユーザースコープ構成ファイルは、 `%appdata%\NuGet\NuGet.Config` (Windows) と `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) にあります。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="8bf6a-107">ここで、nuget.org のソース URL は `https://api.nuget.org/v3/index.json` となります。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="8bf6a-108">使用法</span><span class="sxs-lookup"><span data-stu-id="8bf6a-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="8bf6a-109">ここで `<operation>` 、は *List、Add、Remove、Enable、Disable、* または *Update*のいずれかで、は `<name>` ソースの名前、 `<source>` はソースの URL です。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="8bf6a-110">操作できるソースは一度に1つだけです。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="8bf6a-111">Options</span><span class="sxs-lookup"><span data-stu-id="8bf6a-111">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="8bf6a-112">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8bf6a-113">指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="8bf6a-114">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Format`**

  <span data-ttu-id="8bf6a-115">アクションに適用され、 `list` `Detailed` (既定値) またはにすることができ `Short` ます。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-115">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span>

- **`-?|-help`**

  <span data-ttu-id="8bf6a-116">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-116">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="8bf6a-117">ソースの名前。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-117">Name of the source.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="8bf6a-118">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Password`**

  <span data-ttu-id="8bf6a-119">ソースでの認証に使用するパスワードを指定します。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-119">Specifies the password for authenticating with the source.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="8bf6a-120">パッケージソースへのパス。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-120">Path to the package(s) source.</span></span>

- **`-StorePasswordInClearText`**

  <span data-ttu-id="8bf6a-121">暗号化されたフォームを格納する既定の動作ではなく、暗号化されていないテキストにパスワードを格納することを示します。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-121">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span>

- **`-UserName`**

  <span data-ttu-id="8bf6a-122">ソースでの認証に使用するユーザー名を指定します。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-122">Specifies the user name for authenticating with the source.</span></span>

- **`-ValidAuthenticationTypes`**

  <span data-ttu-id="8bf6a-123">このソースに対して有効な認証の種類のコンマ区切りのリスト。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-123">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="8bf6a-124">既定では、すべての認証の種類が有効です。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-124">By default, all authentication types are valid.</span></span> <span data-ttu-id="8bf6a-125">例: `basic,negotiate`.</span><span class="sxs-lookup"><span data-stu-id="8bf6a-125">Example: `basic,negotiate`.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="8bf6a-126">出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-126">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

> [!Note]
> <span data-ttu-id="8bf6a-127">後でパッケージソースへのアクセスに使用する nuget.exe と同じユーザーコンテキストで、ソースのパスワードを追加してください。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-127">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="8bf6a-128">パスワードは暗号化されて構成ファイルに格納され、暗号化されたときと同じユーザーコンテキストでのみ暗号化を解除できます。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-128">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="8bf6a-129">たとえば、ビルドサーバーを使用して NuGet パッケージを復元する場合、ビルドサーバータスクを実行するのと同じ Windows ユーザーでパスワードを暗号化する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-129">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="8bf6a-130">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="8bf6a-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8bf6a-131">使用例</span><span class="sxs-lookup"><span data-stu-id="8bf6a-131">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
