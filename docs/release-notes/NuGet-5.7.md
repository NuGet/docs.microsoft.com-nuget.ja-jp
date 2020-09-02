---
title: NuGet 5.7 リリースノート
description: 新機能、バグ修正、および DCRs を含む NuGet 5.7 のリリースノート。
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 6c821091983ab0b5d59b759e1ee9930cf449fd9d
ms.sourcegitcommit: 6cda91f135e58cf57a2471b0c7c4a2f748f40024
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "89364152"
---
# <a name="nuget-57-release-notes"></a>NuGet 5.7 リリースノート

NuGet 配布の種類:

| NuGet のバージョン | 利用可能な Visual Studio バージョン | 利用可能な .NET SDK |
|:---|:---|:---|
| [**5.7.0**](https://nuget.org/downloads) | [Visual Studio 2019 バージョン 16.7](https://visualstudio.microsoft.com/downloads/) | [3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Visual Studio 2019 と .net Core ワークロードと共にインストールされる

## <a name="summary-whats-new-in-57"></a>概要: 5.7 の新機能

### <a name="features-added-in-this-release"></a>このリリースで追加された機能

* NuGet パッケージ参照の extern エイリアスサポートを追加しました- [#4989](https://github.com/NuGet/Home/issues/4989)

* では、データソースを共有し、resfreshing を減らすことができる[#8294](https://github.com/NuGet/Home/issues/8294)ので、インストールされているタブと更新プログラムのタブを迅速に切り替えることができました。

* MSBuild スタティック Graph api (dotnet.exe) を呼び出すことにより、復元時間を短縮し、評価を高速化します。 [#9644](https://github.com/NuGet/Home/issues/9644)

* PackageReference プロジェクトの Visual Studio 部分復元を追加しました (非 op + +)- [#9513](https://github.com/NuGet/Home/issues/9513)

* HTTP 要求ごとに要求された数を超える結果を返す、不適切なパッケージソースを検索すると、Visual Studio パッケージマネージャー UI がクラッシュする頻度が低くなります。 - [#8478](https://github.com/NuGet/Home/issues/8478)

* VS [#9236](https://github.com/NuGet/Home/issues/9236)での非 SDK スタイルプロジェクトの PackageVersion 情報の統合を追加しました

* nuget.exe update のサポートが追加されました `-self -Source` https://feed  -  [#1783](https://github.com/NuGet/Home/issues/1783)

* % Appdata% uget ディレクトリに複数の構成ファイルのサポートが追加されました- [#9394](https://github.com/NuGet/Home/issues/9394)

* DeterministicSourcePaths では、NuGet ソースパッケージをアカウントに [#9431](https://github.com/NuGet/Home/issues/9431)

* INuGetProjectService 非同期機能拡張 API が追加されました- [#9702](https://github.com/NuGet/Home/issues/9702)

* ソリューションまたはプロジェクトを必要とせずに、フォールバックフォルダーを列挙する相互運用 API を追加しました。 [#9395](https://github.com/NuGet/Home/issues/9395)

* `latest`#8808 のオプション `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)を追加しました

### <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

**バグ**

* Dotnet CLI の復元で、資格情報プラグインを起動するときに、 `DOTNET_HOST_PATH`  環境変数が定義されていない場合は、システムパスで DOTNET CLI を試してみてください。 - [#7438](https://github.com/NuGet/Home/issues/7438)

* nuget.exe spec は、ハードコーディングされたテキストを使用して著作権タグを生成し、その代わりに著作権情報 YYYY を入力 `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)

* NuGet.exe は、アセンブリ名が変更された場合、プレースホルダーおよび assemblyinfo 属性を無視して、.csproj のパック中に "authors required" という例外をスローし [#4234](https://github.com/NuGet/Home/issues/4234)

* HttpRequestMessage は、 [#8661](https://github.com/NuGet/Home/issues/8661) SocketHttpHandler でサポートされていない複数回再利用を行うことができます。

* 5.6.0 preview 3 以降のインデックス作成では、別の公開キートークンを使用して [#9481](https://github.com/NuGet/Home/issues/9481)

* NuGet パッケージの作成時に TreatWarningsAsErrors を優先する- [#7404](https://github.com/NuGet/Home/issues/7404)

* [CPVM]複数の p2p プロジェクトの誤ったパッケージダウングレード- [#9549](https://github.com/NuGet/Home/issues/9549)

* [参照] タブは、検索ボックスに左揃えになっていません- [#9559](https://github.com/NuGet/Home/issues/9559)

* インストールされているバージョンが、複数のバージョンがインストールされている1つのパッケージ id について、ソリューションレベル PM の UI に埋め込まれたアイコンと一致しません- [#9321](https://github.com/NuGet/Home/issues/9321)

* リーク: Partのポリシー ("共有しないポリシー................. RestoreOperationLogger- [#9595](https://github.com/NuGet/Home/issues/9595)

* 操作なしの復元でアセットファイルを読み取らないようにする- [#9693](https://github.com/NuGet/Home/issues/9693)

* NuGet. プロトコルは、検索からバージョンのダウンロード数を取得することをサポートしていません [#9086](https://github.com/NuGet/Home/issues/9086)

* JObject の依存関係を減らすことで PackageMetadataResourceV3 のメモリパフォーマンスを向上させる- [#9719](https://github.com/NuGet/Home/issues/9719)

**変更要求のデザイン:**

* `<owners>`冗長である場合に要素を抑制した[#5134](https://github.com/NuGet/Home/issues/5134)

* ETW イベントとしてのログ IntervalTrackers- [#9593](https://github.com/NuGet/Home/issues/9593)

* 機能がプレビュー中であることを CPVM ユーザーに通知するために、復元時に情報メッセージを追加しました- [#9340](https://github.com/NuGet/Home/issues/9340)

* アセットファイルからソリューションエクスプローラーパッケージ/プロジェクトの推移的な依存関係を設定する- [#9580](https://github.com/NuGet/Home/issues/9580)

* [インストールされたパッケージ] タブでパッケージの一覧を改ページすることはありません- [#6995](https://github.com/NuGet/Home/issues/6995)

**[このリリースで修正されるすべての問題の一覧-5.7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**

### <a name="community-contributions"></a>コミュニティからの投稿

この NuGet のリリースに役立ったすべての共同作成者に感謝します。

|担当者|Pr|issue|
|----|----|----|
|[campersau](https://github.com/campersau)|[3433](https://github.com/NuGet/NuGet.Client/pull/3433)、 [3120](https://github.com/NuGet/NuGet.Client/pull/3120)|NuGet. プロトコルは、検索からバージョンのダウンロード数を取得することをサポートしていません [#9086](https://github.com/NuGet/Home/issues/9086) </br>HttpRequestMessage は、 [#8661](https://github.com/NuGet/Home/issues/8661) SocketHttpHandler でサポートされていない複数回再利用を行うことができます。|
|[ジョセフ・マス・ Ser (jnm2)](https://github.com/jnm2)|[3241](https://github.com/NuGet/NuGet.Client/pull/3241)|`<owners>`冗長である場合に要素を抑制した[#5134](https://github.com/NuGet/Home/issues/5134)|
|[Volodymyr Shkolka (BlackGad)](https://github.com/BlackGad)|[3273](https://github.com/NuGet/NuGet.Client/pull/3273)|NuGet では、クライアント証明書を必要とする HTTPS ソースからは復元できません- [#5773](https://github.com/NuGet/Home/issues/5773)|
|[Marius Ungureanu (ole Zok)](https://github.com/Therzok)|[3357](https://github.com/NuGet/NuGet.Client/pull/3357)|HttpSourceAuthenticationHandler SemaphoreSlim 未来の校正- [#9463](https://github.com/NuGet/Home/issues/9463)|
|[Sunner ()](https://github.com/SuNNjek)|[3088](https://github.com/NuGet/NuGet.Client/pull/3088)|nuget.exe spec は、ハードコーディングされたテキストを使用して著作権タグを生成し、その代わりに著作権情報 YYYY を入力 `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)|
|[Olivier Spinelli (olivier-spinelli)](https://github.com/olivier-spinelli)|[3335](https://github.com/NuGet/NuGet.Client/pull/3335)|Dotnet CLI の復元で、資格情報プラグインを起動するときに、 `DOTNET_HOST_PATH`  環境変数が定義されていない場合は、システムパスで DOTNET CLI を試してみてください。 - [#7438](https://github.com/NuGet/Home/issues/7438)|
|[goyzhang](https://github.com/goyzhang)|[3370](https://github.com/NuGet/NuGet.Client/pull/3370)|`latest`#8808 のオプション `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)を追加しました|
