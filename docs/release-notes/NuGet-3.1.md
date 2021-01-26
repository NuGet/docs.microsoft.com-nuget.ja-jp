---
title: NuGet 3.1 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.1 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776540"
---
# <a name="nuget-31-release-notes"></a>NuGet 3.1 リリースノート

[NuGet 3.0 リリースノート](../release-notes/nuget-3.0.0.md)  | [NuGet 3.1.1 リリースノート](../release-notes/nuget-3.1.1.md)

NuGet 3.1 は、ユニバーサル Windows プラットフォーム SDK for Visual Studio 2015 のバンドル拡張として2015年7月27日にリリースされました。 Windows 開発者が以前に開始された NuGet クロスプラットフォームの作業を利用できるように、Windows プラットフォーム SDK を使用してこのリリースを提供しています。 この NuGet 拡張機能のバージョンは、Visual Studio 2015 でのみ使用できます。

Visual Studio ギャラリーへのアクセス権を持つ開発者は、常にバグ修正と新機能を使用して更新プログラムを公開するため、利用可能な最新バージョンに更新することをお勧めします。

## <a name="nuget-visual-studio-extension"></a>NuGet Visual Studio 拡張機能

このリリースの問題と機能については、GitHub で ["3.1 RTM UWP 推移サポート"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  というマイルストーンの合計について説明しています。3.1 リリースでは67の問題が解決されました。

### <a name="new-features"></a>新機能

* `project.json` Windows UWP および ASP.NET 5 サポートのサポート
* 推移的パッケージのインストール

これらの機能の説明と定義は、ドキュメント内の他の場所にあります。

### <a name="deprecated"></a>非推奨

Visual Studio 2015 では、次の機能は使用できなくなりました。

* ソリューションレベルのパッケージはインストールできなくなりました

次の機能は、Visual Studio 2015 および仕様を使用するプロジェクトでは使用できなくなりました。 `project.json`

* `install.ps1``uninstall.ps1`これらのスクリプトは、パッケージのインストール、復元、更新、およびアンインストール中は無視されます
* 構成の変換は無視されます
* コンテンツは実行されますが、プロジェクトにコピーされることはありません。
    * チームはこの機能の再実装に取り組んでおり、以下の説明と進行状況に従ってください。 [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>既知の問題

このリリースでは、いくつかの既知の問題が配信されました。

* Windows 10 SDK を使用して3.1 リリースをインストールすると、以前にインストールされたすべてのバージョンの NuGet 拡張機能がダウングレードされます

## <a name="nuget-command-line"></a>NuGet コマンドライン

NuGet コマンドラインの実行可能ファイルが更新され、新しい再配布可能な場所に移動されたため、nuget.exe の履歴バージョンを引き続き使用できます。  Windows 用 nuget.exe の3.1 ベータ版は、次の場所からダウンロードできます。 [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

新しい再配布可能な場所は dist.nuget.org ホスト上にあり、このテンプレートの後にフォルダー構造があります。

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a>新機能

* nuget.exe では、ファイルを使用するプロジェクトにパッケージを復元してインストールでき `project.json` ます。
* nuget.exe は、次の場所で NuGet v3 プロトコルに接続して使用できます。 [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>既知の問題 ##

1.    ファイルに対してパックを実行できません `project.json` - [928](https://github.com/NuGet/Home/issues/928)
2.    Mono- [1059](https://github.com/NuGet/Home/issues/1059)ではサポートされていません
3.    ローカライズされていない- [1058](https://github.com/NuGet/Home/issues/1058)、   [1057](https://github.com/NuGet/Home/issues/1057)
4.    既存の1073と同じように、署名されていません http://nuget.org/nuget.exe  -  [](https://github.com/NuGet/Home/issues/1073)
