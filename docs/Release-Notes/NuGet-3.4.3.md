---
title: NuGet 3.4.3 リリース ノート
description: NuGet 3.4.3 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6c25d3b678e6e72eca3e1157f91a75bfa8cbb18e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-343-release-notes"></a>NuGet 3.4.3 リリース ノート

[NuGet 3.4.2 リリース ノート](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 リリース ノート](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 は、2016 年 4 月 22 日 3.4 以降のリリースで識別されたいくつかの問題を解決するにリリースされました。

VSIX と nuget.exe の両方をダウンロードする[ここ](https://dist.nuget.org/index.html)です。

## <a name="updates-and-improvements"></a>更新プログラムと機能強化

* Visual Studio、信頼性が向上します。 Visual Studio でのクラッシュの原因となった NuGet でいくつかの問題が解決されました。

## <a name="fixes"></a>修正プログラム

* 固定いくつかの認証の問題はパスワードで保護されたプライベート nuget フィードです。
* 問題を修正、周囲から PCL を復元することができません`project.json`指定されたランタイムを使用します。
* 一部のお客様は、パッケージをインストールするときに断続的なエラーに実行されていた。 これは、このリリースで修正されましたがようになりました。
* C + の復元の障害の原因となった問題を修正しました + CLI プロジェクトに関するプロジェクト`project.json`です。
* 一部のパッケージ (例: ModernHttpClient) 場所にない解凍正しくモノラルで nuget を使用する場合。 これは、このリリースで修正されましたがようになりました。

、修正し、このリリースの機能強化の完全な一覧を確認して問題の一覧[ここ](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)です。