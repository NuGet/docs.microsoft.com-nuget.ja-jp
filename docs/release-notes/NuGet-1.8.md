---
title: NuGet 1.8 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 1.8 のリリースノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9d55534ffe765137731b7fbf4be4bbaa618c769c
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236844"
---
# <a name="nuget-18-release-notes"></a>NuGet 1.8 リリースノート

[NuGet 1.7 リリースノート](../release-notes/nuget-1.7.md)  | [NuGet 2.0 リリースノート](../release-notes/nuget-2.0.md)

NuGet 1.8 は、2012年5月23日にリリースされました。

## <a name="known-installation-issue"></a>インストールに関する既知の問題
VS 2010 SP1 を実行している場合は、以前のバージョンがインストールされている場合に NuGet をアップグレードしようとすると、インストールエラーが発生することがあります。

この回避策は、単純に NuGet をアンインストールし、VS 拡張機能ギャラリーからインストールすることです。  詳細については、「」を参照 <https://support.microsoft.com/kb/2581019> するか、 [VS 修正プログラムに直接アクセス](http://bit.ly/vsixcertfix)してください。

注: Visual Studio で拡張機能をアンインストールできない場合 ([アンインストール] ボタンが無効になっている場合)、"管理者として実行" を使用して Visual Studio を再起動する必要が生じる可能性があります。

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 は Windows XP と互換性がありません。修正プログラムが公開されました

NuGet 1.8 がリリースされた直後、1.8 での暗号化の変更が Windows XP でユーザーによって中断されたことがわかりました。

この問題に対処する修正プログラムがリリースされました。  Visual Studio 拡張機能ギャラリーから NuGet を更新すると、この修正プログラムが提供されます。

## <a name="features"></a>特徴

### <a name="satellite-packages-for-localized-resources"></a>ローカライズされたリソースのサテライトパッケージ
NuGet 1.8 では、.NET Framework のサテライトアセンブリ機能と同様に、ローカライズされたリソース用に個別のパッケージを作成する機能がサポートされるようになりました。  サテライトパッケージは、他の NuGet パッケージと同じように、いくつかの規則を追加して作成されます。

* サテライトパッケージ ID とファイル名には、 [.NET Framework によって使用される標準カルチャ文字列](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)の1つに一致するサフィックスを含める必要があります。
* ファイルでは、 `.nuspec` サテライトパッケージは、ID で使用されているのと同じカルチャ文字列を持つ言語要素を定義する必要があります。
* サテライトパッケージは、そのファイルのコアパッケージに対する依存関係を定義する必要があり `.nuspec` ます。これは、単に同じ ID を持つパッケージを言語サフィックスから引いたものです。  インストールを成功させるには、コアパッケージがリポジトリで使用可能である必要があります。

ローカライズされたリソースを含むパッケージをインストールするには、開発者がリポジトリからローカライズされたパッケージを明示的に選択します。 現時点では、NuGet ギャラリーでは、サテライトパッケージに特別な処理は一切提供されません。

![ローカライズされたパッケージを含むパッケージマネージャーダイアログ](./media/dlg-w-loc-packs.png)

サテライトパッケージはコアパッケージへの依存関係を一覧表示するため、サテライトパッケージとコアパッケージの両方が NuGet パッケージフォルダーに取り込まれ、インストールされます。

![ローカライズされたパッケージを含むパッケージフォルダー](./media/fldr-loc-packs.png)

さらに、サテライトパッケージをインストールするときに、NuGet はカルチャ文字列の名前付け規則も認識して、ローカライズされたリソースアセンブリをコアパッケージ内の適切なサブフォルダーにコピーして、.NET Framework で選択できるようにします。

![リソースフォルダーがコピーされたコアパッケージフォルダー](./media/fldr-copied-loc.png)

サテライトパッケージでメモする既存のバグの1つは、NuGet がローカライズされたリソースを `bin` Web サイトプロジェクトのフォルダーにコピーしないことです。  この問題は、NuGet の次のリリースで修正される予定です。

サテライトパッケージを作成して使用する方法を示す完全なサンプルについては、「」を参照してください [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample) 。

### <a name="package-restore-consent"></a>パッケージの復元の同意
NuGet 1.8 では、ユーザーのプライバシーを保護するために、パッケージの復元に関する重要な制約をサポートするための基礎を説明しています。 この制約には、パッケージの復元をオンラインにして、構成されたパッケージソースからパッケージをダウンロードすることに明示的に同意するために、パッケージの復元を使用するプロジェクトとソリューションを作成する開発者が必要です。

この同意を提供するには2つの方法があります。 最初の例は、次に示すように、[パッケージマネージャーの構成] ダイアログボックスにあります。  このメソッドは、主に開発者用のコンピューターを対象としています。

![パッケージマネージャーの構成ダイアログ](./media/pr-consent-configdlg.png)

2つ目の方法では、環境変数 "EnableNuGetPackageRestore" を値 "true" に設定します。  この方法は、CI やビルドサーバーなどの無人マシンを対象としています。

前述のように、この機能の基礎については、NuGet 1.8 で説明しました。  実際には、この機能を有効にするためにすべてのロジックを追加している間は、このバージョンでは現在適用されていません。 ただし、NuGet の次のリリースで有効になります。そのため、環境を適切に構成し、同意制約の適用を開始したときに影響を受けることがないように、できるだけ早くそのことを認識する必要がありました。

詳細については、この機能に関する [チームのブログ投稿](http://blog.nuget.org/20120518/package-restore-and-consent.html) を参照してください。

### <a name="nugetexe-performance-improvements"></a>nuget.exe のパフォーマンスの向上
パッケージを並列でダウンロードしてインストールするように install コマンドを変更することにより、NuGet 1.8 は nuget.exe と拡張機能パッケージの復元によって大幅なパフォーマンスの向上をもたらします。  高レベルのテストでは、6つのパッケージをプロジェクトにインストールする場合のパフォーマンスが NuGet 1.8 で約35% 向上しています。  パッケージの数を25に増やすと、約60% のパフォーマンスが向上します。

## <a name="bug-fixes"></a>バグ修正
NuGet 1.8 では、パッケージマネージャーコンソールとパッケージ復元ワークフローに重点を置いて、いくつかのバグ修正が行われています。特に、パッケージ復元の同意と Windows 8 Express の統合に関連しています。
NuGet 1.8 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)を参照してください。