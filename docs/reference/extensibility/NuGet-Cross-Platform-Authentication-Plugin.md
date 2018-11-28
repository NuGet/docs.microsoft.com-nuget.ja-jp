---
title: NuGet のクロス プラットフォーム認証プラグイン
description: NuGet.exe、dotnet.exe、msbuild.exe および Visual Studio の NuGet がプラットフォームの認証プラグインをクロスします。
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: b76fab1028ec9a4172d2390083fbf9adb4290a6c
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453508"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>NuGet のクロス プラットフォーム認証プラグイン

バージョン 4.8 以降、クライアント (NuGet.exe を Visual Studio、dotnet.exe、MSBuild.exe) は、上に構築された認証プラグインを使用できるすべての NuGet で、[クロス プラットフォーム プラグイン NuGet](NuGet-Cross-Platform-Plugins.md)モデル。

## <a name="authentication-in-dotnetexe"></a>Dotnet.exe の認証

Visual Studio と NuGet.exe は、対話型の既定では。 NuGet.exe にはようにするためのスイッチが含まれています[非対話型](../../tools/nuget-exe-CLI-Reference.md)します。
さらに、NuGet.exe および Visual Studio のプラグインは、ユーザーに入力を求めます。
Dotnet.exe のない入力を求めると、既定値は非対話型です。

Dotnet.exe での認証メカニズムでは、デバイスのフローです。 ときに、復元またはパッケージの操作は、操作がブロックと指示する方法を完全な認証ことが、コマンドラインでユーザーに対話的に実行を追加します。
ユーザーが認証を完了すると、操作を続行します。

操作を対話型にするために、1 つ渡す必要があります`--interactive`します。
現在のみ明示的な`dotnet restore`と`dotnet add package`コマンドは、対話型のスイッチをサポートします。
対話型のスイッチがない`dotnet build`と`dotnet publish`します。

## <a name="authentication-in-msbuild"></a>MSBuild での認証

Dotnet.exe と同様に、MSBuild.exe が既定で非対話型 MSBuild.exe の認証メカニズムはデバイスのフローです。
一時停止し、認証を待つ復元できるように、復元を呼び出す`msbuild -t:restore -p:NuGetInteractive="true"`します。

## <a name="creating-a-cross-platform-authentication-plugin"></a>クロス プラットフォーム認証プラグインを作成します。

実装のサンプルが記載[Microsoft 資格情報プロバイダー プラグイン](https://github.com/Microsoft/artifacts-credprovider)します。

プラグインは、NuGet クライアント ツールによって設定されたセキュリティ要件に準拠していることが非常に重要です。
最低限必要な認証プラグインを使用するプラグイン バージョンは*2.0.0*します。
NuGet はサポートされている操作の信頼性情報と、プラグインとクエリのハンドシェイクを実行します。
クロス プラットフォームのプラグインの NuGet を参照してください[プロトコル メッセージ](NuGet-Cross-Platform-Plugins.md#protocol-messages-index)特定のメッセージの詳細についてはします。

NuGet はログ レベルを設定し、該当する場合、プラグインにプロキシ情報を提供します。
NuGet へのログ記録コンソールはのみ許容可能な NuGet がプラグインにログ レベルを設定後します。

- .NET framework プラグインの認証の動作

.NET framework、プラグインは、ダイアログ ボックスの形式での入力をユーザーに求めるが許可されます。

- .NET core プラグインの認証の動作

.NET Core では、ダイアログを表示することはできません。 プラグインは、認証にデバイスのフローを使用する必要があります。
プラグインは、ユーザーに指示を NuGet にログ メッセージを送信できます。
ログ レベルが、プラグインを設定した後のログ記録が使用できることに注意してください。
NuGet では、コマンドラインから対話型の入力は実行されません。

クライアントが取得の認証資格情報を使ってプラグインを呼び出すと、プラグインは対話機能のスイッチに準拠しているし、ダイアログのスイッチを尊重する必要があります。 

次の表では、すべての組み合わせに対して、プラグインの動作方法を示します。

| IsNonInteractive | CanShowDialog | プラグインの動作 |
| ---------------- | ------------- | --------------- |
| true | true | IsNonInteractive スイッチは、ダイアログのスイッチよりも優先されます。 ダイアログ ボックスをポップアップ表示には、プラグインすることはできません。 この組み合わせは .NET Framework のプラグインの有効なのみ |
| true | False | IsNonInteractive スイッチは、ダイアログのスイッチよりも優先されます。 ブロックには、プラグインすることはできません。 この組み合わせは、.NET コア プラグインの有効なのみ |
| False | true | プラグインは、ダイアログ ボックスを表示する必要があります。 この組み合わせは .NET Framework のプラグインの有効なのみ |
| False | False | プラグインする必要があります/ことに、ダイアログを表示されません。 プラグインは、命令メッセージ ロガーを使用してログに記録して認証するデバイスのフローを使用してください。 この組み合わせは、.NET コア プラグインの有効なのみ |

プラグインを記述する前に、次の仕様を参照してください。

- [NuGet パッケージのダウンロードのプラグイン](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [フォーム認証のプラグイン相互の NuGet](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
