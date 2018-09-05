---
title: NuGet 1.8 のリリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 1.8 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ff6d12606b1bed479e63eebccd978ff9cd4a7faf
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546622"
---
# <a name="nuget-18-release-notes"></a>NuGet 1.8 のリリース ノート

[NuGet 1.7 のリリース ノート](../release-notes/nuget-1.7.md) | [NuGet 2.0 のリリース ノート](../release-notes/nuget-2.0.md)

NuGet 1.8 は、2012 年 5 月 23 日にリリースされました。

## <a name="known-installation-issue"></a>インストールの既知の問題
VS 2010 SP1 を実行している場合は、インストールされている以前のバージョンがある場合は、NuGet をアップグレードしようとしています。 インストール エラーが発生実行可能性があります。

回避策では、単に NuGet をアンインストールしてから、VS 拡張ギャラリーからインストールします。  参照してください[ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019)詳細については、または[VS 修正プログラムに直接移動](http://bit.ly/vsixcertfix)します。

注: Visual Studio ([アンインストール] ボタンは無効です) 拡張機能をアンインストールすることができず、しの場合必要があります「管理者として実行」を使用して Visual Studio を再起動するには

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 と互換性のない Windows XP では、修正プログラムの発行

NuGet 1.8 がリリースされた後すぐ、1.8 の暗号化の変更が Windows XP でユーザーを解約することがわかりました。

この問題に対処する修正プログラムをリリースしましたので。  Visual Studio の拡張機能ギャラリーから NuGet を更新することでは、この修正プログラムが表示されます。

## <a name="features"></a>フィーチャー

### <a name="satellite-packages-for-localized-resources"></a>ローカライズされたリソースのサテライト パッケージ
NuGet 1.8 で .NET Framework のサテライト アセンブリの機能に似ています、ローカライズされたリソースの個別のパッケージを作成できるようになりました。  サテライト パッケージは、いくつかの規則を追加すると、他の NuGet パッケージと同じ方法で作成されます。

* サテライトのパッケージ ID とファイル名は、標準のいずれかに一致するサフィックスを含める必要があります[、.NET Framework で使用される文字列のカルチャ](http://msdn.microsoft.com/goglobal/bb896001.aspx)します。
* その`.nuspec`ファイル、サテライト パッケージする必要があります定義言語要素を ID で使用されている同じカルチャ文字列
* サテライト パッケージの依存関係を定義する必要があります、`.nuspec`ファイルをそのコア パッケージに言語サフィックスを差し引いた同じ ID を持つパッケージだけです。  コア パッケージは、インストールの成功のリポジトリで利用できる必要があります。

でローカライズされたリソースを、パッケージをインストールするには、開発者は、リポジトリからローカライズされたパッケージを明示的に選択します。 現時点では、NuGet ギャラリーでは任意の種類の特別な処理をサテライト パッケージは提供されません。

![ローカライズされたパッケージとパッケージ マネージャー ダイアログ](./media/dlg-w-loc-packs.png)

サテライト パッケージは、そのコア パッケージに依存関係を一覧表示、ため、サテライトとコアの両方のパッケージは NuGet パッケージ フォルダーに取り込むし、インストールされています。

![ローカライズされたパッケージのパッケージ フォルダー](./media/fldr-loc-packs.png)

さらに、サテライト パッケージをインストールするときに、NuGet もカルチャ文字列の名前付け規則を認識し、ローカライズされたリソース アセンブリには、.NET Framework で選択できるように、コア パッケージ内で適切なサブフォルダーにコピーされます。

![コピーしたリソースのフォルダーとコア パッケージ フォルダー](./media/fldr-copied-loc.png)

サテライト パッケージに注意してください。 1 つの既存のバグは NuGet では、ローカライズされたリソースはコピーされません、 `bin` Web サイト プロジェクトのフォルダー。  この問題は、次の NuGet のリリースで修正されます。

作成し、サテライト パッケージを使用する方法を示す完全なサンプルを参照してください。 [ https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample)します。

### <a name="package-restore-consent"></a>パッケージの復元の同意
NuGet 1.8 は、ユーザーのプライバシーを保護するパッケージの復元での重要な制約をサポートするための土台を配置します。 この制約は、プロジェクトとパッケージの復元に明示的に同意するパッケージの復元を使用しているソリューションを構築する開発者が構成済みのパッケージ ソースからパッケージをダウンロードするオンラインの移動が必要です。

この同意を提供する 2 つの方法はあります。 1 つ目は、次に示すように、パッケージ マネージャーの構成ダイアログで確認できます。  このメソッドは主に、開発者のコンピューターのものです。

![パッケージ マネージャーの構成 ダイアログ](./media/pr-consent-configdlg.png)

2 番目のメソッドでは、環境変数"EnableNuGetPackageRestore"を値"true"に設定します。  このメソッドは、CI ビルド サーバーなどの自動マシン向けです。

ここで、前述のようは、この機能を土台を NuGet 1.8 でに作り上げていますのみいます。  実際には、すべての機能を有効にロジックを追加したときに、現在強制されているこのバージョンでこれを意味します。 有効になります、ただし、次のリリースを利用することに注意してください、できるだけ早くお使いの環境を適切に構成することができますので影響を受けなくを起動したときと使用できるように、NuGet の制約を適用する同意します。

詳細についてを参照してください、[チームのブログの投稿](http://blog.nuget.org/20120518/package-restore-and-consent.html)この機能にします。

### <a name="nugetexe-performance-improvements"></a>nuget.exe のパフォーマンスの向上
ダウンロードしてパッケージを並列でインストールするインストール コマンドを変更すると、NuGet 1.8 は大幅なパフォーマンスの向上 – nuget.exe へと拡張機能パッケージの復元が表示されます。  高レベルのテストは、NuGet 1.8 で約 35% が 6 のパッケージをプロジェクトにインストールするためのパフォーマンスを向上することを示します。  25 にパッケージの数を増やすには、約 60% のパフォーマンスの向上は示しています。

## <a name="bug-fixes"></a>バグ修正
NuGet 1.8 には、パッケージ復元の同意と Windows 8 の Express の統合に関連する、特にパッケージ マネージャー コンソールと、パッケージの復元ワークフローを重視した、かなり多くのバグ修正が含まれています。
作業の完全な一覧の項目を修正しました NuGet 1.8 でくださいビュー、[このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)します。
