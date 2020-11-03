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
# <a name="long-path-support-nuget-cli"></a>長いパスのサポート (NuGet CLI)

**適用対象:** &bullet; **サポートされているすべてのバージョン:** 4.8 +

NuGet.exe 4.8 以降では、パック、復元、インストール、およびファイルパスを必要とするその他のほとんどのシナリオで、ファイルとディレクトリの長いパスをサポートしています。

## <a name="required-operating-system"></a>必要なオペレーティングシステム

-   Windows 10 (バージョン1607以降)
-   .NET Framework をバージョン4.6.2 以降にアップグレードする場合は、Windows 10 (2015 年7月リリースまたはバージョン 1511)。
-   Windows Server 2016 (すべてのバージョン)

## <a name="enable-win32-long-paths-group-policy"></a>"Win32 長いパス" を有効にするグループポリシー

グループポリシーを設定することによって、これらのシステムで長いパスのサポートを有効にする必要があります。

手順:
1. [スタート] メニューの [グループポリシーの編集] を開始するか、または [実行] コマンド (Windows-R) から "gpedit.msc" を実行して **グループポリシーエディター** を起動します。
2. **ローカルグループポリシーエディター** で、[ローカルコンピューターポリシー/コンピューターの構成]、[管理用テンプレート/すべての設定]、[Win32 長いパスを有効にする] の順に有効にします。

![長いパスのポリシー](media/LongPathPolicy.png)


> [!Note]
> 他の NuGet ツールが長いパスをサポートできるようにする
>
> -   Dotnet CLI では、オペレーティングシステムまたはバージョンに関係なく、長いパスがサポートされます。
> -   Visual Studio またはは、 `msbuild -t:restore` 長いパスをまだサポートしていません。
> -   NuGet ライブラリを使用して復元やその他のコマンドを実行するソフトウェアは、windows マニフェストにも設定されていて、 `longPathAware` `UseLegacyPathHandling` を使用してを構成し `false` [て](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)いる場合に、NuGet.exe が動作する同じシステム上の長いパスをサポート App.Config