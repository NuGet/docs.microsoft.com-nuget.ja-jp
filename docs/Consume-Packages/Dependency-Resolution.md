---
title: "NuGet パッケージの依存関係の解決 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 1d530a72-3486-4a0d-b6fb-017524616f91
description: "NuGet 2.x と NuGet 3.x 以降の両方について、NuGet パッケージの依存関係が解決されてインストールされるプロセスを詳しく説明します。"
keywords: "NuGet パッケージの依存関係, NuGet のバージョン管理, 依存関係のバージョン, バージョン グラフ, バージョンの解決, 推移的な復元"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 93a3d077a6dd1946485fc8c48f97c8009280890c
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2018
---
# <a name="how-nuget-resolves-package-dependencies"></a>NuGet でのパッケージ依存関係の解決方法

パッケージがインストールまたは再インストールされるときは常に ([復元](../consume-packages/package-restore.md)プロセスの一部としてインストールされる場合も含めて)、NuGet はその最初のパッケージが依存する他のパッケージもすべてインストールします。

これらの直接依存するものにもそれぞれに独自の依存関係が存在する可能性があり、任意の深さまでそれが続きます。 これにより、すべてのレベルにおけるパッケージ間の関係が記述された "*依存関係グラフ*" と呼ばれるものが生成されます。

複数のパッケージに同じ依存関係がある場合、グラフに同じパッケージ ID が異なるバージョン制約で複数回出現する可能性があります。 ただし、プロジェクトで使うことができる指定されたパッケージのバージョンは 1 つだけなので、NuGet は使うバージョンを選ぶ必要があります。 実際のプロセスは、使われているパッケージ参照の形式によって異なります。

