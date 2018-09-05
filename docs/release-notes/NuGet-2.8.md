---
title: NuGet 2.8 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 2.8 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547460"
---
# <a name="nuget-28-release-notes"></a>NuGet 2.8 リリース ノート

[NuGet 2.7.2 リリース ノート](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 のリリース ノート](../release-notes/nuget-2.8.1.md)

NuGet 2.8 は、2014 年 1 月 29 日にリリースされました。

## <a name="acknowledgements"></a>謝辞

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) - パッケージの依存関係パッケージの Id を確認しています。
2. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -persistening フィードの資格情報には、$metadata サフィックスを削除します。
3. [Filip De の](https://www.codeplex.com/site/users/view/FilipDeVos)([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) - nuget.exe の update コマンド用のプロジェクト ファイルの指定をサポートします。
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -- IncludeReferencedProjects と共に渡すできません置換トークン。
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -修正 nuget.push 大きなパッケージをプッシュするときは、OutOfMemoryException をスローします。
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -プロジェクトが別の CLI と C++ プロジェクトを参照するときの修正プログラムのターゲットが正しくないパス。
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -既定では開発依存関係としてインストールするパッケージを許可します。
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -最新のパッチ バージョンへの暗黙的なアップグレードの削除
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - いくつかのバグ修正と改善 NuGet.Server、nuget.exe ミラー コマンド、およびその他のユーザー。
    - この作業は、数か月間、2.8 のマスターに統合する適切なタイミングで協力 Gregory で行われました。

## <a name="patch-resolution-for-dependencies"></a>依存関係の修正プログラムの解決

パッケージの依存関係を解決するときに NuGet は従来のパッケージの依存関係を満たす最下位のメジャーおよびマイナーのパッケージ バージョンを選択する戦略を実装しました。 メジャーおよびマイナーのバージョンとは異なり、修正プログラムのバージョン常に解決された最上位のバージョンを。 動作は、理由の 1 つが、依存関係を持つパッケージをインストールするための決定性の欠如が作成されます。 次に例を示します。

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

この例では、たとえ Developer1 と Developer2 インストールPackageA@1.0.0PackageB の別のバージョンをそれぞれに終了しました。 NuGet 2.8 では、修正プログラムのバージョンの依存関係の解決の動作は、メジャーおよびマイナーのバージョンの動作と一致するようにこの既定の動作が変わります。 次に、上記の例でPackageB@1.0.0をインストールすると、インストールPackageA@1.0.0新しいパッチ バージョンに関係なく、します。

## <a name="-dependencyversion-switch"></a>-DependencyVersion スイッチ

NuGet 2.8 の変更が、_既定_動作の依存関係を解決するためも追加されます。 これに DependencyVersion スイッチを使用して依存関係解決プロセスをより細かく制御パッケージ マネージャー コンソール。 スイッチは、最下位の可能なバージョン (既定の動作)、最高の可能なバージョンや最上位のマイナーまたは修正プログラムのバージョンに依存関係を解決できます。  このスイッチは、powershell コマンドでインストール パッケージにのみ機能します。

![DependencyVersion スイッチ](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>DependencyVersion 属性

上記の詳細、NuGet が必要なアクセス許可も使用できます。 Nuget.Config ファイルに新しい属性を設定する - DependencyVersion スイッチだけでなくを定義する既定値の呼び出しでは、- DependencyVersion スイッチが指定されていない場合インストール パッケージです。 この値は、任意の操作のインストール パッケージを NuGet パッケージ マネージャー ダイアログでも適用されます。 この値を設定するには、Nuget.Config ファイルに次の属性を追加します。

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>-Whatif をプレビュー NuGet の操作

NuGet パッケージの一部は、厳密な依存関係のグラフを持つことができ、そのため、そのことができます、インストール中に立つ、アンインストール、または更新操作がまずどうなるかを確認します。 NuGet 2.8 は、パッケージのインストール、アンインストール、パッケージ、およびコマンドの適用先となるパッケージのクロージャ全体をビジュアル化を有効にする更新プログラム パッケージのコマンドに標準の PowerShell-whatif スイッチを追加します。 たとえば、実行している`install-package Microsoft.AspNet.WebApi -whatif`空の ASP.NET Web アプリケーションには、次が得られます。

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

新しい機能を調査するために、パッケージのプレリリース版をインストールし、最後の安定したバージョンにロールバックすることは珍しくありません。 NuGet 2.8、前に、プレリリースのパッケージとその依存関係をアンインストールすると、以前のバージョンをインストールし、複数の手順をしました。 NuGet 2.8 でただし、更新プログラム パッケージはようになりました (例: パッケージの依存関係ツリー) 全体のパッケージ クロージャにロールバック以前のバージョン。

## <a name="development-dependencies"></a>開発の依存関係

さまざまな種類の機能は、開発プロセスを最適化するために使用されるツールを含む - NuGet パッケージとして配信できます。 これらのコンポーネントを新しいパッケージの開発に役立つ可能性があるときに見なされない新しいパッケージの依存関係後で発行されているとします。 NuGet 2.8 により、パッケージ自体を識別するために、`.nuspec`では developmentDependency としてのファイル。 このメタデータに追加することも、インストールされている場合、`packages.config`パッケージがインストールされたプロジェクトのファイル。 時を`packages.config`ファイルは後の中に、NuGet の依存関係分析`nuget.exe pack`開発の依存関係としてマークされているこれらの依存関係が除外されます。

## <a name="individual-packagesconfig-files-for-different-platforms"></a>さまざまなプラットフォーム向けの個々 の packages.config ファイル

複数のターゲット プラットフォーム用のアプリケーションを開発する場合は、別のプロジェクト ファイルのそれぞれのビルド環境を持つ一般的なは。 パッケージがあるさまざまなレベルのさまざまなプラットフォームのサポートのためにも別のプロジェクト ファイルで別の NuGet パッケージを使用する一般的です。 NuGet 2.8 別に作成してこのシナリオのサポートの強化を提供します`packages.config`さまざまなプラットフォーム固有プロジェクト ファイルのファイル。

![複数の package.config ファイル](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>ローカル キャッシュへのフォールバック

NuGet パッケージの通常使用される、リモート ギャラリーからなど、 [NuGet ギャラリー](http://www.nuget.org/)ネットワーク接続を使用して、クライアントが接続されていないシナリオはよくあります。 ネットワーク接続を行わず、NuGet クライアントはこれらのパッケージは、ローカル NuGet キャッシュ内で、クライアント コンピューターに存在した場合でもパッケージを正常にインストールできませんでした。 NuGet 2.8 は、パッケージ マネージャー コンソールをキャッシュの自動フォールバックを追加します。 たとえば、ときに、ネットワーク アダプターを切断して、jQuery をインストールする、コンソール次に示します。

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

キャッシュ フォールバック機能では、特定のコマンド引数は必要ありません。 さらに、フォールバックのキャッシュは、現在、パッケージ マネージャー コンソールでのみ機能 - パッケージ マネージャー ダイアログで、動作が現在機能しません。

## <a name="webmatrix-nuget-client-updates"></a>WebMatrix の NuGet クライアントの更新プログラムします。

NuGet 2.8、と共に、WebMatrix の NuGet 拡張機能はで提供される主な機能の多くに更新もが[NuGet 2.5](../release-notes/nuget-2.5.md)します。 新機能では、' Update All'、' 最小 NuGet バージョン '、およびコンテンツ ファイルの上書きの許可などがあります。

WebMatrix 3 で NuGet パッケージ マネージャー拡張機能の更新。

1. WebMatrix 3 を開く
1. リボンの拡張機能アイコンをクリックします
1. [更新] タブを選択します。
1. 2.5.0 を NuGet パッケージ マネージャーを更新する をクリックします。
1. 閉じて再起動 WebMatrix 3

これは、WebMatrix 用の NuGet パッケージ マネージャー拡張機能に NuGet チームの初回リリースです。  コードが最近、オープン ソースの NuGet プロジェクトに Microsoft によって提供されました。 以前は、WebMatrix に、NuGet は統合が組み込まれているし、WebMatrix から帯域外更新できませんでした。  さらに、NuGet のクライアント ツールの残りの部分と共に更新する機能があるようになりました。

## <a name="bug-fixes"></a>バグ修正

更新プログラム パッケージのパフォーマンスの向上が行われた主要なバグ修正のいずれかのコマンドを再インストールします。

NuGet のこのリリースには、これらの機能および上記のパフォーマンスの修正プログラム、に加えて、他の多くのバグ修正も含まれます。 リリースで対処された 181 合計問題が発生しました。 作業の完全な一覧の項目で修正された NuGet 2.8、くださいビュー、[このリリースの NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)します。
