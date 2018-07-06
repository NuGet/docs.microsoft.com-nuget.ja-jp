---
title: NuGet のエラーと警告のリファレンス
description: 警告やエラーはさまざまな NuGet 操作中に、NuGet から発行された完全なリファレンスです。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 25c8a22fc0bce2372c54cf29b904a8d9fbbe9ace
ms.sourcegitcommit: 8e3546ab630a24cde8725610b6a68f8eb87afa47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/05/2018
ms.locfileid: "37843431"
---
# <a name="errors-and-warnings"></a>エラーと警告

NuGet 4.3.0 では、このトピックで説明したように番号がエラーと警告し、関連する問題に対処するための詳細情報を提供します。

エラーと警告の次のとおりでのみ使用可能な[PackageReference ベース](../consume-packages/package-references-in-project-files.md)プロジェクトと NuGet 4.3.0 です。 NuGet では、警告を抑制するかをエラーに昇格する MSBuild プロパティも容認されます。 詳細については、次を参照してください。[方法: コンパイラの警告を抑制する](/visualstudio/ide/how-to-suppress-compiler-warnings)Visual Studio のドキュメント。

**エラー**

| グループ化 | エラー番号 |
| --- | --- |
| 無効な入力エラー | [NU1001](./errors-and-warnings/NU1001.md)、 [NU1002](./errors-and-warnings/NU1002.md)、 [NU1003](./errors-and-warnings/NU1003.md) |
| パッケージとプロジェクトの不足エラー | [NU1100](./errors-and-warnings/NU1100.md)、 [NU1101](./errors-and-warnings/NU1101.md)、 [NU1102](./errors-and-warnings/NU1102.md)、 [NU1103](./errors-and-warnings/NU1103.md)、 [NU1104](./errors-and-warnings/NU1104.md)、 [NU1105](./errors-and-warnings/NU1105.md)、 [NU1106](./errors-and-warnings/NU1106.md)、 [NU1107](./errors-and-warnings/NU1107.md) (NU1607 以前) [NU1108](./errors-and-warnings/NU1108.md) (NU1606 以前) |
| 互換性エラー | [NU1201](./errors-and-warnings/NU1201.md)、 [NU1202](./errors-and-warnings/NU1202.md)、 [NU1203](./errors-and-warnings/NU1203.md)、 [NU1401](./errors-and-warnings/NU1401.md) |
| NuGet 内部エラー | [NU1000](./errors-and-warnings/NU1000.md) |
| 署名済みパッケージのエラー (作成と検証) | [NU3000](./errors-and-warnings/NU3000.md)、 [NU3001](./errors-and-warnings/NU3001.md)、 [NU3004](./errors-and-warnings/NU3004.md)、 [NU3008](./errors-and-warnings/NU3008.md) |

**Warnings**

| グループ化 | 警告番号 |
| --- | --- |
| 無効な入力の警告 | [NU1501](./errors-and-warnings/NU1501.md)、 [NU1502](./errors-and-warnings/NU1502.md)、 [NU1503](./errors-and-warnings/NU1503.md) |
| 予期しないパッケージのバージョンの警告 | [NU1601](./errors-and-warnings/NU1601.md)、 [NU1602](./errors-and-warnings/NU1602.md)、 [NU1603](./errors-and-warnings/NU1603.md)、 [NU1604](./errors-and-warnings/NU1604.md)、 [NU1605](./errors-and-warnings/NU1605.md) |
| 競合回避モジュールの競合の警告 | [NU1608](./errors-and-warnings/NU1608.md) |
| パッケージ フォールバック警告 | [NU1701](./errors-and-warnings/NU1701.md) |
| フィードの警告 | [NU1801](./errors-and-warnings/NU1801.md) |
| NuGet 内部の警告 | [NU1500](./errors-and-warnings/NU1500.md) |
| 署名済みパッケージの警告 (作成と検証) | [NU3002](./errors-and-warnings/NU3002.md)、 [NU3018](./errors-and-warnings/NU3018.md)、 [NU3028](./errors-and-warnings/NU3028.md) |
