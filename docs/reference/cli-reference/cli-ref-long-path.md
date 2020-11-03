---
title: NuGet CLI の長いパスのサポート
description: nuget.exe 長いパスのサポートのリファレンス
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 1143da911c80125a9d60e4b98798b11871e9988a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238193"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="84fb4-103">長いパスのサポート (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="84fb4-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="84fb4-104">**適用対象:** &bullet; **サポートされているすべてのバージョン:** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="84fb4-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="84fb4-105">NuGet.exe 4.8 以降では、パック、復元、インストール、およびファイルパスを必要とするその他のほとんどのシナリオで、ファイルとディレクトリの長いパスをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="84fb4-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="84fb4-106">必要なオペレーティングシステム</span><span class="sxs-lookup"><span data-stu-id="84fb4-106">Required Operating System</span></span>

-   <span data-ttu-id="84fb4-107">Windows 10 (バージョン1607以降)</span><span class="sxs-lookup"><span data-stu-id="84fb4-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="84fb4-108">.NET Framework をバージョン4.6.2 以降にアップグレードする場合は、Windows 10 (2015 年7月リリースまたはバージョン 1511)。</span><span class="sxs-lookup"><span data-stu-id="84fb4-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="84fb4-109">Windows Server 2016 (すべてのバージョン)</span><span class="sxs-lookup"><span data-stu-id="84fb4-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="84fb4-110">"Win32 長いパス" を有効にするグループポリシー</span><span class="sxs-lookup"><span data-stu-id="84fb4-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="84fb4-111">グループポリシーを設定することによって、これらのシステムで長いパスのサポートを有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="84fb4-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="84fb4-112">手順:</span><span class="sxs-lookup"><span data-stu-id="84fb4-112">Steps:</span></span>
1. <span data-ttu-id="84fb4-113">[スタート] メニューの [グループポリシーの編集] を開始するか、または [実行] コマンド (Windows-R) から "gpedit.msc" を実行して **グループポリシーエディター** を起動します。</span><span class="sxs-lookup"><span data-stu-id="84fb4-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="84fb4-114">**ローカルグループポリシーエディター** で、[ローカルコンピューターポリシー/コンピューターの構成]、[管理用テンプレート/すべての設定]、[Win32 長いパスを有効にする] の順に有効にします。</span><span class="sxs-lookup"><span data-stu-id="84fb4-114">In the **Local Group Policy Editor** , enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![長いパスのポリシー](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="84fb4-116">他の NuGet ツールが長いパスをサポートできるようにする</span><span class="sxs-lookup"><span data-stu-id="84fb4-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="84fb4-117">Dotnet CLI では、オペレーティングシステムまたはバージョンに関係なく、長いパスがサポートされます。</span><span class="sxs-lookup"><span data-stu-id="84fb4-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="84fb4-118">Visual Studio またはは、 `msbuild -t:restore` 長いパスをまだサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="84fb4-118">Visual Studio or `msbuild -t:restore` does not yet support long paths.</span></span>
> -   <span data-ttu-id="84fb4-119">NuGet ライブラリを使用して復元やその他のコマンドを実行するソフトウェアは、windows マニフェストにも設定されていて、 `longPathAware` `UseLegacyPathHandling` を使用してを構成し `false` [て](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)いる場合に、NuGet.exe が動作する同じシステム上の長いパスをサポート App.Config</span><span class="sxs-lookup"><span data-stu-id="84fb4-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set `longPathAware` in their windows manifest and configure `UseLegacyPathHandling` to `false` via App.Config [See more information](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)</span></span>