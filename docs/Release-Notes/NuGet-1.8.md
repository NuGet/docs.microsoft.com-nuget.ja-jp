---
title: "NuGet 1.8 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 1.8 のリリース ノートします。"
keywords: "NuGet 1.8 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 139c30e29d8148eab7298329a07d8e412259e595
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2018
---
# <a name="nuget-18-release-notes"></a>NuGet 1.8 のリリース ノート

[NuGet 1.7 リリース ノート](../release-notes/nuget-1.7.md) | [NuGet 2.0 リリース ノート](../release-notes/nuget-2.0.md)

NuGet 1.8 は、2012 年 5 月 23 日にリリースされました。

## <a name="known-installation-issue"></a>インストールの既知の問題
VS 2010 SP1 を実行している場合、インストールされている古いバージョンがある場合は、NuGet をアップグレードしようとしています。 インストール エラーに発生する可能性があります。

回避策では、NuGet をシンプルにアンインストールし、VS 拡張機能ギャラリーからインストールします。  参照してください[http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)詳細については、または[VS 修正プログラムに直接進んで](http://bit.ly/vsixcertfix)です。

注意: Visual Studio には、(削除 ボタンは無効になっている) 拡張機能をアンインストールすることを許可しません、可能性の高い場合"管理者として実行 を使用して Visual Studio を再起動するには

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 と互換性のない Windows XP では、修正プログラムの発行

NuGet 1.8 のリリース後すぐ 1.8 の暗号化の変更が、Windows XP でユーザーを超えたことがわかりました。

この問題に対処する修正プログラムをリリースしたためです。  NuGet Visual Studio 拡張機能ギャラリーを更新することでは、この修正プログラムを受信します。

## <a name="features"></a>フィーチャー

### <a name="satellite-packages-for-localized-resources"></a>ローカライズされたリソース用サテライト パッケージ
NuGet 1.8 には、.NET Framework のサテライト アセンブリの機能に似ています、ローカライズされたリソースに対して別々 のパッケージを作成する機能がサポートされました。  サテライト パッケージは、いくつかの規則を追加すると、他の NuGet パッケージと同じ方法で作成されます。

* サテライトのパッケージ ID とファイル名は、標準のいずれかに一致するサフィックスを含める必要があります[、.NET Framework で使用される文字列のカルチャ](http://msdn.microsoft.com/goglobal/bb896001.aspx)です。
* その`.nuspec`ファイル、サテライト パッケージする必要がありますを定義する言語要素 ID で使用されている同じカルチャ文字列
* サテライト パッケージ内の依存関係を定義する必要があります、`.nuspec`言語サフィックス マイナス同じ ID を持つパッケージだけでは、そのコア パッケージにファイル。  コア パッケージでは、インストールの成功のリポジトリで使用できる必要があります。

パッケージをインストールするには、ローカライズされたリソースで、開発者は明示的にリポジトリからローカライズされたパッケージを選択します。 現時点では、NuGet ギャラリーにサテライト パッケージへの特別な処理の任意の種類は許可されません。

![ローカライズされたパッケージとパッケージ マネージャー ダイアログ](./media/dlg-w-loc-packs.png)

サテライト パッケージ一覧のコア パッケージに依存関係があるので、サテライトとコア パッケージの NuGet パッケージ フォルダーに取り込まれたされインストールされます。

![ローカライズ版パッケージとパッケージ フォルダー](./media/fldr-loc-packs.png)

さらに、サテライト パッケージのインストール中に、NuGet はカルチャ文字列の名前付け規則にも認識され、ローカライズされたリソース アセンブリ、.NET Framework で選択できるようにコア パッケージ内で適切なサブフォルダーにコピーされます。

![コア パッケージ フォルダーをコピーしたリソースのフォルダーと](./media/fldr-copied-loc.png)

サテライト パッケージに注意して 1 つの既存のバグは NuGet では、ローカライズされたリソースにはコピーされません、 `bin` Web サイト プロジェクトのフォルダーです。  この問題は、NuGet の次のリリースで修正されます。

完全なサンプルを作成し、サテライト パッケージを使用する方法を示す、次を参照してください。 [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample)です。

### <a name="package-restore-consent"></a>パッケージの復元の同意
NuGet 1.8 は、ユーザーのプライバシーを保護するパッケージの復元での重要な制約をサポートするための基礎が配置されます。 この制約は、プロジェクトおよびパッケージの復元に明示的に同意するパッケージの復元を使用しているソリューションを構築する開発者のオンラインへの移行を構成済みのパッケージ ソースからパッケージをダウンロードする必要があります。

この同意を提供する 2 つの方法はあります。 最初は、次のように、パッケージ マネージャーの構成ダイアログで確認できます。  このメソッドは、主に、開発者のマシンのものです。

![パッケージ マネージャーの構成 ダイアログ](./media/pr-consent-configdlg.png)

2 番目のメソッドでは、環境変数"EnableNuGetPackageRestore"を値"true"に設定します。  このメソッドは CI またはビルド サーバーなどの無人のコンピューターものです。

ここで、前述のように、おがのみの基礎この機能を NuGet 1.8 でします。  実際には、すべての機能を有効にロジックを追加したときが現在強制されているこのバージョンでこれを意味します。 有効になります、ただし、次のリリースようにすることを認識できるだけ早く、環境を適切に構成することができ、したがっては影響を受けませんが開始したかったため、NuGet の制約を適用する同意します。

詳細についてを参照してください、[チームのブログの投稿](http://blog.nuget.org/20120518/package-restore-and-consent.html)この機能にします。

### <a name="nugetexe-performance-improvements"></a>nuget.exe パフォーマンスの向上
ダウンロードして、パッケージを並列でインストールするインストール コマンドを変更すると、NuGet 1.8 は nuget.exe – へと拡張機能パッケージの復元によって大幅なパフォーマンスの向上が表示されます。  高レベルのテストは、NuGet 1.8 の約 35 %6 パッケージをプロジェクトにインストールするためのパフォーマンスを向上することを示します。  25 へのパッケージの数を増やすことを示しています約 60% のパフォーマンスが向上します。

## <a name="bug-fixes"></a>バグ修正
NuGet 1.8 には、パッケージの復元の同意画面および Windows 8 の Express の統合に関連するように特にパッケージ マネージャー コンソールとパッケージの復元のワークフローに重点を置いて、かなり多くのバグ修正が含まれています。
作業の完全な一覧の項目で修正 NuGet 1.8 くださいビュー、[今回のリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)です。
