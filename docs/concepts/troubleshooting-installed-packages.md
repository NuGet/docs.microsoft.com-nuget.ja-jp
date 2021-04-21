---
title: インストールされているパッケージのトラブルシューティング
description: 個々のパッケージに使用されたパッケージ ソースを見つける方法
author: JonDouglas
ms.author: jodou
ms.date: 03/26/2021
ms.topic: conceptual
ms.openlocfilehash: 22fb51ebb996c66e10b860f0158676fd2d9da295
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387531"
---
# <a name="troubleshooting-installed-packages"></a>インストールされているパッケージのトラブルシューティング

特定のパッケージがどのソースからインストールされたかを確認したい場合があります。 ここでは、いくつかの確認方法を示します。

> [!Note]
> 一部のパッケージ ソースでは、アップストリーム ソースと呼ばれる概念がサポートされています。 たとえば、[Azure Artifacts アップストリーム ソース](/azure/devops/artifacts/concepts/upstream-sources)です。 NuGet クライアントでは、パッケージがアップストリーム ソースからのものであるかどうかが認識されません。 そのため、パッケージ ソースのログ記録には、アップストリーム ソースではなく、構成されているソースが記載されます。

## <a name="nupkgmetadata-file-in-global-packages-folder"></a>グローバル パッケージ フォルダー内の `.nupkg.metadata` ファイル

パッケージが *global-packages* フォルダーに抽出されるときに、ファイル `.nupkg.metadata` が書き込まれます。 NuGet 5.9.0 から、NuGet ではパッケージ ソースが追加されます。 NuGet のバージョンを Visual Studio または .NET SDK のバージョンにマップするには、以下を参照してください。 次に例を示します。

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> NuGet 5.9.0 を持つ新しいバージョンのツールにアップグレードする前に抽出したパッケージが *global-packages* フォルダーにある場合、`.nupkg.metadata` ファイルはバージョン 1 になり、パッケージ ソースは含まれません。 [*global-packages* フォルダーをクリア](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders)して、すべてのパッケージにパッケージ ソースが含まれるようにすることができます。

> [!Tip]
> NuGet によって `.nupkg.metadata` ファイルが書き込まれるのは、*global-packages* フォルダーに対してのみです。 `packages.config` を使用するプロジェクトではソリューション パッケージ フォルダーが使用されますが、`.nupkg.metadata` ファイルは作成されません。

## <a name="installed-package-log-message"></a>インストールされたパッケージのログ メッセージ

NuGet 5.9.0 から、NuGet では、パッケージがインストールされたことを通知する復元メッセージに、パッケージ ソースが出力されます。 次に例を示します。

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> このメッセージは、通常または情報の詳細度で出力されます。 Visual Studio と `dotnet` CLI では最小の詳細度に既定値が設定されるため、このメッセージは既定では表示されません。 `msbuild` と `nuget` CLI ツールでは通常の詳細度に既定値が設定されるため、このメッセージは既定で表示されます。

## <a name="http-log-message"></a>HTTP ログ メッセージ

パッケージをローカルで利用できない場合は、*global-packages* フォルダー、フォールバック フォルダー、またはローカル ファイル ソースのいずれかに、NuGet によって、任意の構成されたパッケージ ソースから HTTP 経由でパッケージがダウンロードされます。 HTTP 要求と応答は通常の詳細度レベルでログに記録されます。また、パッケージのバージョンごとに 1 つの要求と応答のみが表示されます。 次に例を示します。

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

ファイルが最近ダウンロードされていた場合は、NuGet の *http-cache* から取得される可能性があります

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

URL 形式は、異なる NuGet HTTP サーバーの実装や、NuGet V2 または V3 HTTP プロトコルが実装されているかどうかによって、異なる場合があります。

`nuget.config` に複数の HTTP ソースが定義されている場合は、各パッケージの `index.json` ファイルに対して複数の要求が表示されます (各ソースにつき 1 つ)。 ただし、パッケージの各バージョンについて、ダウンロードされるのは 1 つの `nupkg` だけになります。

## <a name="package-signature-log-message"></a>パッケージの署名のログ メッセージ

ダウンロードするパッケージが署名されている場合、NuGet によって署名が検証され、詳細度が高い場合は次のメッセージが記録されます。

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

このメッセージでは、パッケージが HTTP パッケージ ソースからダウンロードされたか、またはローカル パッケージ ソースからコピーされたかが報告されます。 パッケージが *global-packages* フォルダーまたはフォールバック フォルダーで既に使用可能な場合は、出力されません。

> [!Important]
> [VeriSign CA の信頼の削除](https://github.com/dotnet/announcements/issues/180)により、NuGet では、特定のプラットフォームで、特定のバージョンの NuGet および .NET SDK において、署名付きパッケージの検証が無効になっています。 そのため、復元を実行しているプラットフォームや、使用している .NET または NuGet のバージョンによっては、同じパッケージに `PackageSignatureVerificationLog` ログがある場合と、それらのログが見つからない場合があります。

## <a name="nuget-version-map"></a>NuGet のバージョンのマップ

次のバージョンの NuGet には、パッケージ ソースのログに関する重要な変更点があります。

|NuGet のバージョン|Visual Studio のバージョン|.NET SDK のバージョン|
|---|---|---|
|NuGet 5.9.0|Visual Studio 2019 16.9.0|.NET 5 SDK 5.0.200|
