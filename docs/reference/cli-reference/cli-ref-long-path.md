---
title: NuGet CLI の長いパスのサポート
description: Nuget.exe の長いパスのサポートのリファレンス
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 9b5a97d963eab7fbbde4aefae1c9b1a8bfcdeb11
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036956"
---
# <a name="long-path-support-nuget-cli"></a>長いパスのサポート (NuGet CLI)

**適用対象:** &bullet;**サポートされているすべてのバージョン:** 4.8 +

Nuget.exe 4.8 以降では、パック、復元、インストールなど、ファイルパスを必要とするその他のシナリオのために、ファイルおよびディレクトリの長いパスがサポートされます。

## <a name="required-operating-system"></a>必要なオペレーティングシステム

-   Windows 10 (バージョン1607以降)
-   .NET Framework をバージョン4.6.2 以降にアップグレードする場合は、Windows 10 (2015 年7月リリースまたはバージョン 1511)。
-   Windows Server 2016 (すべてのバージョン)

## <a name="enable-win32-long-paths-group-policy"></a>"Win32 長いパス" を有効にするグループポリシー

グループポリシーを設定することによって、これらのシステムで長いパスのサポートを有効にする必要があります。

手順:
1. [スタート] メニューの [グループポリシーの編集] を開始するか、または [実行] コマンド (Windows-R) から "gpedit.msc" を実行して**グループポリシーエディター**を起動します。
2. **ローカルグループポリシーエディター**で、[ローカルコンピューターポリシー/コンピューターの構成]、[管理用テンプレート/すべての設定]、[Win32 長いパスを有効にする] の順に有効にします。

![長いパスのポリシー](media/LongPathPolicy.png)


> [!Note]
> 他の NuGet ツールが長いパスをサポートできるようにする
>
> -   Dotnet CLI では、オペレーティングシステムまたはバージョンに関係なく、長いパスがサポートされます。
> -   Visual Studio または `msbuild -t:restore` は、長いパスをまだサポートしていません。
> -   NuGet ライブラリを使用して復元などのコマンドを実行するソフトウェアでは、Nuget.exe が動作するのと同じシステム上の長いパスがサポートされます。これは、windows マニフェストで `longPathAware` を設定し、App.config を使用して `false` するように `UseLegacyPathHandling` を構成する場合は、[詳細を参照してください](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)。

