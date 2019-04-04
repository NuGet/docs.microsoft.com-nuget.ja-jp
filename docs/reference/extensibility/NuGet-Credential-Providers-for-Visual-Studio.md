---
title: Visual Studio 向け NuGet 資格情報プロバイダー
description: NuGet 資格情報プロバイダーは、Visual Studio 拡張機能で IVsCredentialProvider インターフェイスを実装することによって、フィードで認証します。
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: abe009fee5863c55a188f4d7c71ed0924dd067ff
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547955"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>NuGet 資格情報プロバイダーでフィードを Visual Studio での認証

NuGet Visual Studio Extension 3.6 以降では、資格情報プロバイダーは、認証されたフィードを使用する NuGet を有効にするサポートしています。
Visual Studio 向け NuGet 資格情報プロバイダーをインストールした後、Visual Studio の NuGet 拡張機能が自動的に獲得および必要に応じて、認証されたフィードの資格情報を更新します。

実装のサンプルが記載[VsCredentialProvider サンプル](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)します。

4.8 + 以降、Visual Studio の NuGet が新しいクロス プラットフォーム認証プラグインを同様に、サポートしていますが、パフォーマンス上の理由から推奨されるアプローチではありません。

> [!Note]
> Visual Studio 向け NuGet 資格情報プロバイダーを選択し、通常 Visual Studio 拡張機能としてインストールする必要がありますが必要になります[Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe)以降。
>
> Visual Studio 向け NuGet 資格情報プロバイダーは、(dotnet 復元または nuget.exe) ではなく Visual Studio でのみ動作します。 Nuget.exe 資格情報プロバイダーは、[nuget.exe 資格情報プロバイダー](nuget-exe-Credential-providers.md)を参照してください。
> 資格情報プロバイダーでは、dotnet と msbuild を参照してください[NuGet クロス プラットフォームのプラグイン](nuget-cross-platform-authentication-plugin.md)

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Visual Studio 用の利用可能な NuGet 資格情報プロバイダー

Visual Studio Team Services をサポートするために、Visual Studio の NuGet 拡張機能に組み込まれている資格情報プロバイダーがあります。

Visual Studio の NuGet 拡張機能を使用して内部`VsCredentialProviderImporter`もプラグインの資格情報プロバイダーがスキャンします。 これらのプラグインの資格情報プロバイダーは、型の MEF エクスポートとして検出可能である必要があります`IVsCredentialProvider`します。

使用可能なプラグインの資格情報プロバイダーは次のとおりです。

- [Visual Studio 2017 向け MyGet 資格情報プロバイダー](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Visual Studio 向け NuGet 資格情報プロバイダーを作成します。

NuGet Visual Studio Extension 3.6 以降では、資格情報を取得するために使用される内部の CredentialService を実装します。 CredentialService には、組み込みおよびプラグインの資格情報プロバイダーの一覧があります。 各プロバイダーが資格情報を取得するまで順番に試されます。

資格情報の取得中に資格情報サービスに資格情報が取得されるとすぐに停止する次の順序で資格情報プロバイダーは試してください。

1. NuGet 構成ファイルから資格情報がフェッチされます (組み込みの`SettingsCredentialProvider`)。
1. Visual Studio Team Services では、パッケージ ソースがある場合、`VisualStudioAccountProvider`使用されます。
1. プラグインしている他の Visual Studio の資格情報プロバイダーは順番に試行されます。
1. 順番にクロス プラットフォームの資格情報プロバイダーのすべての NuGet を使用してください。
1. 資格情報はまだ取得されていない場合、ユーザーは標準の基本認証ダイアログを使用して資格情報を求めます。

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>IVsCredentialProvider.GetCredentialsAsync を実装します。

Visual Studio 向け NuGet 資格情報プロバイダーを作成するには、公開するパブリック MEF エクスポートを実装する Visual Studio 拡張機能を作成、`IVsCredentialProvider`以下に示す原則に準拠している型します。

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

実装のサンプルが記載[VsCredentialProvider サンプル](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)します。

Visual Studio の各 NuGet 資格情報プロバイダーが必要です。

1. かどうかを対象となる URI の資格情報が提供資格情報の取得を開始する前に決定します。 返されます場合、プロバイダーは、対象のソースの資格情報を提供できません`null`します。
1. 場合は、プロバイダーは、対象となる URI の要求を処理するには、資格情報を指定することはできません、例外がスローする必要があります。

Visual Studio 向けカスタム NuGet 資格情報プロバイダーを実装する必要があります、`IVsCredentialProvider`インターフェイスで使用できる、 [NuGet.VisualStudio パッケージ](https://www.nuget.org/packages/NuGet.VisualStudio/)します。

#### <a name="getcredentialasync"></a>GetCredentialAsync

| 入力パラメーター |説明|
| ----------------|-----------|
| Uri の uri | 資格情報が要求されているパッケージのソース Uri。|
| IWebProxy プロキシ | Web プロキシ、ネットワークで通信を行うときに使用します。 プロキシ認証の構成が存在しない場合は null です。 |
| bool isProxyRequest | この要求は、プロキシ認証の資格情報を取得する場合は true。 実装がプロキシの資格情報を取得するために有効でない場合は null が返されます。 |
| bool isRetry | True の場合、以前に資格情報が、この Uri の要求が、指定された資格情報は、承認されたアクセスを許可しませんでした。 |
| 非対話型の bool | True の場合、資格情報プロバイダーはすべてのユーザー メッセージを非表示し、既定値の代わりに使用する必要があります。 |
| CancellationToken cancellationToken | このキャンセル トークンをチェックして、操作要求元の資格情報が取り消されましたかどうかを判断する必要があります。 |

**値を返す**: 実装する資格情報オブジェクト、 [ `System.Net.ICredentials`インターフェイス](/dotnet/api/system.net.icredentials?view=netstandard-2.0)します。
