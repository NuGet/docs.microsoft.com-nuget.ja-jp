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
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a>Visual Studio でのパッケージの復元エラーのトラブルシューティング

> [!Note]
> このページでは、Visual Studio でパッケージを復元するときの一般的なエラーと、これらのエラーを解決する手順に重点を置いて説明しています。 パッケージの復元方法については、「[パッケージの復元](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore)」を参照してください。

既定では、Visual Studio でプロジェクトをビルドすると、プロジェクトで参照される NuGet パッケージが自動的に復元されます。 ただし、パッケージの復元が **[ツール] > [オプション] > [NuGet パッケージ マネージャー] > [パッケージの復元]** の設定で無効になっていて、必要なパッケージが自分のコンピューター上で利用できない場合、ビルドは失敗します。 このような場合、次のエラーが表示される可能性があります。

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

パッケージの復元を有効にするには、**[ツール] > [オプション] > [NuGet パッケージ マネージャー]** を開いて、**[見つからないパッケージのダウンロードを NuGet に許可]** と **[Visual Studio でのビルド中に見つからないパッケージを自動的に確認]** のオプションを選択します。

![[ツール]/[オプション] で NuGet パッケージの復元を有効にする](../Consume-Packages/media/restore-01-autorestoreoptions.png)

