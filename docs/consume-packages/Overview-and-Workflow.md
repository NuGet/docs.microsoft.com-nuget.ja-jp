---
title: NuGet パッケージの使用の概要とワークフロー
description: プロジェクトで NuGet パッケージを利用する場合のプロセスの概要と、プロセスの他の特定の部分へのリンク。
author: karann-msft
ms.author: karann
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: ddd1d163e18ed4ce1e7cbf41ed152acc40c1c423
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428517"
---
# <a name="package-consumption-workflow"></a>パッケージ利用のワークフロー

nuget.org と組織が確立する可能性のあるプライベート パッケージ ギャラリーの間で、アプリとサービスで使用する数万の非常に有用なパッケージを見つけることができます。 ただし、ソースに関係なく、パッケージを利用する場合は一般的なワークフローに従います。

![パッケージ ソースへの移動、パッケージの検索、プロジェクトへのインストール、パッケージ API への using ステートメントと呼び出しの追加を示すフロー](media/Overview-01-GeneralFlow.png)

\* _Visual Studio および `dotnet.exe` のみ。`nuget install` コマンドは、プロジェクト ファイルまたは `packages.config` ファイルを変更しません。エントリは、手動で管理する必要があります。_

詳細については、「[プロジェクトの NuGet パッケージの検索と評価](../consume-packages/finding-and-choosing-packages.md)」および「[パッケージ インストールのしくみ](../concepts/package-installation-process.md)」を参照してください。

NuGet では、インストールされている各パッケージの ID とバージョン番号が記憶されます。これは、プロジェクトの種類と使用している NuGet のバージョンに応じて、プロジェクト ファイル ([PackageReference](../consume-packages/package-references-in-project-files.md) を使用) または [`packages.config`](../reference/packages-config.md) のいずれかに記録されます。 PackageReference は[パッケージ マネージャーの UI](install-use-packages-visual-studio.md) を利用して Visual Studio で構成できますが、NuGet 4.0 以降では、PackageReference をお勧めします。 いずれの場合も、適切なファイルでいつでもプロジェクトの依存関係の完全なリストを確認することができます。

> [!Tip]
> ソフトウェアで使用する予定の各パッケージのライセンスを常に確認することをお勧めます。 nuget.org には、各パッケージの説明ページの右側に **[ライセンス情報]** リンクが表示されます。 パッケージでライセンス条項が指定されていない場合は、パッケージ ページの **[Contact owners]\(所有者に問い合わせる\)** リンクを使用して、パッケージ所有者に直接問い合わせてください。 Microsoft はサードパーティのパッケージ プロバイダーを通じてユーザーに知的財産ライセンスを付与することはありません。また、サードパーティによって提供される情報について責任を負いません。

パッケージのインストール時に、NuGet は通常、パッケージがそのキャッシュから既に使用可能であるかどうかを確認します。 「[Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md)」 (グローバル パッケージおよびキャッシュ フォルダーを管理する) で説明されているように、コマンド ラインからこのキャッシュを手動でクリアすることができます。

また、NuGet は、パッケージでサポートされるターゲット フレームワークがプロジェクトと互換性があることを確認します。 パッケージに互換性のあるアセンブリが含まれていない場合、NuGet はエラーを示します。 「[互換性のないパッケージのエラーの解決](../concepts/dependency-resolution.md#resolving-incompatible-package-errors)」を参照してください。

プロジェクト コードをソース リポジトリを追加する場合、通常は NuGet パッケージを含めません。 Visual Studio Team Services などのシステムのビルド エージェントを含む、リポジトリを後で複製するか、そうでない場合はプロジェクトを取得するユーザーは、ビルドを実行する前に必要なパッケージを復元する必要があります。

![リポジトリの複製およびいずれかの復元コマンドの使用による NuGet パッケージの復元フロー](media/Overview-02-RestoreFlow.png)

「[パッケージの復元](../consume-packages/package-restore.md)」では、プロジェクト ファイルまたは `packages.config` の情報を使用して、すべての依存関係を再インストールします。 「[Dependency Resolution](../concepts/dependency-resolution.md)」 (依存関係の解決) で説明されているように、関係するプロセスには違いがあることに注意してください。 また、上図にはパッケージ マネージャー コンソールの復元コマンドは示されていませんが、これはコンソールで作業している場合、既に Visual Studio のコンテキスト内にいるからです。この場合は通常、パッケージは自動で復元され、図に示されているようにソリューション レベルのコマンドが提供されます。

場合によっては、プロジェクトに既に含まれているパッケージの再インストールが必要になります。その場合、依存関係も再インストールされる可能性があります。 これは、`nuget reinstall` コマンド使用するか、NuGet パッケージ マネージャー コンソールを使用して簡単に行うことができます。 詳細については、「[Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md)」 (パッケージの再インストールと更新) を参照してください。

最後に、NuGet の動作は `Nuget.Config` ファイルによって駆動されます。 「[Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md)」 (NuGet の動作の構成) で説明されているように、複数のファイルを使用して、さまざまなレベルの特定の設定を一元化することができます。

## <a name="ways-to-install-a-nuget-package"></a>NuGet パッケージのインストール方法

NuGet パッケージは、次の表にあるメソッドのいずれかを使用して、ダウンロードされ、インストールされます。

| ツール | 説明 |
| --- | --- |
| [dotnet.exe CLI](install-use-packages-dotnet-cli.md) | (すべてのプラットフォーム) .NET Core と .NET Standard ライブラリ、および .NET Framework を対象とする SDK スタイルのプロジェクト (「[SDK 属性](/dotnet/core/tools/csproj#additions)」を参照) のための CLI ツール。 \<package_name\> によって指定されたパッケージを取得し、参照をプロジェクト ファイルに追加します。 また、依存関係も取得してインストールします。 |
| Visual Studio | (Windows および Mac) 用意された UI を使用して、指定したパッケージ ソースからパッケージとその依存関係を参照して選択し、プロジェクトにインストールできます。 インストールされたプロジェクトへの参照をプロジェクト ファイルに追加します。<ul><li>[Visual Studio を使用してパッケージをインストールして管理する](install-use-packages-visual-studio.md)</li><li>[プロジェクトに NuGet パッケージを含める (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| [パッケージ マネージャー コンソール (Visual Studio)](install-use-packages-powershell.md) | (Windows のみ) 選択したソースから、\<package_name\> で指定したパッケージを取得して、ソリューションで指定されたプロジェクトにインストールし、参照をプロジェクト ファイルに追加します。 また、依存関係も取得してインストールします。 |
| [nuget.exe CLI](install-use-packages-nuget-cli.md) | (すべてのプラットフォーム) .NET Framework ライブラリと、.NET Standard ライブラリを対象とする非 SDK スタイルのプロジェクトのための CLI ツール。 \<package_name\> で指定したパッケージを取得して、その内容を現在のディレクトリのフォルダーに展開します。`packages.config` ファイルでリストされたすべてのパッケージを取得することもできます。 また、依存関係を取得してインストールしますが、プロジェクト ファイルまたは `packages.config` は変更されません。 |
