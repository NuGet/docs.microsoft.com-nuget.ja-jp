---
title: NuGet 5.4 リリースノート
description: 新機能、バグ修正、および DCRs を含む NuGet 5.4 のリリースノート。
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 69f78ba5483fcc92887624584663e8c496cfc497
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74828394"
---
# <a name="nuget-54-release-notes"></a>NuGet 5.4 リリースノート

NuGet 配布の種類:

| NuGet のバージョン | 利用可能な Visual Studio バージョン| 利用可能な .NET SDK|
|:---|:---|:---|
| [**5.4.0**](https://nuget.org/downloads) | [Visual Studio 2019 バージョン16.4](https://visualstudio.microsoft.com/downloads/) | [3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup>.NET Core ワークロードを含む Visual Studio 2019 と共にインストールされます。

## <a name="summary-whats-new-in-54"></a>概要: 5.4 の新機能

* ソリューションの読み込み時間の短縮-最初のソリューションの読み込み中に NuGet コードを実行するオーバーヘッドが、JIT コストを削減するために部分的な ngen を使用して削減されました- [#6007](https://github.com/NuGet/Home/issues/6007)

* 新しいヘルパー関数-パッケージ id とバージョンの一覧が表示されたら、最上位レベルのパッケージを取得します。 - [#8316](https://github.com/NuGet/Home/issues/8316)

### <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

**バグ**

* プラグイン: linux/Mac [#8747](https://github.com/NuGet/Home/issues/8747)での時間の精度のログ記録がオフになっています

* プラグインを破棄すると、操作全体がスローされ、失敗する場合があります。 - [#8732](https://github.com/NuGet/Home/issues/8732)

* PMUI- [#8679](https://github.com/NuGet/Home/issues/8679)で、許可されているバージョンとブロックされているバージョンの一覧でのバージョンの重複の表示を停止します

* ロックファイルが正しく生成されませんでした。フレームワークの順序付けは、 [#8645](https://github.com/NuGet/Home/issues/8645) lockedmode による復元に影響しないようにしてください。

* SDK 3.0.100 で <RuntimeIdentifiers> が設定されるプロジェクトの LockFile 検証が失敗する- [#8639](https://github.com/NuGet/Home/issues/8639)

* 署名の検証では、同じ OID の下に2つの値を持つタイムスタンプの署名が適切に拒否されるようになりました- [#8629](https://github.com/NuGet/Home/issues/8629)

* ライセンスリストを更新する- [#8544](https://github.com/NuGet/Home/issues/8544)

**Dcr**

* 診断ファイルを IFeedbackDiagnosticFileProvider にオンボードする[#8535](https://github.com/NuGet/Home/issues/8535)

**[このリリースで修正されるすべての問題の一覧-5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**
