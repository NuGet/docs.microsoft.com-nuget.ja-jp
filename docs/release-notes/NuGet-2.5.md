---
title: NuGet 2.5 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 2.5 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 29d0b33714a574281680e110b967269699afbaf1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550484"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="2993c-103">NuGet 2.5 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="2993c-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="2993c-104">[NuGet 2.2.1 リリース ノート](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 リリース ノート](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="2993c-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="2993c-105">NuGet 2.5 は、2013 年 4 月 25 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="2993c-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="2993c-106">このリリースがそれほど、バージョン 2.3、2.4 をスキップする感じました。</span><span class="sxs-lookup"><span data-stu-id="2993c-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="2993c-107">これまで、これは、最大のリリースで、NuGet のあった経由で[160 作業項目](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all)のリリースでします。</span><span class="sxs-lookup"><span data-stu-id="2993c-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="2993c-108">謝辞</span><span class="sxs-lookup"><span data-stu-id="2993c-108">Acknowledgements</span></span>

<span data-ttu-id="2993c-109">今回は外部の共同作成者、次の NuGet 2.5 に、多大な貢献に感謝します。</span><span class="sxs-lookup"><span data-stu-id="2993c-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="2993c-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="2993c-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="2993c-111">[#2847](https://nuget.codeplex.com/workitem/2847) -追加 MonoAndroid、MonoTouch、および既知のターゲット フレームワーク識別子の一覧に MonoMac します。</span><span class="sxs-lookup"><span data-stu-id="2993c-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="2993c-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="2993c-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="2993c-113">[#2865](https://nuget.codeplex.com/workitem/2865) -のスペルの修正`NuGet.targets`大文字の os</span><span class="sxs-lookup"><span data-stu-id="2993c-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="2993c-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="2993c-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="2993c-115">Mono 上でビルドするソリューションを作成します。</span><span class="sxs-lookup"><span data-stu-id="2993c-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="2993c-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="2993c-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="2993c-117">Mono で失敗した単体テストを修正します。</span><span class="sxs-lookup"><span data-stu-id="2993c-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="2993c-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="2993c-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="2993c-119">[#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe パック コマンドに msbuild プロパティが伝達されません</span><span class="sxs-lookup"><span data-stu-id="2993c-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="2993c-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="2993c-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="2993c-121">[#1511](https://nuget.codeplex.com/workitem/1511) - 変更 XML 処理コードを書式設定を保持します。</span><span class="sxs-lookup"><span data-stu-id="2993c-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="2993c-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="2993c-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="2993c-123">認識された単語を成功させる build.cmd を許可するカスタム辞書に追加されます。</span><span class="sxs-lookup"><span data-stu-id="2993c-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="2993c-124">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="2993c-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="2993c-125">ローカライズされた VS で実行する場合は、単体テストを修正します。</span><span class="sxs-lookup"><span data-stu-id="2993c-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="2993c-126">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="2993c-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="2993c-127">PackageService から抽出されたインターフェイス</span><span class="sxs-lookup"><span data-stu-id="2993c-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="2993c-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="2993c-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="2993c-129">[#936](https://nuget.codeplex.com/workitem/936)にパックするときに、プロジェクトの依存関係を処理</span><span class="sxs-lookup"><span data-stu-id="2993c-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="2993c-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="2993c-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="2993c-131">[#2991](https://nuget.codeplex.com/workitem/2991)、 [#3164](https://nuget.codeplex.com/workitem/3164) -サポート クリア テキスト パスワード nuget.cofig ファイルにパッケージ ソースの資格情報を格納する場合</span><span class="sxs-lookup"><span data-stu-id="2993c-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="2993c-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="2993c-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="2993c-133">[#3190](http://nuget.codeplex.com/workitem/3190)、 [#3191](http://nuget.codeplex.com/workitem/3191) -修正 Get-package ヘルプの説明</span><span class="sxs-lookup"><span data-stu-id="2993c-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="2993c-134">次のユーザーを魅力的に NuGet 2.5 Beta/RC が承認され、最終リリースの前に修正されたバグを見つけるため。</span><span class="sxs-lookup"><span data-stu-id="2993c-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="2993c-135">[Tony 壁](https://www.codeplex.com/site/users/view/CodeChief)([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="2993c-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="2993c-136">[#3200](https://nuget.codeplex.com/workitem/3200) - 最新の NuGet 2.4、2.5 ビルドで MSTest</span><span class="sxs-lookup"><span data-stu-id="2993c-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="2993c-137">リリースで注目すべき機能</span><span class="sxs-lookup"><span data-stu-id="2993c-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="2993c-138">ユーザーが既に存在するコンテンツ ファイルの上書きを許可します。</span><span class="sxs-lookup"><span data-stu-id="2993c-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="2993c-139">NuGet パッケージに含まれるときにディスクに既に存在するコンテンツのファイルを上書きする機能をすべての時間の最も多く要求された機能の 1 つされました。</span><span class="sxs-lookup"><span data-stu-id="2993c-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="2993c-140">NuGet 2.5 以降では、これらの競合が識別され、これらのファイルがスキップされた常に以前は、ファイルを上書きするように求められます。</span><span class="sxs-lookup"><span data-stu-id="2993c-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![コンテンツ ファイルを上書きします。](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="2993c-142">'nuget.exe update' および 'Install-package' 両方が、新しいオプション '-FileConflictAction' コマンド ライン シナリオのいくつかの既定値を設定します。</span><span class="sxs-lookup"><span data-stu-id="2993c-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="2993c-143">対象のプロジェクトにパッケージからのファイルが既に存在する場合は、既定のアクションを設定します。</span><span class="sxs-lookup"><span data-stu-id="2993c-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="2993c-144">「上書き」に設定すると、常にファイルを上書きします。</span><span class="sxs-lookup"><span data-stu-id="2993c-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="2993c-145">ファイルをスキップする '無視' に設定します。</span><span class="sxs-lookup"><span data-stu-id="2993c-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="2993c-146">指定しない場合、競合するファイルごとに求められます。</span><span class="sxs-lookup"><span data-stu-id="2993c-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="2993c-147">MSBuild ターゲットおよびプロパティ ファイルの自動インポート</span><span class="sxs-lookup"><span data-stu-id="2993c-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="2993c-148">NuGet パッケージの最上位レベルでは、従来の新しいフォルダーが用意されています。</span><span class="sxs-lookup"><span data-stu-id="2993c-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="2993c-149">ピアとして`\lib`、 `\content`、および`\tools`、できるようになりました、`\build`パッケージ内のフォルダー。</span><span class="sxs-lookup"><span data-stu-id="2993c-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="2993c-150">このフォルダーの下には、固定の名前を持つ 2 つのファイルを配置することができます`{packageid}.targets`または`{packageid}.props`します。</span><span class="sxs-lookup"><span data-stu-id="2993c-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="2993c-151">これら 2 つのファイルがあるか直接`build`またはその他のフォルダーと同じようフレームワークに固有のフォルダーの下。</span><span class="sxs-lookup"><span data-stu-id="2993c-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="2993c-152">一致する最適なフレームワーク フォルダーを選択するための規則ではものと同じです。</span><span class="sxs-lookup"><span data-stu-id="2993c-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="2993c-153">NuGet は \build ファイルでパッケージをインストールと、は、MSBuild が追加されます`<Import>`を指すプロジェクト ファイル内の要素、`.targets`と`.props`ファイル。</span><span class="sxs-lookup"><span data-stu-id="2993c-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="2993c-154">`.props`は、上部にあるファイルが追加された、`.targets`ファイル下部に追加されます。</span><span class="sxs-lookup"><span data-stu-id="2993c-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="2993c-155">使用するプラットフォームごとに異なる参照を指定`<References/>`要素</span><span class="sxs-lookup"><span data-stu-id="2993c-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="2993c-156">2.5 では前に、の`.nuspec`ファイル、ユーザーはすべてのフレームワーク用に追加する、参照ファイルを指定してできますのみです。</span><span class="sxs-lookup"><span data-stu-id="2993c-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="2993c-157">2.5 ではこの新しい機能では、ユーザーを作成できるので、`<reference/>`要素ごとの例では、サポートされているプラットフォーム。</span><span class="sxs-lookup"><span data-stu-id="2993c-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

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

<span data-ttu-id="2993c-158">NuGet がに基づいてプロジェクトへの参照を追加する方法のフローを次に示します、`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="2993c-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="2993c-159">検索、`lib`フォルダー ターゲット フレームワークの適切なは、そのフォルダーからアセンブリの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="2993c-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="2993c-160">個別にターゲット フレームワークの適切な参照グループを検索し、そのグループからのアセンブリの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="2993c-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="2993c-161">ターゲット フレームワークを指定せず、参照グループは、フォールバックのグループです。</span><span class="sxs-lookup"><span data-stu-id="2993c-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="2993c-162">2 つのリストの積集合を検索し、追加する参照として使用します。</span><span class="sxs-lookup"><span data-stu-id="2993c-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="2993c-163">参照機能を使用して、それ以外の場合、複数の重複するアセンブリを実行するために必要なはときに、さまざまなフレームワークをアセンブリのサブセットを適用するパッケージの作成者により、この新しい機能`lib`フォルダー。</span><span class="sxs-lookup"><span data-stu-id="2993c-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="2993c-164">メモ: する必要があります現在を使用する nuget.exe パック。 この機能を使用するにはNuGet パッケージ エクスプ ローラーはまだサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="2993c-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="2993c-165">すべてのパッケージを一度に更新できるようにするすべてのボタンを更新します。</span><span class="sxs-lookup"><span data-stu-id="2993c-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="2993c-166">皆さんの多くはすべてのパッケージ; を更新する「更新プログラム パッケージ」PowerShell コマンドレットについて知っておくこれは、UI もで実行する簡単な方法があるようになりました。</span><span class="sxs-lookup"><span data-stu-id="2993c-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="2993c-167">この機能を試す。</span><span class="sxs-lookup"><span data-stu-id="2993c-167">To try this feature out:</span></span>

1. <span data-ttu-id="2993c-168">新しい ASP.NET MVC アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="2993c-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="2993c-169">NuGet パッケージの管理 ダイアログを起動します。</span><span class="sxs-lookup"><span data-stu-id="2993c-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="2993c-170">「更新プログラム」を選択します。</span><span class="sxs-lookup"><span data-stu-id="2993c-170">Select 'Updates'</span></span>
1. <span data-ttu-id="2993c-171">[すべて更新] ボタンをクリックします</span><span class="sxs-lookup"><span data-stu-id="2993c-171">Click the 'Update All' button</span></span>

![更新 ダイアログ ボックスすべて ボタン](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="2993c-173">Nuget.exe パックの強化されたプロジェクト参照のサポート</span><span class="sxs-lookup"><span data-stu-id="2993c-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="2993c-174">Nuget.exe パック コマンド プロセスが、次の規則を使用したプロジェクトを参照しているようになりました。</span><span class="sxs-lookup"><span data-stu-id="2993c-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="2993c-175">対応する参照先のプロジェクトに含まれる場合`.nuspec`ファイルなどという名前のファイルがある`proj1.nuspec`と同じフォルダーに`proj1.csproj`、このプロジェクトは、id を使用して、パッケージに依存関係として追加は、およびバージョンを読み取ったり、`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="2993c-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="2993c-176">それ以外の場合、参照先のプロジェクトのファイルがパッケージにバンドルされています。</span><span class="sxs-lookup"><span data-stu-id="2993c-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="2993c-177">このプロジェクトで参照されているプロジェクトは、そのままルールを再帰的を使用して処理されます。</span><span class="sxs-lookup"><span data-stu-id="2993c-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="2993c-178">すべての DLL `.pdb`、および`.exe`ファイルが追加されます。</span><span class="sxs-lookup"><span data-stu-id="2993c-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="2993c-179">その他のすべてのコンテンツ ファイルが追加されます。</span><span class="sxs-lookup"><span data-stu-id="2993c-179">All other content files are added.</span></span>
1. <span data-ttu-id="2993c-180">すべての依存関係がマージされます。</span><span class="sxs-lookup"><span data-stu-id="2993c-180">All dependencies are merged.</span></span>

<span data-ttu-id="2993c-181">これにより、参照先のプロジェクトがある場合は、依存関係として扱う場合に、`.nuspec`ファイルで、それ以外の場合、パッケージの一部となります。</span><span class="sxs-lookup"><span data-stu-id="2993c-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="2993c-182">詳細についてはこちら: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="2993c-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="2993c-183">パッケージに ' 最小 NuGet の Version' プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="2993c-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="2993c-184">'MinClientVersion' と呼ばれる新しいメタデータ属性は、パッケージを使用するために必要な最小の NuGet クライアント バージョンを示すようになりましたことができます。</span><span class="sxs-lookup"><span data-stu-id="2993c-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="2993c-185">この機能には、特定のバージョンの NuGet の後にのみ、パッケージが動作するかを指定するパッケージの作成者が役立ちます。</span><span class="sxs-lookup"><span data-stu-id="2993c-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="2993c-186">新しい`.nuspec`パッケージは NuGet の最小バージョンを要求できる NuGet 2.5 では、後に機能が追加されました。</span><span class="sxs-lookup"><span data-stu-id="2993c-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="2993c-187">ユーザーがインストールされている NuGet 2.5、2.6 を必要とすると、パッケージが識別される場合は、パッケージがインストールできないようにすることを示す視覚的な手掛かりを与えられます。</span><span class="sxs-lookup"><span data-stu-id="2993c-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="2993c-188">ユーザーは、NuGet のバージョンを更新する、ガイド付きされます。</span><span class="sxs-lookup"><span data-stu-id="2993c-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="2993c-189">これは、パッケージのインストールが失敗するように、認識できないスキーマ バージョンの識別を示す開始位置、既存のエクスペリエンスに向上します。</span><span class="sxs-lookup"><span data-stu-id="2993c-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="2993c-190">依存関係がパッケージのインストール中に更新される不必要に不要になった</span><span class="sxs-lookup"><span data-stu-id="2993c-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="2993c-191">NuGet 2.5 では、前に、プロジェクトに既にインストールされているパッケージに依存するパッケージのインストール時に、依存関係が更新されます、新しいインストールの一部として既存のバージョンには、依存関係が満たされている場合でも。</span><span class="sxs-lookup"><span data-stu-id="2993c-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="2993c-192">以降、NuGet 2.5 では依存関係のバージョンが既に満たされている場合、依存関係は更新されません他のパッケージのインストール中にします。</span><span class="sxs-lookup"><span data-stu-id="2993c-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="2993c-193">**シナリオ:**</span><span class="sxs-lookup"><span data-stu-id="2993c-193">**The scenario:**</span></span>

1. <span data-ttu-id="2993c-194">ソース リポジトリには、バージョン 1.0.0 と 1.0.2 でパッケージ B が含まれています。</span><span class="sxs-lookup"><span data-stu-id="2993c-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="2993c-195">B に依存しているパッケージ A も含まれています (> = 1.0.0)。</span><span class="sxs-lookup"><span data-stu-id="2993c-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="2993c-196">現在のプロジェクトが既にパッケージ B のバージョン 1.0.0 がインストールされていることを想定しています。</span><span class="sxs-lookup"><span data-stu-id="2993c-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="2993c-197">A. のパッケージをインストールするようになりました</span><span class="sxs-lookup"><span data-stu-id="2993c-197">Now you want to install package A.</span></span>

<span data-ttu-id="2993c-198">**Nuget 2.2 と古い。**</span><span class="sxs-lookup"><span data-stu-id="2993c-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="2993c-199">パッケージ A をインストールするときに NuGet は自動更新 B 1.0.2、既存のバージョン 1.0.0 が既にには依存関係のバージョンの制約を満たす場合でも > 1.0.0 を = です。</span><span class="sxs-lookup"><span data-stu-id="2993c-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="2993c-200">**Nuget 2.5 以降。**</span><span class="sxs-lookup"><span data-stu-id="2993c-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="2993c-201">NuGet、既存のバージョン 1.0.0 が依存関係のバージョン制約を満たすことが検出されたため、B が不要になった更新されます。</span><span class="sxs-lookup"><span data-stu-id="2993c-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="2993c-202">この変更の詳細については、読み取り、詳細な[作業項目](http://nuget.codeplex.com/workitem/1681)と関連する[ディスカッション スレッド](http://nuget.codeplex.com/discussions/436712)します。</span><span class="sxs-lookup"><span data-stu-id="2993c-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="2993c-203">nuget.exe 詳細な http 要求を出力します。</span><span class="sxs-lookup"><span data-stu-id="2993c-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="2993c-204">Nuget.exe のトラブルシューティングを行うか、単どのような HTTP 要求が、処理中に行われた興味がある、'-詳細度の詳細な ' スイッチが行われたすべての HTTP 要求を出力するようになりました。</span><span class="sxs-lookup"><span data-stu-id="2993c-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Nuget.exe からの HTTP 出力](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="2993c-206">nuget.exe プッシュでは、UNC およびフォルダーのソースをサポートします。</span><span class="sxs-lookup"><span data-stu-id="2993c-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="2993c-207">NuGet 2.5 では、前に、UNC パスまたはローカルのフォルダーに基づくパッケージのソースに 'nuget.exe push' を実行しようとしました、プッシュは失敗します。</span><span class="sxs-lookup"><span data-stu-id="2993c-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="2993c-208">階層的な構成を最近追加された機能を使用には、UNC/フォルダーのソース、または HTTP ベースの NuGet ギャラリーのいずれかを指定する必要する nuget.exe の一般的なの操作になる必要があります。</span><span class="sxs-lookup"><span data-stu-id="2993c-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="2993c-209">NuGet 2.5 以降 nuget.exe UNC/フォルダーのソースを指定する場合、ソース ファイルのコピーが実行されます。</span><span class="sxs-lookup"><span data-stu-id="2993c-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="2993c-210">次のコマンドは機能ようになりました。</span><span class="sxs-lookup"><span data-stu-id="2993c-210">The following command will now work:</span></span>

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="2993c-211">nuget.exe が明示的に指定された構成ファイルをサポートしています</span><span class="sxs-lookup"><span data-stu-id="2993c-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="2993c-212">('仕様' と"pack"を除くすべて) の構成を今すぐアクセス nuget.exe コマンド サポートを新しい '-ConfigFile' オプションは、%appdata%\nuget\nuget.config で既定の構成ファイルの代わりに使用される固有の構成ファイルを強制します。</span><span class="sxs-lookup"><span data-stu-id="2993c-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="2993c-213">例:</span><span class="sxs-lookup"><span data-stu-id="2993c-213">Example:</span></span>

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="2993c-214">ネイティブ プロジェクトのサポート</span><span class="sxs-lookup"><span data-stu-id="2993c-214">Support for Native projects</span></span>

<span data-ttu-id="2993c-215">NuGet 2.5 では、NuGet ツールは、Visual Studio でのネイティブ プロジェクトで使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="2993c-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="2993c-216">予定最もネイティブ パッケージは、MSBuild インポート機能を利用して作成ツールを使用して、 [CoApp プロジェクト](http://coapp.org)します。</span><span class="sxs-lookup"><span data-stu-id="2993c-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="2993c-217">詳細については、読み取る[ツールに関する詳細](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html)coapp.org web サイト。</span><span class="sxs-lookup"><span data-stu-id="2993c-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="2993c-218">"Native"のターゲット フレームワークの名前には、ネイティブ プロジェクトに、パッケージをインストールするときに、\build、\content、および \tools にファイルを含めるパッケージが導入されました。</span><span class="sxs-lookup"><span data-stu-id="2993c-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="2993c-219">\`Lib' ネイティブ プロジェクトのフォルダーは使用されません。</span><span class="sxs-lookup"><span data-stu-id="2993c-219">The \`lib` folder is not used for native projects.</span></span>
