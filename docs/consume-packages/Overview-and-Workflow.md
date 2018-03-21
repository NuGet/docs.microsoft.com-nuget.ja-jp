---
title: "NuGet パッケージの使用の概要とワークフロー | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "プロジェクトで NuGet パッケージを利用する場合のプロセスの概要と、プロセスの他の特定の部分へのリンク。"
keywords: "NuGet パッケージの利用, NuGet 利用の概要, NuGet 利用のワークフロー, パッケージ利用のワークフロー, パッケージ利用の概要"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 731e0d3eb4ccb887624e4e46a18b4cc77857a784
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2018
---
# <a name="package-consumption-workflow"></a>パッケージ利用のワークフロー

nuget.org と組織が確立する可能性のあるプライベート パッケージ ギャラリーの間で、アプリとサービスで使用する数万の非常に有用なパッケージを見つけることができます。 ただし、ソースに関係なく、パッケージを利用する場合は以下と同じ一般的なワークフローに従います。 詳細については、「[プロジェクトの NuGet パッケージの検索と評価](../consume-packages/finding-and-choosing-packages.md)」および「[Different ways to install a NuGet package](ways-to-install-a-package.md)」(NuGet パッケージをインストールするためのさまざまな方法) を参照してください。

![パッケージ ソースへの移動、パッケージの検索、プロジェクトへのインストール、パッケージ API への using ステートメントと呼び出しの追加を示すフロー](media/Overview-01-GeneralFlow.png)

\* _コマンドラインから `nuget install` を使用する場合を除く。使用する場合は、構成ファイルを手動で編集する必要があります。[install コマンド リファレンス](../tools/cli-ref-install.md)に関するページを参照してください。_

NuGet は、インストールされている各パッケージの ID とバージョン番号を記憶し、プロジェクトの種類と使用している NuGet のバージョンに応じて、[`packages.config`](../reference/packages-config.md) またはプロジェクト ファイルのいずれかに記録します。 NuGet 4.0+ では、通常、既定により、[プロジェクト ファイルまたは PackageReference に依存関係が格納](../consume-packages/package-references-in-project-files.md)されます。ただし、Visual Studio で [パッケージ マネージャー UI のオプション](../tools/package-manager-ui.md)を使用して、これを構成することができます。 いずれの場合も、適切なファイルでいつでもプロジェクトの依存関係の完全なリストを確認することができます。

> [!Tip]
> ソフトウェアで使用する予定の各パッケージのライセンスを常に確認することをお勧めます。 nuget.org には、各パッケージの説明ページの右側に **[ライセンス情報]** リンクが表示されます。 パッケージでライセンス条項が指定されていない場合は、パッケージ ページの **[Contact owners]\(所有者に問い合わせる\)** リンクを使用して、パッケージ所有者に直接問い合わせてください。 Microsoft はサードパーティのパッケージ プロバイダーを通じてユーザーに知的財産ライセンスを付与することはありません。また、サードパーティによって提供される情報について責任を負いません。

パッケージのインストール時に、NuGet は通常、パッケージがそのキャッシュから既に使用可能であるかどうかを確認します。 「[NuGet のキャッシュを管理する](../consume-packages/managing-the-nuget-cache.md)」で説明されているように、コマンド ラインからこのキャッシュを手動でクリアすることができます。

また、NuGet は、パッケージでサポートされるターゲット フレームワークがプロジェクトと互換性があることを確認します。 パッケージに互換性のあるアセンブリが含まれていない場合、NuGet はエラー メッセージを示します。 「[互換性のないパッケージのエラーの解決](dependency-resolution.md#resolving-incompatible-package-errors)」を参照してください。

プロジェクト コードをソース リポジトリを追加する場合、通常は NuGet パッケージを含めません。 Visual Studio Team Services などのシステムのビルド エージェントを含む、リポジトリを後で複製するユーザーは、ビルドを実行する前に必要なパッケージを復元する必要があります。

![リポジトリの複製およびいずれかの復元コマンドの使用による NuGet パッケージの復元フロー](media/Overview-02-RestoreFlow.png)

「[パッケージの復元](../consume-packages/package-restore.md)」では、プロジェクト ファイルまたは `packages.config` の情報を使用して、すべての依存関係を再インストールします。 「[Dependency Resolution](../consume-packages/dependency-resolution.md)」 (依存関係の解決) で説明されているように、関係するプロセスには違いがあることに注意してください。

場合によっては、プロジェクトに既に含まれているパッケージの再インストールが必要になります。その場合、依存関係も再インストールされる可能性があります。 これは、NuGet コマンド ラインで `reinstall` コマンドを使用するか、NuGet パッケージ マネージャー コンソールを使用して簡単に行うことができます。 詳細については、「[Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md)」 (パッケージの再インストールと更新) を参照してください。

最後に、NuGet の動作は `Nuget.Config` 構成ファイルによって駆動されます。 「[Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md)」 (NuGet の動作の構成) で説明されているように、複数のファイルを使用して、さまざまなレベルの特定の設定を一元化することができます。

それでは NuGet パッケージでの生産性の高いコーディングをお楽しみください。
