---
title: Visual Studio 向け NuGet 資格情報プロバイダー
description: NuGet 資格情報プロバイダーは、Visual Studio 拡張機能で IVsCredentialProvider インターフェイスを実装することによって、フィードで認証を行います。
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: ab3bde0d320375f854a8f0a98fb90acfecf54aa3
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859097"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>NuGet 資格情報プロバイダーを使用した Visual Studio でのフィードの認証

NuGet Visual Studio 拡張機能3.6 以降では、認証済みのフィードを NuGet で使用できるようにする資格情報プロバイダーがサポートされています。
Visual Studio の NuGet 資格情報プロバイダーをインストールすると、NuGet Visual Studio 拡張機能は、認証されたフィードの資格情報を必要に応じて自動的に取得して更新します。

サンプルの実装については [、VsCredentialProvider サンプル](https://github.com/NuGet/Samples/tree/main/VsCredentialProvider)を参照してください。

Visual Studio では、NuGet は内部 `VsCredentialProviderImporter` のを使用します。これはプラグイン資格情報プロバイダーもスキャンします。 これらのプラグイン資格情報プロバイダーは、型の MEF エクスポートとして検出可能である必要があり `IVsCredentialProvider` ます。

Visual Studio の 4.8 + NuGet 以降では、新しいクロスプラットフォーム認証プラグインもサポートされていますが、パフォーマンス上の理由から推奨される方法ではありません。

> [!Note]
> Visual Studio の NuGet 資格情報プロバイダーは、通常の Visual Studio 拡張機能としてインストールする必要があり、 [Visual studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) 以降が必要になります。
>
> Visual Studio の NuGet 資格情報プロバイダーは、Visual Studio でのみ動作します (dotnet restore または nuget.exe では使用できません)。 nuget.exe の資格情報プロバイダーについては、「 [nuget.exe 資格情報プロバイダー](nuget-exe-Credential-providers.md)」を参照してください。
> Dotnet と msbuild の資格情報プロバイダーについては、「 [NuGet クロスプラットフォームプラグイン](nuget-cross-platform-authentication-plugin.md)」を参照してください。

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Visual Studio の NuGet 資格情報プロバイダーを作成する

NuGet Visual Studio 拡張機能3.6 以降では、資格情報の取得に使用される内部 CredentialService が実装されています。 CredentialService には、組み込みおよびプラグインの資格情報プロバイダーの一覧があります。 各プロバイダーは、資格情報が取得されるまで順番に試行されます。

資格情報の取得中、資格情報サービスは次の順序で資格情報プロバイダーを試行し、資格情報が取得されるとすぐに停止します。

1. 資格情報は、(組み込みのを使用して) NuGet 構成ファイルからフェッチされ `SettingsCredentialProvider` ます。
1. パッケージソースが Visual Studio Team Services にある場合は、が `VisualStudioAccountProvider` 使用されます。
1. その他のすべてのプラグイン Visual Studio 資格情報プロバイダーは、順番に試行されます。
1. すべての NuGet クロスプラットフォーム資格情報プロバイダーを順番に使用してください。
1. 資格情報がまだ取得されていない場合、ユーザーは標準の基本認証ダイアログを使用して資格情報の入力を求められます。

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>IVsCredentialProvider を実装しています。 GetCredentialsAsync

Visual Studio の NuGet 資格情報プロバイダーを作成するには、型を実装するパブリック MEF エクスポートを公開する Visual Studio 拡張機能を作成 `IVsCredentialProvider` し、次に示す原則に従います。

```cs
public interface IVsCredentialProvider
{
    Task<ICredentials> GetCredentialsAsync(
        Uri uri,
        IWebProxy proxy,
        bool isProxyRequest,
        bool isRetry,
        bool nonInteractive,
        CancellationToken cancellationToken);
}
```

サンプルの実装については [、VsCredentialProvider サンプル](https://github.com/NuGet/Samples/tree/main/VsCredentialProvider)を参照してください。

Visual Studio の各 NuGet 資格情報プロバイダーは、次のことを行う必要があります。

1. 資格情報の取得を開始する前に、対象の URI の資格情報を提供できるかどうかを判断します。 プロバイダーが対象のソースの資格情報を提供できない場合は、を返し `null` ます。
1. プロバイダーが対象 URI の要求を処理するが、資格情報を提供できない場合は、例外をスローする必要があります。

Visual Studio のカスタム NuGet 資格情報プロバイダーは、 `IVsCredentialProvider` [VisualStudio パッケージ](https://www.nuget.org/packages/NuGet.VisualStudio/)で使用可能なインターフェイスを実装する必要があります。

#### <a name="getcredentialasync"></a>GetCredentialAsync

| 入力パラメーター |Description|
| ----------------|-----------|
| Uri uri | 資格情報が要求されているパッケージソース Uri。|
| IWebProxy プロキシ | ネットワーク上で通信するときに使用する Web プロキシ。 プロキシ認証が構成されていない場合は Null です。 |
| bool isProxyRequest | この要求がプロキシ認証資格情報を取得する場合は True。 実装がプロキシ資格情報の取得に対して有効でない場合は、null が返されます。 |
| bool isRetry | この Uri に対して資格情報が以前に要求されていたが、指定された資格情報が承認済みアクセスを許可していない場合は True。 |
| bool 非対話型 | True の場合、資格情報プロバイダーはすべてのユーザープロンプトを非表示にし、代わりに既定値を使用する必要があります。 |
| CancellationToken cancellationToken | 資格情報を要求している操作が取り消されたかどうかを確認するには、このキャンセルトークンを確認する必要があります。 |

**戻り値**: [ `System.Net.ICredentials` インターフェイス](/dotnet/api/system.net.icredentials)を実装する資格情報オブジェクト。
