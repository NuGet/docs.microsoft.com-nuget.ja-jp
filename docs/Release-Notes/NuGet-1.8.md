---
title: NuGet 1.8 リリース ノート |Microsoft ドキュメント
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 1.8 のリリース ノートします。
keywords: NuGet 1.8 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: b94382f79143cac6bd5deccb5e5253ba8c6f60ec
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-18-release-notes"></a><span data-ttu-id="258c4-104">NuGet 1.8 のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="258c4-104">NuGet 1.8 Release Notes</span></span>

<span data-ttu-id="258c4-105">[NuGet 1.7 リリース ノート](../release-notes/nuget-1.7.md) | [NuGet 2.0 リリース ノート](../release-notes/nuget-2.0.md)</span><span class="sxs-lookup"><span data-stu-id="258c4-105">[NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md) | [NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md)</span></span>

<span data-ttu-id="258c4-106">NuGet 1.8 は、2012 年 5 月 23 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="258c4-106">NuGet 1.8 was released on May 23, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="258c4-107">インストールの既知の問題</span><span class="sxs-lookup"><span data-stu-id="258c4-107">Known Installation Issue</span></span>
<span data-ttu-id="258c4-108">VS 2010 SP1 を実行している場合、インストールされている古いバージョンがある場合は、NuGet をアップグレードしようとしています。 インストール エラーに発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="258c4-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="258c4-109">回避策では、NuGet をシンプルにアンインストールし、VS 拡張機能ギャラリーからインストールします。</span><span class="sxs-lookup"><span data-stu-id="258c4-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="258c4-110">参照してください[ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019)詳細については、または[VS 修正プログラムに直接進んで](http://bit.ly/vsixcertfix)です。</span><span class="sxs-lookup"><span data-stu-id="258c4-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="258c4-111">注意: Visual Studio には、(削除 ボタンは無効になっている) 拡張機能をアンインストールすることを許可しません、可能性の高い場合"管理者として実行 を使用して Visual Studio を再起動するには</span><span class="sxs-lookup"><span data-stu-id="258c4-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a><span data-ttu-id="258c4-112">NuGet 1.8 と互換性のない Windows XP では、修正プログラムの発行</span><span class="sxs-lookup"><span data-stu-id="258c4-112">NuGet 1.8 Incompatible with Windows XP, hotfix published</span></span>

<span data-ttu-id="258c4-113">NuGet 1.8 のリリース後すぐ 1.8 の暗号化の変更が、Windows XP でユーザーを超えたことがわかりました。</span><span class="sxs-lookup"><span data-stu-id="258c4-113">Shortly after NuGet 1.8 was released, we learned that a cryptography change in 1.8 broke users on Windows XP.</span></span>

<span data-ttu-id="258c4-114">この問題に対処する修正プログラムをリリースしたためです。</span><span class="sxs-lookup"><span data-stu-id="258c4-114">We have since released a hotfix that addresses this issue.</span></span>  <span data-ttu-id="258c4-115">NuGet Visual Studio 拡張機能ギャラリーを更新することでは、この修正プログラムを受信します。</span><span class="sxs-lookup"><span data-stu-id="258c4-115">By updating NuGet through the Visual Studio Extension Gallery, you receive this hotfix.</span></span>

## <a name="features"></a><span data-ttu-id="258c4-116">フィーチャー</span><span class="sxs-lookup"><span data-stu-id="258c4-116">Features</span></span>

### <a name="satellite-packages-for-localized-resources"></a><span data-ttu-id="258c4-117">ローカライズされたリソース用サテライト パッケージ</span><span class="sxs-lookup"><span data-stu-id="258c4-117">Satellite Packages for Localized Resources</span></span>
<span data-ttu-id="258c4-118">NuGet 1.8 には、.NET Framework のサテライト アセンブリの機能に似ています、ローカライズされたリソースに対して別々 のパッケージを作成する機能がサポートされました。</span><span class="sxs-lookup"><span data-stu-id="258c4-118">NuGet 1.8 now supports the ability to create separate packages for localized resources, similar to the satellite assembly capabilities of the .NET Framework.</span></span>  <span data-ttu-id="258c4-119">サテライト パッケージは、いくつかの規則を追加すると、他の NuGet パッケージと同じ方法で作成されます。</span><span class="sxs-lookup"><span data-stu-id="258c4-119">A satellite package is created in the same way as any other NuGet package with the addition of a few conventions:</span></span>

* <span data-ttu-id="258c4-120">サテライトのパッケージ ID とファイル名は、標準のいずれかに一致するサフィックスを含める必要があります[、.NET Framework で使用される文字列のカルチャ](http://msdn.microsoft.com/goglobal/bb896001.aspx)です。</span><span class="sxs-lookup"><span data-stu-id="258c4-120">The satellite package ID and file name should include a suffix that matches one of the standard [culture strings used by the .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).</span></span>
* <span data-ttu-id="258c4-121">その`.nuspec`ファイル、サテライト パッケージする必要がありますを定義する言語要素 ID で使用されている同じカルチャ文字列</span><span class="sxs-lookup"><span data-stu-id="258c4-121">In its `.nuspec` file, the satellite package should define a language element with the same culture string used in the ID</span></span>
* <span data-ttu-id="258c4-122">サテライト パッケージ内の依存関係を定義する必要があります、`.nuspec`言語サフィックス マイナス同じ ID を持つパッケージだけでは、そのコア パッケージにファイル。</span><span class="sxs-lookup"><span data-stu-id="258c4-122">The satellite package should define a dependency in its `.nuspec` file to its core package, which is simply the package with the same ID minus the language suffix.</span></span>  <span data-ttu-id="258c4-123">コア パッケージでは、インストールの成功のリポジトリで使用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="258c4-123">The core package needs to be available in the repository for successful installation.</span></span>

<span data-ttu-id="258c4-124">パッケージをインストールするには、ローカライズされたリソースで、開発者は明示的にリポジトリからローカライズされたパッケージを選択します。</span><span class="sxs-lookup"><span data-stu-id="258c4-124">To install a package with localized resources, a developer explicitly selects the localized package from the repository.</span></span> <span data-ttu-id="258c4-125">現時点では、NuGet ギャラリーにサテライト パッケージへの特別な処理の任意の種類は許可されません。</span><span class="sxs-lookup"><span data-stu-id="258c4-125">At present, the NuGet gallery does not give any kind of special treatment to satellite packages.</span></span>

![ローカライズされたパッケージとパッケージ マネージャー ダイアログ](./media/dlg-w-loc-packs.png)

<span data-ttu-id="258c4-127">サテライト パッケージ一覧のコア パッケージに依存関係があるので、サテライトとコア パッケージの NuGet パッケージ フォルダーに取り込まれたされインストールされます。</span><span class="sxs-lookup"><span data-stu-id="258c4-127">Because the satellite package lists a dependency to its core package, both the satellite and core packages are pulled into the NuGet packages folder and installed.</span></span>

![ローカライズ版パッケージとパッケージ フォルダー](./media/fldr-loc-packs.png)

<span data-ttu-id="258c4-129">さらに、サテライト パッケージのインストール中に、NuGet はカルチャ文字列の名前付け規則にも認識され、ローカライズされたリソース アセンブリ、.NET Framework で選択できるようにコア パッケージ内で適切なサブフォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="258c4-129">Additionally, while installing the satellite package, NuGet also recognizes the culture string naming convention and then copies the localized resource assembly into the correct subfolder within the core package so that it can be picked by the .NET Framework.</span></span>

![コア パッケージ フォルダーをコピーしたリソースのフォルダーと](./media/fldr-copied-loc.png)

<span data-ttu-id="258c4-131">サテライト パッケージに注意して 1 つの既存のバグは NuGet では、ローカライズされたリソースにはコピーされません、 `bin` Web サイト プロジェクトのフォルダーです。</span><span class="sxs-lookup"><span data-stu-id="258c4-131">One existing bug to note with satellite packages is that NuGet does not copy localized resources to the `bin` folder for Web site projects.</span></span>  <span data-ttu-id="258c4-132">この問題は、NuGet の次のリリースで修正されます。</span><span class="sxs-lookup"><span data-stu-id="258c4-132">This issue will be fixed in the next release of NuGet.</span></span>

<span data-ttu-id="258c4-133">完全なサンプルを作成し、サテライト パッケージを使用する方法を示す、次を参照してください。 [ https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample)です。</span><span class="sxs-lookup"><span data-stu-id="258c4-133">For a complete sample demonstrating how to create and use satellite packages, see [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).</span></span>

### <a name="package-restore-consent"></a><span data-ttu-id="258c4-134">パッケージの復元の同意</span><span class="sxs-lookup"><span data-stu-id="258c4-134">Package Restore Consent</span></span>
<span data-ttu-id="258c4-135">NuGet 1.8 は、ユーザーのプライバシーを保護するパッケージの復元での重要な制約をサポートするための基礎が配置されます。</span><span class="sxs-lookup"><span data-stu-id="258c4-135">In NuGet 1.8, we laid the groundwork for supporting an important constraint on package restore to protect user privacy.</span></span> <span data-ttu-id="258c4-136">この制約は、プロジェクトおよびパッケージの復元に明示的に同意するパッケージの復元を使用しているソリューションを構築する開発者のオンラインへの移行を構成済みのパッケージ ソースからパッケージをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="258c4-136">This constraint requires developers building projects and solutions that are using package restore to explicitly consent to package restore’s going online to download packages from configured package sources.</span></span>

<span data-ttu-id="258c4-137">この同意を提供する 2 つの方法はあります。</span><span class="sxs-lookup"><span data-stu-id="258c4-137">There are 2 ways to provide this consent.</span></span> <span data-ttu-id="258c4-138">最初は、次のように、パッケージ マネージャーの構成ダイアログで確認できます。</span><span class="sxs-lookup"><span data-stu-id="258c4-138">The first can be found in the package manager configuration dialog as shown below.</span></span>  <span data-ttu-id="258c4-139">このメソッドは、主に、開発者のマシンのものです。</span><span class="sxs-lookup"><span data-stu-id="258c4-139">This method is primarily intended for developer machines.</span></span>

![パッケージ マネージャーの構成 ダイアログ](./media/pr-consent-configdlg.png)

<span data-ttu-id="258c4-141">2 番目のメソッドでは、環境変数"EnableNuGetPackageRestore"を値"true"に設定します。</span><span class="sxs-lookup"><span data-stu-id="258c4-141">The second method is to set the environment variable “EnableNuGetPackageRestore” to the value “true”.</span></span>  <span data-ttu-id="258c4-142">このメソッドは CI またはビルド サーバーなどの無人のコンピューターものです。</span><span class="sxs-lookup"><span data-stu-id="258c4-142">This method is intended for unattended machines such as CI or build servers.</span></span>

<span data-ttu-id="258c4-143">ここで、前述のように、おがのみの基礎この機能を NuGet 1.8 でします。</span><span class="sxs-lookup"><span data-stu-id="258c4-143">Now, as stated above, we have only laid the groundwork for this feature in NuGet 1.8.</span></span>  <span data-ttu-id="258c4-144">実際には、すべての機能を有効にロジックを追加したときが現在強制されているこのバージョンでこれを意味します。</span><span class="sxs-lookup"><span data-stu-id="258c4-144">Practically, this means that while we’ve added all of the logic to enable the feature, it's not currently enforced in this version.</span></span> <span data-ttu-id="258c4-145">有効になります、ただし、次のリリースようにすることを認識できるだけ早く、環境を適切に構成することができ、したがっては影響を受けませんが開始したかったため、NuGet の制約を適用する同意します。</span><span class="sxs-lookup"><span data-stu-id="258c4-145">It will be enabled, however, in the next release of NuGet, so we wanted to make you aware of it as soon as possible so that you can configure your environments appropriately and therefore not be impacted when we start enforce the consent constraint.</span></span>

<span data-ttu-id="258c4-146">詳細についてを参照してください、[チームのブログの投稿](http://blog.nuget.org/20120518/package-restore-and-consent.html)この機能にします。</span><span class="sxs-lookup"><span data-stu-id="258c4-146">For more details, please see the [team blog post](http://blog.nuget.org/20120518/package-restore-and-consent.html) on this feature.</span></span>

### <a name="nugetexe-performance-improvements"></a><span data-ttu-id="258c4-147">nuget.exe パフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="258c4-147">nuget.exe Performance Improvements</span></span>
<span data-ttu-id="258c4-148">ダウンロードして、パッケージを並列でインストールするインストール コマンドを変更すると、NuGet 1.8 は nuget.exe – へと拡張機能パッケージの復元によって大幅なパフォーマンスの向上が表示されます。</span><span class="sxs-lookup"><span data-stu-id="258c4-148">By modifying the install command to download and install packages in parallel, NuGet 1.8 brings dramatic performance improvements to nuget.exe – and by extension package restore.</span></span>  <span data-ttu-id="258c4-149">高レベルのテストは、NuGet 1.8 の約 35 %6 パッケージをプロジェクトにインストールするためのパフォーマンスを向上することを示します。</span><span class="sxs-lookup"><span data-stu-id="258c4-149">High level testing shows that performance for installing 6 packages into a project improves by about 35% in NuGet 1.8.</span></span>  <span data-ttu-id="258c4-150">25 へのパッケージの数を増やすことを示しています約 60% のパフォーマンスが向上します。</span><span class="sxs-lookup"><span data-stu-id="258c4-150">Increasing the number of packages to 25 shows a performance gain of about 60%.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="258c4-151">バグ修正</span><span class="sxs-lookup"><span data-stu-id="258c4-151">Bug Fixes</span></span>
<span data-ttu-id="258c4-152">NuGet 1.8 には、パッケージの復元の同意画面および Windows 8 の Express の統合に関連するように特にパッケージ マネージャー コンソールとパッケージの復元のワークフローに重点を置いて、かなり多くのバグ修正が含まれています。</span><span class="sxs-lookup"><span data-stu-id="258c4-152">NuGet 1.8 includes quite a few bug fixes with an emphasis on the package manager console and package restore workflow, particularly as it relates to package restore consent and Windows 8 Express integration.</span></span>
<span data-ttu-id="258c4-153">作業の完全な一覧の項目で修正 NuGet 1.8 くださいビュー、[今回のリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)です。</span><span class="sxs-lookup"><span data-stu-id="258c4-153">For a full list of work items fixed in NuGet 1.8, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
