---
title: "NuGet 2.8 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 2.8 のリリース ノートします。"
keywords: "NuGet 2.8 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 39b885adc9e23eb815f65639875c4a4c27d61a4c
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-28-release-notes"></a>NuGet 2.8 のリリース ノート

[NuGet 2.7.2 リリース ノート](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 リリース ノート](../release-notes/nuget-2.8.1.md)

NuGet 2.8 は、2014 年 1 月 29 日にリリースされました。

## <a name="acknowledgements"></a>謝辞

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466)梱包パッケージ、依存関係パッケージの Id を検証するときにします。
1. [マルテン Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -persistening 資格情報をフィードするときに、$metadata サフィックスを削除します。
1. [Filip De の](https://www.codeplex.com/site/users/view/FilipDeVos)([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) - nuget.exe update コマンド用のプロジェクト ファイルの指定をサポートします。
1. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -- IncludeReferencedProjects と共に渡すできません置換トークンです。
1. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -修正 nuget.push 大きなパッケージのプッシュ時に、OutOfMemoryException をスローします。
1. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -プロジェクトが別の CLI と C++ プロジェクトを参照するときの修正プログラムの無効なターゲット パス。
1. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -開発の依存関係として既定でインストールするパッケージを許可します。
1. [David ファウラー](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -最新のパッチ バージョンにアップグレードする暗黙の型を削除します。
1. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - いくつかのバグの修正と NuGet.Server、nuget.exe ミラー コマンドおよびその他の機能強化。
    - この作業は、2.8 のマスターに統合する右のタイミングで協力 Gregory を使用して数か月間、経由で行われました。

## <a name="patch-resolution-for-dependencies"></a>依存関係の解決の修正プログラム

パッケージの依存関係を解決するときに NuGet はパッケージへの依存関係を満たすメジャーおよびマイナーのパッケージの最も低いバージョンを選択した場合の戦略を実装してきました。 メジャーおよびマイナーのバージョンとは異なりただし、修正プログラムのバージョンが常に解決最高のバージョン。 動作が善意、依存関係を持つパッケージをインストールするための決定性の欠如が作成されます。 次に例を示します。

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

この例では、たとえ Developer1 と Developer2 インストールPackageA@1.0.0PackageB の別のバージョンのそれぞれに終了しました。 NuGet 2.8 は、修正プログラムのバージョンの依存関係の解決の動作がメジャーおよびマイナー バージョンの動作と一致するように、この既定の動作を変更します。 上記の例で、次に、PackageB@1.0.0インストールの結果としてインストールされるPackageA@1.0.0修正プログラムの新しいバージョンに関係なく、します。

## <a name="-dependencyversion-switch"></a>-DependencyVersion Switch

NuGet 2.8 の変更が、_既定_動作の依存関係を解決するためにも追加 - DependencyVersion スイッチ経由で依存関係の解決プロセスを細かく制御パッケージ マネージャー コンソールです。 スイッチは、最下位の可能なバージョン (既定の動作)、最大の可能なバージョンまたは最高のマイナーまたは修正プログラムのバージョンに依存関係を解決できます。  このスイッチは、powershell コマンドでのインストール パッケージに対してのみ機能します。

![DependencyVersion スイッチ](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>DependencyVersion 属性

に加えて、上述 NuGet が必要なアクセス許可も許可されている Nuget.Config ファイルの新しい属性を設定する - DependencyVersion スイッチを定義する既定値の呼び出しでは、- DependencyVersion スイッチが指定されていない場合インストール パッケージです。 この値が、任意の操作のインストール パッケージの NuGet Package Manager ダイアログ ボックスでも適用されます。 この値を設定するには、Nuget.Config ファイルに以下の属性を追加します。

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>-Whatif でプレビュー NuGet 操作

そのため、そのことができますのインストール中に役に立ちます、アンインストール、または更新操作が最初に何が起こるかを確認するおよび一部の NuGet パッケージの詳細な依存関係グラフがあります。 NuGet 2.8 は、パッケージのインストール、アンインストール パッケージおよびコマンドの適用先となるパッケージの全体のクロージャをビジュアル化を有効にする更新プログラム パッケージのコマンドを標準の PowerShell-whatif スイッチを追加します。 たとえば、実行している`install-package Microsoft.AspNet.WebApi -whatif`空の ASP.NET Web アプリケーションには、次が得られます。

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

## <a name="downgrade-package"></a>パッケージのダウン グレード

新機能を調査するために、パッケージのプレリリース版をインストールし、最後の安定したバージョンにロールバックするには珍しいことはできません。 NuGet 2.8 の前に、これはプレリリースのパッケージとその依存関係をアンインストールし、以前のバージョンをインストールのプロセスを複数のステップをでした。 NuGet 2.8 を使用ただし、更新プログラム パッケージは今すぐパッケージ全体のクロージャ (例: パッケージの依存関係ツリー) にロールバック前のバージョン。

## <a name="development-dependencies"></a>開発の依存関係

さまざまな種類の機能は、NuGet パッケージの開発プロセスを最適化するために使用されるツールを含むとして配信することができます。 これらのコンポーネントは、新しいパッケージの開発に役立つ可能性があるときに区別しない新しいパッケージの依存関係後で発行されているとします。 自身を識別するパッケージの NuGet 2.8 を有効、 `.nuspec` developmentDependency としてファイル。 このメタデータに追加することも、インストールされている場合、`packages.config`プロジェクト、パッケージのインストール先のファイルです。 時を`packages.config`ファイルは後の中に、NuGet の依存関係の分析`nuget.exe pack`開発の依存関係としてマークされているこれらの依存関係が除外されます。

## <a name="individual-packagesconfig-files-for-different-platforms"></a>さまざまなプラットフォーム用の個別の packages.config ファイル

複数のターゲット プラットフォーム用のアプリケーションを開発するときは、それぞれのビルド環境のそれぞれに対して別のプロジェクト ファイルを一般的なです。 パッケージがさまざまなプラットフォームのサポートのさまざまなレベルにも、別のプロジェクト ファイル内の別の NuGet パッケージを使用する一般的なです。 NuGet 2.8 のサポートの強化このシナリオを作成することにより異なる`packages.config`さまざまなプラットフォーム固有のプロジェクト ファイルのファイルです。

![複数の package.config ファイル](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>ローカル キャッシュにフォールバック

NuGet パッケージの通常使用されるリモート ギャラリーからなど、 [NuGet ギャラリー](http://www.nuget.org/)ネットワーク接続を使用するシナリオは多くのクライアントが接続されていません。 ネットワーク接続を行わず NuGet クライアントは、それらのパッケージは NuGet のローカル キャッシュ内のクライアント コンピューターに存在した場合でも、パッケージ - を正常にインストールできませんでした。 NuGet 2.8 は、キャッシュの自動フォールバックをパッケージ マネージャー コンソールに追加します。 たとえば、ときに、ネットワーク アダプターを切断して、jQuery をインストールする、コンソール次に示します。

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

キャッシュのフォールバック機能には、特定のコマンド引数は不要です。 さらに、フォールバック キャッシュが現在パッケージ マネージャー コンソールでのみ機能 - パッケージ マネージャー ダイアログで、動作が現在機能しません。

## <a name="webmatrix-nuget-client-updates"></a>WebMatrix NuGet クライアントの更新プログラムします。

NuGet 2.8 と共に WebMatrix の NuGet 拡張機能も更新されたで提供される主要な機能の多くを[NuGet 2.5](../release-notes/nuget-2.5.md)です。 新機能では、' All Update'、' 最小 NuGet バージョン ' などのコンテンツ ファイルが上書きされることがあります。

WebMatrix 3 での NuGet Package Manager 拡張機能を更新します。

1. WebMatrix 3 を開く
1. リボンの拡張機能のアイコンをクリックします。
1. 更新プログラム タブを選択します。
1. 2.5.0 に NuGet Package Manager を更新する をクリックします。
1. 終了し、WebMatrix 3 の再起動

これは、NuGet チームの最初のリリースの NuGet Package Manager 拡張機能の WebMatrix 用です。  コードが最近から提供された Microsoft オープン ソース NuGet のプロジェクトにします。 以前は、NuGet の統合された、WebMatrix に組み込まれているし、帯域外 WebMatrix から更新できませんでした。  さらに、NuGet のクライアント ツールの残りの部分と共にに更新する機能があるようになりました。

## <a name="bug-fixes"></a>バグ修正

更新プログラム パッケージのパフォーマンスの向上が加えられた主なバグの修正のいずれかのコマンドを再インストールします。

NuGet の今回のリリースには、これらの機能と、上記のパフォーマンス修正に加えて、他の多くのバグ修正も含まれます。 リリースで対処 181 の合計の問題が発生しました。 作業の完全な一覧の項目で修正 NuGet 2.8 くださいビュー、[今回のリリースの NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)です。
