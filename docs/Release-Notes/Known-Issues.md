---
title: "NuGet の既知の問題 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "認証、パッケージのインストール、ツールなど、NuGet に関する既知の問題。"
keywords: "NuGet の既知の問題, NuGet の問題"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2b9190c058215d9e63894de45c0c55c8ddae0e0f
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2018
---
# <a name="known-issues-with-nuget"></a><span data-ttu-id="c4e68-104">NuGet に関する既知の問題</span><span class="sxs-lookup"><span data-stu-id="c4e68-104">Known Issues with NuGet</span></span>

<span data-ttu-id="c4e68-105">繰り返し報告されている NuGet に関する最も一般的な問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="c4e68-105">These are the most common known issues with NuGet that are repeatedly reported.</span></span> <span data-ttu-id="c4e68-106">NuGet のインストール時またはパッケージの管理時に問題が発生している場合は、このページの既知の問題とその解決策を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c4e68-106">If you are having trouble installing NuGet or managing packages, please take a look through these known issues and their resolutions.</span></span>

> [!Note]
> <span data-ttu-id="c4e68-107">NuGet 4.0 以降、既知の問題は各リリース ノートに記載されています。</span><span class="sxs-lookup"><span data-stu-id="c4e68-107">Starting with NuGet 4.0, known issues are a part of the respective release notes.</span></span>

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a><span data-ttu-id="c4e68-108">NuGet に関する認証の問題は、nuget.exe v3.4.3 が付属している VSTS で提供されています。</span><span class="sxs-lookup"><span data-stu-id="c4e68-108">Authentication issues with NuGet feeds in VSTS with nuget.exe v3.4.3</span></span>

<span data-ttu-id="c4e68-109">**問題:**</span><span class="sxs-lookup"><span data-stu-id="c4e68-109">**Problem:**</span></span>

<span data-ttu-id="c4e68-110">次のコマンドを使用して資格情報を格納すると、個人用アクセス トークンを二重に暗号化することになります。</span><span class="sxs-lookup"><span data-stu-id="c4e68-110">When we use the following command to store the credentials, we end up double encrypting the Personal Access Token.</span></span>

<span data-ttu-id="c4e68-111">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span><span class="sxs-lookup"><span data-stu-id="c4e68-111">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span></span>

<span data-ttu-id="c4e68-112">**回避策:**</span><span class="sxs-lookup"><span data-stu-id="c4e68-112">**Workaround:**</span></span>

<span data-ttu-id="c4e68-113">[-StorePasswordInClearText](../tools/cli-ref-sources.md) オプションを使用して、クリア テキストにパスワードを格納します。</span><span class="sxs-lookup"><span data-stu-id="c4e68-113">Store passwords in clear text using the [-StorePasswordInClearText](../tools/cli-ref-sources.md) option.</span></span>

## <a name="error-installing-packages-with-nuget-34-341"></a><span data-ttu-id="c4e68-114">NuGet 3.4、3.4.1 を使用してパッケージをインストールするときのエラー</span><span class="sxs-lookup"><span data-stu-id="c4e68-114">Error installing packages with NuGet 3.4, 3.4.1</span></span>

<span data-ttu-id="c4e68-115">**問題:**</span><span class="sxs-lookup"><span data-stu-id="c4e68-115">**Problem:**</span></span>

<span data-ttu-id="c4e68-116">NuGet 3.4 および 3.4.1 で NuGet アドインを使用している場合、使用できると報告されているソースがありません。また、構成ウィンドウで新しいソースを追加できません。</span><span class="sxs-lookup"><span data-stu-id="c4e68-116">In NuGet 3.4 and 3.4.1, when using the NuGet add-in, no sources are reported as available and you are unable to add new sources in the configuration window.</span></span> <span data-ttu-id="c4e68-117">その結果、次の画像のようになります。</span><span class="sxs-lookup"><span data-stu-id="c4e68-117">The result is similar to the image below:</span></span>

![ソースがない NuGet の構成](./media/knownIssue-34-NoSources.PNG)

