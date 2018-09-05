---
title: NuGet CLI 長いパスのサポート
description: Nuget.exe 長いパスのサポートへの参照
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 7cd387e3eb05d149da9a88cc1c76dc08588d04b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547827"
---
# <a name="long-path-support-nuget-cli"></a>長いパスのサポート (NuGet CLI)

**適用対象:** すべて&bullet;**サポートされているバージョン:** 4.8 +

NuGet.exe 4.8 以降のサポートで長いパスのファイルとディレクトリのシナリオなどのパック、復元、インストール、およびその他のほとんどのシナリオにも、ファイルのパスを必要があります。

## <a name="required-operating-system"></a>必要なオペレーティング システム

-   Windows 10 (バージョン 1607 以降)
-   Windows 10 の 2015 年 7 月リリース (バージョン 1511) .NET Framework 4.6.2 のバージョンにアップグレードする場合またはそれ以降。
-   Windows Server 2016 (すべてのバージョン)

## <a name="enable-win32-long-paths-group-policy"></a>「長いパスの Win32」グループ ポリシーを有効にします。

1 つは、グループ ポリシーを設定してこれらのシステムで長いパスのサポートを有効にする必要があります。

手順:
1. 起動**グループ ポリシー エディター** - 開始の検索バーに「グループ ポリシーの編集」を入力するか、[実行] コマンド (Windows R) から"gpedit.msc"を実行します。
2. **ローカル グループ ポリシー エディター**、有効にする"ローカル コンピューター ポリシー/コンピューターの構成/管理用テンプレート/すべての設定を有効/Win32 長いパス"。

![長いパスのポリシー](media/LongPathPolicy.png)


> [!Note]
> 長いパスをサポートするその他の NuGet ツールを有効にします。
>
> -   Dotnet CLI には、オペレーティング システムやバージョンに関係なく、長いパスがサポートしています。
> -   Visual Studio と msbuild/t:restore は、長いパスをまだサポートしていません。
> -   NuGet ライブラリを使用して、復元、およびその他のコマンドを実行するソフトウェアは、長いパスのサポート、同じシステムで NuGet.exe が動作するも設定する場合は、windows で longPathAware マニフェスト UseLegacyPathHandling を App.Configでfalseに設定[詳細についてを参照してください。](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)

