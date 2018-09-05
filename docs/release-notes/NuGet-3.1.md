---
title: NuGet 3.1 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 3.1 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 779567d94a5a9a1b3eacddaa4c882201a446cb4b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545348"
---
# <a name="nuget-31-release-notes"></a>NuGet 3.1 リリース ノート

[NuGet 3.0 リリース ノート](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 リリース ノート](../release-notes/nuget-3.1.1.md)

NuGet 3.1 は、Visual Studio 2015 用ユニバーサル Windows プラットフォーム SDK にバンドルされている拡張機能として、2015 年 7 月 27 日にリリースされました。 このリリースには、Windows プラットフォーム SDK を配信される、その Windows 開発のエクスペリエンスは以前に起動されている NuGet のクロスプラット フォームで作業の利用可能性があります。 この NuGet 拡張機能のバージョンは、Visual Studio 2015 のできるだけです。

バグ修正と新機能と更新プログラムを常に公開するように使用可能な最新バージョンの Visual Studio ギャラリー更新プログラムにアクセスできる開発者をお勧めします。

## <a name="nuget-visual-studio-extension"></a>NuGet Visual Studio の拡張機能

問題と、このリリースの機能を使用して GitHub にタグが付けられた、 [「3.1 の RTM UWP 推移的なサポート」マイルス トーン](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)3.1 のリリースでは 67 の問題の合計を終了します。

### <a name="new-features"></a>新機能

* `project.json` Windows UWP および ASP.NET 5 のサポートのサポート
* 推移的なパッケージのインストール

これらの機能の説明と定義は、ドキュメントの他の場所で見つかんだことができます。

### <a name="deprecated"></a>非推奨とされます。

Visual Studio 2015 の次の機能は無効になります。

* ソリューション レベル パッケージをインストールすることができません。

次の機能は Visual Studio 2015 を使用するプロジェクトを利用できなく、`project.json`仕様

* `install.ps1` `uninstall.ps1` -これらのスクリプトは、パッケージのインストール時に無視する、復元、更新、およびアンインストール
* 構成の変換は無視されます。
* コンテンツは、実行しますが、プロジェクトにコピーされません。
    * チームはこの機能を再実装やディスカッションをフォローするで進行状況に取り組んでいます。 [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>既知の問題

このリリースで提供される既知の問題が発生しました。

* Windows 10 SDK を使用した 3.1 リリースのインストールが以前にインストールされた NuGet 拡張機能の任意のバージョンをダウン グレードします。

## <a name="nuget-command-line"></a>NuGet コマンドライン

NuGet コマンドライン実行可能ファイルが更新され、使用可能にする履歴のバージョンの nuget.exe を続行するために、新しい再頒布可能場所に移動します。  Windows のベータ版の 3.1 バージョンの nuget.exe をダウンロードできます。 [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Dist.nuget.org ホストでこのテンプレートを次のフォルダー構造を持つ、新しい配布可能な場所に存在します。

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>新機能

* nuget.exe を復元し、使用するプロジェクトにパッケージをインストール、`project.json`ファイル。
* nuget.exe に接続しで NuGet v3 プロトコルを使用できます。 [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>既知の問題 ##

1.    に対してパックを実行することはできません、`project.json`ファイル - [928](https://github.com/NuGet/Home/issues/928)
2.    Mono のではサポートされていません[1059](https://github.com/NuGet/Home/issues/1059)
3.    ローカライズされていない - [1058](https://github.com/NuGet/Home/issues/1058)、 [1057](https://github.com/NuGet/Home/issues/1057)
4.    既存のと同じように、署名されていない http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)
