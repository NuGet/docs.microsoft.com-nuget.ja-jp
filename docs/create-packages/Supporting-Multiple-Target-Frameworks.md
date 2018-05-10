---
title: NuGet パッケージの複数バージョン対応
description: 1 つの NuGet パッケージ内から複数の .NET Framework バージョンに対応するためのさまざま方法の説明。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 09/27/2017
ms.topic: conceptual
ms.openlocfilehash: d1a64c61954381b7ab3a7ecc8aa5a812cfa14e8b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="supporting-multiple-net-framework-versions"></a>複数の .NET Framework バージョンのサポート

*NuGet 4.0+ を使用する .NET Core プロジェクトについては、「[NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md)」 (MSBuild ターゲットとしての NuGet pack および restore) をご覧ください。複数バージョン対応に関する詳細があります。*

多くのライブラリは、特定のバージョンの .NET Framework に対応しています。 たとえば、あるバージョンのライブラリは UWP に固有であり、別のバージョンは .NET Framework 4.6 の機能を活用します。

それに対応するために、NuGet では、「[パッケージを作成する](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)」に説明がある、規則ベースの作業ディレクトリ方法を利用するとき、1 つのパッケージに同じライブラリの複数のバージョンを置くことができます。

## <a name="framework-version-folder-structure"></a>フレームワーク バージョンのフォルダー構造

1 つだけのバージョンのライブラリを含むパッケージまたは複数のフレームワークを対象とするパッケージをビルドするときは常に、小文字と大文字を区別するフレームワーク名を利用し、`lib` の下にサブフォルダーを作ります。次の規則を利用します。

    lib\{framework name}[{version}]

サポートされている名前の完全一覧については、[ターゲット フレームワーク参照](../reference/target-frameworks.md#supported-frameworks)を参照してください。

フレームワークに固有ではないライブラリ バージョンは、ルート `lib` フォルダーに直接置かないでください。 (この機能は `packages.config` でのみサポートされていました。) それを行うと、あらゆるターゲット フレームワークに対応するようになり、どこでもインストールできてしまいます。その結果、予想外のランタイム エラーが発生します。 ルート フォルダー (`lib\abc.dll` など) またはサブフォルダー (`lib\abc\abc.dll` など) へのアセンブリ追加は非推奨となりました。PackagesReference 形式を使用するときは無視されます。

たとえば、次のフォルダー構造では、フレームワーク固有の 4 つのバージョンのアセンブリがサポートされています。

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

パッケージのビルド時、これらすべてのファイルを簡単に含めるには、`.nuspec` の `<files>` セクションに再帰的 `**` ワイルドカードを使用します。

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>アーキテクチャ固有フォルダー

アーキテクチャ固有のアセンブリがあるとき、つまり、個々のアセンブリが ARM、x86、x64 を対象とするとき、`runtimes` という名前のフォルダーの `{platform}-{architecture}\lib\{framework}` または `{platform}-{architecture}\native` という名前のサブフォルダー内にそれを置く必要があります。 たとえば、次のフォルダー構造は、Windows 10 と `uap10.0` フレームワークを対象とするネイティブ DLL とマネージ DLL の両方に対応します。

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

`.nuspec` マニフェストでこれらのファイルを参照する例については、「[Create UWP Packages](../guides/create-uwp-packages.md)」 (UWP パッケージの作成) を参照してください。

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>プロジェクトでアセンブリ バージョンとターゲット フレームワークを組み合わせる

複数のアセンブリ バージョンを含むパッケージを NuGet がインストールすると、アセンブリのフレームワーク名とプロジェクトのターゲット フレームワークの照合が試行されます。

一致が見つからない場合、プロジェクトのターゲット フレームワークと同じかそれより下のバージョンの中で最も上のバージョンのアセンブリがコピーされます。 互換性のあるアセンブリが見つからない場合、エラー メッセージが返されます。

たとえば、パッケージに次のフォルダー構造があるとします。

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

.NET Framework 4.6 を対象とするプロジェクトにこのパッケージをインストールすると、NuGet は `net45` フォルダーにアセンブリをインストールします。4.6 以下で利用できる最も上のバージョンであるためです。

一方、プロジェクトが .NET Framework 4.6.1 を対象とする場合、NuGet は `net461` フォルダーにアセンブリをインストールします。

プロジェクトが .NET Framework 4.0 以前を対象とする場合、NuGet はエラー メッセージを出し、互換性のあるアセンブリが見つからないことを伝えます。

## <a name="grouping-assemblies-by-framework-version"></a>フレームワーク バージョン別にアセンブリをグループ化する

NuGet は、パッケージ内の 1 つだけのライブラリ フォルダーからアセンブリをコピーします。 たとえば、パッケージに次のフォルダー構造があるとします。

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

.NET Framework 4.5 を対象とするプロジェクトにパッケージがインストールされるとき、インストールされる唯一のアセンブリは `MyAssembly.dll` (v2.0) です。 `MyAssembly.Core.dll` (v1.0) はインストールされません。`net45` フォルダーの一覧にないためです。 `MyAssembly.Core.dll` が `MyAssembly.dll` のバージョン 2.0 に結合されている可能性があるため、NuGet はこのように動作します。

.NET Framework 4.5 で `MyAssembly.Core.dll` をインストールする場合、`net45` フォルダーにコピーを置きます。

## <a name="grouping-assemblies-by-framework-profile"></a>フレームワーク プロファイル別にアセンブリをグループ化する

NuGet ではまた、ダッシュとプロファイル名をフォルダーの最後に付けることで特定のフレームワーク プロファイルを対象にすることができます。

    lib\{framework name}-{profile}

サポートされているプロファイルは次のとおりです。

- `client`: Client Profile
- `full`: Full Profile
- `wp`: Windows Phone
- `cf`: Compact Framework

## <a name="determining-which-nuget-target-to-use"></a>使用する NuGet ターゲットを決定する

ポータブル クラス ライブラリを対象とするライブラリをパッケージ化するとき、フォルダー名と `.nuspec` ファイルで使用する NuGet ターゲットの決定にはこつが要ります。PCL のサブセットのみを対象とする場合は特にそうです。 次の外部リソースが役立ちます。

- [.NET のフレームワーク プロファイル](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)
- [ポータブル クラス ライブラリ プロファイル](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): PCL プロファイルとそれと同等の NuGet ターゲットを列挙するテーブル
- [ポータブル クラス ライブラリ プロファイル ツール](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): システムで利用できる PCL プロファイルを決定するためのコマンド ライン ツール

## <a name="content-files-and-powershell-scripts"></a>コンテンツ ファイルと PowerShell スクリプト

> [!Warning]
> 変更可能なコンテンツ ファイルとスクリプト実行は `packages.config` 形式のみで利用できます。これらは、他のすべての形式を使用するときは非推奨とされます。また、新しいパッケージにはこれらを使用しないでください。

`packages.config` では、コンテンツ ファイルと PowerShell スクリプトを、`content` フォルダーと `tools` フォルダー内で同じフォルダー規則を使用し、ターゲット フレームワーク別にグループ化できます。 例:

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

フレームワーク フォルダーを空のまま残す場合、NuGet はアセンブリ参照やコンテンツ ファイルを追加せず、そのフレームワークの PowerShell スクリプトを実行しません。

> [!Note]
> `init.ps1` はソリューション レベルで実行され、プロジェクトに依存しないため、`tools` フォルダーの下に直接置く必要があります。 フレームワーク フォルダーの下に置いた場合は無視されます。
