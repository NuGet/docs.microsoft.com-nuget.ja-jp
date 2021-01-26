---
title: NuGet 2.5 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.5 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: efcfb9767772c9e27372b4616f817656d51efed8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776859"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="671e9-103">NuGet 2.5 リリースノート</span><span class="sxs-lookup"><span data-stu-id="671e9-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="671e9-104">[NuGet 2.2.1 リリースノート](../release-notes/nuget-2.2.1.md)  | [NuGet 2.6 リリースノート](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="671e9-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="671e9-105">NuGet 2.5 は、2013年4月25日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="671e9-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="671e9-106">このリリースでは、バージョン2.3 と2.4 をスキップすることになりました。</span><span class="sxs-lookup"><span data-stu-id="671e9-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="671e9-107">これは、NuGet に関して私たちが経験した最大のリリースであり、 [160 の作業項目](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) がリリースに含まれています。</span><span class="sxs-lookup"><span data-stu-id="671e9-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="671e9-108">謝辞</span><span class="sxs-lookup"><span data-stu-id="671e9-108">Acknowledgements</span></span>

<span data-ttu-id="671e9-109">NuGet 2.5 への重要な貢献について、次の外部の共同作成者に感謝いたします。</span><span class="sxs-lookup"><span data-stu-id="671e9-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="671e9-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ( [@dsplaisted](https://twitter.com/dsplaisted) )</span><span class="sxs-lookup"><span data-stu-id="671e9-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="671e9-111">[#2847](https://nuget.codeplex.com/workitem/2847) -モノ Android、monotouch.dialog、およびモノ mac を既知のターゲットフレームワーク識別子の一覧に追加します。</span><span class="sxs-lookup"><span data-stu-id="671e9-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="671e9-112">[Andres Aragoneses](https://www.codeplex.com/site/users/view/knocte) ( [@knocte](https://twitter.com/knocte) )</span><span class="sxs-lookup"><span data-stu-id="671e9-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="671e9-113">[#2865](https://nuget.codeplex.com/workitem/2865) - `NuGet.targets` 大文字と小文字を区別する OS のスペル修正</span><span class="sxs-lookup"><span data-stu-id="671e9-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="671e9-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ( [@davidfowl](https://twitter.com/davidfowl) )</span><span class="sxs-lookup"><span data-stu-id="671e9-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="671e9-115">ソリューションを Mono で構築します。</span><span class="sxs-lookup"><span data-stu-id="671e9-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="671e9-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ( [@atheken](https://twitter.com/atheken) )</span><span class="sxs-lookup"><span data-stu-id="671e9-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="671e9-117">Mono で失敗する単体テストを修正します。</span><span class="sxs-lookup"><span data-stu-id="671e9-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="671e9-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ( [@OliIsCool](https://twitter.com/oliiscool) )</span><span class="sxs-lookup"><span data-stu-id="671e9-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="671e9-119">[#2920](https://nuget.codeplex.com/workitem/2920) nuget.exe パックのコマンドでは、プロパティが MSBuild に反映されません</span><span class="sxs-lookup"><span data-stu-id="671e9-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="671e9-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ( [@bajtos](https://twitter.com/bajtos) )</span><span class="sxs-lookup"><span data-stu-id="671e9-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="671e9-121">[#1511](https://nuget.codeplex.com/workitem/1511) -書式設定を保持するために変更された XML 処理コード。</span><span class="sxs-lookup"><span data-stu-id="671e9-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="671e9-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )</span><span class="sxs-lookup"><span data-stu-id="671e9-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="671e9-123">ビルド .cmd を成功させるために、認識された単語をカスタム辞書に追加しました。</span><span class="sxs-lookup"><span data-stu-id="671e9-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="671e9-124">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="671e9-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="671e9-125">ローカライズされたおよびでの実行時に単体テストを修正する</span><span class="sxs-lookup"><span data-stu-id="671e9-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="671e9-126">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="671e9-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="671e9-127">パッケージを展開する</span><span class="sxs-lookup"><span data-stu-id="671e9-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="671e9-128">最大活用[e Bridou](https://www.codeplex.com/site/users/view/brugidou) ( [@brugidou](https://twitter.com/brugidou) )</span><span class="sxs-lookup"><span data-stu-id="671e9-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="671e9-129">[#936](https://nuget.codeplex.com/workitem/936) -パッキング時にプロジェクトの依存関係を処理する</span><span class="sxs-lookup"><span data-stu-id="671e9-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="671e9-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ( [@XavierDecoster](https://twitter.com/xavierdecoster) )</span><span class="sxs-lookup"><span data-stu-id="671e9-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="671e9-131">[#2991](https://nuget.codeplex.com/workitem/2991)、 [#3164](https://nuget.codeplex.com/workitem/3164) 、パッケージソースの資格情報を nuget に保存するときにクリアテキストのパスワードをサポートします。 cofig</span><span class="sxs-lookup"><span data-stu-id="671e9-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="671e9-132">[James manning](http://www.codeplex.com/site/users/view/jmanning) [@manningj](https://twitter.com/manningj) )</span><span class="sxs-lookup"><span data-stu-id="671e9-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="671e9-133">[#3190](http://nuget.codeplex.com/workitem/3190)、 [#3191](http://nuget.codeplex.com/workitem/3191) 修正 Get-Package ヘルプの説明</span><span class="sxs-lookup"><span data-stu-id="671e9-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="671e9-134">また、次の各担当者は、最終リリースの前に承認および修正された NuGet 2.5 Beta/RC でバグを見つけることにも感謝します。</span><span class="sxs-lookup"><span data-stu-id="671e9-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="671e9-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ( [@CodeChief](https://twitter.com/codechief) )</span><span class="sxs-lookup"><span data-stu-id="671e9-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="671e9-136">[#3200](https://nuget.codeplex.com/workitem/3200) -MSTest が最新 NuGet 2.4 および2.5 ビルドで破損する</span><span class="sxs-lookup"><span data-stu-id="671e9-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="671e9-137">リリースの注目すべき機能</span><span class="sxs-lookup"><span data-stu-id="671e9-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="671e9-138">既に存在するコンテンツファイルをユーザーが上書きできるようにする</span><span class="sxs-lookup"><span data-stu-id="671e9-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="671e9-139">常に要求される機能の1つは、NuGet パッケージに含まれている場合に、既にディスク上に存在するコンテンツファイルを上書きする機能です。</span><span class="sxs-lookup"><span data-stu-id="671e9-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="671e9-140">NuGet 2.5 以降では、これらの競合が特定され、ファイルを上書きするように求められますが、以前はこれらのファイルは常にスキップされていました。</span><span class="sxs-lookup"><span data-stu-id="671e9-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![コンテンツファイルの上書き](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="671e9-142">' nuget.exe update ' と ' FileConflictAction ' の両方に、コマンドラインシナリオに既定値を設定する新しいオプション '-' が追加されました。</span><span class="sxs-lookup"><span data-stu-id="671e9-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="671e9-143">ターゲットプロジェクトにパッケージのファイルが既に存在する場合の既定のアクションを設定します。</span><span class="sxs-lookup"><span data-stu-id="671e9-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="671e9-144">常にファイルを上書きするには、[上書き] に設定します。</span><span class="sxs-lookup"><span data-stu-id="671e9-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="671e9-145">ファイルをスキップするには、[無視] に設定します。</span><span class="sxs-lookup"><span data-stu-id="671e9-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="671e9-146">指定しない場合は、競合しているファイルごとにプロンプトが表示されます。</span><span class="sxs-lookup"><span data-stu-id="671e9-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="671e9-147">MSBuild ターゲットと props ファイルの自動インポート</span><span class="sxs-lookup"><span data-stu-id="671e9-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="671e9-148">NuGet パッケージの最上位レベルで、新しい従来のフォルダーが作成されています。</span><span class="sxs-lookup"><span data-stu-id="671e9-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="671e9-149">、、およびのピアとして、 `\lib` `\content` `\tools` パッケージにフォルダーを含めることができるようになりました `\build` 。</span><span class="sxs-lookup"><span data-stu-id="671e9-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="671e9-150">このフォルダーには、固定名またはの2つのファイルを配置でき `{packageid}.targets` `{packageid}.props` ます。</span><span class="sxs-lookup"><span data-stu-id="671e9-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="671e9-151">これらの2つのファイルは、 `build` 他のフォルダーと同じように、フレームワーク固有のフォルダーの下に配置できます。</span><span class="sxs-lookup"><span data-stu-id="671e9-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="671e9-152">最も一致するフレームワークフォルダーを選択するルールは、これらのフォルダーとまったく同じです。</span><span class="sxs-lookup"><span data-stu-id="671e9-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="671e9-153">NuGet が \ ビルドファイルを含むパッケージをインストールすると、ファイル `<Import>` とファイルを指す MSBuild 要素がプロジェクトファイルに追加され `.targets` `.props` ます。</span><span class="sxs-lookup"><span data-stu-id="671e9-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="671e9-154">ファイルが一番上に追加され、 `.props` `.targets` ファイルが一番下に追加されます。</span><span class="sxs-lookup"><span data-stu-id="671e9-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="671e9-155">要素を使用してプラットフォームごとに異なる参照を指定する `<References/>`</span><span class="sxs-lookup"><span data-stu-id="671e9-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="671e9-156">2.5 より前のファイルでは、 `.nuspec` ユーザーは参照ファイルを指定するだけで、すべてのフレームワークに追加することができます。</span><span class="sxs-lookup"><span data-stu-id="671e9-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="671e9-157">2.5 のこの新機能により、ユーザーは `<reference/>` サポートされているプラットフォームごとに要素を作成できます。たとえば、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="671e9-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

<span data-ttu-id="671e9-158">ファイルに基づいて NuGet がプロジェクトに参照を追加する方法のフローを次に示し `.nuspec` ます。</span><span class="sxs-lookup"><span data-stu-id="671e9-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="671e9-159">`lib`ターゲットフレームワークに適したフォルダーを探し、そのフォルダーからアセンブリの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="671e9-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="671e9-160">ターゲットフレームワークに適した参照グループを個別に検索し、そのグループからアセンブリの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="671e9-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="671e9-161">ターゲットフレームワークが指定されていない参照グループがフォールバックグループです。</span><span class="sxs-lookup"><span data-stu-id="671e9-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="671e9-162">2つのリストの交差部分を検索し、それを追加する参照として使用します。</span><span class="sxs-lookup"><span data-stu-id="671e9-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="671e9-163">この新機能により、パッケージの作成者は参照機能を使用して、複数のフォルダーで重複するアセンブリを実行する必要がある場合に、アセンブリのサブセットを異なるフレームワークに適用でき `lib` ます。</span><span class="sxs-lookup"><span data-stu-id="671e9-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="671e9-164">注: 現在、この機能を使用するには nuget.exe パックを使用する必要があります。NuGet Package Explorer ではまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="671e9-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="671e9-165">すべてのパッケージを一度に更新できるように、すべてのボタンを更新します</span><span class="sxs-lookup"><span data-stu-id="671e9-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="671e9-166">すべてのパッケージを更新するための "パッケージの更新" PowerShell コマンドレットについて多くの知識を持っています。UI でも簡単に実行できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="671e9-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="671e9-167">この機能を試すには、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="671e9-167">To try this feature out:</span></span>

1. <span data-ttu-id="671e9-168">新しい ASP.NET MVC アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="671e9-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="671e9-169">[NuGet パッケージの管理] ダイアログを起動します。</span><span class="sxs-lookup"><span data-stu-id="671e9-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="671e9-170">[更新プログラム] を選択します。</span><span class="sxs-lookup"><span data-stu-id="671e9-170">Select 'Updates'</span></span>
1. <span data-ttu-id="671e9-171">[すべて更新] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="671e9-171">Click the 'Update All' button</span></span>

![ダイアログの [すべて更新] ボタン](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="671e9-173">nuget.exe パックのプロジェクト参照サポートの向上</span><span class="sxs-lookup"><span data-stu-id="671e9-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="671e9-174">ここで nuget.exe pack コマンドは、次の規則で参照されるプロジェクトを処理します。</span><span class="sxs-lookup"><span data-stu-id="671e9-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="671e9-175">参照先のプロジェクトに対応するファイルがある場合 `.nuspec` (たとえば、と同じフォルダーにという名前のファイルが存在する場合)、 `proj1.nuspec` `proj1.csproj` ファイルから読み取られた id とバージョンを使用して、このプロジェクトがパッケージへの依存関係として追加されます。 `.nuspec`</span><span class="sxs-lookup"><span data-stu-id="671e9-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="671e9-176">それ以外の場合は、参照されるプロジェクトのファイルがパッケージにバンドルされます。</span><span class="sxs-lookup"><span data-stu-id="671e9-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="671e9-177">その後、このプロジェクトで参照されるプロジェクトは、sames 規則を再帰的に使用して処理されます。</span><span class="sxs-lookup"><span data-stu-id="671e9-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="671e9-178">すべての DLL、 `.pdb` 、および `.exe` ファイルが追加されます。</span><span class="sxs-lookup"><span data-stu-id="671e9-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="671e9-179">その他のすべてのコンテンツファイルが追加されます。</span><span class="sxs-lookup"><span data-stu-id="671e9-179">All other content files are added.</span></span>
1. <span data-ttu-id="671e9-180">すべての依存関係がマージされます。</span><span class="sxs-lookup"><span data-stu-id="671e9-180">All dependencies are merged.</span></span>

<span data-ttu-id="671e9-181">これにより、ファイルが存在する場合、参照先のプロジェクトを依存関係として扱うことができ `.nuspec` ます。それ以外の場合は、パッケージの一部になります。</span><span class="sxs-lookup"><span data-stu-id="671e9-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="671e9-182">詳細については、こちらをご覧ください。 [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="671e9-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="671e9-183">' 最小 NuGet バージョン ' プロパティをパッケージに追加します</span><span class="sxs-lookup"><span data-stu-id="671e9-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="671e9-184">"MinClientVersion" という名前の新しいメタデータ属性は、パッケージを使用するために必要な最小限の NuGet クライアントバージョンを示すようになりました。</span><span class="sxs-lookup"><span data-stu-id="671e9-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="671e9-185">この機能を使用すると、パッケージの作成者は、特定のバージョンの NuGet の後でのみパッケージを使用するように指定できます。</span><span class="sxs-lookup"><span data-stu-id="671e9-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="671e9-186">`.nuspec`Nuget 2.5 の後に新しい機能が追加されると、パッケージは最小限の nuget バージョンを要求できるようになります。</span><span class="sxs-lookup"><span data-stu-id="671e9-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="671e9-187">ユーザーに NuGet 2.5 がインストールされており、パッケージが "2.6 が必要" と識別されている場合は、パッケージがインストールできないことを示す視覚的な手掛かりがユーザーに与えられます。</span><span class="sxs-lookup"><span data-stu-id="671e9-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="671e9-188">その後、ユーザーは NuGet のバージョンを更新するように指示されます。</span><span class="sxs-lookup"><span data-stu-id="671e9-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="671e9-189">これにより、パッケージのインストールが開始されるが、認識できないスキーマバージョンが識別されたことを示すエラーが発生した場合に、機能が向上します。</span><span class="sxs-lookup"><span data-stu-id="671e9-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="671e9-190">パッケージのインストール中に、依存関係が不必要に更新されなくなりました</span><span class="sxs-lookup"><span data-stu-id="671e9-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="671e9-191">NuGet 2.5 より前では、プロジェクトに既にインストールされているパッケージに依存するパッケージがインストールされている場合、既存のバージョンが依存関係を満たしていても、新しいインストールの一部として依存関係が更新されます。</span><span class="sxs-lookup"><span data-stu-id="671e9-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="671e9-192">NuGet 2.5 以降では、依存関係のバージョンが既に満たされている場合、他のパッケージのインストール中に依存関係は更新されません。</span><span class="sxs-lookup"><span data-stu-id="671e9-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="671e9-193">**シナリオは次のとおりです。**</span><span class="sxs-lookup"><span data-stu-id="671e9-193">**The scenario:**</span></span>

1. <span data-ttu-id="671e9-194">ソースリポジトリには、バージョン1.0.0 と1.0.2 のパッケージ B が含まれています。</span><span class="sxs-lookup"><span data-stu-id="671e9-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="671e9-195">また、B (>= 1.0.0) に依存するパッケージ A も含まれています。</span><span class="sxs-lookup"><span data-stu-id="671e9-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="671e9-196">現在のプロジェクトにパッケージ B バージョン1.0.0 が既にインストールされているとします。</span><span class="sxs-lookup"><span data-stu-id="671e9-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="671e9-197">ここで、パッケージ A をインストールします。</span><span class="sxs-lookup"><span data-stu-id="671e9-197">Now you want to install package A.</span></span>

<span data-ttu-id="671e9-198">**NuGet 2.2 以前:**</span><span class="sxs-lookup"><span data-stu-id="671e9-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="671e9-199">パッケージ A をインストールすると、既存のバージョン1.0.0 が既に依存関係バージョンの制約 (>= 1.0.0) を満たしていても、NuGet は B を自動的に1.0.2 に更新します。</span><span class="sxs-lookup"><span data-stu-id="671e9-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="671e9-200">**NuGet 2.5 以降:**</span><span class="sxs-lookup"><span data-stu-id="671e9-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="671e9-201">既存のバージョン1.0.0 が依存関係バージョンの制約を満たしていることが検出されるため、NuGet は B を更新しなくなります。</span><span class="sxs-lookup"><span data-stu-id="671e9-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="671e9-202">この変更の背景の詳細については、関連する[ディスカッションスレッド](http://nuget.codeplex.com/discussions/436712)だけでなく、詳細な[作業項目](http://nuget.codeplex.com/workitem/1681)も参照してください。</span><span class="sxs-lookup"><span data-stu-id="671e9-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="671e9-203">nuget.exe は、詳細な詳細度で http 要求を出力します</span><span class="sxs-lookup"><span data-stu-id="671e9-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="671e9-204">nuget.exe のトラブルシューティングを行う場合や、操作中に HTTP 要求が行われた場合は、'-詳細詳細 ' スイッチによって行われたすべての HTTP 要求が出力されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="671e9-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![nuget.exe からの HTTP 出力](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="671e9-206">nuget.exe プッシュで UNC およびフォルダーソースがサポートされるようになりました</span><span class="sxs-lookup"><span data-stu-id="671e9-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="671e9-207">NuGet 2.5 より前では、UNC パスまたはローカルフォルダーに基づいて "nuget.exe push" をパッケージソースに対して実行しようとすると、プッシュは失敗します。</span><span class="sxs-lookup"><span data-stu-id="671e9-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="671e9-208">最近追加された階層構成機能を使用すると、nuget.exe が UNC/フォルダーソースまたは HTTP ベースの NuGet ギャラリーをターゲットにする必要があることがよくありました。</span><span class="sxs-lookup"><span data-stu-id="671e9-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="671e9-209">NuGet 2.5 以降、nuget.exe が UNC/フォルダーソースを識別する場合、ソースへのファイルコピーを実行します。</span><span class="sxs-lookup"><span data-stu-id="671e9-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="671e9-210">次のコマンドが機能するようになります。</span><span class="sxs-lookup"><span data-stu-id="671e9-210">The following command will now work:</span></span>

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="671e9-211">明示的に指定された構成ファイルをサポート nuget.exe</span><span class="sxs-lookup"><span data-stu-id="671e9-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="671e9-212">構成にアクセスする nuget.exe コマンド (' spec ' と ' pack ' を除く) は、新しい '-ConfigFile ' オプションをサポートするようになりました。これにより、% AppData% \nuget\Nuget.Config の既定の構成ファイルの代わりに特定の構成ファイルが強制的に使用されます。</span><span class="sxs-lookup"><span data-stu-id="671e9-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="671e9-213">例:</span><span class="sxs-lookup"><span data-stu-id="671e9-213">Example:</span></span>

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="671e9-214">ネイティブプロジェクトのサポート</span><span class="sxs-lookup"><span data-stu-id="671e9-214">Support for Native projects</span></span>

<span data-ttu-id="671e9-215">NuGet 2.5 では、Visual Studio のネイティブプロジェクトで NuGet ツールを使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="671e9-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="671e9-216">ほとんどのネイティブパッケージは、 [Coapp プロジェクト](http://coapp.org)によって作成されたツールを使用して、上記の MSBuild インポート機能を利用することを想定しています。</span><span class="sxs-lookup"><span data-stu-id="671e9-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="671e9-217">詳細については、coapp.org web サイトの [ツールに関する詳細](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="671e9-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="671e9-218">パッケージがネイティブプロジェクトにインストールされている場合、パッケージでは、[ビルド]、[コンテンツ]、[ツール] の順に移動して、パッケージにファイルを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="671e9-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="671e9-219">\`Lib フォルダーはネイティブプロジェクトには使用されません。</span><span class="sxs-lookup"><span data-stu-id="671e9-219">The \`lib\` folder is not used for native projects.</span></span>
