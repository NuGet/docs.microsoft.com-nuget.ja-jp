---
title: NuGet 3.4.3 リリース ノート
description: NuGet 3.4.3 などのリリース ノートには、問題、バグの修正、追加機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549166"
---
# <a name="nuget-343-release-notes"></a>NuGet 3.4.3 リリース ノート

[NuGet 3.4.2 リリース ノート](../release-notes/nuget-3.4.2.md) | [3.4.4 を NuGet のリリース ノート](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 は 3.4 以降のリリースで識別されたいくつかの問題に対処する、2016 年 4 月 22 日にリリースされました。

VSIX と nuget.exe の両方をダウンロードする[ここ](https://dist.nuget.org/index.html)します。

## <a name="updates-and-improvements"></a>更新プログラムと機能強化

* Visual Studio の信頼性の向上。 Visual Studio でのクラッシュの原因となった NuGet でいくつかの問題を修正しました。

## <a name="fixes"></a>修正プログラム

* パスワードで保護されたプライベート nuget フィードのいくつかの承認の問題を修正しました。
* 周囲の PCL を復元できない問題を修正しました`project.json`指定されたランタイムを使用します。
* 一部のお客様は、パッケージをインストールするときに断続的エラーに実行されていた。 これは、このリリースで修正されましたがようになりました。
* C + での復元の障害を原因となった問題を修正しました/cli CLI を使用するとプロジェクト`project.json`します。
* 一部のパッケージ (例: ModernHttpClient) 場所にない解凍正しく mono で nuget を使用する場合。 これは、このリリースで修正されましたがようになりました。

修正し、このリリースの機能強化の完全な一覧で、問題の一覧をご覧ください[ここ](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)します。