<span data-ttu-id="c4e68-119">`%AppData%\NuGet\` フォルダーの `NuGet.Config` ファイルが誤って空になっています。</span><span class="sxs-lookup"><span data-stu-id="c4e68-119">The `NuGet.Config` file in your `%AppData%\NuGet\` folder has accidentally been emptied.</span></span> <span data-ttu-id="c4e68-120">この問題を解決するには: Visual Studio 2015 を終了し、`%AppData%\NuGet\` フォルダーの `NuGet.Config` ファイルを削除し、Visual Studio を再起動します。</span><span class="sxs-lookup"><span data-stu-id="c4e68-120">To fix this: Close Visual Studio 2015, delete the `NuGet.Config` file in the `%AppData%\NuGet\` folder and restart Visual Studio.</span></span>  <span data-ttu-id="c4e68-121">新しい `NuGet.Config` ファイルが生成され、続行できるようになります。</span><span class="sxs-lookup"><span data-stu-id="c4e68-121">A new `NuGet.Config` file will be generated and you are able to proceed.</span></span>

## <a name="error-installing-packages-with-nuget-27"></a><span data-ttu-id="c4e68-122">NuGet 2.7 を使用してパッケージをインストールするときのエラー</span><span class="sxs-lookup"><span data-stu-id="c4e68-122">Error installing packages with NuGet 2.7</span></span>

<span data-ttu-id="c4e68-123">**問題:**</span><span class="sxs-lookup"><span data-stu-id="c4e68-123">**Problem:**</span></span>

<span data-ttu-id="c4e68-124">NuGet 2.7 以降、アセンブリの参照を含むパッケージをインストールしようとすると、次のように **"入力文字列の形式が正しくありません"** というエラー メッセージを受け取ることがあります。</span><span class="sxs-lookup"><span data-stu-id="c4e68-124">In NuGet 2.7 or above, when you attempt to install any package which contains assembly references, you may receive the error message **"Input string was not in a correct format."**, like below:</span></span>

```ps
install-package log4net
    Installing 'log4net 2.0.0'.
    Successfully installed 'log4net 2.0.0'.
    Adding 'log4net 2.0.0' to Tyson.OperatorUpload.
    Install failed. Rolling back...
    install-package : Input string was not in a correct format.
    At line:1 char:1
        install-package log4net
        ~~~~~~~~~~~~~~~~~~~~~~~
        CategoryInfo : NotSpecified: (:) [Install-Package], FormatException
        FullyQualifiedErrorId : NuGetCmdletUnhandledException,NuGet.PowerShell.Commands.InstallPackageCommand
