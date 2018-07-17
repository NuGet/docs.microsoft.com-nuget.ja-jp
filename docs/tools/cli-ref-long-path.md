---
title: NuGet CLI 長いパスのサポート
description: Nuget.exe 長いパスのサポートへの参照
author: zhili1208
ms.author: lzhi
manager: rob
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 0119be3fd8fd6c2e06e0135de5e498e0730bb0cc
ms.sourcegitcommit: a76ecc58f41c2c5b3536ff4a3f3fcbdf5258177c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/17/2018
ms.locfileid: "39072735"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="18505-103">長いパスのサポート (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="18505-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="18505-104">**適用対象:** すべて&bullet;**サポートされているバージョン:** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="18505-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="18505-105">NuGet.exe 4.8 以降のサポートで長いパスのファイルとディレクトリのシナリオなどのパック、復元、インストール、およびその他のほとんどのシナリオにも、ファイルのパスを必要があります。</span><span class="sxs-lookup"><span data-stu-id="18505-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="18505-106">必要なオペレーティング システム</span><span class="sxs-lookup"><span data-stu-id="18505-106">Required Operating System</span></span>

-   <span data-ttu-id="18505-107">Windows 10 (バージョン 1607 以降)</span><span class="sxs-lookup"><span data-stu-id="18505-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="18505-108">Windows 10 の 2015 年 7 月リリース (バージョン 1511) .NET Framework 4.6.2 のバージョンにアップグレードする場合またはそれ以降。</span><span class="sxs-lookup"><span data-stu-id="18505-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="18505-109">Windows Server 2016 (すべてのバージョン)</span><span class="sxs-lookup"><span data-stu-id="18505-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="18505-110">「長いパスの Win32」グループ ポリシーを有効にします。</span><span class="sxs-lookup"><span data-stu-id="18505-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="18505-111">1 つは、グループ ポリシーを設定してこれらのシステムで長いパスのサポートを有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="18505-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="18505-112">手順:</span><span class="sxs-lookup"><span data-stu-id="18505-112">Steps:</span></span>
1. <span data-ttu-id="18505-113">起動**グループ ポリシー エディター** - 開始の検索バーに「グループ ポリシーの編集」を入力するか、[実行] コマンド (Windows R) から"gpedit.msc"を実行します。</span><span class="sxs-lookup"><span data-stu-id="18505-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="18505-114">**ローカル グループ ポリシー エディター**、有効にする"ローカル コンピューター ポリシー/コンピューターの構成/管理用テンプレート/すべての設定を有効/Win32 長いパス"。</span><span class="sxs-lookup"><span data-stu-id="18505-114">In the **Local Group Policy Editor**, enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![長いパスのポリシー](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="18505-116">長いパスをサポートするその他の NuGet ツールを有効にします。</span><span class="sxs-lookup"><span data-stu-id="18505-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="18505-117">Dotnet CLI には、オペレーティング システムやバージョンに関係なく、長いパスがサポートしています。</span><span class="sxs-lookup"><span data-stu-id="18505-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="18505-118">Visual Studio と msbuild/t:restore は、長いパスをまだサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="18505-118">Visual Studio or msbuild /t:restore does not yet support long paths.</span></span>
> -   <span data-ttu-id="18505-119">NuGet ライブラリを使用して、復元、およびその他のコマンドを実行するソフトウェアは、長いパスのサポート、同じシステムで NuGet.exe が動作するも設定する場合は、windows で longPathAware マニフェスト UseLegacyPathHandling を App.Configでfalseに設定[詳細についてを参照してください。](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span><span class="sxs-lookup"><span data-stu-id="18505-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set longPathAware in their windows manifest and configure UseLegacyPathHandling to false via App.Config [See more information](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span></span>

