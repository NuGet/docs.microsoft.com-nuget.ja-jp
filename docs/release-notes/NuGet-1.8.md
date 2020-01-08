---
title: NuGet 1.8 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 1.8 のリリースノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 973a2d010cb75eeeb383be94baf2fb17a999dd7c
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383462"
---
# <a name="nuget-18-release-notes"></a><span data-ttu-id="0c40b-103">NuGet 1.8 リリースノート</span><span class="sxs-lookup"><span data-stu-id="0c40b-103">NuGet 1.8 Release Notes</span></span>

<span data-ttu-id="0c40b-104">Nuget [1.7 リリースノート](../release-notes/nuget-1.7.md) | [Nuget 2.0 リリースノート](../release-notes/nuget-2.0.md)</span><span class="sxs-lookup"><span data-stu-id="0c40b-104">[NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md) | [NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md)</span></span>

<span data-ttu-id="0c40b-105">NuGet 1.8 は、2012年5月23日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="0c40b-105">NuGet 1.8 was released on May 23, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="0c40b-106">インストールに関する既知の問題</span><span class="sxs-lookup"><span data-stu-id="0c40b-106">Known Installation Issue</span></span>
<span data-ttu-id="0c40b-107">VS 2010 SP1 を実行している場合は、以前のバージョンがインストールされている場合に NuGet をアップグレードしようとすると、インストールエラーが発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="0c40b-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="0c40b-108">この回避策は、単純に NuGet をアンインストールし、VS 拡張機能ギャラリーからインストールすることです。</span><span class="sxs-lookup"><span data-stu-id="0c40b-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="0c40b-109">詳細については、「<https://support.microsoft.com/kb/2581019>」を参照するか、 [VS 修正プログラムに直接アクセス](http://bit.ly/vsixcertfix)してください。</span><span class="sxs-lookup"><span data-stu-id="0c40b-109">See <https://support.microsoft.com/kb/2581019> for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="0c40b-110">注: Visual Studio で拡張機能をアンインストールできない場合 ([アンインストール] ボタンが無効になっている場合)、"管理者として実行" を使用して Visual Studio を再起動する必要が生じる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0c40b-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a><span data-ttu-id="0c40b-111">NuGet 1.8 は Windows XP と互換性がありません。修正プログラムが公開されました</span><span class="sxs-lookup"><span data-stu-id="0c40b-111">NuGet 1.8 Incompatible with Windows XP, hotfix published</span></span>

<span data-ttu-id="0c40b-112">NuGet 1.8 がリリースされた直後、1.8 での暗号化の変更が Windows XP でユーザーによって中断されたことがわかりました。</span><span class="sxs-lookup"><span data-stu-id="0c40b-112">Shortly after NuGet 1.8 was released, we learned that a cryptography change in 1.8 broke users on Windows XP.</span></span>

<span data-ttu-id="0c40b-113">この問題に対処する修正プログラムがリリースされました。</span><span class="sxs-lookup"><span data-stu-id="0c40b-113">We have since released a hotfix that addresses this issue.</span></span>  <span data-ttu-id="0c40b-114">Visual Studio 拡張機能ギャラリーから NuGet を更新すると、この修正プログラムが提供されます。</span><span class="sxs-lookup"><span data-stu-id="0c40b-114">By updating NuGet through the Visual Studio Extension Gallery, you receive this hotfix.</span></span>

## <a name="features"></a><span data-ttu-id="0c40b-115">フィーチャー</span><span class="sxs-lookup"><span data-stu-id="0c40b-115">Features</span></span>

### <a name="satellite-packages-for-localized-resources"></a><span data-ttu-id="0c40b-116">ローカライズされたリソースのサテライトパッケージ</span><span class="sxs-lookup"><span data-stu-id="0c40b-116">Satellite Packages for Localized Resources</span></span>
<span data-ttu-id="0c40b-117">NuGet 1.8 では、.NET Framework のサテライトアセンブリ機能と同様に、ローカライズされたリソース用に個別のパッケージを作成する機能がサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="0c40b-117">NuGet 1.8 now supports the ability to create separate packages for localized resources, similar to the satellite assembly capabilities of the .NET Framework.</span></span>  <span data-ttu-id="0c40b-118">サテライトパッケージは、他の NuGet パッケージと同じように、いくつかの規則を追加して作成されます。</span><span class="sxs-lookup"><span data-stu-id="0c40b-118">A satellite package is created in the same way as any other NuGet package with the addition of a few conventions:</span></span>

