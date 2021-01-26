---
title: WebMatrix の NuGet 2.6.1 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む、NuGet 2.6.1 向けのリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780418"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>WebMatrix の NuGet 2.6.1 のリリースノート

[NuGet 2.6 リリースノート](../release-notes/nuget-2.6.md)  | [NuGet 2.7 リリースノート](../release-notes/nuget-2.7.md)

NuGet チームは、2014年3月26日に WebMatrix 用に更新された NuGet パッケージマネージャー拡張機能をリリースしました。  この更新プログラムは、次の手順を使用して [WebMatrix 拡張機能ギャラリー](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) からインストールできます。

1. WebMatrix 3 を開く
1. [ホーム] リボンの [拡張機能] アイコンをクリックします。
1. [更新] タブを選択します。
1. クリックして NuGet パッケージマネージャーを2.6.1 に更新します
1. WebMatrix 3 を閉じて再起動する

## <a name="notable-changes"></a>注目すべき変更点

この拡張機能の更新では、ユーザーが WebMatrix で NuGet パッケージを使用することに直面した最大の問題の2つに対処します。  1つ目は NuGet スキーマバージョンエラーで、2番目はフォルダー内のゼロバイト Dll に先行するバグでした `bin` 。

### <a name="nuget-schema-version-error"></a>NuGet スキーマバージョンエラー

WebMatrix 3 がリリースされたため、nuget パッケージの新しいスキーマバージョンを必要とする新しい機能が NuGet に導入されました。  Web サイトで NuGet パッケージを管理しようとすると、これらの新しいパッケージによって、WebMatrix に表示されるエラーが発生する可能性があります。

![エラーが発生しました。 スキーマのバージョンに互換性がありません。 NuGet を最新バージョンにアップグレードしてください。](./media/NuGet-2.8/webmatrix-schema-version.png)

この最新リリースでは、最新の NuGet パッケージとの互換性が確保されているため、このエラーの発生を回避できます。 WebMatrix を含む新しいバージョンのパッケージを WebMatrix にインストールできるようになりました。  これらのパッケージの一部では、現在 WebMatrix ではサポートされていない [Xdt 構成変換](../release-notes/nuget-2.6.md#xdt)などの NuGet 機能を使用していました。

### <a name="zero-byte-dlls-in-bin-folder"></a>Bin フォルダー内の Dll の Zero-Byte

Bin にコピーされる Dll を含む、WebMatrix で NuGet パッケージをインストールした後、Dll が `bin` 0 バイトファイルとしてフォルダーに表示されることが、一部のユーザーに報告されています。  これにより、実行時にアプリケーションが中断されます。

[この問題](https://nuget.codeplex.com/workitem/4060) は修正されました。

## <a name="other-recent-improvements"></a>その他の最新の機能強化

Visual Studio の NuGet パッケージマネージャー2.8 がリリースされたときに、WebMatrix の NuGet パッケージマネージャー2.5.0 もリリースしました。  これは [NuGet 2.8 リリースノート](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)に記載されていますが、更新された特定の新機能については触れませんでした。

### <a name="update-all"></a>すべて更新

これで、すべての web サイトのパッケージを1回の手順で更新できるようになりました。  WebMatrix で NuGet 拡張機能を開くと、ギャラリーのすべてのパッケージ、インストールされているパッケージ、および更新プログラムが利用可能なすべてのパッケージの一覧が表示されます。  以前は、すべてのパッケージを個別に更新する必要がありましたが、[更新] タブに表示される [すべて更新] ボタンがあります。

![[すべて更新] をクリックして、利用可能な更新プログラムを含むすべてのパッケージを更新します](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>既存のファイルを上書きする

Web サイトに既に存在するファイルを含むパッケージをインストールする場合、NuGet は常にそのファイルを自動的に無視しただけです (既存のファイルはそのままです)。  これにより、パッケージが正しくインストールまたは更新されたという印象が生じる可能性があります。  ファイルの上書きを確認するメッセージが表示されるようになりました。

![ファイルの競合の解決](./media/NuGet-2.8/webmatrix-overwrite-file.png)