このトピックの内容:
- [PackageReference と project.json での依存関係の解決](#dependency-resolution-with-packagereference-and-projectjson)
- [packages.config での依存関係の解決](#dependency-resolution-with-packagesconfig)
- [参照の除外](#excluding-references)。あるプロジェクトで指定されている依存関係と、別のプロジェクトによって生成されるアセンブリの間に競合があるときに必要になります。
- [パッケージをインストールする間の依存関係の更新](#dependency-updates-during-package-install)
- [互換性のないパッケージのエラーの解決](#resolving-incompatible-package-errors)

## <a name="dependency-resolution-with-packagereference-and-projectjson"></a>PackageReference と project.json での依存関係の解決

PackageReference または `project.json` の形式を使ってプロジェクトにパッケージをインストールする場合、NuGet はフラットなパッケージ グラフへの参照を適切なファイルに追加して、事前に競合を解決します。 このプロセスは、"*推移的な復元*" と呼ばれます。 この場合、パッケージの再インストールまたは復元はグラフに列記されているパッケージをダウンロードするプロセスであり、結果としてビルドはいっそう高速で予測可能になります。 また、ワイルドカード (浮動) バージョン (2.8\* など) を利用することもでき、コストがかかってエラーが発生しやすい `nuget update` の呼び出しをクライアント コンピューターやビルド サーバーで回避できます。

ビルド前に実行した NuGet の復元プロセスは、最初にメモリ内で依存関係を解決した後、結果のグラフを、PackageReference を使うプロジェクトの `obj` フォルダーの `project.assets.json` という名前のファイルに、または `project.json` と共に使われる `project.lock.json` という名前のファイルに書き込みます。 その後、MSBuild はこのファイルを読み取り、潜在的な参照が見つかるフォルダーのセットに変換して、メモリ内のプロジェクト ツリーに追加します。

ロック ファイルは一時的なものであり、ソース管理に追加してはなりません。 ロック ファイルは既定で `.gitignore` と `.tfignore` の両方に一覧表示されます。 「[パッケージとソース管理](Packages-and-Source-Control.md)」をご覧ください。

### <a name="dependency-resolution-rules"></a>依存関係の解決ルール

推移的な復元では、依存関係を解決するために、適用可能な最低バージョン、浮動バージョン、最近優先、いとこ依存関係の 4 つの主要なルールが適用されます。

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>適用可能な最低バージョン

適用可能な最低バージョン ルールは、依存関係によって定義されている最低の可能なバージョンのパッケージを復元します。 また、[浮動](#floating-versions)と宣言されていない限り、アプリケーションまたはクラス ライブラリの依存関係にも適用されます。

次の図では、たとえば 1.0-beta は 1.0 より低いと見なされるので、NuGet は 1.0 バージョンを選びます。

![適用可能な最低バージョンの選択](media/projectJson-dependency-1.png)

次の図では、バージョン 2.1 はフィードで利用できませんが、バージョンの制約が 2.1 以上なので、NuGet は見つかった次に低いバージョンである 2.2 を選びます。

![フィードで利用可能な次に低いバージョンの選択](media/projectJson-dependency-2.png)

アプリケーションで厳密なバージョン (1.2 など) が指定されていて、フィードでそれを利用できない場合、パッケージをインストールまたは復元しようとした NuGet はエラーで失敗します。

![厳密に指定されたバージョンのパッケージを利用できない場合、NuGet はエラーを生成する](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a>浮動 (ワイルドカード) バージョン

浮動依存関係バージョンまたはワイルドカード依存関係バージョンは、6.0.\* のように \* ワイルドカードを使って指定します。 このバージョン指定は、"最新の 6.0.x バージョンを使う" ということです。たとえば、4.\* は "最新の 4.x バージョンを使う" ことを意味します。 ワイルドカードを使うと、使用する側のアプリケーション (またはパッケージ) を変更することなく、依存関係のパッケージのバージョンを上げることができます。

ワイルドカードを使った場合、NuGet はバージョン パターンと一致する最高バージョンのパッケージを解決します。たとえば、6.0.\* は 6.0 で始まるパッケージの最高バージョンになります。

![浮動バージョン 6.0.* が要求されたときは、バージョン 6.0.1 を選ぶ](media/projectJson-dependency-4.png)

> [!Note]
> ワイルドカードの動作およびプレリリース バージョンについては、「[パッケージのバージョン管理](../reference/package-versioning.md#version-ranges-and-wildcards)」をご覧ください。


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>最近優先

アプリケーションのパッケージ グラフに同じパッケージの異なるバージョンが含まれる場合、NuGet はグラフ内でアプリケーションに最も近いパッケージを選び、他のすべてのパッケージは無視します。 この動作により、アプリケーションは依存関係グラフ内で特定のパッケージのバージョンを上書きできます。

次の例では、アプリケーションはバージョン制約 2.0 以上でパッケージ B に直接依存しています。 また、アプリケーションはパッケージ A にも依存していますが、パッケージ A も 1.0 以上の制約でパッケージ B に依存しています。 パッケージ B 2.0 に対する依存関係の方がグラフでアプリケーションに近いので、バージョン 2.0 が使われます。

![最近優先ルールを使うアプリケーション](media/projectJson-dependency-5.png)

>[!Warning]
> 最近優先ルールでは、パッケージのバージョンのダウングレードが発生することがあるので、グラフ内の他の依存関係が損なわれる可能性があります。 そのため、このルールを適用するとユーザーに警告が通知されます。

また、このルールでは、指定された依存関係が無視されると、NuGet はグラフのその分岐にある残りの依存関係もすべて無視するので、大規模な依存関係グラフ (BCL パッケージを含むものなど) での効率が大幅に向上する効果もあります。 たとえば、次の図では、パッケージ C 2.0 が使われるため、NuGet は古いバージョンのパッケージ C を参照しているグラフ内のすべての分岐を無視します。

![NuGet は、グラフ内のパッケージを無視するとき、その分岐全体を無視する](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>いとこ依存関係

グラフ内のアプリケーションから同じ距離で、同じパッケージの異なるバージョンが参照されている場合、NuGet はすべてのバージョン要件が満たされる最低バージョンを使います ([適用可能な最低バージョン](#lowest-applicable-version)および[浮動バージョン](#floating-versions) ルールと同様)。 たとえば、次の図では、パッケージ B のバージョン 2.0 はいとこの 1.0 以上という制約を満たすので、バージョン 2.0 が使われます。

![すべての制約を満たす最低バージョンを使う、いとこ依存関係の解決](media/projectJson-dependency-7.png)

状況によっては、すべてのバージョン要件を満たすことができない場合があります。 次に示すように、パッケージ A ではパッケージ B 1.0 だけが必要であり、パッケージ C ではパッケージ B 2.0 以上が必要である場合、NuGet は依存関係を解決できずエラーを生成します。

![厳密なバージョン要件のために解決できない依存関係](media/projectJson-dependency-8.png)

このような状況では、最上位のコンシューマー (アプリケーションまたはパッケージ) がパッケージ B に対する独自の直接依存関係を追加して、[最近優先](#nearest-wins)ルールが適用されるようにする必要があります。

## <a name="dependency-resolution-with-packagesconfig"></a>packages.config での依存関係の解決

`packages.config` では、プロジェクトの依存関係はフラット リストとして `packages.config` に書き込まれます。 これらのパッケージの依存関係も、同じリストに書き込まれます。 パッケージがインストールされると、NuGet は `.csproj` ファイル、`app.config`、`web.config`、および他の個別ファイルも変更する場合があります。

`packages.config` の場合、NuGet は個々のパッケージのインストール中に依存関係の競合の解決を試みます。 つまり、パッケージ B に依存するパッケージ A がインストールされていて、パッケージ B が別のものの依存関係として `packages.config` のリストに既に含まれる場合、NuGet は要求されているパッケージ B のバージョンを比較し、すべてのバージョン制約を満たすバージョンの発見を試みます。 具体的には、NuGet は依存関係を満たす低い方の *major.minor* バージョンを選びます。

既定では、2.7 以前の NuGet は最も高い "*パッチ*" バージョンを解決します (*major.minor.patch.build* 表記規則を使います)。 [NuGet 2.8 以降](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)では、この動作が最低のパッチ バージョンを既定で探すように変更されています。 この設定は、`Nuget.Config` の `DependencyVersion` 属性およびコマンド ラインの `-DependencyVersion` スイッチで制御できます。  

`packages.config` の依存関係解決プロセスは、大規模な依存関係グラフでは複雑になります。 パッケージの各新規インストールでは、グラフ全体を走査して、バージョン間の競合の可能性を明らかにする必要があります。 競合が発生するときは、インストールが停止されて、プロジェクトは不明な状態のままになります (特に、プロジェクト ファイル自体への変更の可能性がある場合)。 他のパッケージ参照形式を使うと、このような問題はありません。


## <a name="managing-dependency-assets"></a>依存関係の資産の管理

`project.json` 形式または PackageReference 形式を使うと、依存関係から最上位レベルのプロジェクトへの資産のフローを制御できます。 詳しくは、「[project.json reference](../Schema/project-json.md)」(project.json リファレンス) および「[Package references in project files](Package-References-in-Project-Files.md#controlling-dependency-assets)」(プロジェクト ファイルでのパッケージ参照) をご覧ください。

最上位レベルのプロジェクト自体がパッケージである場合は、`include` および `exclude` 属性と `.nuspec` ファイルの依存関係リストを使って、このフローを制御することもできます。 「.nuspec Reference」(.nuspec リファレンス) の「[Dependencies](../Schema/nuspec.md#dependencies)」(依存関係) をご覧ください。

## <a name="excluding-references"></a>参照の除外

同じ名前のアセンブリがプロジェクト内の複数の箇所で参照されていて、設計時エラーおよびビルド時エラーが発生することがあります。 あるプロジェクトは、`C.dll` のカスタム バージョンを含み、やはり `C.dll` を含むパッケージ C を参照しているものとします。 同時に、このプロジェクトはパッケージ B にも依存しており、パッケージ B もパッケージ C と `C.dll` に依存しています。 結果として、NuGet はどの `C.dll` を使えばよいのか決定できず、かといってパッケージ B もパッケージ C に依存しているため、プロジェクトでのパッケージ C に対する依存関係を単に削除するわけにもいきません。

これを解決するには、必要な `C.dll` を直接参照し (または、適切なパッケージを参照している別のパッケージを使い)、すべての資産を除外するパッケージ C への依存関係を追加します。 これは、使われているパッケージ参照形式に応じて、次のように行われます。

- [PackageReference](../consume-packages/package-references-in-project-files.md): 依存関係に `Exclude="All"` を追加します。

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" Exclude="All" />
    ```

- `packages.config`: 必要なバージョンの `C.dll` だけを参照するように、`.csproj` ファイルからパッケージ C への参照を削除します。
    
- `project.json`: パッケージ C の依存関係に `"exclude" : "all"` を追加します。

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

- [プロジェクト ファイル内のパッケージ参照](../consume-packages/package-references-in-project-files.md)で (NuGet 4.0 以降のみ)、次のように依存関係に `ExcludeAssets="All"` を追加します。

    ```xml
    <PackageReference Include="packageC" Version="1.0.0" ExcludeAssets="All" />
    ```

## <a name="dependency-updates-during-package-install"></a>パッケージをインストールする間の依存関係の更新 

2.4.x 以前の NuGet では、依存関係がプロジェクトに既に存在するパッケージがインストールされるときに、既存のバージョンが制約を満たしている場合であっても、バージョンの制約を満たす最新のバージョンに依存関係が更新されます。 

たとえば、パッケージ A はパッケージ B に依存し、バージョン番号として 1.0 が指定されているものとします。 ソース リポジトリには、パッケージ B のバージョン 1.0、1.1、1.2 が含まれます。B のバージョン 1.0 が既に含まれるプロジェクトに A をインストールした場合、B はバージョン 1.2 に更新されます。 

NuGet 2.5 以降では、依存関係のバージョンが既に満たされている場合、他のパッケージのインストール中に依存関係は更新されません。 

上と同じ例で、NuGet 2.5 以降のプロジェクトにパッケージ A をインストールすると、パッケージ B は既にバージョン制約を満たしているので 1.0 のままになります。 ただし、パッケージ A で B のバージョン 1.1 以上が要求されていた場合は、B 1.2 がインストールします。 

## <a name="resolving-incompatible-package-errors"></a>互換性のないパッケージのエラーの解決

パッケージの復元操作の間に、"1 つ以上のパッケージは <プロジェクトのターゲット フレームワーク> と互換性がありません" またはパッケージはプロジェクトのターゲット フレームワークと "互換性がありません" という内容のエラーが表示されることがあります。

このエラーは、プロジェクトで参照されているパッケージの 1 つ以上が、プロジェクトのターゲット フレームワークをサポートしていることを示さない場合に発生します。つまり、パッケージの `lib` フォルダーには、プロジェクトと互換性のあるターゲット フレームワーク用の適切な DLL が含まれません  (「[Target frameworks](../Schema/Target-Frameworks.md)」(ターゲット フレームワーク) をご覧ください)。 

たとえば、プロジェクトのターゲットが `netstandard1.6` である場合に、`lib\net20` および `\lib\net45` フォルダーだけに DLL が含まれるパッケージをインストールしようとすると、パッケージおよび場合によっては依存関係に対し、次のようなメッセージが表示されます。

```output
Restoring packages for myproject.csproj...
Package ContosoUtilities 2.1.2.3 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoUtilities 2.1.2.3 supports:
  - net20 (.NETFramework,Version=v2.0)
  - net45 (.NETFramework,Version=v4.5)
Package ContosoCore 0.86.0 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoCore 0.86.0 supports:
  - 11 (11,Version=v0.0)
  - net20 (.NETFramework,Version=v2.0)
  - sl3 (Silverlight,Version=v3.0)
  - sl4 (Silverlight,Version=v4.0)
One or more packages are incompatible with .NETStandard,Version=v1.6.
Package restore failed. Rolling back package changes for 'MyProject'.
```

互換性の問題を解決するには、次のいずれかのようにします。

- 使うパッケージでサポートされているフレームワークに、プロジェクトのターゲットを変更します。
- パッケージの作成者に連絡し、協力して、選んだフレームワークに対するサポートを追加します。 [nuget.org](https://www.nuget.org/) の各パッケージ リスト ページには、そのための **[Contact Owners]** リンクがあります。
- **お勧めしません**: パッケージ作成者と作業するときの一時的な解決策として、`netcore`、`netstandard`、および `netcoreapp` を対象とするプロジェクトでは、他のフレームワークを互換性があるものとして指定し、これらの他のフレームワークを対象とするパッケージを使うことができます。 [project.json のインポート](../Schema/project-json.md#imports)に関するページおよび [MSBuild 復元ターゲットの PackageTargetFallback](../Schema/msbuild-targets.md#packagetargetfallback) に関するページをご覧ください。 この方法では予期しない動作が発生する可能性があるので、繰り返しますが、パッケージ作成者との共同作業または更新によってパッケージの非互換性を解決することをお勧めします。
