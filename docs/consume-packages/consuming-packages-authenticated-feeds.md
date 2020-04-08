---
title: 認証済みフィードからのパッケージの使用
description: すべての NuGet クライアント シナリオでの認証済みフィードからのパッケージの使用
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231741"
---
# <a name="consuming-packages-from-authenticated-feeds"></a>認証済みフィードからのパッケージの使用

nuget.org [パブリック フィード](https://api.nuget.org/v3/index.json)に加えて、NuGet クライアントでは、ファイル フィードとプライベート http フィードを操作することができます。


プライベート http フィードで認証するには、次の 2 つの方法があります。

* [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials) で資格情報を追加する
* 使用するクライアントに応じて、多くの拡張モデルのいずれかを使用して認証する

## <a name="nuget-clients-authentication-extensibility"></a>NuGet クライアントの認証の拡張性

さまざまな NuGet クライアントでは、プライベート フィード プロバイダーそのものが認証を担当します。
すべての NuGet クライアントには、これをサポートするための拡張メソッドがあります。 これらは、Visual Studio の拡張機能、または NuGet と通信して資格情報を取得できるプラグインのいずれかです。

### <a name="visual-studio"></a>Visual Studio

Visual Studio では、フィード プロバイダーが実装して顧客に提供できるインターフェイスが NuGet によって公開されます。 詳細については、[Visual Studio 資格情報プロバイダーの作成方法](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)に関するドキュメントを参照してください。

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>Visual Studio 向けの使用可能な NuGet 資格情報プロバイダー

Azure DevOps をサポートするために、Visual Studio に組み込まれている資格情報プロバイダーがあります。


利用可能なプラグイン資格情報プロバイダーは次のとおりです。

* [Visual Studio 向け MyGet 資格情報プロバイダー](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

`nuget.exe` では、フィードによる認証のために資格情報が必要な場合に、次の方法でそれらが検索されます。

1. `NuGet.config` ファイル内で資格情報を検索します。
1. V2 プラグイン資格情報プロバイダーを使用します。
1. V1 プラグイン資格情報プロバイダーを使用します。
1. その後、NuGet がコマンド ラインでユーザーに資格情報の入力を求めます。

#### <a name="nugetexe-and-v2-credential-providers"></a>nuget.exe と V2 の資格情報プロバイダー

バージョン `4.8` では、NuGet によって新しい認証プラグイン メカニズムが定義され、これ以降、V2 資格情報プロバイダーと呼ばれています。
これらのプロバイダーのインストールと検出については、「[NuGet のクロス プラットフォーム プラグイン](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)」を参照してください。

#### <a name="nugetexe-and-v1-credential-providers"></a>nuget.exe と V1 の資格情報プロバイダー

バージョン `3.3` では、NuGet で認証プラグインの最初のバージョンが導入されました。
これらのプロバイダーのインストールと検出については、[nuget.exe 資格情報プロバイダー](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)に関するセクションを参照してください。

#### <a name="available-credential-providers-for-nugetexe"></a>nuget.exe の利用可能な資格情報プロバイダー

* [Azure DevOps V2 資格情報プロバイダー](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) または [Azure Artifacts 資格情報プロバイダー](https://github.com/microsoft/artifacts-credprovider)

Visual Studio 2017 バージョン 15.9 以降では、Azure DevOps 資格情報プロバイダーが Visual Studio にバンドルされています。
`nuget.exe` がその特定の Visual Studio ツールセットから MSBuild を使用している場合、プラグインは自動的に検出されます。

### <a name="dotnetexe"></a>dotnet.exe

`dotnet.exe` では、フィードによる認証のために資格情報が必要な場合に、次の方法でそれらが検索されます。

1. `NuGet.config` ファイル内で資格情報を検索します。
1. V2 プラグイン資格情報プロバイダーを使用します。

既定では `dotnet.exe` は対話型ではないため、認証をブロックするツールを取得するには、`--interactive` フラグを渡す必要がある場合があります。

#### <a name="dotnetexe-and-v2-credential-providers"></a>dotnet.exe と V2 の資格情報プロバイダー

SDK のバージョン `2.2.100` で、すべてのクライアントで動作する認証プラグイン メカニズムが NuGet によって定義されました。
これらのプロバイダーのインストールと検出については、「[NuGet のクロス プラットフォーム プラグイン](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)」を参照してください。

#### <a name="available-credential-providers-for-dotnetexe"></a>dotnet.exe の利用可能な資格情報プロバイダー

* [Azure Artifacts 資格情報プロバイダー](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>MSBuild.exe

`MSBuild.exe` では、フィードによる認証のために資格情報が必要な場合に、次の方法でそれらが検索されます。

1. `NuGet.config` ファイル内で資格情報を検索します。
1. V2 プラグイン資格情報プロバイダーを使用します。

既定では `MSBuild.exe` は対話型ではないため、認証をブロックするツールを取得するには、`/p:NuGetInteractive=true` プロパティを設定する必要がある場合があります。

#### <a name="msbuildexe-and-v2-credential-providers"></a>MSBuild.exe と V2 の資格情報プロバイダー

Visual Studio 2019 Update 9 で、すべてのクライアントで動作する認証プラグイン メカニズムが NuGet によって定義されました。
これらのプロバイダーのインストールと検出については、「[NuGet のクロス プラットフォーム プラグイン](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)」を参照してください。

#### <a name="available-credential-providers-for-msbuildexe"></a>MSBuild.exe の利用可能な資格情報プロバイダー

* [Azure Artifacts 資格情報プロバイダー](https://github.com/microsoft/artifacts-credprovider)

Visual Studio 2017 Update 9 以降では、Azure DevOps 資格情報プロバイダーが Visual Studio にバンドルされています。 追加の手順は必要ありません。
