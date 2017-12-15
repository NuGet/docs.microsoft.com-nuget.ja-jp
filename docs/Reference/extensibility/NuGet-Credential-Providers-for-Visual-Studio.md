---
title: "Visual Studio の NuGet の資格情報プロバイダー |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 9c7f6d16-f437-47c4-82d4-6c996e0b18ec
description: "NuGet の資格情報プロバイダーは、Visual Studio 拡張機能で IVsCredentialProvider インターフェイスを実装することによって、フィードで認証します。"
keywords: "NuGet の資格情報プロバイダー、フィードでの認証、ギャラリー、NuGet の visual studio 拡張機能での認証"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2b2fac23102865a08509acc1cc3d09f0cd375f26
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>NuGet の資格情報プロバイダーと Visual Studio でのフィードの認証

NuGet Visual Studio 拡張機能、3.6 以降には、認証されているフィードを使用する NuGet を有効にする資格情報プロバイダーがサポートしています。
Visual Studio の NuGet の資格情報プロバイダーをインストールした後、NuGet の Visual Studio 拡張機能が自動的に獲得および必要に応じて、フィードの認証された資格情報を更新します。

実装のサンプルは含まれて[VsCredentialProvider サンプル](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)です。

> [!Note]
> Visual Studio の NuGet の資格情報プロバイダーが通常の Visual Studio 拡張機能としてインストールする必要があり、必要になります[Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (現在プレビュー中) またはそれ以降。
>
> Visual Studio の NuGet の資格情報プロバイダーは、(dotnet 復元や nuget.exe) ではなく Visual Studio でのみ動作します。 Nuget.exe、資格情報プロバイダーを参照してください。 [nuget.exe 資格情報プロバイダー](nuget-exe-Credential-providers.md)です。

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Visual Studio の使用可能な NuGet 資格情報プロバイダー

Visual Studio Team Services をサポートするために、Visual Studio の NuGet 拡張機能に組み込まれている資格情報プロバイダーがあります。

NuGet の Visual Studio 拡張機能を使用して、内部`VsCredentialProviderImporter`プラグインの資格情報プロバイダーのスキャンが実行します。 これらのプラグインの資格情報プロバイダーは、型の MEF エクスポートとして探索可能である必要があります`IVsCredentialProvider`です。

使用可能なプラグインの資格情報プロバイダーは次のとおりです。

- [Visual Studio 2017 向け MyGet 資格情報プロバイダー](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Visual Studio の NuGet 資格情報プロバイダーを作成します。

NuGet Visual Studio 拡張機能、3.6 以降では、資格情報の取得に使用される内部 CredentialService を実装します。 CredentialService には、組み込みおよびプラグインの資格情報プロバイダーの一覧があります。 資格情報を取得するまで、各プロバイダーは順番に試されます。

資格情報の取得中に資格情報のサービスは資格情報を取得するとすぐに停止する次の順序で資格情報プロバイダーをしてください。

1. NuGet の構成ファイルから資格情報がフェッチされます (組み込みを使用して`SettingsCredentialProvider`)。
1. パッケージ ソースが Visual Studio Team Services にある場合、`VisualStudioAccountProvider`使用されます。
1. その他のすべてのプラグインの資格情報プロバイダーは順番に試行されます。
1. 資格情報はまだ取得されていない、ユーザーは、標準の基本認証ダイアログを使用する資格情報を求められます。

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>IVsCredentialProvider.GetCredentialsAsync を実装します。

Visual Studio の NuGet の資格情報プロバイダーを作成するには、公開するパブリック MEF エクスポートを実装する、Visual Studio 拡張機能を作成、 `IVsCredentialProvider` 「」とは大きく分けて次原則に従います。

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

実装のサンプルは含まれて[VsCredentialProvider サンプル](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)です。

Visual Studio の各 NuGet 資格情報プロバイダーが必要です。

1. かどうか、資格情報を入力、対象となる URI の資格情報の取得を開始する前に決定します。 かどうかは、プロバイダーは、対象のソースの資格情報を提供できません、返すか`null`です。
1. プロバイダーでは、対象となる URI の要求を処理している場合、資格情報を指定することはできません、例外がスローされます。

Visual Studio のカスタム NuGet 資格情報プロバイダーを実装する必要があります、`IVsCredentialProvider`インターフェイスで使用できる、 [NuGet.VisualStudio パッケージ](https://www.nuget.org/packages/NuGet.VisualStudio/)です。

#### <a name="getcredentialasync"></a>GetCredentialAsync

| 入力パラメーター |説明|
| ----------------|-----------|
| Uri の uri | 資格情報が要求されているパッケージ ソースの Uri。|
| IWebProxy プロキシ | ネットワークで通信を行うときに使用する web プロキシです。 プロキシ認証の構成が存在しない場合は null です。 |
| bool isProxyRequest | この要求はプロキシ認証の資格情報を取得する場合は true。 実装がプロキシ資格情報を取得するために有効でない場合 null を返される必要があります。 |
| bool isRetry | True の場合、資格情報がこの Uri は、以前要求したが、指定された資格情報は、承認されたアクセスを許可しませんでした。 |
| 非対話型の bool | True の場合、資格情報プロバイダーはすべてのユーザー メッセージを抑制して、既定値の代わりに使用する必要があります。 |
| CancellationToken cancellationToken | このキャンセル トークンを確認して、操作要求元の資格情報が取り消されましたかどうかを特定する必要があります。 |
  
**戻り値**: 資格情報オブジェクトを実装する、 [ `System.Net.ICredentials`インターフェイス](https://msdn.microsoft.com/library/system.net.icredentials.aspx)です。
