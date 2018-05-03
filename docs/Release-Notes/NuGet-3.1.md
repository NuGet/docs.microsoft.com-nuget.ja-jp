---
title: NuGet 3.1 リリース ノート
description: 既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 3.1 リリース ノートです。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d14455da6f8af4db92f7105ea1b0e88eb9e71600
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-31-release-notes"></a>NuGet 3.1 リリース ノート

[NuGet 3.0 リリース ノート](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 リリース ノート](../release-notes/nuget-3.1.1.md)

NuGet 3.1 は、Visual Studio 2015 用、2015 年 7 月 27 日に、ユニバーサル Windows プラットフォーム SDK にバンドルされている拡張機能としてリリースされました。 このリリースには、Windows プラットフォーム SDK を配信される、以前に起動されている NuGet クロスプラット フォームの作業の Windows 開発エクスペリエンスを利用できるようにします。 この NuGet 拡張機能のバージョンは Visual Studio 2015 のできるだけです。

開発者はバグ修正と新機能と更新プログラムを常に公開として使用すると、最新のバージョンの Visual Studio ギャラリーの更新にアクセスできることをお勧めします。

## <a name="nuget-visual-studio-extension"></a>NuGet の Visual Studio 拡張機能

問題およびこのリリースの機能が github でタグ付け、 [「3.1 の RTM UWP 推移的なサポート」マイルス トーン](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)おの合計、閉じられた 3.1 リリースで 67 の問題です。

### <a name="new-features"></a>新機能

* `project.json` Windows UWP と ASP.NET 5 のサポートのサポート
* 推移的なパッケージのインストール

これらの機能の説明と定義は、ドキュメントの他の場所で確認できます。

### <a name="deprecated"></a>非推奨

Visual Studio 2015 の次の機能を利用できなく。

* レベルのソリューション パッケージはインストールできません。

次の機能が Visual Studio 2015 とを使用するプロジェクトで使用可能では不要になった、`project.json`仕様

* `install.ps1` `uninstall.ps1` -これらのスクリプトは、パッケージのインストール時に無視する、復元、更新、およびアンインストール
* 構成の変換は無視されます。
* コンテンツは、実行しますが、プロジェクトにコピーされません。
    * この機能を再実装、説明に従って、およびで進行状況をチームが動作します。 [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>既知の問題

このリリースで提供される既知の問題の数が発生しました。

* Windows 10 SDK に 3.1 リリースのインストールが以前にインストールされた NuGet 拡張機能の任意のバージョンをダウン グレードします。

## <a name="nuget-command-line"></a>コマンド ライン NuGet

NuGet コマンドライン実行可能ファイルが更新され、利用可能になる nuget.exe の過去のバージョンを継続できるように、新しい配布可能な場所に移動します。  Windows での nuget.exe の 3.1 ベータ版をダウンロードできます。 [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Dist.nuget.org ホストで、このテンプレートに依存しているフォルダー構造を新しい配布可能な場所に存在します。

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>新機能

* nuget.exe を復元しを使用するプロジェクトにパッケージをインストール、`project.json`ファイル。
* nuget.exe がへの接続およびで NuGet v3 プロトコルを使用できます。 [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>既知の問題 ##

1.    に対してパックを実行することはできません、`project.json`ファイル - [928](https://github.com/NuGet/Home/issues/928)
2.    モノラル - でサポートされていない[1059](https://github.com/NuGet/Home/issues/1059)
3.    ローカライズされません - [1058](https://github.com/NuGet/Home/issues/1058)、 [1057](https://github.com/NuGet/Home/issues/1057)
4.    既存のと同じように、署名されていないhttp://nuget.org/nuget.exe- [1073](https://github.com/NuGet/Home/issues/1073)
