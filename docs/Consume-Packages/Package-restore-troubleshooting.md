---
title: "Visual Studio での NuGet パッケージの復元に関するトラブルシューティング | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: b70326a0-5bfc-4b7c-881d-7a7d5ebeeed5
description: "Visual Studio の一般的な NuGet の復元エラーの説明とトラブルシューティングの方法です。"
keywords: "NuGet パッケージの復元、パッケージの復元、トラブルシューティング、問題解決"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c23a9ed2b7cffbf904018a089ccde000adaa517f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a><span data-ttu-id="b1e24-104">Visual Studio でのパッケージの復元エラーのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="b1e24-104">Troubleshooting package restore errors in Visual Studio</span></span>

> [!Note]
> <span data-ttu-id="b1e24-105">このページでは、Visual Studio でパッケージを復元するときの一般的なエラーと、これらのエラーを解決する手順に重点を置いて説明しています。</span><span class="sxs-lookup"><span data-stu-id="b1e24-105">This page focuses on common errors when restoring packages in Visual Studio and steps to resolve them.</span></span> <span data-ttu-id="b1e24-106">パッケージの復元方法については、「[パッケージの復元](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b1e24-106">For how-to restore packages, see [Package restore](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="b1e24-107">既定では、Visual Studio でプロジェクトをビルドすると、プロジェクトで参照される NuGet パッケージが自動的に復元されます。</span><span class="sxs-lookup"><span data-stu-id="b1e24-107">By default, building a project in Visual Studio automatically restores NuGet packages referenced in the project.</span></span> <span data-ttu-id="b1e24-108">ただし、パッケージの復元が **[ツール] > [オプション] > [NuGet パッケージ マネージャー] > [パッケージの復元]** の設定で無効になっていて、必要なパッケージが自分のコンピューター上で利用できない場合、ビルドは失敗します。</span><span class="sxs-lookup"><span data-stu-id="b1e24-108">However, builds will fail if package restore is disabled in the **Tools > Options > NuGet Package Manager > Package Restore** settings and the necessary packages are not available on your computer.</span></span> <span data-ttu-id="b1e24-109">このような場合、次のエラーが表示される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b1e24-109">In these cases you may see the following errors:</span></span>

```
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

```
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name} 
```

<span data-ttu-id="b1e24-110">パッケージの復元を有効にするには、**[ツール] > [オプション] > [NuGet パッケージ マネージャー]** を開いて、**[見つからないパッケージのダウンロードを NuGet に許可]** と **[Visual Studio でのビルド中に見つからないパッケージを自動的に確認]** のオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="b1e24-110">To enable package restore, open **Tools > Options > NuGet Package Manager** and select the options for **Allow NuGet to download missing packages** and **Automatically check for missing packages during build in Visual Studio**:</span></span>

![[ツール]/[オプション] で NuGet パッケージの復元を有効にする](../Consume-Packages/media/restore-01-autorestoreoptions.png)

