---
title: "NuGet パッケージをインストールする方法 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "ディスクおよび適用可能なプロジェクト ファイルで何が発生するかなど、NuGet パッケージをプロジェクトにインストールするプロセスを説明します。"
keywords: "NuGet をインストールする、NuGet パッケージの使用、NuGet パッケージをインストールする、NuGet パッケージ参照"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3bae03e148a366388c10d08e83c89dac6ff56d06
ms.sourcegitcommit: 33436d122873249dbb20616556cd8c6783f38909
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>NuGet パッケージをインストールするためのさまざまな方法

NuGet パッケージをダウンロードしてインストールするには、次のいずれかのメソッドを使用します (これらのメソッドをまだインストールしていない場合は、「[Install NuGet client tools](../install-nuget-client-tools.md)」(NuGet クライアント ツールのインストール) を参照してください)。

| メソッド | 説明 |
| --- | --- |
| dotnet.exe CLI<br/>`dotnet install <package_name>` | (すべてのプラットフォーム) \<package_name\> によって指定されたパッケージをダウンロードして、その内容を現在のディレクトリのフォルダーに展開し、参照をプロジェクト ファイルに追加します。 さらに、依存関係もダウンロードしてインストールします。<ul><li>[パッケージをインストールして使用する (dotnet CLI)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[dotnet コマンド](../tools/dotnet-commands.md)</li></ul> |
| パッケージ マネージャー UI (Visual Studio) | (Windows および Mac) パッケージとその依存関係を参照して選択し、プロジェクトにインストールできる UI を提供します。 インストールされたプロジェクトへの参照をプロジェクト ファイルに追加します。<ul><li>[パッケージをインストールして使用する (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[パッケージ マネージャー UI のリファレンス (Windows)](../tools/package-manager-ui.md)</li><li>[プロジェクトに NuGet パッケージを含める (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| パッケージ マネージャー コンソール (Visual Studio)<br/>`Install-Package <package_name>` | (Windows のみ) \<package_name\> によって指定されたパッケージをダウンロードして、ソリューションで指定されたプロジェクトにインストールし、参照をプロジェクト ファイルに追加します。 さらに、依存関係もダウンロードしてインストールします。<ul><li>[パッケージをインストールして使用する (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[パッケージ マネージャー コンソールのガイド](../tools/package-manager-console.md)</li></ul> |
| nuget.exe CLI<br/>`nuget install <package_name>` | (すべてのプラットフォーム) \<package_name\> によって指定されたパッケージをダウンロードして、その内容を現在のディレクトリのフォルダーに展開します。また、`packages.config`ファイルの一覧にあるすべてのパッケージもダウンロードできます。 依存関係をダウンロードしてインストールしますが、プロジェクト ファイルは変更しません。<ul><li>[install コマンド](../tools/cli-ref-install.md)</li></ul> |

## <a name="general-install-process"></a>一般的なインストール プロセス

通常、NuGet は次のことを実行した後、パッケージのインストールを要求します。

1. パッケージを取得します。
    - 要求されたパッケージが既にキャッシュ内にあるかどうかを確認します (「[NuGet のキャッシュを管理する](managing-the-nuget-cache.md)」を参照してください)。
    - パッケージがキャッシュ内にない場合、[構成ファイル](Configuring-NuGet-Behavior.md)の一覧にあるソースからパッケージのダウンロードを試みます。
      - `packages.config` 参照形式を使用したプロジェクトについて、NuGet は、構成内のソースの順序を使用します。
      - PackageReference 形式を使用しているプロジェクトについて、NuGet は、最初に、ローカル フォルダーにあるソースを確認し、次にネットワーク共有上のソースを確認し、HTTP (インターネット) ソースを確認します。
      - 一般的に、特定の識別子およびバージョン番号を持つ任意のパッケージは、パッケージが見つかったソースにかかわらずまったく同じであるため、NuGet がソースを確認する順序に特定の意味はありません。
    - パッケージがいずれかのソースから正常に取得されたら、NuGet により、キャッシュに追加されます。 それ以外の場合、インストールは失敗します。

1. パッケージをプロジェクトに展開します。
    - 展開するということは、パッケージの内容を適切なサブフォルダーに解凍することを意味します。 `.nupkg`自体のコピーもそのサブフォルダーに格納されます。
    - パッケージを Visual Studio プロジェクトまたは .NET Core プロジェクトにインストールする場合は、そのプロジェクトのターゲット フレームワークに関連するファイルのみが展開されます。 nuget.exe コマンド ラインを使用してインストールする場合は、すべてのアセンブリが展開されます。

1. パッケージを Visual Studio または dotnet CLI 内でインストールする場合、参照は適切なプロジェクト ファイル (または、Visual Studio 内の一部のプロジェクトの種類については、`packages.config`) に追加されます。

## <a name="related-topics"></a>関連トピック

- [パッケージ使用の概要とワークフロー](../consume-packages/overview-and-workflow.md)
- [パッケージの検索と選択](../consume-packages/finding-and-choosing-packages.md)
- [NuGet の動作を構成する](../consume-packages/configuring-nuget-behavior.md)
- [NuGet のキャッシュを管理する](managing-the-nuget-cache.md)
