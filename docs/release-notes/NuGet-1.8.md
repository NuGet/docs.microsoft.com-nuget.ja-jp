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
# <a name="nuget-18-release-notes"></a><span data-ttu-id="0314a-103">NuGet 1.8 のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="0314a-103">NuGet 1.8 Release Notes</span></span>

<span data-ttu-id="0314a-104">[NuGet 1.7 のリリース ノート](../release-notes/nuget-1.7.md) | [NuGet 2.0 のリリース ノート](../release-notes/nuget-2.0.md)</span><span class="sxs-lookup"><span data-stu-id="0314a-104">[NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md) | [NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md)</span></span>

<span data-ttu-id="0314a-105">NuGet 1.8 は、2012 年 5 月 23 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="0314a-105">NuGet 1.8 was released on May 23, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="0314a-106">インストールの既知の問題</span><span class="sxs-lookup"><span data-stu-id="0314a-106">Known Installation Issue</span></span>
<span data-ttu-id="0314a-107">VS 2010 SP1 を実行している場合は、インストールされている以前のバージョンがある場合は、NuGet をアップグレードしようとしています。 インストール エラーが発生実行可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0314a-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="0314a-108">回避策では、単に NuGet をアンインストールしてから、VS 拡張ギャラリーからインストールします。</span><span class="sxs-lookup"><span data-stu-id="0314a-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="0314a-109">参照してください[ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019)詳細については、または[VS 修正プログラムに直接移動](http://bit.ly/vsixcertfix)します。</span><span class="sxs-lookup"><span data-stu-id="0314a-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="0314a-110">注: Visual Studio ([アンインストール] ボタンは無効です) 拡張機能をアンインストールすることができず、しの場合必要があります「管理者として実行」を使用して Visual Studio を再起動するには</span><span class="sxs-lookup"><span data-stu-id="0314a-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a><span data-ttu-id="0314a-111">NuGet 1.8 と互換性のない Windows XP では、修正プログラムの発行</span><span class="sxs-lookup"><span data-stu-id="0314a-111">NuGet 1.8 Incompatible with Windows XP, hotfix published</span></span>

<span data-ttu-id="0314a-112">NuGet 1.8 がリリースされた後すぐ、1.8 の暗号化の変更が Windows XP でユーザーを解約することがわかりました。</span><span class="sxs-lookup"><span data-stu-id="0314a-112">Shortly after NuGet 1.8 was released, we learned that a cryptography change in 1.8 broke users on Windows XP.</span></span>

<span data-ttu-id="0314a-113">この問題に対処する修正プログラムをリリースしましたので。</span><span class="sxs-lookup"><span data-stu-id="0314a-113">We have since released a hotfix that addresses this issue.</span></span>  <span data-ttu-id="0314a-114">Visual Studio の拡張機能ギャラリーから NuGet を更新することでは、この修正プログラムが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0314a-114">By updating NuGet through the Visual Studio Extension Gallery, you receive this hotfix.</span></span>

## <a name="features"></a><span data-ttu-id="0314a-115">フィーチャー</span><span class="sxs-lookup"><span data-stu-id="0314a-115">Features</span></span>

### <a name="satellite-packages-for-localized-resources"></a><span data-ttu-id="0314a-116">ローカライズされたリソースのサテライト パッケージ</span><span class="sxs-lookup"><span data-stu-id="0314a-116">Satellite Packages for Localized Resources</span></span>
<span data-ttu-id="0314a-117">NuGet 1.8 で .NET Framework のサテライト アセンブリの機能に似ています、ローカライズされたリソースの個別のパッケージを作成できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="0314a-117">NuGet 1.8 now supports the ability to create separate packages for localized resources, similar to the satellite assembly capabilities of the .NET Framework.</span></span>  <span data-ttu-id="0314a-118">サテライト パッケージは、いくつかの規則を追加すると、他の NuGet パッケージと同じ方法で作成されます。</span><span class="sxs-lookup"><span data-stu-id="0314a-118">A satellite package is created in the same way as any other NuGet package with the addition of a few conventions:</span></span>

