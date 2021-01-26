---
title: NuGet 3.4.3 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.4.3 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776466"
---
# <a name="nuget-343-release-notes"></a>NuGet 3.4.3 のリリースノート

[NuGet 3.4.2 のリリースノート](../release-notes/nuget-3.4.2.md)  | [NuGet 3.4.4 のリリースノート](../release-notes/nuget-3.4.4.md)

2016年4月22日にリリースされた NuGet 3.4.3 は、3.4 以降のリリースで特定されたいくつかの問題に対処しています。

VSIX と nuget.exe の両方を [ここで](https://dist.nuget.org/index.html)ダウンロードできます。

## <a name="updates-and-improvements"></a>更新プログラムと機能強化

* Visual Studio の信頼性が向上しました。 Visual Studio のクラッシュの原因となった NuGet のいくつかの問題を修正しました。

## <a name="fixes"></a>修正

* パスワードで保護されたプライベート nuget フィードに関する一部の承認の問題を修正した。
* 指定されたランタイムで PCL のを復元できない問題を修正 `project.json` しました。
* 一部のお客様は、パッケージのインストール時に断続的にエラーが発生していました。 これは、今回のリリースで修正されました。
* での C++/CLI プロジェクトの復元エラーの原因となった問題を修正しました `project.json` 。
* Mono で nuget を使用すると、正しく解凍されていないパッケージ (ModernHttpClient など) があります。 これは、今回のリリースで修正されました。

このリリースの修正プログラムと機能強化の完全な一覧については、 [ここ](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)で問題の一覧を確認してください。