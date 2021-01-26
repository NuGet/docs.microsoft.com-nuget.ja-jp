---
title: NuGet 2.8 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.8 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cb77cf0f049b5b3cfe1039d83ab58e33457674bf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776715"
---
# <a name="nuget-28-release-notes"></a>NuGet 2.8 リリースノート

[NuGet 2.7.2 のリリースノート](../release-notes/nuget-2.7.2.md)  | [NuGet 2.8.1 のリリースノート](../release-notes/nuget-2.8.1.md)

NuGet 2.8 は、2014年1月29日にリリースされました。

## <a name="acknowledgements"></a>謝辞

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ( [@leppie](https://twitter.com/leppie) )
    - [#3466](https://nuget.codeplex.com/workitem/3466) -パッケージをパックするときに、依存関係パッケージの Id を確認しています。
2. [マールテン島 balliauw 氏](https://www.codeplex.com/site/users/view/maartenba) ( [@maartenballiauw](https://twitter.com/maartenballiauw) )
    - [#2379](https://nuget.codeplex.com/workitem/2379) -persistening フィードの資格情報を持っている場合に、$metadata サフィックスを削除します。
3. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ( [@foxtricks](https://twitter.com/foxtricks) )
    - [#3538](http://nuget.codeplex.com/workitem/3538) -nuget.exe update コマンドに対してプロジェクトファイルを指定する機能をサポートしています。
4. [フアン Gonzalez。](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) 置換トークンが-IncludeReferencedProjects で渡されません。
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ( [@Sarkie_Dave](https://twitter.com/Sarkie_Dave) )
    - [#3677](http://nuget.codeplex.com/workitem/3677) -大きなパッケージをプッシュするときに OutOfMemoryException をスローします。
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -プロジェクトが別の CLI/c + + プロジェクトを参照している場合に、不適切なターゲットパスを修正します。
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )
    - [#3639](https://nuget.codeplex.com/workitem/3639) -既定でパッケージを開発の依存関係としてインストールできるようにする
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ( [@davidfowl](https://twitter.com/davidfowl) )
    - [#3717](https://nuget.codeplex.com/workitem/3717) -最新の修正プログラムのバージョンへの暗黙的なアップグレードを削除する
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - いくつかのバグ修正と、NuGet. Server、nuget.exe mirror コマンド、およびその他の機能強化。
    - この作業は数か月にわたって行われました。 Gregory は、2.8 のマスターに統合するための適切なタイミングで動作します。

## <a name="patch-resolution-for-dependencies"></a>依存関係の修正プログラムの解像度

パッケージの依存関係を解決するとき、NuGet では、パッケージの依存関係を満たす最低メジャーおよびマイナーパッケージバージョンを選択するための戦略が実装されていました。 ただし、メジャーバージョンとマイナーバージョンとは異なり、修正プログラムのバージョンは常に最も高いバージョンに解決されていました。 動作は攻撃者でしたが、依存関係を含むパッケージをインストールするための決定性が欠如しています。 次の例を確認してください。

```
PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

PackageB@1.0.1 is published

Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1
```

この例では、Developer1 と Developer2 がインストールされていても PackageA@1.0.0 、それぞれ異なるバージョンの PackageB で終了しています。 NuGet 2.8 では、修正プログラムのバージョンの依存関係の解決動作がメジャーバージョンとマイナーバージョンの動作に一致するように、この既定の動作が変更されています。 上の例では、 PackageB@1.0.0 PackageA@1.0.0 新しい修正プログラムのバージョンに関係なく、をインストールした結果としてがインストールされます。

## <a name="-dependencyversion-switch"></a>-DependencyVersion スイッチ

NuGet 2.8 では、依存関係を解決するための _既定_ の動作が変更されますが、パッケージマネージャーコンソールの-dependencyversion スイッチを使用して依存関係の解決プロセスをさらに細かく制御することもできます。 スイッチを使用すると、依存関係を、可能な限り低いバージョン (既定の動作)、可能な限り高いバージョン、または最新のマイナーバージョンまたは修正プログラムバージョンに解決できます。  このスイッチは、powershell コマンドのインストールパッケージに対してのみ機能します。

![DependencyVersion スイッチ](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>DependencyVersion 属性

前に説明した-DependencyVersion スイッチに加えて、NuGet では、-DependencyVersion スイッチがインストールパッケージの呼び出しで指定されていない場合に、既定値を定義する Nuget.Config ファイルに新しい属性を設定することもできます。 この値は、すべてのインストールパッケージ操作の [NuGet パッケージマネージャー] ダイアログでも尊重されます。 この値を設定するには、次の属性を Nuget.Config ファイルに追加します。

```xml
<config>
    <add key="dependencyversion" value="Highest" />
</config>
```

## <a name="preview-nuget-operations-with--whatif"></a>-Whatif を使用した NuGet 操作のプレビュー

一部の NuGet パッケージには、深い依存関係グラフを含めることができます。そのため、インストール、アンインストール、または更新の操作中に、何が発生するかを最初に確認するのに役立ちます。 NuGet 2.8 では、コマンドが適用されるパッケージのクロージャ全体を視覚化できるように、パッケージのインストール、アンインストール、および更新パッケージの各コマンドに標準の PowerShell-whatif スイッチが追加されています。 たとえば、空の `install-package Microsoft.AspNet.WebApi -whatif` ASP.NET Web アプリケーションでを実行すると、次のようになります。

```
PM> install-package Microsoft.AspNet.WebApi -whatif
Attempting to resolve dependency 'Microsoft.AspNet.WebApi.WebHost (≥ 5.0.0)'.
Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Core (≥ 5.0.0)'.
Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Client (≥ 5.0.0)'.
Attempting to resolve dependency 'Newtonsoft.Json (≥ 4.5.11)'.
Install Newtonsoft.Json 4.5.11
Install Microsoft.AspNet.WebApi.Client 5.0.0
Install Microsoft.AspNet.WebApi.Core 5.0.0
Install Microsoft.AspNet.WebApi.WebHost 5.0.0
Install Microsoft.AspNet.WebApi 5.0.0
```

## <a name="downgrade-package"></a>パッケージのダウングレード

新しい機能を調査し、最新の安定したバージョンにロールバックすることを決定するために、パッケージのプレリリース版をインストールすることは珍しくありません。 NuGet 2.8 より前では、これはプレリリースパッケージとその依存関係をアンインストールしてから、以前のバージョンをインストールする、複数の手順から成るプロセスでした。 ただし、NuGet 2.8 では、更新プログラムパッケージはパッケージのクロージャ全体 (パッケージの依存関係ツリーなど) を以前のバージョンにロールバックします。

## <a name="development-dependencies"></a>開発の依存関係

さまざまな種類の機能を NuGet パッケージとして提供できます。これには、開発プロセスの最適化に使用するツールが含まれます。 これらのコンポーネントは、新しいパッケージの開発に役立ちますが、後で公開するときに新しいパッケージの依存関係とは見なさないでください。 NuGet 2.8 を使用すると、パッケージは `.nuspec` developmentDependency としてファイル内で自身を識別できます。 このメタデータは、インストールされると、パッケージがインストールされ `packages.config` たプロジェクトのファイルにも追加されます。 その `packages.config` ファイルが後で NuGet の依存関係を分析したときに `nuget.exe pack` 、開発の依存関係としてマークされた依存関係は除外されます。

## <a name="individual-packagesconfig-files-for-different-platforms"></a>さまざまなプラットフォームの個々の packages.config ファイル

複数のターゲットプラットフォーム用のアプリケーションを開発する場合は、それぞれのビルド環境に対して異なるプロジェクトファイルを使用するのが一般的です。 さまざまなプロジェクトファイルで異なる NuGet パッケージを使用することもよくあります。パッケージには、プラットフォームごとに異なるレベルのサポートが用意されているためです。 NuGet 2.8 では、 `packages.config` プラットフォーム固有のさまざまなプロジェクトファイルごとに異なるファイルを作成することによって、このシナリオのサポートが向上しています。

![複数の package.config ファイル](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>ローカルキャッシュへのフォールバック

通常、NuGet パッケージは、ネットワーク接続を使用する [nuget ギャラリー](http://www.nuget.org/) などのリモートギャラリーから使用されますが、クライアントが接続されていないシナリオは多数あります。 ネットワーク接続がないと、NuGet クライアントは、パッケージがローカルの NuGet キャッシュ内のクライアントコンピューターに既に存在する場合でも、パッケージを正常にインストールできませんでした。 NuGet 2.8 では、自動キャッシュフォールバックがパッケージマネージャーコンソールに追加されます。 たとえば、ネットワークアダプターを切断して jQuery をインストールする場合、コンソールには次のように表示されます。

```
PM> Install-Package jquery
The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
Installing 'jQuery 2.0.3'.
Successfully installed 'jQuery 2.0.3'.
Adding 'jQuery 2.0.3' to WebApplication18.
Successfully added 'jQuery 2.0.3' to WebApplication18.
```

キャッシュフォールバック機能では、特定のコマンド引数は必要ありません。 さらに、現在、キャッシュフォールバックはパッケージマネージャーコンソールでのみ機能します。現在、[パッケージマネージャー] ダイアログボックスで動作は機能しません。

## <a name="webmatrix-nuget-client-updates"></a>WebMatrix NuGet クライアントの更新プログラム

Nuget 2.8 と共に、nuget [2.5](../release-notes/nuget-2.5.md)で提供される主な機能の多くを含むように、WebMatrix 用の nuget 拡張機能も更新されました。 新しい機能としては、' Update All '、' Minimum NuGet Version ' などがあり、コンテンツファイルの上書きが許可されています。

WebMatrix 3 で NuGet パッケージマネージャー拡張機能を更新するには、次のようにします。

1. WebMatrix 3 を開く
1. リボンの [拡張機能] アイコンをクリックします。
1. [更新] タブを選択します。
1. クリックして NuGet パッケージマネージャーを2.5.0 に更新します
1. WebMatrix 3 を閉じて再起動する

これは、WebMatrix の nuget パッケージマネージャー拡張機能の最初のリリースです。  このコードは、Microsoft がオープンソースの NuGet プロジェクトに最近貢献しました。 以前は、NuGet 統合は WebMatrix に組み込まれており、WebMatrix から帯域外で更新することはできませんでした。  NuGet のクライアントツールの残りの部分と共に、さらに更新する機能が追加されました。

## <a name="bug-fixes"></a>バグの修正

バグを修正した主な問題の1つは、更新プログラムパッケージの再インストールコマンドでパフォーマンスを向上させることでした。

これらの機能と上記のパフォーマンスの修正に加えて、この NuGet のリリースには他にも多くのバグ修正が含まれています。 リリースで解決された問題の合計は181でした。 NuGet 2.8 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)を参照してください。