* <span data-ttu-id="0314a-119">サテライトのパッケージ ID とファイル名は、標準のいずれかに一致するサフィックスを含める必要があります[、.NET Framework で使用される文字列のカルチャ](http://msdn.microsoft.com/goglobal/bb896001.aspx)します。</span><span class="sxs-lookup"><span data-stu-id="0314a-119">The satellite package ID and file name should include a suffix that matches one of the standard [culture strings used by the .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).</span></span>
* <span data-ttu-id="0314a-120">その`.nuspec`ファイル、サテライト パッケージする必要があります定義言語要素を ID で使用されている同じカルチャ文字列</span><span class="sxs-lookup"><span data-stu-id="0314a-120">In its `.nuspec` file, the satellite package should define a language element with the same culture string used in the ID</span></span>
* <span data-ttu-id="0314a-121">サテライト パッケージの依存関係を定義する必要があります、`.nuspec`ファイルをそのコア パッケージに言語サフィックスを差し引いた同じ ID を持つパッケージだけです。</span><span class="sxs-lookup"><span data-stu-id="0314a-121">The satellite package should define a dependency in its `.nuspec` file to its core package, which is simply the package with the same ID minus the language suffix.</span></span>  <span data-ttu-id="0314a-122">コア パッケージは、インストールの成功のリポジトリで利用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="0314a-122">The core package needs to be available in the repository for successful installation.</span></span>

<span data-ttu-id="0314a-123">でローカライズされたリソースを、パッケージをインストールするには、開発者は、リポジトリからローカライズされたパッケージを明示的に選択します。</span><span class="sxs-lookup"><span data-stu-id="0314a-123">To install a package with localized resources, a developer explicitly selects the localized package from the repository.</span></span> <span data-ttu-id="0314a-124">現時点では、NuGet ギャラリーでは任意の種類の特別な処理をサテライト パッケージは提供されません。</span><span class="sxs-lookup"><span data-stu-id="0314a-124">At present, the NuGet gallery does not give any kind of special treatment to satellite packages.</span></span>

![ローカライズされたパッケージとパッケージ マネージャー ダイアログ](./media/dlg-w-loc-packs.png)

<span data-ttu-id="0314a-126">サテライト パッケージは、そのコア パッケージに依存関係を一覧表示、ため、サテライトとコアの両方のパッケージは NuGet パッケージ フォルダーに取り込むし、インストールされています。</span><span class="sxs-lookup"><span data-stu-id="0314a-126">Because the satellite package lists a dependency to its core package, both the satellite and core packages are pulled into the NuGet packages folder and installed.</span></span>

![ローカライズされたパッケージのパッケージ フォルダー](./media/fldr-loc-packs.png)

<span data-ttu-id="0314a-128">さらに、サテライト パッケージをインストールするときに、NuGet もカルチャ文字列の名前付け規則を認識し、ローカライズされたリソース アセンブリには、.NET Framework で選択できるように、コア パッケージ内で適切なサブフォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="0314a-128">Additionally, while installing the satellite package, NuGet also recognizes the culture string naming convention and then copies the localized resource assembly into the correct subfolder within the core package so that it can be picked by the .NET Framework.</span></span>

![コピーしたリソースのフォルダーとコア パッケージ フォルダー](./media/fldr-copied-loc.png)

<span data-ttu-id="0314a-130">サテライト パッケージに注意してください。 1 つの既存のバグは NuGet では、ローカライズされたリソースはコピーされません、 `bin` Web サイト プロジェクトのフォルダー。</span><span class="sxs-lookup"><span data-stu-id="0314a-130">One existing bug to note with satellite packages is that NuGet does not copy localized resources to the `bin` folder for Web site projects.</span></span>  <span data-ttu-id="0314a-131">この問題は、次の NuGet のリリースで修正されます。</span><span class="sxs-lookup"><span data-stu-id="0314a-131">This issue will be fixed in the next release of NuGet.</span></span>

<span data-ttu-id="0314a-132">作成し、サテライト パッケージを使用する方法を示す完全なサンプルを参照してください。 [ https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample)します。</span><span class="sxs-lookup"><span data-stu-id="0314a-132">For a complete sample demonstrating how to create and use satellite packages, see [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).</span></span>

### <a name="package-restore-consent"></a><span data-ttu-id="0314a-133">パッケージの復元の同意</span><span class="sxs-lookup"><span data-stu-id="0314a-133">Package Restore Consent</span></span>
<span data-ttu-id="0314a-134">NuGet 1.8 は、ユーザーのプライバシーを保護するパッケージの復元での重要な制約をサポートするための土台を配置します。</span><span class="sxs-lookup"><span data-stu-id="0314a-134">In NuGet 1.8, we laid the groundwork for supporting an important constraint on package restore to protect user privacy.</span></span> <span data-ttu-id="0314a-135">この制約は、プロジェクトとパッケージの復元に明示的に同意するパッケージの復元を使用しているソリューションを構築する開発者が構成済みのパッケージ ソースからパッケージをダウンロードするオンラインの移動が必要です。</span><span class="sxs-lookup"><span data-stu-id="0314a-135">This constraint requires developers building projects and solutions that are using package restore to explicitly consent to package restore’s going online to download packages from configured package sources.</span></span>

<span data-ttu-id="0314a-136">この同意を提供する 2 つの方法はあります。</span><span class="sxs-lookup"><span data-stu-id="0314a-136">There are 2 ways to provide this consent.</span></span> <span data-ttu-id="0314a-137">1 つ目は、次に示すように、パッケージ マネージャーの構成ダイアログで確認できます。</span><span class="sxs-lookup"><span data-stu-id="0314a-137">The first can be found in the package manager configuration dialog as shown below.</span></span>  <span data-ttu-id="0314a-138">このメソッドは主に、開発者のコンピューターのものです。</span><span class="sxs-lookup"><span data-stu-id="0314a-138">This method is primarily intended for developer machines.</span></span>

![パッケージ マネージャーの構成 ダイアログ](./media/pr-consent-configdlg.png)

<span data-ttu-id="0314a-140">2 番目のメソッドでは、環境変数"EnableNuGetPackageRestore"を値"true"に設定します。</span><span class="sxs-lookup"><span data-stu-id="0314a-140">The second method is to set the environment variable “EnableNuGetPackageRestore” to the value “true”.</span></span>  <span data-ttu-id="0314a-141">このメソッドは、CI ビルド サーバーなどの自動マシン向けです。</span><span class="sxs-lookup"><span data-stu-id="0314a-141">This method is intended for unattended machines such as CI or build servers.</span></span>

<span data-ttu-id="0314a-142">ここで、前述のようは、この機能を土台を NuGet 1.8 でに作り上げていますのみいます。</span><span class="sxs-lookup"><span data-stu-id="0314a-142">Now, as stated above, we have only laid the groundwork for this feature in NuGet 1.8.</span></span>  <span data-ttu-id="0314a-143">実際には、すべての機能を有効にロジックを追加したときに、現在強制されているこのバージョンでこれを意味します。</span><span class="sxs-lookup"><span data-stu-id="0314a-143">Practically, this means that while we’ve added all of the logic to enable the feature, it's not currently enforced in this version.</span></span> <span data-ttu-id="0314a-144">有効になります、ただし、次のリリースを利用することに注意してください、できるだけ早くお使いの環境を適切に構成することができますので影響を受けなくを起動したときと使用できるように、NuGet の制約を適用する同意します。</span><span class="sxs-lookup"><span data-stu-id="0314a-144">It will be enabled, however, in the next release of NuGet, so we wanted to make you aware of it as soon as possible so that you can configure your environments appropriately and therefore not be impacted when we start enforce the consent constraint.</span></span>

<span data-ttu-id="0314a-145">詳細についてを参照してください、[チームのブログの投稿](http://blog.nuget.org/20120518/package-restore-and-consent.html)この機能にします。</span><span class="sxs-lookup"><span data-stu-id="0314a-145">For more details, please see the [team blog post](http://blog.nuget.org/20120518/package-restore-and-consent.html) on this feature.</span></span>

### <a name="nugetexe-performance-improvements"></a><span data-ttu-id="0314a-146">nuget.exe のパフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="0314a-146">nuget.exe Performance Improvements</span></span>
<span data-ttu-id="0314a-147">ダウンロードしてパッケージを並列でインストールするインストール コマンドを変更すると、NuGet 1.8 は大幅なパフォーマンスの向上 – nuget.exe へと拡張機能パッケージの復元が表示されます。</span><span class="sxs-lookup"><span data-stu-id="0314a-147">By modifying the install command to download and install packages in parallel, NuGet 1.8 brings dramatic performance improvements to nuget.exe – and by extension package restore.</span></span>  <span data-ttu-id="0314a-148">高レベルのテストは、NuGet 1.8 で約 35% が 6 のパッケージをプロジェクトにインストールするためのパフォーマンスを向上することを示します。</span><span class="sxs-lookup"><span data-stu-id="0314a-148">High level testing shows that performance for installing 6 packages into a project improves by about 35% in NuGet 1.8.</span></span>  <span data-ttu-id="0314a-149">25 にパッケージの数を増やすには、約 60% のパフォーマンスの向上は示しています。</span><span class="sxs-lookup"><span data-stu-id="0314a-149">Increasing the number of packages to 25 shows a performance gain of about 60%.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="0314a-150">バグ修正</span><span class="sxs-lookup"><span data-stu-id="0314a-150">Bug Fixes</span></span>
<span data-ttu-id="0314a-151">NuGet 1.8 には、パッケージ復元の同意と Windows 8 の Express の統合に関連する、特にパッケージ マネージャー コンソールと、パッケージの復元ワークフローを重視した、かなり多くのバグ修正が含まれています。</span><span class="sxs-lookup"><span data-stu-id="0314a-151">NuGet 1.8 includes quite a few bug fixes with an emphasis on the package manager console and package restore workflow, particularly as it relates to package restore consent and Windows 8 Express integration.</span></span>
<span data-ttu-id="0314a-152">作業の完全な一覧の項目を修正しました NuGet 1.8 でくださいビュー、[このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)します。</span><span class="sxs-lookup"><span data-stu-id="0314a-152">For a full list of work items fixed in NuGet 1.8, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