```

<span data-ttu-id="c4e68-125">システムで `VSLangProj.dll` COM コンポーネントの登録が解除されている場合に、タイプ ライブラリによってこのエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="c4e68-125">This is caused by the type library for the `VSLangProj.dll` COM component being unregistered on your system.</span></span> <span data-ttu-id="c4e68-126">このエラーは、たとえば 2 つのバージョンの Visual Studio が並列でインストールされていて、古い方のバージョンをアンインストールしたときなどに発生します。</span><span class="sxs-lookup"><span data-stu-id="c4e68-126">This can happen, for example, when you have two versions of Visual Studio installed side-by-side and you then uninstall the older version.</span></span> <span data-ttu-id="c4e68-127">その結果、上記の COM ライブラリの登録が誤って解除されることがあります。</span><span class="sxs-lookup"><span data-stu-id="c4e68-127">Doing so may inadvertently unregister the above COM library.</span></span>

<span data-ttu-id="c4e68-128">**解決策:**</span><span class="sxs-lookup"><span data-stu-id="c4e68-128">**Solution:**:</span></span>

<span data-ttu-id="c4e68-129">**管理者特権のプロンプト**からこのコマンドを実行して、`VSLangProj.dll` のタイプ ライブラリを再登録します。</span><span class="sxs-lookup"><span data-stu-id="c4e68-129">Run this command from an **elevated prompt** to re-register the type library for `VSLangProj.dll`</span></span>

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

<span data-ttu-id="c4e68-130">このコマンドが失敗する場合は、その場所にファイルが存在するかどうかを確認してください。</span><span class="sxs-lookup"><span data-stu-id="c4e68-130">If the command fails, check to see if the file exists in that location.</span></span>

<span data-ttu-id="c4e68-131">このエラーの詳細については、この[作業項目](https://nuget.codeplex.com/workitem/3609 "作業項目 3609") を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c4e68-131">For more information about this error, see this [work item](https://nuget.codeplex.com/workitem/3609 "Work item 3609").</span></span>

## <a name="build-failure-after-package-update-in-vs-2012"></a><span data-ttu-id="c4e68-132">VS 2012 のパッケージの更新後のビルド エラー</span><span class="sxs-lookup"><span data-stu-id="c4e68-132">Build failure after package update in VS 2012</span></span>

<span data-ttu-id="c4e68-133">問題: VS 2012 RTM を使用しています。</span><span class="sxs-lookup"><span data-stu-id="c4e68-133">The problem: You are using VS 2012 RTM.</span></span> <span data-ttu-id="c4e68-134">NuGet パッケージを更新すると、"完全にアンインストールできなかったパッケージがあります" というメッセージを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="c4e68-134">When updating NuGet packages, you get this message: "One or more packages could not be completed uninstalled."</span></span> <span data-ttu-id="c4e68-135">また、Visual Studio を再起動するように求められます。</span><span class="sxs-lookup"><span data-stu-id="c4e68-135">and you are prompted to restart Visual Studio.</span></span> <span data-ttu-id="c4e68-136">VS を再起動すると、通常とは異なるビルド エラーを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="c4e68-136">After VS restart, you get weird build errors.</span></span>

<span data-ttu-id="c4e68-137">この原因は、以前のパッケージに含まれる特定のファイルが、バックグラウンドの MSBuild プロセスでロックされていることです。</span><span class="sxs-lookup"><span data-stu-id="c4e68-137">The cause is that certain files in the old packages are locked by a background MSBuild process.</span></span> <span data-ttu-id="c4e68-138">VS の再起動後も、バックグラウンドの MSBuild プロセスで、以前のパッケージに含まれるファイルが継続して使用されているため、ビルド エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="c4e68-138">Even after VS restart, the background MSBuild process still uses the files in the old packages, causing the build failures.</span></span>

<span data-ttu-id="c4e68-139">この問題を解決するには、VS 2012 Update (VS 2012 Update 2 など) をインストールします。</span><span class="sxs-lookup"><span data-stu-id="c4e68-139">The fix is to install VS 2012 Update, e.g. VS 2012 Update 2.</span></span>

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a><span data-ttu-id="c4e68-140">以前のバージョンから最新の NuGet にアップグレードすると、署名の検証エラーが発生する</span><span class="sxs-lookup"><span data-stu-id="c4e68-140">Upgrading to latest NuGet from an older version causes a signature verification error</span></span>

<span data-ttu-id="c4e68-141">VS 2010 SP1 を実行していて、NuGet の以前のバージョンをインストールしている場合、NuGet をアップグレードしようとすると、次のエラー メッセージを受け取ることがあります。</span><span class="sxs-lookup"><span data-stu-id="c4e68-141">If you are running VS 2010 SP1, you might run into the following error message when attempting to upgrade NuGet if you have an older version installed.</span></span>

![Visual Studio 拡張機能インストーラー](./media/Visual-Studio-Extension-Installer.png)

<span data-ttu-id="c4e68-143">ログを表示すると、`SignatureMismatchException` のメンションが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="c4e68-143">When viewing the logs, you might see a mention of a `SignatureMismatchException`.</span></span>

<span data-ttu-id="c4e68-144">これを防ぐには、[Visual Studio 2010 SP1 修正プログラム](http://bit.ly/vsixcertfix)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="c4e68-144">To prevent this from occurring, there is a [Visual Studio 2010 SP1 hotfix](http://bit.ly/vsixcertfix) you can install.</span></span>
<span data-ttu-id="c4e68-145">または、(管理者として Visual Studio を実行しているときに) NuGet をアンインストールし、VS 拡張ギャラリーから NuGet をインストールするだけ、という回避策もあります。</span><span class="sxs-lookup"><span data-stu-id="c4e68-145">Alternatively, the workaround is to simply uninstall NuGet (while running Visual Studio as Administrator) and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="c4e68-146">詳細については、[http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c4e68-146">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a><span data-ttu-id="c4e68-147">Reflector Visual Studio アドインもインストールされている場合、パッケージ マネージャー コンソールから例外がスローされます。</span><span class="sxs-lookup"><span data-stu-id="c4e68-147">Package Manager Console throws an exception when the Reflector Visual Studio Add-In is also installed.</span></span>

<span data-ttu-id="c4e68-148">Reflector VS アドインをインストールしている場合、パッケージ マネージャー コンソールを実行すると、次の例外メッセージが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="c4e68-148">When running the Package Manager console, you may run into the following exception message if you have the Reflector VS Add-in installed.</span></span>

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

<span data-ttu-id="c4e68-149">または</span><span class="sxs-lookup"><span data-stu-id="c4e68-149">or</span></span>

    System.Management.Automation.CmdletInvocationException: Could not load file or assembly 'Scripts\nuget.psm1' or one of its dependencies. <br />The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) ---&gt; System.IO.FileLoadException: Could not load file or <br />assembly 'Scripts\nuget.psm1' or one of its dependencies. The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) <br />---&gt; System.ArgumentException: Illegal characters in path.
       at System.IO.Path.CheckInvalidPathChars(String path)
       at System.IO.Path.Combine(String path1, String path2)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.<AssemblyPaths>d__1.MoveNext()
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.InnerResolveHandler(String name)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.ResolveHandler(Object sender, ResolveEventArgs args)
       at System.AppDomain.OnAssemblyResolveEvent(RuntimeAssembly assembly, String assemblyFullName)
       --- End of inner exception stack trace ---
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadBinaryModule(Boolean trySnapInName, String moduleName, String fileName, <br />Assembly assemblyToLoad, String moduleBase, SessionState ss, String prefix, Boolean loadTypes, Boolean loadFormats, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleNamedInManifest(String moduleName, String moduleBase, <br />Boolean searchModulePath, <br />String prefix, SessionState ss, Boolean loadTypesFiles, Boolean loadFormatFiles, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleManifest(ExternalScriptInfo scriptInfo, ManifestProcessingFlags <br />manifestProcessingFlags, Version version)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModule(String fileName, String moduleBase, String prefix, SessionState ss, <br />Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ImportModuleCommand.ProcessRecord()
       at System.Management.Automation.Cmdlet.DoProcessRecord()
       at System.Management.Automation.CommandProcessor.ProcessRecord()
       --- End of inner exception stack trace ---
       at System.Management.Automation.Runspaces.PipelineBase.Invoke(IEnumerable input)
       at System.Management.Automation.Runspaces.Pipeline.Invoke()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Invoke(String command, Object input, Boolean outputResults)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHostExtensions.ImportModule(PowerShellHost host, String modulePath)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.LoadStartupScripts()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Initialize()
       at NuGetConsole.Implementation.Console.ConsoleDispatcher.Start()
       at NuGetConsole.Implementation.PowerConsoleToolWindow.MoveFocus(FrameworkElement consolePane)

<span data-ttu-id="c4e68-150">解決できるように、アドインの作成者に連絡しました。</span><span class="sxs-lookup"><span data-stu-id="c4e68-150">We've contacted the author of the add-in in the hopes of working out a resolution.</span></span>

<p class="info"><span data-ttu-id="c4e68-151">更新プログラム: 最新バージョンの Reflector 6.5 を使用すると、コンソールでこの例外が発生しないことを確認しました。</span><span class="sxs-lookup"><span data-stu-id="c4e68-151">Update: We have verified that the latest version of Reflector, 6.5, no longer causes this exception in the console.</span></span></p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a><span data-ttu-id="c4e68-152">ObjectSecurity 例外でパッケージ マネージャー コンソールを開くことができない</span><span class="sxs-lookup"><span data-stu-id="c4e68-152">Opening Package Manager Console fails with ObjectSecurity exception</span></span>

<span data-ttu-id="c4e68-153">パッケージ マネージャー コンソールを開くときに、次のエラーが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="c4e68-153">You might see these errors when trying to open the Package Manager Console:</span></span>

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

<span data-ttu-id="c4e68-154">その場合は、[StackOverflow について説明した解決策](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm)に従って解決してください。</span><span class="sxs-lookup"><span data-stu-id="c4e68-154">If so, follow the solution [discussed on StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) to fix them.</span></span>

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a><span data-ttu-id="c4e68-155">ソリューションに InstallShield Limited Edition プロジェクトが含まれている場合、[Add Package Library Reference]\(パッケージ ライブラリ参照の追加\) ダイアログから例外がスローされる</span><span class="sxs-lookup"><span data-stu-id="c4e68-155">The Add Package Library Reference dialog throws an exception if the solution contains InstallShield Limited Edition Project</span></span>

<span data-ttu-id="c4e68-156">ソリューションに 1 つ以上の InstallShield Limited Edition プロジェクトが含まれている場合、**[Add Package Library Reference]\(パッケージ ライブラリ参照の追加\)** ダイアログを開くと、例外がスローされることがわかっています。</span><span class="sxs-lookup"><span data-stu-id="c4e68-156">We have identified that if your solution contains one or more InstallShield Limited Edition project, the **Add Package Library Reference** dialog will throw an exception when opened.</span></span> <span data-ttu-id="c4e68-157">現時点では、InstallShield プロジェクトを削除するかアンロードする以外の回避策がまだありません。</span><span class="sxs-lookup"><span data-stu-id="c4e68-157">There is currently no workaround yet except either removing InstallShield projects or unloading them.</span></span>

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a><span data-ttu-id="c4e68-158">[アンインストール] ボタンが淡色表示されている場合は</span><span class="sxs-lookup"><span data-stu-id="c4e68-158">Uninstall Button Greyed out?</span></span> <span data-ttu-id="c4e68-159">NuGet のインストール/アンインストールに管理者特権が必要</span><span class="sxs-lookup"><span data-stu-id="c4e68-159">NuGet Requires Admin Privileges to Install/Uninstall</span></span>

<span data-ttu-id="c4e68-160">Visual Studio 拡張機能マネージャーを使用して NuGet をアンインストールしようとすると、[アンインストール] ボタンが無効になっていることがあります。</span><span class="sxs-lookup"><span data-stu-id="c4e68-160">If you try to uninstall NuGet via the Visual Studio Extension Manager, you may notice that the Uninstall button is disabled.</span></span> <span data-ttu-id="c4e68-161">NuGet のインストール/アンインストールには管理者特権が必要です。</span><span class="sxs-lookup"><span data-stu-id="c4e68-161">NuGet requires admin access to install and uninstall.</span></span> <span data-ttu-id="c4e68-162">拡張機能をアンインストールするには、管理者として Visual Studio を再起動します。</span><span class="sxs-lookup"><span data-stu-id="c4e68-162">Relaunch Visual Studio as an administrator to uninstall the extension.</span></span> <span data-ttu-id="c4e68-163">NuGet の使用には管理者アクセス権は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="c4e68-163">NuGet does not require admin access to use it.</span></span>

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a><span data-ttu-id="c4e68-164">Windows XP でパッケージ マネージャー コンソールを開こうとするとクラッシュする</span><span class="sxs-lookup"><span data-stu-id="c4e68-164">The Package Manager Console crashes when I open it in Windows XP.</span></span> <span data-ttu-id="c4e68-165">理由</span><span class="sxs-lookup"><span data-stu-id="c4e68-165">What's wrong?</span></span>

<span data-ttu-id="c4e68-166">NuGet には PowerShell 2.0 ランタイムが必要です。</span><span class="sxs-lookup"><span data-stu-id="c4e68-166">NuGet requires Powershell 2.0 runtime.</span></span> <span data-ttu-id="c4e68-167">Windows XP の既定では PowerShell 2.0 がインストールされていません。</span><span class="sxs-lookup"><span data-stu-id="c4e68-167">Windows XP, by default, doesn't have Powershell 2.0.</span></span> <span data-ttu-id="c4e68-168">PowerShell 2.0 ランタイムは、[http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929) からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="c4e68-168">You can download the Powershell 2.0 runtime from [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span></span> <span data-ttu-id="c4e68-169">インストール後に Visual Studio を再起動すると、パッケージ マネージャー コンソールを開くことができるようになります。</span><span class="sxs-lookup"><span data-stu-id="c4e68-169">After you install it, restart Visual Studio and you should be able to open Package Manager Console.</span></span>

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a><span data-ttu-id="c4e68-170">パッケージ マネージャー コンソールが開いていると、Visual Studio 2010 SP1 ベータ版の終了時にクラッシュします。</span><span class="sxs-lookup"><span data-stu-id="c4e68-170">Visual Studio 2010 SP1 Beta crashes on exit if the Package Manager Console is open.</span></span>

<span data-ttu-id="c4e68-171">Visual Studio 2010 SP1 ベータ版をインストールした場合、パッケージ マネージャー コンソールを開いたままにして Visual Studio を終了するとクラッシュすることがあります。</span><span class="sxs-lookup"><span data-stu-id="c4e68-171">If you have installed Visual Studio 2010 SP1 Beta, you may notice that if you leave the Package Manager Console open and close Visual Studio, it will crash.</span></span> <span data-ttu-id="c4e68-172">これは、Visual Studio の既知の問題であり、SP1 RTM リリースで修正される予定です。</span><span class="sxs-lookup"><span data-stu-id="c4e68-172">This is a known issue of Visual Studio and will be fixed in SP1 RTM release.</span></span> <span data-ttu-id="c4e68-173">現在のところは、クラッシュを無視するか、可能であれば SP1 ベータ版をアンインストールしてください。</span><span class="sxs-lookup"><span data-stu-id="c4e68-173">For now, just ignore the crash or uninstall SP1 Beta if you can.</span></span>

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a><span data-ttu-id="c4e68-174">"'metadata' に無効な子要素が含まれています" 例外が発生する</span><span class="sxs-lookup"><span data-stu-id="c4e68-174">The element 'metadata' ... has invalid child element exception occurs</span></span>

<span data-ttu-id="c4e68-175">プレリリース バージョンの NuGet を使用してビルドしたパッケージをインストールすると、そのプロジェクトを含む RTM バージョンの NuGet を実行しているときに、"名前空間 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' の要素 'metadata' に無効な子要素が含まれています" というエラー メッセージが発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="c4e68-175">If you installed packages built with a pre-release version of NuGet, you might encounter an error message stating "The element 'metadata' in namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' has invalid child element" when running the RTM version of NuGet with that project.</span></span> <span data-ttu-id="c4e68-176">各パッケージをアンインストールし、RTM バージョンの NuGet を使用して再インストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4e68-176">You need to uninstall and then re-install each package using the RTM version of NuGet.</span></span>

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a><span data-ttu-id="c4e68-177">インストールまたはアンインストールをしようとすると、"既に存在するファイルを作成することはできません。" というエラーが発生する</span><span class="sxs-lookup"><span data-stu-id="c4e68-177">Attempting to install or uninstall results in the error "Cannot create a file when that file already exists."</span></span>

<span data-ttu-id="c4e68-178">Visual Studio 拡張機能は、なんらかの理由で、VSIX 拡張機能をアンインストールしたにもかかわらず一部のファイルが残っているという正常ではない状態になっています。</span><span class="sxs-lookup"><span data-stu-id="c4e68-178">For some reason, Visual Studio extensions can get in a weird state where you've uninstalled the VSIX extension, but some files were left behind.</span></span> <span data-ttu-id="c4e68-179">この問題を解決するには:</span><span class="sxs-lookup"><span data-stu-id="c4e68-179">To work around this issue:</span></span>

1. <span data-ttu-id="c4e68-180">Visual Studio の終了</span><span class="sxs-lookup"><span data-stu-id="c4e68-180">Exit Visual Studio</span></span>
1. <span data-ttu-id="c4e68-181">次のフォルダーを開きます (コンピューターの別のドライブにある可能性があります)</span><span class="sxs-lookup"><span data-stu-id="c4e68-181">Open the following folder (it might be on a different drive on your machine)</span></span>

    <span data-ttu-id="c4e68-182">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span><span class="sxs-lookup"><span data-stu-id="c4e68-182">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span></span>

1. <span data-ttu-id="c4e68-183">拡張子が *.deleteme* のファイルをすべて削除します。</span><span class="sxs-lookup"><span data-stu-id="c4e68-183">Delete all the files with the *.deleteme* extensions.</span></span>
1. <span data-ttu-id="c4e68-184">Visual Studio を再起動します</span><span class="sxs-lookup"><span data-stu-id="c4e68-184">Re-open Visual Studio</span></span>

<span data-ttu-id="c4e68-185">これらの手順を実行すると、続行できるようになります。</span><span class="sxs-lookup"><span data-stu-id="c4e68-185">After following these steps, you should be able to continue.</span></span>

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a><span data-ttu-id="c4e68-186">まれに、コード分析を有効にしてコンパイルするとエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="c4e68-186">In rare cases, compiling with Code Analysis turned on causes error.</span></span>

<span data-ttu-id="c4e68-187">パッケージ マネージャー コンソールを使用して FluentNHibernate をインストールし、"コード分析" を有効にしてプロジェクトをコンパイルすると、次のエラーが発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="c4e68-187">You might get the following error if you installs FluentNHibernate with the Package Manager console and then compile your project with "Code Analysis" turned on.</span></span>

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

<span data-ttu-id="c4e68-188">既定では FluentNHibernate には NHibernate 3.0.0.2001 が必要です。</span><span class="sxs-lookup"><span data-stu-id="c4e68-188">By default, FluentNHibernate requires NHibernate 3.0.0.2001.</span></span> <span data-ttu-id="c4e68-189">ただし、設計上、NuGet ではプロジェクトに NHibernate 3.0.0.4000 がインストールされ、適切なバインディングのリダイレクトが追加されるので、機能します。</span><span class="sxs-lookup"><span data-stu-id="c4e68-189">However, by design NuGet will install NHibernate 3.0.0.4000 in your project and add the appropriate binding redirects so that it will work.</span></span> <span data-ttu-id="c4e68-190">コード分析が有効でない場合、プロジェクトは正常にコンパイルされます。</span><span class="sxs-lookup"><span data-stu-id="c4e68-190">You project will compile just fine if code analysis is not turned on.</span></span> <span data-ttu-id="c4e68-191">コンパイラとは対照的に、コード分析ツールは 3.0.0.2001 ではなく 3.0.0.4000 を使用するようにバインディングのリダイレクトに適切に従っていません。</span><span class="sxs-lookup"><span data-stu-id="c4e68-191">In contrast to the compiler, code analysis tool doesn't properly follow the binding redirects to use 3.0.0.4000 instead of 3.0.0.2001.</span></span> <span data-ttu-id="c4e68-192">この問題を回避するには、NHibernate 3.0.0.2001 をインストールするか、次のようにコンパイラと同様に動作するようにコード分析ツールに指示します。</span><span class="sxs-lookup"><span data-stu-id="c4e68-192">You can work around the issue by either installing NHibernate 3.0.0.2001 or tell the code analysis tool to behave the same as the compiler by doing the following:</span></span>

1. <span data-ttu-id="c4e68-193">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span><span class="sxs-lookup"><span data-stu-id="c4e68-193">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span></span>
1. <span data-ttu-id="c4e68-194">FxCopCmd.exe.config を開き、`AssemblyReferenceResolveMode` を `StrongName` から `StrongNameIgnoringVersion` に変更します。</span><span class="sxs-lookup"><span data-stu-id="c4e68-194">Open FxCopCmd.exe.config and change `AssemblyReferenceResolveMode` from `StrongName` to `StrongNameIgnoringVersion`.</span></span>
1. <span data-ttu-id="c4e68-195">変更を保存し、プロジェクトをリビルドします。</span><span class="sxs-lookup"><span data-stu-id="c4e68-195">Save the change and rebuild your project.</span></span>

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a><span data-ttu-id="c4e68-196">Write-Error コマンドが install.ps1/uninstall.ps1/init.ps1 内で動作しない</span><span class="sxs-lookup"><span data-stu-id="c4e68-196">Write-Error command doesn't work inside install.ps1/uninstall.ps1/init.ps1</span></span>

<span data-ttu-id="c4e68-197">これは既知の問題です。</span><span class="sxs-lookup"><span data-stu-id="c4e68-197">This is a known issue.</span></span> <span data-ttu-id="c4e68-198">Write-Error を呼び出す代わりに、throw を呼び出してみてください。</span><span class="sxs-lookup"><span data-stu-id="c4e68-198">Instead of calling Write-Error, try calling throw.</span></span>

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a><span data-ttu-id="c4e68-199">Windows 2003 で制限されたアクセス権を使用して NuGet をインストールすると、Visual Studio がクラッシュすることがある</span><span class="sxs-lookup"><span data-stu-id="c4e68-199">Installing NuGet with restricted access on Windows 2003 can crash Visual Studio</span></span>

<span data-ttu-id="c4e68-200">Visual Studio 拡張機能マネージャーを使用して、管理者特権を使用せずに NuGet をインストールしようとすると、既定で [制限されたアクセス権でこのプログラムを実行する] がオンの [実行] ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c4e68-200">When attempting to install NuGet using the Visual Studio Extension Manager and not running as an administrator, the &#8220;Run As&#8221; dialog is displayed with the checkbox labeled &#8220;Run this program with restricted access&#8221; checked by default.</span></span>

![制限付きの実行ダイアログ](./media/RunAsRestricted.png)

<span data-ttu-id="c4e68-202">オンのまま [OK] をクリックすると、Visual Studio がクラッシュします。</span><span class="sxs-lookup"><span data-stu-id="c4e68-202">Clicking OK with that checked crashes Visual Studio.</span></span> <span data-ttu-id="c4e68-203">このオプションをオフにしてから NuGet をインストールしてください。</span><span class="sxs-lookup"><span data-stu-id="c4e68-203">Make sure to uncheck that option before installing NuGet.</span></span>

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a><span data-ttu-id="c4e68-204">NuGet for Windows Phone Tools をアンインストールできない</span><span class="sxs-lookup"><span data-stu-id="c4e68-204">Cannot uninstall NuGet for Windows Phone Tools</span></span>

<span data-ttu-id="c4e68-205">Windows Phone Tools は Visual Studio 拡張機能マネージャーをサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="c4e68-205">Windows Phone Tools does not have support for the Visual Studio Extension Manager.</span></span> <span data-ttu-id="c4e68-206">NuGet をアンインストールするには、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="c4e68-206">In order to uninstall NuGet, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a><span data-ttu-id="c4e68-207">NuGet パッケージ ID の大文字と小文字を変更すると、パッケージの復元が中断する</span><span class="sxs-lookup"><span data-stu-id="c4e68-207">Changing the capitalization of NuGet package IDs breaks package restore</span></span>

<span data-ttu-id="c4e68-208">[この GitHub の問題](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932)で議論されているように、NuGet パッケージの大文字と小文字を変更することは NuGet でサポートされていますが、既存の大文字と小文字が異なるパッケージがローカル パッケージ キャッシュに存在する場合、パッケージの復元時に複雑な状況になります。</span><span class="sxs-lookup"><span data-stu-id="c4e68-208">As discussed at length on [this GitHub issue](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), changing the capitalization of NuGet packages can be done by NuGet support, but causes complications during package restore for users who have existing, differently-cased, packages in their local package cache.</span></span> <span data-ttu-id="c4e68-209">ビルド時のパッケージの復元で発生する可能性のある中断について、パッケージの既存のユーザーに伝える方法がある場合にのみ、大文字と小文字の変更を要求することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c4e68-209">We recommend only requesting a case change when you have a way to communicate with existing users of your package about the break that may occur to their build-time package restore.</span></span>

## <a name="reporting-issues"></a><span data-ttu-id="c4e68-210">レポートの問題</span><span class="sxs-lookup"><span data-stu-id="c4e68-210">Reporting issues</span></span>

<span data-ttu-id="c4e68-211">NuGet の問題を報告するには、[https://github.com/nuget/home/issues](https://github.com/nuget/home/issues) にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="c4e68-211">To report NuGet issues, visit [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span></span>
