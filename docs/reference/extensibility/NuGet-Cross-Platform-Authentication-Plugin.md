---
title: NuGet のクロス プラットフォーム認証プラグイン
description: Nuget.exe、dotnet、msbuild.exe、および Visual Studio 用の NuGet クロスプラットフォーム認証プラグイン
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: a716737343ea826d28da6de46c32ca73aef590bd
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317278"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>NuGet のクロス プラットフォーム認証プラグイン

バージョン4.8 以降では、すべての NuGet クライアント (Nuget.exe、Visual Studio、dotnet、および Msbuild.exe) は、 [nuget クロスプラットフォームプラグイン](NuGet-Cross-Platform-Plugins.md)モデル上に構築された認証プラグインを使用できます。

## <a name="authentication-in-dotnetexe"></a>Dotnet での認証

既定では、Visual Studio と Nuget.exe は対話型です。 Nuget.exe には、対話型になら[ない](../nuget-exe-CLI-Reference.md)ようにするスイッチが含まれています。
さらに、Nuget.exe および Visual Studio プラグインによって、ユーザーに入力を求めるプロンプトが表示されます。
Dotnet では、プロンプトは表示されず、既定値は非対話型です。

Dotnet の認証メカニズムはデバイスフローです。 復元またはパッケージの追加操作を対話的に実行すると、認証を完了するための操作ブロックとユーザーへの指示がコマンドラインに表示されます。
ユーザーが認証を完了すると、操作は続行されます。

操作を対話形式にするには、 `--interactive`1 つを渡す必要があります。
現時点では、 `dotnet restore`明示`dotnet add package`的なコマンドとコマンドのみが対話型スイッチをサポートしています。
`dotnet build` と`dotnet publish`には対話型スイッチがありません。

## <a name="authentication-in-msbuild"></a>MSBuild での認証

Dotnet と同様に、Msbuild.exe は既定で非対話型になります。 Msbuild.exe の認証メカニズムはデバイスフローです。
復元を一時停止して認証を待機させるには、 `msbuild -t:restore -p:NuGetInteractive="true"`を使用して restore を呼び出します。

## <a name="creating-a-cross-platform-authentication-plugin"></a>クロスプラットフォーム認証プラグインを作成する

サンプルの実装については、「 [Microsoft Credential Provider plugin](https://github.com/Microsoft/artifacts-credprovider)」を参照してください。

プラグインは、NuGet クライアントツールによって設定されたセキュリティ要件に準拠していることが非常に重要です。
プラグインを認証プラグインとして使用するために必要な最小バージョンは*2.0.0*です。
NuGet は、サポートされている操作要求に対して、プラグインとクエリを使用してハンドシェイクを実行します。
特定のメッセージの詳細については、NuGet クロスプラットフォームプラグイン[プロトコルメッセージ](NuGet-Cross-Platform-Plugins.md#protocol-messages-index)を参照してください。

NuGet はログレベルを設定し、必要に応じてプロキシ情報をプラグインに提供します。
Nuget コンソールへのログ記録は、NuGet がログレベルをプラグインに設定した後でのみ許容されます。

- .NET Framework プラグインの認証動作

.NET Framework では、プラグインは、ダイアログの形式でユーザーに入力を求めることができます。

- .NET Core プラグインの認証動作

.NET Core では、ダイアログを表示できません。 プラグインは、デバイスフローを使用して認証する必要があります。
プラグインは、ユーザーへの指示と共にログメッセージを NuGet に送信できます。
ログレベルがプラグインに設定されている場合は、ログ記録が使用可能であることに注意してください。
NuGet は、コマンドラインから対話型の入力を受け取りません。

クライアントが Get 認証資格情報を使用してプラグインを呼び出す場合、プラグインは対話スイッチに準拠し、ダイアログスイッチを尊重する必要があります。 

次の表は、すべての組み合わせに対してプラグインがどのように動作するかをまとめたものです。

| IsNonInteractive 型 | CanShowDialog | プラグインの動作 |
| ---------------- | ------------- | --------------- |
| true | true | IsNonInteractive スイッチは、ダイアログスイッチよりも優先されます。 プラグインは、ダイアログをポップすることが許可されていません。 この組み合わせは .NET Framework プラグインに対してのみ有効です。 |
| true | False | IsNonInteractive スイッチは、ダイアログスイッチよりも優先されます。 プラグインをブロックすることはできません。 この組み合わせは、.NET Core プラグインに対してのみ有効です。 |
| False | true | プラグインにダイアログが表示されます。 この組み合わせは .NET Framework プラグインに対してのみ有効です。 |
| False | False | プラグインは、ダイアログを表示しないようにする必要があります。 プラグインは、logger 経由で命令メッセージをログに記録することによって、デバイスフローを使用して認証する必要があります。 この組み合わせは、.NET Core プラグインに対してのみ有効です。 |

プラグインを作成する前に、次の仕様を参照してください。

- [NuGet パッケージのダウンロードプラグイン](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet のクロスプラットフォーム認証プラグイン](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
