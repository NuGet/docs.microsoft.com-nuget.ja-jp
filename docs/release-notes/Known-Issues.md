---
title: 既知の問題
description: 認証、パッケージのインストール、ツールなど、NuGet に関する既知の問題。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fc338ba3810a125f638a937cf14456bf519a24a8
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548475"
---
# <a name="known-issues-with-nuget"></a>NuGet に関する既知の問題

繰り返し報告されている NuGet に関する最も一般的な問題について説明します。 NuGet のインストール時またはパッケージの管理時に問題が発生している場合は、このページの既知の問題とその解決策を参照してください。

> [!Note]
> NuGet 4.0 以降、既知の問題は各リリース ノートに記載されています。

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a>NuGet に関する認証の問題は、nuget.exe v3.4.3 が付属している VSTS で提供されています。

**問題:**

次のコマンドを使用して資格情報を格納すると、個人用アクセス トークンを二重に暗号化することになります。

$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT

**回避策:**

[-StorePasswordInClearText](../tools/cli-ref-sources.md) オプションを使用して、クリア テキストにパスワードを格納します。

## <a name="error-installing-packages-with-nuget-34-341"></a>NuGet 3.4、3.4.1 を使用してパッケージをインストールするときのエラー

**問題:**

NuGet 3.4 および 3.4.1 で NuGet アドインを使用している場合、使用できると報告されているソースがありません。また、構成ウィンドウで新しいソースを追加できません。 その結果、次の画像のようになります。

![ソースがない NuGet の構成](./media/knownIssue-34-NoSources.PNG)

