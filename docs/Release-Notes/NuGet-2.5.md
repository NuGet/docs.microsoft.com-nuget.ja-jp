---
title: "NuGet 2.5 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 2.5 のリリース ノートします。"
keywords: "NuGet 2.5 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4fb696a1f4d76bdd3461df6af461f279f9f0a8b0
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="d3354-104">NuGet 2.5 のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="d3354-104">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="d3354-105">[NuGet 2.2.1 リリース ノート](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 リリース ノート](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="d3354-105">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="d3354-106">NuGet 2.5 は、2013 年 4 月 25 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="d3354-106">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="d3354-107">このリリースが大きすぎて、バージョン 2.3 および 2.4 をスキップする感じました。</span><span class="sxs-lookup"><span data-stu-id="d3354-107">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="d3354-108">までに、これは、最大のリリースと、NuGet のきました経由で[160 作業項目](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all)リリースします。</span><span class="sxs-lookup"><span data-stu-id="d3354-108">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="d3354-109">謝辞</span><span class="sxs-lookup"><span data-stu-id="d3354-109">Acknowledgements</span></span>

<span data-ttu-id="d3354-110">NuGet 2.5 に大幅な貢献の次の外部共同作成者いただき、ありがとうたいと思います。</span><span class="sxs-lookup"><span data-stu-id="d3354-110">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="d3354-111">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="d3354-111">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="d3354-112">[#2847](https://nuget.codeplex.com/workitem/2847) -追加 MonoAndroid、MonoTouch、および既知のターゲット フレームワーク識別子の一覧に MonoMac です。</span><span class="sxs-lookup"><span data-stu-id="d3354-112">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
1. <span data-ttu-id="d3354-113">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="d3354-113">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="d3354-114">[#2865](https://nuget.codeplex.com/workitem/2865) -のスペル修正`NuGet.targets`大文字小文字を区別 os</span><span class="sxs-lookup"><span data-stu-id="d3354-114">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
1. <span data-ttu-id="d3354-115">[David ファウラー](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="d3354-115">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="d3354-116">ソリューションの Mono でビルドを確認します。</span><span class="sxs-lookup"><span data-stu-id="d3354-116">Make the solution build on Mono.</span></span>
1. <span data-ttu-id="d3354-117">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="d3354-117">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="d3354-118">モノラルで失敗する単体テストを修正します。</span><span class="sxs-lookup"><span data-stu-id="d3354-118">Fix unit tests failing on Mono.</span></span>
1. <span data-ttu-id="d3354-119">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="d3354-119">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="d3354-120">[#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe パック コマンドは、msbuild プロパティを反映しません</span><span class="sxs-lookup"><span data-stu-id="d3354-120">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
1. <span data-ttu-id="d3354-121">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="d3354-121">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="d3354-122">[#1511](https://nuget.codeplex.com/workitem/1511) - 変更された XML 処理コードの書式設定を保持するためにします。</span><span class="sxs-lookup"><span data-stu-id="d3354-122">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
1. <span data-ttu-id="d3354-123">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="d3354-123">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="d3354-124">Build.cmd を正常に使用できるようにカスタム辞書に認識された単語を追加します。</span><span class="sxs-lookup"><span data-stu-id="d3354-124">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
1. [<span data-ttu-id="d3354-125">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="d3354-125">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="d3354-126">ローカライズされた VS で実行されている場合は、単体テストを修正します。</span><span class="sxs-lookup"><span data-stu-id="d3354-126">Fix unit tests when running in localized VS.</span></span>
1. [<span data-ttu-id="d3354-127">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="d3354-127">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="d3354-128">PackageService から抽出されたインターフェイス</span><span class="sxs-lookup"><span data-stu-id="d3354-128">Extracted interface from PackageService</span></span>
1. <span data-ttu-id="d3354-129">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="d3354-129">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
    - <span data-ttu-id="d3354-130">[#936](https://nuget.codeplex.com/workitem/936) -梱包する場合のプロジェクトの依存関係の処理</span><span class="sxs-lookup"><span data-stu-id="d3354-130">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
1. <span data-ttu-id="d3354-131">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="d3354-131">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
    - <span data-ttu-id="d3354-132">[#2991](https://nuget.codeplex.com/workitem/2991)、 [#3164](https://nuget.codeplex.com/workitem/3164) -サポート クリア テキスト パスワード nuget.cofig ファイルにパッケージ ソースの資格情報を格納する場合</span><span class="sxs-lookup"><span data-stu-id="d3354-132">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
1. <span data-ttu-id="d3354-133">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="d3354-133">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
    - <span data-ttu-id="d3354-134">[#3190](http://nuget.codeplex.com/workitem/3190)、 [#3191](http://nuget.codeplex.com/workitem/3191) -修正 Get-package ヘルプの説明</span><span class="sxs-lookup"><span data-stu-id="d3354-134">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="d3354-135">次の個人用を認めるように NuGet 2.5 ベータ/RC が承認され、最終リリース前に修正されたバグを見つけるため。</span><span class="sxs-lookup"><span data-stu-id="d3354-135">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="d3354-136">[Tony 壁](https://www.codeplex.com/site/users/view/CodeChief)([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="d3354-136">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="d3354-137">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest 最新 NuGet 2.4 と 2.5 ビルド分割</span><span class="sxs-lookup"><span data-stu-id="d3354-137">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="d3354-138">リリースで注目に値する機能</span><span class="sxs-lookup"><span data-stu-id="d3354-138">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="d3354-139">ユーザーが既に存在するコンテンツのファイルの上書きを許可します。</span><span class="sxs-lookup"><span data-stu-id="d3354-139">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="d3354-140">NuGet パッケージに含まれるときにディスクに既に存在するコンテンツのファイルを上書きする権限をすべての時間の多かった機能の 1 つされました。</span><span class="sxs-lookup"><span data-stu-id="d3354-140">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="d3354-141">NuGet 2.5 以降では、これらの競合識別され、これらのファイルがスキップされた常に以前は、ファイルを上書きするように求められます。</span><span class="sxs-lookup"><span data-stu-id="d3354-141">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![コンテンツ ファイルを上書き](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="d3354-143">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span><span class="sxs-lookup"><span data-stu-id="d3354-143">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="d3354-144">対象のプロジェクトにパッケージからファイルが既に存在する場合は、既定のアクションを設定します。</span><span class="sxs-lookup"><span data-stu-id="d3354-144">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="d3354-145">常にファイルを上書きする「上書き」に設定します。</span><span class="sxs-lookup"><span data-stu-id="d3354-145">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="d3354-146">'Ignore' に設定すると、ファイルをスキップします。</span><span class="sxs-lookup"><span data-stu-id="d3354-146">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="d3354-147">指定しない場合、競合している各ファイルが求められます。</span><span class="sxs-lookup"><span data-stu-id="d3354-147">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="d3354-148">MSBuild のターゲットと props ファイルの自動インポート</span><span class="sxs-lookup"><span data-stu-id="d3354-148">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="d3354-149">NuGet パッケージの最上位レベルには、従来の新しいフォルダーが用意されています。</span><span class="sxs-lookup"><span data-stu-id="d3354-149">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="d3354-150">ピアとして`\lib`、 `\content`、および`\tools`、するできるようになりました、`\build`パッケージ内のフォルダーです。</span><span class="sxs-lookup"><span data-stu-id="d3354-150">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="d3354-151">このフォルダーの下には、固定名は、2 つのファイルを配置することができます`{packageid}.targets`または`{packageid}.props`です。</span><span class="sxs-lookup"><span data-stu-id="d3354-151">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="d3354-152">これら 2 つのファイルがあるか直接`build`またはフレームワーク固有のフォルダーに、他のフォルダーと同じようにします。</span><span class="sxs-lookup"><span data-stu-id="d3354-152">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="d3354-153">最も一致するフレームワーク フォルダーを選択するためのルールは、ものと同じではまったくです。</span><span class="sxs-lookup"><span data-stu-id="d3354-153">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="d3354-154">NuGet \build ファイルとパッケージのインストール時に、MSBuild が追加`<Import>`要素を指すプロジェクト ファイルで、`.targets`と`.props`ファイル。</span><span class="sxs-lookup"><span data-stu-id="d3354-154">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="d3354-155">`.props`一方、上部にあるファイルが追加、`.targets`ファイルが下部に追加します。</span><span class="sxs-lookup"><span data-stu-id="d3354-155">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="d3354-156">プラットフォームごとの別の参照を指定`<References/>`要素</span><span class="sxs-lookup"><span data-stu-id="d3354-156">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="d3354-157">2.5 では前に、の`.nuspec`ファイル、ユーザーがすべてのフレームワーク用に追加する、参照ファイルを指定できますのみです。</span><span class="sxs-lookup"><span data-stu-id="d3354-157">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="d3354-158">これで、この新しい機能により 2.5 では、ユーザーを作成できます、`<reference/>`例については、サポートされているプラットフォームごとの要素。</span><span class="sxs-lookup"><span data-stu-id="d3354-158">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

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

<span data-ttu-id="d3354-159">ここでは、NuGet がに基づいてプロジェクトへの参照を追加する方法のフロー、`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="d3354-159">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="d3354-160">検索、`lib`フォルダー ターゲット フレームワークの適切なは、そのフォルダーからアセンブリの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="d3354-160">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="d3354-161">別に、ターゲット フレームワークを適切な参照グループを検索し、そのグループからのアセンブリの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="d3354-161">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="d3354-162">指定されたターゲット フレームワークなしの参照グループは、フォールバックのグループです。</span><span class="sxs-lookup"><span data-stu-id="d3354-162">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="d3354-163">2 つのリストの積集合を検索し、追加する参照として使用します。</span><span class="sxs-lookup"><span data-stu-id="d3354-163">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="d3354-164">この新機能によって、それ以外の場合は複数の重複するアセンブリを実行する必要がある場合は、さまざまなフレームワークにアセンブリのサブセットを適用する参照機能を使用するパッケージ作成者`lib`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="d3354-164">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="d3354-165">メモ: する必要があります現在を使用する nuget.exe パック。 この機能を使用するにはNuGet パッケージ エクスプ ローラーはまだサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="d3354-165">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="d3354-166">すべてのパッケージを一度に更新を許可するすべてのボタンを更新します。</span><span class="sxs-lookup"><span data-stu-id="d3354-166">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="d3354-167">多くは次のトピック、「更新プログラム パッケージ」PowerShell コマンドレットを更新するすべてのパッケージです。も、UI を使用する簡単な方法があるようになりました。</span><span class="sxs-lookup"><span data-stu-id="d3354-167">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="d3354-168">この機能を試してみてください。</span><span class="sxs-lookup"><span data-stu-id="d3354-168">To try this feature out:</span></span>

1. <span data-ttu-id="d3354-169">新しい ASP.NET MVC アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="d3354-169">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="d3354-170">NuGet パッケージの管理 ダイアログを起動します。</span><span class="sxs-lookup"><span data-stu-id="d3354-170">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="d3354-171">'更新' を選択します。</span><span class="sxs-lookup"><span data-stu-id="d3354-171">Select 'Updates'</span></span>
1. <span data-ttu-id="d3354-172">[すべて更新] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="d3354-172">Click the 'Update All' button</span></span>

![ダイアログ ボックスで [すべて] ボタンを更新します。](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="d3354-174">Nuget.exe パックの強化されたプロジェクト参照のサポート</span><span class="sxs-lookup"><span data-stu-id="d3354-174">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="d3354-175">Nuget.exe パック コマンド、プロセスが次の規則にプロジェクトを参照しているようになりました。</span><span class="sxs-lookup"><span data-stu-id="d3354-175">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="d3354-176">場合は、参照先プロジェクトに対応する`.nuspec`ファイル、たとえばという名前のファイルがある`proj1.nuspec`と同じフォルダーに`proj1.csproj`し、このプロジェクトが追加の依存関係として、id を使用して、パッケージ、およびバージョンからの読み取り、`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="d3354-176">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="d3354-177">それ以外の場合、参照先のプロジェクトのファイルは、パッケージにまとめられます。</span><span class="sxs-lookup"><span data-stu-id="d3354-177">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="d3354-178">このプロジェクトによって参照されるプロジェクトは、sames ルールを再帰的を使用して処理されます。</span><span class="sxs-lookup"><span data-stu-id="d3354-178">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="d3354-179">すべての DLL `.pdb`、および`.exe`ファイルが追加されます。</span><span class="sxs-lookup"><span data-stu-id="d3354-179">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="d3354-180">その他のすべてのコンテンツ ファイルが追加されます。</span><span class="sxs-lookup"><span data-stu-id="d3354-180">All other content files are added.</span></span>
1. <span data-ttu-id="d3354-181">すべての依存関係がマージされます。</span><span class="sxs-lookup"><span data-stu-id="d3354-181">All dependencies are merged.</span></span>

<span data-ttu-id="d3354-182">これにより、参照先のプロジェクトがある場合、依存関係として扱われる、`.nuspec`ファイルで、それ以外の場合、パッケージの一部になります。</span><span class="sxs-lookup"><span data-stu-id="d3354-182">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="d3354-183">詳細については、ここ: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="d3354-183">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="d3354-184">パッケージに '最低限の NuGet バージョン' プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="d3354-184">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="d3354-185">という新しいメタデータの属性 'minClientVersion' は、パッケージを使用するために必要な最小の NuGet クライアント バージョンを示すようになりましたことができます。</span><span class="sxs-lookup"><span data-stu-id="d3354-185">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="d3354-186">この機能を使用すると、パッケージの作成者を特定のバージョンの NuGet の後にパッケージが動作するを指定します。</span><span class="sxs-lookup"><span data-stu-id="d3354-186">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="d3354-187">新しい`.nuspec`機能後に追加された NuGet 2.5 では、パッケージは NuGet の最小バージョンを要求することができます。</span><span class="sxs-lookup"><span data-stu-id="d3354-187">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="d3354-188">ユーザーがインストールされている NuGet 2.5 2.6 を必要とすると、パッケージが識別される場合は、パッケージをインストール可能にすることはできませんを示すユーザーへ視覚的な手掛かりが与えられます。</span><span class="sxs-lookup"><span data-stu-id="d3354-188">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="d3354-189">ユーザーは、NuGet のバージョンを更新するガイドします。</span><span class="sxs-lookup"><span data-stu-id="d3354-189">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="d3354-190">これは、パッケージをインストールし、失敗する可能性が認識されていないスキーマ バージョンが識別されたことを示すに開始する位置を示す既存のエクスペリエンスに向上します。</span><span class="sxs-lookup"><span data-stu-id="d3354-190">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="d3354-191">依存関係がパッケージのインストール中に更新されなく不必要に</span><span class="sxs-lookup"><span data-stu-id="d3354-191">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="d3354-192">NuGet 2.5 では、前に、プロジェクトに既にインストールされているパッケージに依存していたパッケージのインストール時に、依存関係が更新されます、新しいインストールの一部として、既存のバージョンには、依存関係が満たされる場合でもです。</span><span class="sxs-lookup"><span data-stu-id="d3354-192">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="d3354-193">NuGet 2.5 から始めて、依存関係のバージョンを既に満たしている場合、依存関係は更新されません他のパッケージのインストール中にします。</span><span class="sxs-lookup"><span data-stu-id="d3354-193">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="d3354-194">**シナリオ:**</span><span class="sxs-lookup"><span data-stu-id="d3354-194">**The scenario:**</span></span>

1. <span data-ttu-id="d3354-195">ソース リポジトリには、バージョン 1.0.0 1.0.2 パッケージ B が含まれています。</span><span class="sxs-lookup"><span data-stu-id="d3354-195">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="d3354-196">パッケージ A が B に依存しているも含まれています (> = 1.0.0)。</span><span class="sxs-lookup"><span data-stu-id="d3354-196">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="d3354-197">現在のプロジェクトは既にパッケージ B のバージョン 1.0.0 がインストールされていることを想定しています。</span><span class="sxs-lookup"><span data-stu-id="d3354-197">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="d3354-198">A. のパッケージをインストールするようになりました</span><span class="sxs-lookup"><span data-stu-id="d3354-198">Now you want to install package A.</span></span>

<span data-ttu-id="d3354-199">**NuGet 2.2 と古い: で**</span><span class="sxs-lookup"><span data-stu-id="d3354-199">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="d3354-200">パッケージ A をインストールするときに NuGet が自動更新 B 1.0.2、既存のバージョン 1.0.0 が既にこれは依存関係のバージョンの制約を満たす場合でも > 1.0.0 を = です。</span><span class="sxs-lookup"><span data-stu-id="d3354-200">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="d3354-201">**NuGet 2.5 と新しい: で**</span><span class="sxs-lookup"><span data-stu-id="d3354-201">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="d3354-202">既存のバージョン 1.0.0 が依存関係のバージョンの制約を満たすことが検出されたために、NuGet は B を不要になった更新されます。</span><span class="sxs-lookup"><span data-stu-id="d3354-202">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="d3354-203">この変更の詳細については、読み取り、詳細な[作業項目](http://nuget.codeplex.com/workitem/1681)、関連するだけでなく[ディスカッション スレッド](http://nuget.codeplex.com/discussions/436712)です。</span><span class="sxs-lookup"><span data-stu-id="d3354-203">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="d3354-204">nuget.exe 詳細な詳細レベルでの http 要求を出力します。</span><span class="sxs-lookup"><span data-stu-id="d3354-204">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="d3354-205">Nuget.exe のトラブルシューティングを行うか、単興味があるどの HTTP 要求が行われる操作中に、'-詳細な詳細度 ' スイッチが行われるすべての HTTP 要求を出力するようになりました。</span><span class="sxs-lookup"><span data-stu-id="d3354-205">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Nuget.exe から HTTP 出力](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="d3354-207">nuget.exe プッシュに今すぐ UNC とフォルダーのソースがサポートしています</span><span class="sxs-lookup"><span data-stu-id="d3354-207">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="d3354-208">NuGet 2.5 では、前に、UNC パスまたはローカル フォルダーに基づくパッケージ ソース 'nuget.exe プッシュ' を実行する試行する場合は、プッシュは失敗します。</span><span class="sxs-lookup"><span data-stu-id="d3354-208">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="d3354-209">階層構造の構成を最近追加された機能を使用して、UNC/フォルダーのソース、または HTTP ベース NuGet ギャラリーのいずれかを対象とする必要がある nuget.exe の一般的なになる必要があります。</span><span class="sxs-lookup"><span data-stu-id="d3354-209">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="d3354-210">NuGet 2.5 から始めて nuget.exe UNC/フォルダーのソースを識別する場合、ソース ファイルのコピーを実行します。</span><span class="sxs-lookup"><span data-stu-id="d3354-210">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="d3354-211">次のコマンドが動作します。</span><span class="sxs-lookup"><span data-stu-id="d3354-211">The following command will now work:</span></span>

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="d3354-212">nuget.exe が明示的に指定された構成ファイルをサポートしています</span><span class="sxs-lookup"><span data-stu-id="d3354-212">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="d3354-213">('仕様' と 'pack' を除くすべて) の構成を今すぐアクセスする nuget.exe のコマンドは、新しいサポート '-ConfigFile' オプションは、%appdata%\nuget\nuget.config で既定の構成ファイルの代わりに使用する固有の構成ファイルを強制します。</span><span class="sxs-lookup"><span data-stu-id="d3354-213">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="d3354-214">例:</span><span class="sxs-lookup"><span data-stu-id="d3354-214">Example:</span></span>

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="d3354-215">ネイティブ プロジェクトのサポート</span><span class="sxs-lookup"><span data-stu-id="d3354-215">Support for Native projects</span></span>

<span data-ttu-id="d3354-216">NuGet 2.5 で NuGet ツールは Visual Studio でのネイティブ プロジェクトで使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="d3354-216">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="d3354-217">予定最もネイティブ パッケージは、上記の MSBuild のインポート機能を利用して作成ツールを使用して、 [CoApp プロジェクト](http://coapp.org)です。</span><span class="sxs-lookup"><span data-stu-id="d3354-217">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="d3354-218">詳細については、「[詳細についてはツール、](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) coapp.org web サイトです。</span><span class="sxs-lookup"><span data-stu-id="d3354-218">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="d3354-219">"Native"のターゲット フレームワークの名前には、ファイルを含める \build、\content、および \tools でネイティブ プロジェクトにパッケージがインストールされているときにパッケージが導入されました。</span><span class="sxs-lookup"><span data-stu-id="d3354-219">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="d3354-220">\`Lib' フォルダーは、ネイティブ プロジェクトには使用されません。</span><span class="sxs-lookup"><span data-stu-id="d3354-220">The \`lib` folder is not used for native projects.</span></span>