* <span data-ttu-id="0c40b-119">サテライトパッケージ ID とファイル名には、 [.NET Framework によって使用される標準カルチャ文字列](https://docs.microsoft.com/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)の1つに一致するサフィックスを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c40b-119">The satellite package ID and file name should include a suffix that matches one of the standard [culture strings used by the .NET Framework](https://docs.microsoft.com/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).</span></span>
* <span data-ttu-id="0c40b-120">この `.nuspec` ファイルでは、サテライトパッケージは、ID で使用されているものと同じカルチャ文字列を持つ言語要素を定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c40b-120">In its `.nuspec` file, the satellite package should define a language element with the same culture string used in the ID</span></span>
* <span data-ttu-id="0c40b-121">サテライトパッケージでは、その `.nuspec` ファイル内の依存関係をそのコアパッケージに定義する必要があります。これは、単に同じ ID を持つパッケージを言語サフィックスから引いたものです。</span><span class="sxs-lookup"><span data-stu-id="0c40b-121">The satellite package should define a dependency in its `.nuspec` file to its core package, which is simply the package with the same ID minus the language suffix.</span></span>  <span data-ttu-id="0c40b-122">インストールを成功させるには、コアパッケージがリポジトリで使用可能である必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c40b-122">The core package needs to be available in the repository for successful installation.</span></span>

<span data-ttu-id="0c40b-123">ローカライズされたリソースを含むパッケージをインストールするには、開発者がリポジトリからローカライズされたパッケージを明示的に選択します。</span><span class="sxs-lookup"><span data-stu-id="0c40b-123">To install a package with localized resources, a developer explicitly selects the localized package from the repository.</span></span> <span data-ttu-id="0c40b-124">現時点では、NuGet ギャラリーでは、サテライトパッケージに特別な処理は一切提供されません。</span><span class="sxs-lookup"><span data-stu-id="0c40b-124">At present, the NuGet gallery does not give any kind of special treatment to satellite packages.</span></span>

![ローカライズされたパッケージを含むパッケージマネージャーダイアログ](./media/dlg-w-loc-packs.png)

<span data-ttu-id="0c40b-126">サテライトパッケージはコアパッケージへの依存関係を一覧表示するため、サテライトパッケージとコアパッケージの両方が NuGet パッケージフォルダーに取り込まれ、インストールされます。</span><span class="sxs-lookup"><span data-stu-id="0c40b-126">Because the satellite package lists a dependency to its core package, both the satellite and core packages are pulled into the NuGet packages folder and installed.</span></span>

![ローカライズされたパッケージを含むパッケージフォルダー](./media/fldr-loc-packs.png)

<span data-ttu-id="0c40b-128">さらに、サテライトパッケージをインストールするときに、NuGet はカルチャ文字列の名前付け規則も認識して、ローカライズされたリソースアセンブリをコアパッケージ内の適切なサブフォルダーにコピーして、.NET Framework で選択できるようにします。</span><span class="sxs-lookup"><span data-stu-id="0c40b-128">Additionally, while installing the satellite package, NuGet also recognizes the culture string naming convention and then copies the localized resource assembly into the correct subfolder within the core package so that it can be picked by the .NET Framework.</span></span>

![リソースフォルダーがコピーされたコアパッケージフォルダー](./media/fldr-copied-loc.png)

<span data-ttu-id="0c40b-130">サテライトパッケージでメモする既存のバグの1つは、NuGet が Web サイトプロジェクトの `bin` フォルダーにローカライズされたリソースをコピーしないことです。</span><span class="sxs-lookup"><span data-stu-id="0c40b-130">One existing bug to note with satellite packages is that NuGet does not copy localized resources to the `bin` folder for Web site projects.</span></span>  <span data-ttu-id="0c40b-131">この問題は、NuGet の次のリリースで修正される予定です。</span><span class="sxs-lookup"><span data-stu-id="0c40b-131">This issue will be fixed in the next release of NuGet.</span></span>

<span data-ttu-id="0c40b-132">サテライトパッケージを作成して使用する方法を示す完全なサンプルについては、「 [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0c40b-132">For a complete sample demonstrating how to create and use satellite packages, see [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).</span></span>

### <a name="package-restore-consent"></a><span data-ttu-id="0c40b-133">パッケージの復元の同意</span><span class="sxs-lookup"><span data-stu-id="0c40b-133">Package Restore Consent</span></span>
<span data-ttu-id="0c40b-134">NuGet 1.8 では、ユーザーのプライバシーを保護するために、パッケージの復元に関する重要な制約をサポートするための基礎を説明しています。</span><span class="sxs-lookup"><span data-stu-id="0c40b-134">In NuGet 1.8, we laid the groundwork for supporting an important constraint on package restore to protect user privacy.</span></span> <span data-ttu-id="0c40b-135">この制約には、パッケージの復元をオンラインにして、構成されたパッケージソースからパッケージをダウンロードすることに明示的に同意するために、パッケージの復元を使用するプロジェクトとソリューションを作成する開発者が必要です。</span><span class="sxs-lookup"><span data-stu-id="0c40b-135">This constraint requires developers building projects and solutions that are using package restore to explicitly consent to package restore’s going online to download packages from configured package sources.</span></span>

<span data-ttu-id="0c40b-136">この同意を提供するには2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="0c40b-136">There are 2 ways to provide this consent.</span></span> <span data-ttu-id="0c40b-137">最初の例は、次に示すように、[パッケージマネージャーの構成] ダイアログボックスにあります。</span><span class="sxs-lookup"><span data-stu-id="0c40b-137">The first can be found in the package manager configuration dialog as shown below.</span></span>  <span data-ttu-id="0c40b-138">このメソッドは、主に開発者用のコンピューターを対象としています。</span><span class="sxs-lookup"><span data-stu-id="0c40b-138">This method is primarily intended for developer machines.</span></span>

![パッケージマネージャーの構成ダイアログ](./media/pr-consent-configdlg.png)

<span data-ttu-id="0c40b-140">2つ目の方法では、環境変数 "EnableNuGetPackageRestore" を値 "true" に設定します。</span><span class="sxs-lookup"><span data-stu-id="0c40b-140">The second method is to set the environment variable “EnableNuGetPackageRestore” to the value “true”.</span></span>  <span data-ttu-id="0c40b-141">この方法は、CI やビルドサーバーなどの無人マシンを対象としています。</span><span class="sxs-lookup"><span data-stu-id="0c40b-141">This method is intended for unattended machines such as CI or build servers.</span></span>

<span data-ttu-id="0c40b-142">前述のように、この機能の基礎については、NuGet 1.8 で説明しました。</span><span class="sxs-lookup"><span data-stu-id="0c40b-142">Now, as stated above, we have only laid the groundwork for this feature in NuGet 1.8.</span></span>  <span data-ttu-id="0c40b-143">実際には、この機能を有効にするためにすべてのロジックを追加している間は、このバージョンでは現在適用されていません。</span><span class="sxs-lookup"><span data-stu-id="0c40b-143">Practically, this means that while we’ve added all of the logic to enable the feature, it's not currently enforced in this version.</span></span> <span data-ttu-id="0c40b-144">ただし、NuGet の次のリリースで有効になります。そのため、環境を適切に構成し、同意制約の適用を開始したときに影響を受けることがないように、できるだけ早くそのことを認識する必要がありました。</span><span class="sxs-lookup"><span data-stu-id="0c40b-144">It will be enabled, however, in the next release of NuGet, so we wanted to make you aware of it as soon as possible so that you can configure your environments appropriately and therefore not be impacted when we start enforce the consent constraint.</span></span>

<span data-ttu-id="0c40b-145">詳細については、この機能に関する[チームのブログ投稿](http://blog.nuget.org/20120518/package-restore-and-consent.html)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0c40b-145">For more details, please see the [team blog post](http://blog.nuget.org/20120518/package-restore-and-consent.html) on this feature.</span></span>

### <a name="nugetexe-performance-improvements"></a><span data-ttu-id="0c40b-146">nuget.exe のパフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="0c40b-146">nuget.exe Performance Improvements</span></span>
<span data-ttu-id="0c40b-147">パッケージを並列でダウンロードしてインストールするように install コマンドを変更することで、nuget 1.8 では、nuget と拡張機能パッケージの復元によって大幅なパフォーマンスが向上します。</span><span class="sxs-lookup"><span data-stu-id="0c40b-147">By modifying the install command to download and install packages in parallel, NuGet 1.8 brings dramatic performance improvements to nuget.exe – and by extension package restore.</span></span>  <span data-ttu-id="0c40b-148">高レベルのテストでは、6つのパッケージをプロジェクトにインストールする場合のパフォーマンスが NuGet 1.8 で約35% 向上しています。</span><span class="sxs-lookup"><span data-stu-id="0c40b-148">High level testing shows that performance for installing 6 packages into a project improves by about 35% in NuGet 1.8.</span></span>  <span data-ttu-id="0c40b-149">パッケージの数を25に増やすと、約60% のパフォーマンスが向上します。</span><span class="sxs-lookup"><span data-stu-id="0c40b-149">Increasing the number of packages to 25 shows a performance gain of about 60%.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="0c40b-150">バグ修正</span><span class="sxs-lookup"><span data-stu-id="0c40b-150">Bug Fixes</span></span>
<span data-ttu-id="0c40b-151">NuGet 1.8 では、パッケージマネージャーコンソールとパッケージ復元ワークフローに重点を置いて、いくつかのバグ修正が行われています。特に、パッケージ復元の同意と Windows 8 Express の統合に関連しています。</span><span class="sxs-lookup"><span data-stu-id="0c40b-151">NuGet 1.8 includes quite a few bug fixes with an emphasis on the package manager console and package restore workflow, particularly as it relates to package restore consent and Windows 8 Express integration.</span></span>
<span data-ttu-id="0c40b-152">NuGet 1.8 で修正された作業項目の完全な一覧については、[このリリースの Nuget Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0c40b-152">For a full list of work items fixed in NuGet 1.8, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
