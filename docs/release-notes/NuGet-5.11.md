---
title: NuGet 5.11 リリース ノート
description: 新機能、バグ修正NuGet DCRs など、NuGet 5.11 のリリース ノート。
author: erdembayar
ms.author: eryondon
ms.date: 8/10/2021
ms.topic: conceptual
ms.openlocfilehash: 97b59be0fa3da2bfb788e540fef795522d938ed4
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2021
ms.locfileid: "122728421"
---
# <a name="nuget-511-release-notes"></a>NuGet 5.11 リリース ノート

NuGet 配布の種類:

| NuGet のバージョン | 利用可能な Visual Studio バージョン | 利用可能な .NET SDK |
|:---|:---|:---|
| [**5.11.0**](https://nuget.org/downloads) | [Visual Studio 2019 バージョン 16.11](https://visualstudio.microsoft.com/downloads/) | [5.0.400](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> .NET Core ワークロードVisual Studio 2019 でインストール済み
  
> [!NOTE]
> Visual Studio 16.11、MSBuild 16.11、および .NET 5.0.400 以降では、NuGet.exe 5.11 以降が必要です。

## <a name="summary-whats-new-in-511"></a>概要: 5.11 の新機能

### <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

**バグ：**

* ツール -> オプション -> NuGet パッケージ マネージャー文字列が切り捨てられる - [#10779](https://github.com/NuGet/Home/issues/10779)

* PackagesMissingStatusChanged イベントが発生すると[ハングする](https://github.com/NuGet/Home/issues/10854)- #10854

* クライアントNuGet設定 - NO_PROXY無視[#10902](https://github.com/NuGet/Home/issues/10902)

**[このリリースで修正された問題の一覧 - 5.11](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTk5MDE)**

**[このリリースのコミットの一覧 - 5.11](https://github.com/NuGet/NuGet.Client/compare/5.10.0.7240...5.11.0.17)**

## <a name="feedback-welcome"></a>フィードバックへようこそ

お客様のフィードバックは Microsoft にとって重要です。  このリリースで問題が発生した場合は、「問題」[](https://github.com/NuGet/Home/issues)と「開発者向けGitHub問題Visual Studio既存[Community確認してください](https://developercommunity.visualstudio.com/)。  このページ内の新しい問題NuGet、問題に関するGitHub[してください](https://github.com/NuGet/Home/issues/new)。
一般的なNuGetエクスペリエンスの問題については、お気に入りの [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)IDE の [問題の報告] オプションの [ヘルプ] の [問題の報告] >**お知らせください**。