`%AppData%\NuGet\` (Windows) フォルダーまたは `~/.nuget/` (Mac/Linux) フォルダーの `NuGet.Config` ファイルが誤って空になります。 この問題を解決するには、Visual Studio を終了し (Windows で該当する場合)、`NuGet.Config` ファイルを削除し、操作をやり直します。 NuGet から新しい `NuGet.Config` が生成され、続行できるようになります。

## <a name="error-installing-packages-with-nuget-27"></a>NuGet 2.7 を使用してパッケージをインストールするときのエラー

**問題:**

NuGet 2.7 以降、アセンブリの参照を含むパッケージをインストールしようとすると、次のように **"入力文字列の形式が正しくありません"** というエラー メッセージを受け取ることがあります。

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

システムで `VSLangProj.dll` COM コンポーネントの登録が解除されている場合に、タイプ ライブラリによってこのエラーが発生します。 このエラーは、たとえば 2 つのバージョンの Visual Studio が並列でインストールされていて、古い方のバージョンをアンインストールしたときなどに発生します。 その結果、上記の COM ライブラリの登録が誤って解除されることがあります。

**解決策:**

**管理者特権のプロンプト**からこのコマンドを実行して、`VSLangProj.dll` のタイプ ライブラリを再登録します。

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

このコマンドが失敗する場合は、その場所にファイルが存在するかどうかを確認してください。

このエラーの詳細については、この[作業項目](https://nuget.codeplex.com/workitem/3609 "作業項目 3609") を参照してください。

## <a name="build-failure-after-package-update-in-vs-2012"></a>VS 2012 のパッケージの更新後のビルド エラー

問題: VS 2012 RTM を使用しています。 NuGet パッケージを更新すると、"完全にアンインストールできなかったパッケージがあります" というメッセージを受け取ります。 また、Visual Studio を再起動するように求められます。 VS を再起動すると、通常とは異なるビルド エラーを受け取ります。

この原因は、以前のパッケージに含まれる特定のファイルが、バックグラウンドの MSBuild プロセスでロックされていることです。 VS の再起動後も、バックグラウンドの MSBuild プロセスで、以前のパッケージに含まれるファイルが継続して使用されているため、ビルド エラーが発生します。

この問題を解決するには、VS 2012 Update (VS 2012 Update 2 など) をインストールします。

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a>以前のバージョンから最新の NuGet にアップグレードすると、署名の検証エラーが発生する

VS 2010 SP1 を実行していて、NuGet の以前のバージョンをインストールしている場合、NuGet をアップグレードしようとすると、次のエラー メッセージを受け取ることがあります。

![Visual Studio 拡張機能インストーラー](./media/Visual-Studio-Extension-Installer.png)

ログを表示すると、`SignatureMismatchException` のメンションが表示されることがあります。

これを防ぐには、[Visual Studio 2010 SP1 修正プログラム](http://bit.ly/vsixcertfix)をインストールします。
または、(管理者として Visual Studio を実行しているときに) NuGet をアンインストールし、VS 拡張ギャラリーから NuGet をインストールするだけ、という回避策もあります。  詳細については、「[http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)」を参照してください。

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a>Reflector Visual Studio アドインもインストールされている場合、パッケージ マネージャー コンソールから例外がスローされます。

Reflector VS アドインをインストールしている場合、パッケージ マネージャー コンソールを実行すると、次の例外メッセージが表示されることがあります。

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

または

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

解決できるように、アドインの作成者に連絡しました。

<p class="info">更新プログラム: 最新バージョンの Reflector 6.5 を使用すると、コンソールでこの例外が発生しないことを確認しました。</p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a>ObjectSecurity 例外でパッケージ マネージャー コンソールを開くことができない

パッケージ マネージャー コンソールを開くときに、次のエラーが表示されることがあります。

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

その場合は、[StackOverflow について説明した解決策](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm)に従って解決してください。

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a>ソリューションに InstallShield Limited Edition プロジェクトが含まれている場合、[Add Package Library Reference]\(パッケージ ライブラリ参照の追加\) ダイアログから例外がスローされる

ソリューションに 1 つ以上の InstallShield Limited Edition プロジェクトが含まれている場合、**[Add Package Library Reference]\(パッケージ ライブラリ参照の追加\)** ダイアログを開くと、例外がスローされることがわかっています。 現時点では、InstallShield プロジェクトを削除するかアンロードする以外の回避策がまだありません。

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a>[アンインストール] ボタンが淡色表示されている場合は NuGet のインストール/アンインストールに管理者特権が必要

Visual Studio 拡張機能マネージャーを使用して NuGet をアンインストールしようとすると、[アンインストール] ボタンが無効になっていることがあります。 NuGet のインストール/アンインストールには管理者特権が必要です。 拡張機能をアンインストールするには、管理者として Visual Studio を再起動します。 NuGet の使用には管理者アクセス権は必要ありません。

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a>Windows XP でパッケージ マネージャー コンソールを開こうとするとクラッシュする 理由

NuGet には PowerShell 2.0 ランタイムが必要です。 Windows XP の既定では PowerShell 2.0 がインストールされていません。 Powershell 2.0 ランタイムは [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929) からダウンロードできます。 インストール後に Visual Studio を再起動すると、パッケージ マネージャー コンソールを開くことができるようになります。

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a>パッケージ マネージャー コンソールが開いていると、Visual Studio 2010 SP1 ベータ版の終了時にクラッシュします。

Visual Studio 2010 SP1 ベータ版をインストールした場合、パッケージ マネージャー コンソールを開いたままにして Visual Studio を終了するとクラッシュすることがあります。 これは、Visual Studio の既知の問題であり、SP1 RTM リリースで修正される予定です。 現在のところは、クラッシュを無視するか、可能であれば SP1 ベータ版をアンインストールしてください。

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a>"'metadata' に無効な子要素が含まれています" 例外が発生する

プレリリース バージョンの NuGet を使用してビルドしたパッケージをインストールすると、そのプロジェクトを含む RTM バージョンの NuGet を実行しているときに、"名前空間 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' の要素 'metadata' に無効な子要素が含まれています" というエラー メッセージが発生することがあります。 各パッケージをアンインストールし、RTM バージョンの NuGet を使用して再インストールする必要があります。

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a>インストールまたはアンインストールをしようとすると、"既に存在するファイルを作成することはできません。" というエラーが発生する

Visual Studio 拡張機能は、なんらかの理由で、VSIX 拡張機能をアンインストールしたにもかかわらず一部のファイルが残っているという正常ではない状態になっています。 この問題を解決するには:

1. Visual Studio の終了
1. 次のフォルダーを開きます (コンピューターの別のドライブにある可能性があります)

    C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\

1. 拡張子が *.deleteme* のファイルをすべて削除します。
1. Visual Studio を再起動します

これらの手順を実行すると、続行できるようになります。

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a>まれに、コード分析を有効にしてコンパイルするとエラーが発生します。

パッケージ マネージャー コンソールを使用して FluentNHibernate をインストールし、"コード分析" を有効にしてプロジェクトをコンパイルすると、次のエラーが発生することがあります。

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

既定では FluentNHibernate には NHibernate 3.0.0.2001 が必要です。 ただし、設計上、NuGet ではプロジェクトに NHibernate 3.0.0.4000 がインストールされ、適切なバインディングのリダイレクトが追加されるので、機能します。 コード分析が有効でない場合、プロジェクトは正常にコンパイルされます。 コンパイラとは対照的に、コード分析ツールは 3.0.0.2001 ではなく 3.0.0.4000 を使用するようにバインディングのリダイレクトに適切に従っていません。 この問題を回避するには、NHibernate 3.0.0.2001 をインストールするか、次のようにコンパイラと同様に動作するようにコード分析ツールに指示します。

1. Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*
1. FxCopCmd.exe.config を開き、`AssemblyReferenceResolveMode` を `StrongName` から `StrongNameIgnoringVersion` に変更します。
1. 変更を保存し、プロジェクトをリビルドします。

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a>Write-Error コマンドが install.ps1/uninstall.ps1/init.ps1 内で動作しない

これは既知の問題です。 Write-Error を呼び出す代わりに、throw を呼び出してみてください。

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a>Windows 2003 で制限されたアクセス権を使用して NuGet をインストールすると、Visual Studio がクラッシュすることがある

Visual Studio 拡張機能マネージャーを使用して、管理者特権を使用せずに NuGet をインストールしようとすると、既定で [制限されたアクセス権でこのプログラムを実行する] がオンの [実行] ダイアログが表示されます。

![制限付きの実行ダイアログ](./media/RunAsRestricted.png)

オンのまま [OK] をクリックすると、Visual Studio がクラッシュします。 このオプションをオフにしてから NuGet をインストールしてください。

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a>NuGet for Windows Phone Tools をアンインストールできない

Windows Phone Tools は Visual Studio 拡張機能マネージャーをサポートしていません。 NuGet をアンインストールするには、次のコマンドを実行します。

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a>NuGet パッケージ ID の大文字と小文字を変更すると、パッケージの復元が中断する

[この GitHub の問題](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932)で議論されているように、NuGet ではパッケージの大文字と小文字の変更がサポートされていますが、自分の "*グローバル パッケージ*" フォルダーに大文字と小文字が異なるパッケージを既に持っているユーザーがいた場合、パッケージを復元する際に困難な状況が発生します。 ビルド時のパッケージの復元で発生する可能性のある中断について、パッケージの既存のユーザーに伝える方法がある場合にのみ、大文字と小文字の変更を要求することをお勧めします。

## <a name="reporting-issues"></a>レポートの問題

NuGet の問題を報告するには、[https://github.com/nuget/home/issues](https://github.com/nuget/home/issues) にアクセスしてください。
