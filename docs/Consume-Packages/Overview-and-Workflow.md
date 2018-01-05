---
title: "NuGet パッケージの使用の概要とワークフロー | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3c60f920-457d-4f43-9efe-210c514e5242
description: "プロジェクトで NuGet パッケージを利用する場合のプロセスの概要と、プロセスの他の特定の部分へのリンク。"
keywords: "NuGet パッケージの利用, NuGet 利用の概要, NuGet 利用のワークフロー, パッケージ利用のワークフロー, パッケージ利用の概要"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c48351cb6fed0ac94bd437d9443811f46c032bd0
ms.sourcegitcommit: 122bf7ce308365ea45da018b0768f0536de76a1f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="package-consumption-workflow"></a>パッケージ利用のワークフロー

nuget.org と組織が確立する可能性のあるプライベート パッケージ ギャラリーの間で、アプリとサービスで使用する数万の非常に有用なパッケージを見つけることができます。 ただし、ソースに関係なく、パッケージを利用する場合は以下と同じ一般的なワークフローに従います。 詳細については、「[パッケージの検索と選択](../consume-packages/finding-and-choosing-packages.md)」と[パッケージの使用に関するクイック スタート](../quickstart/use-a-package.md)を参照してください。

![パッケージ ソースへの移動、パッケージの検索、プロジェクトへのインストール、パッケージ API への using ステートメントと呼び出しの追加を示すフロー](media/Overview-01-GeneralFlow.png)

\* _コマンドラインから `nuget install` を使用する場合を除く。使用する場合は、構成ファイルを手動で編集する必要があります。[install コマンド リファレンス](../tools/cli-ref-install.md)に関するページを参照してください。_

NuGet はインストールされているパッケージごとに ID とバージョン番号を記憶します。その場合、プロジェクトの種類と使用している NuGet のバージョンに応じて、`packages.config`、プロジェクト ファイル、`project.json` ファイルのいずれかに記録します。 NuGet 4.0+ では、既定で[プロジェクト ファイルに依存関係が格納](../consume-packages/package-references-in-project-files.md)されます (Windows 10 RS1 をターゲットとする UWP プロジェクトの場合を除く)。 いずれの場合も、適切なファイルでいつでもプロジェクトの依存関係の完全なリストを確認することができます。

> [!Tip]
> ソフトウェアで使用する予定の各パッケージのライセンスを常に確認することをお勧めます。 nuget.org には、各パッケージの説明ページの右側に **[ライセンス情報]** リンクがあります。 パッケージでライセンス条項が指定されていない場合は、パッケージ ページの **[Contact owners]\(所有者に問い合わせる\)** リンクを使用して、パッケージ所有者に直接問い合わせてください。 Microsoft はサードパーティのパッケージ プロバイダーを通じてユーザーに知的財産ライセンスを付与することはありません。また、サードパーティによって提供される情報について責任を負いません。

パッケージのインストール時に、NuGet は通常、パッケージがそのキャッシュから既に使用可能であるかどうかを確認します。 「[NuGet のキャッシュを管理する](../consume-packages/managing-the-nuget-cache.md)」で説明されているように、コマンド ラインからこのキャッシュを手動でクリアすることができます。

また、NuGet は、パッケージでサポートされるターゲット フレームワークがプロジェクトと互換性があることを確認します。 パッケージに互換性のあるアセンブリが含まれていない場合、NuGet はエラー メッセージを示します。 「[互換性のないパッケージのエラーの解決](dependency-resolution.md#resolving-incompatible-package-errors)」を参照してください。

プロジェクト コードをソース リポジトリを追加する場合、通常は NuGet パッケージを含めません。 Visual Studio Team Services などのシステムのビルド エージェントを含む、リポジトリを後で複製するユーザーは、ビルドを実行する前に必要なパッケージを復元する必要があります。

![リポジトリの複製およびいずれかの復元コマンドの使用による NuGet パッケージの復元フロー](media/Overview-02-RestoreFlow.png)

「[Package Restore](../consume-packages/package-restore.md)」 (パッケージの復元) では、プロジェクト ファイル、`packages.config`、`project.json` の情報を使用して、依存関係をすべて再インストールします。 「[Dependency Resolution](../consume-packages/dependency-resolution.md)」 (依存関係の解決) で説明されているように、関係するプロセスには違いがあることに注意してください。

場合によっては、プロジェクトに既に含まれているパッケージの再インストールが必要になります。その場合、依存関係も再インストールされる可能性があります。 これは、NuGet コマンド ラインで `reinstall` コマンドを使用するか、NuGet パッケージ マネージャー コンソールを使用して簡単に行うことができます。 詳細については、「[Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md)」 (パッケージの再インストールと更新) を参照してください。

最後に、NuGet の動作は `Nuget.Config` 構成ファイルによって駆動されます。 「[Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md)」 (NuGet の動作の構成) で説明されているように、複数のファイルを使用して、さまざまなレベルの特定の設定を一元化することができます。

それでは NuGet パッケージでの生産性の高いコーディングをお楽しみください。
