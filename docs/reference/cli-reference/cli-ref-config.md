---
title: NuGet CLI 構成コマンド
description: nuget.exe config コマンドのリファレンス
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3d50c12e34f71d7a62fe177da1dbb33eb702347a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775956"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="bdfaf-103">config コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="bdfaf-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="bdfaf-104">**適用対象:** &bullet; **サポートされている** すべてのバージョン: すべて</span><span class="sxs-lookup"><span data-stu-id="bdfaf-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="bdfaf-105">NuGet 構成値を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="bdfaf-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="bdfaf-106">その他の使用方法については、「 [Common NuGet の構成](../../consume-packages/configuring-nuget-behavior.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bdfaf-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="bdfaf-107">使用可能なキー名の詳細については、 [NuGet 構成ファイルのリファレンス](../nuget-config-file.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bdfaf-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="bdfaf-108">使用方法</span><span class="sxs-lookup"><span data-stu-id="bdfaf-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="bdfaf-109">とは、 `<name>` `<value>` 構成で設定されるキーと値のペアを指定します。</span><span class="sxs-lookup"><span data-stu-id="bdfaf-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="bdfaf-110">必要に応じて、ペアをいくつでも指定できます。</span><span class="sxs-lookup"><span data-stu-id="bdfaf-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="bdfaf-111">値を削除するには、名前と符号を指定しますが、値は指定し `=` ません。</span><span class="sxs-lookup"><span data-stu-id="bdfaf-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="bdfaf-112">使用可能なキー名については、 [NuGet 構成ファイルのリファレンス](../nuget-config-file.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bdfaf-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="bdfaf-113">NuGet 3.4 以降で `<value>` は、は [環境変数](cli-ref-environment-variables.md)を使用できます。</span><span class="sxs-lookup"><span data-stu-id="bdfaf-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="bdfaf-114">Options</span><span class="sxs-lookup"><span data-stu-id="bdfaf-114">Options</span></span>


- **`AsPath`**

  <span data-ttu-id="bdfaf-115">構成値をパスとして返し `-Set` ます。が使用されている場合は無視されます。</span><span class="sxs-lookup"><span data-stu-id="bdfaf-115">Returns the config value as a path, ignored when `-Set` is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="bdfaf-116">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="bdfaf-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="bdfaf-117">指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="bdfaf-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="bdfaf-118">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="bdfaf-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="bdfaf-119">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="bdfaf-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="bdfaf-120">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="bdfaf-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-Set`**

  <span data-ttu-id="bdfaf-121">1つは config で設定されるキーと値のペアの数です。</span><span class="sxs-lookup"><span data-stu-id="bdfaf-121">One on more key-value pairs to be set in config.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="bdfaf-122">出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。</span><span class="sxs-lookup"><span data-stu-id="bdfaf-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="bdfaf-123">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="bdfaf-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="bdfaf-124">使用例</span><span class="sxs-lookup"><span data-stu-id="bdfaf-124">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
