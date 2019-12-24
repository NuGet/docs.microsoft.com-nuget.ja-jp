---
title: NuGet project.json ファイルと UWP プロジェクト
description: project.json ファイルを使用してユニバーサル Windows プラットフォーム (UWP) プロジェクトで NuGet の依存関係を追跡する方法の説明。
author: karann-msft
ms.author: karann
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: ac3c137dd0ba50571737093eef11c8ab0ef932b2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548665"
---
# <a name="projectjson-and-uwp"></a>project.json および UWP

> [!Important]
> このコンテンツは非推奨とされます。 プロジェクトは、`packages.config` または PackageReference 形式のいずれかを使用する必要があります。

このドキュメントでは、NuGet 3 + (Visual Studio 2015 以降) の機能を採用するパッケージの構造について説明します。 `.nuspec` の `minClientVersion` プロパティを使用して、3.1 に設定することで、ここで説明する機能が必要であることを示すことができます。

## <a name="adding-uwp-support-to-an-existing-package"></a>既存のパッケージへの UWP サポートの追加

既存のパッケージがあり、UWP アプリケーションのサポートを追加する場合、ここで説明するパッケージ化形式を採用する必要はありません。 説明されている機能が必要で、NuGet クライアントをバージョン 3+ に更新したクライアントでのみ使用する場合に、この形式を採用する必要があります。

## <a name="i-already-target-netcore45"></a>netcore45 が既にターゲットとなっている

既に `netcore45` がターゲットとなっており、ここに示す機能を利用する必要がない場合は、何もする必要はありません。 `netcore45` パッケージは UWP アプリケーションで使用することができます。

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a>Windows 10 固有の API を活用したい

この場合は、パッケージに `uap10.0` ターゲット フレームワーク モニカー (TFM または TxM) を追加する必要があります。 パッケージで新しいフォルダーを作成し、そのフォルダーに、Windows 10 で動作するようにコンパイルされたアセンブリを追加します。

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a>Windows 10 固有の API は必要ないが、新しい .NET 機能が必要であるか netcore45 がまだ存在しない

この場合は、パッケージに `dotnet` TxM を追加します。 他の TxMs とは異なり、`dotnet` ではセキュリティ、外部からのアクセスやプラットフォームは暗黙的に指定されません。 これは、依存関係が動作するプラットフォームでパッケージが動作することを示しています。 `dotnet` TxM でパッケージをビルドする場合、`System.Text` や `System.Xml` など、依存する BCL パッケージを定義する必要があるため、`.nuspec` にはさらに多くの TxM 固有の依存関係が存在する可能性があります。これらの依存関係が動作する場所で、パッケージが動作する場所が定義されます。

### <a name="how-do-i-find-out-my-dependencies"></a>依存関係を確認する方法

次のように、リストする依存関係を確認する方法は 2 つあります。

1. [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) という**サードパーティ** ツールを使用します。 このツールはプロセスを自動化し、ビルドに依存するパッケージで `.nuspec` ファイルを更新します。 NuGet パッケージの [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/) から入手できます。

1. (難しい方法) `ILDasm` を使用して、`.dll` で、実行時に実際に必要となるアセンブリを確認します。 次に、それぞれ元の NuGet パッケージを判別します。

`dotnet` TxM をサポートするパッケージの作成に役立つ機能の詳細については、[`project.json`](project-json.md) に関するトピックを参照してください。

> [!Important]
> パッケージを PCL プロジェクトで動作させる場合は、警告や潜在的な互換性の問題を回避するために、`dotnet` フォルダーを作成することを強くお勧めします。

## <a name="directory-structure"></a>ディレクトリの構造

この形式を使用する NuGet パッケージには、次のよく知られているフォルダーとビヘイビアーがあります。

| フォルダー | ビヘイビアー |
| --- | --- |
| Build | このフォルダーには MSBuild ターゲットおよびプロパティ ファイルが含まれ、異なる方法でプロジェクトに統合されますが、それ以外は変わりません。 |
| Tools | `install.ps1` および `uninstall.ps1` は実行されません。 `init.ps1` は従来どおり動作します。 |
| Content | コンテンツは、ユーザーのプロジェクトに自動的にコピーされません。 プロジェクトへのコンテンツの追加サポートは、今後のリリースで予定されています。 |
| Lib | 多くのパッケージに対して、`lib` は NuGet 2.x の場合と同じように動作しますが、内部で使用できる名前に関するオプションが拡張されており、パッケージを使用する際に正しいサブフォルダーを選択するためのロジックが改善されています。 ただし、`ref` と組み合わせて使用する場合、`lib` フォルダーには、`ref` フォルダーのアセンブリで定義されたセキュリティ、外部からのアクセスを実装するアセンブリが含まれます。 |
| Ref | `ref` は省略可能なフォルダーであり、ここには、コンパイル対象のアプリケーションのパブリック公開領域 (パブリック型とメソッド) を定義する .NET アセンブリが含まれます。 このフォルダー内のアセンブリには実装が存在しない可能性があり、単にコンパイラのセキュリティ、外部からのアクセスを定義する場合に使用されます。 パッケージに `ref` フォルダーがない場合は、`lib` が参照アセンブリと実装アセンブリの両方になります。 |
| Runtimes | `runtimes` は省略可能なフォルダーであり、ここには CPU アーキテクチャや OS 固有またはその他のプラットフォームに依存するバイナリなど、OS 固有のコードが含まれます。 |

## <a name="msbuild-targets-and-props-files-in-packages"></a>パッケージ内の MSBuild ターゲットおよびプロパティ ファイル

NuGet パッケージには `.targets` および `.props` ファイルを含めることができます。これらのファイルは、パッケージのインストール先となる MSBuild プロジェクトにインポートされます。 NuGet 2.x では、これは `<Import>` ステートメントを `.csproj` ファイルに挿入することで行われていました。NuGet 3.0 では、特定の "プロジェクトへのインストール" アクションはありません。 代わりに、パッケージの復元プロセスで `[projectname].nuget.props` および `[projectname].NuGet.targets` という 2 つのファイルが記述されます。

MSBuild はこれら 2 つのファイルを検索することを認識しており、プロジェクトのビルド プロセスの開始および終了が近づいたときにこれらのファイルを自動的にインポートします。 これは NuGet 2.x とよく似たビヘイビアーを提供しますが、*この場合、ターゲット/プロパティ ファイルの順序が保証されない*という 1 つの大きな違いがあります。 ただし、MSBuild では、`<Target>` 定義の `BeforeTargets` および `AfterTargets` 属性を使用してターゲットの順序を指定する方法が提供されます (「[Target 要素 (MSBuild)](/visualstudio/msbuild/target-element-msbuild)」を参照)。

## <a name="lib-and-ref"></a>Lib および Ref

NuGet v3 では、`lib` フォルダーのビヘイビアーに大幅な変更はありません。 ただし、すべてのアセンブリは TxM にちなんだ名前の付いたサブフォルダー内にある必要があり、`lib` フォルダーの直下に配置できなくなりました。 TxM は、パッケージ内の指定された資産の動作対象として想定されるプラットフォームの名前です。 論理的には、ターゲット フレームワーク モニカー (TFM) を拡張したものです。たとえば、`net45`、`net46`、`netcore50`、および `dnxcore50` はすべて TxM の例です (「[Target Frameworks](../reference/target-frameworks.md)」 (ターゲット フレームワーク) を参照)。 TxM は、フレームワーク (TFM) と他のプラットフォーム固有のセキュリティ、外部からのアクセスを表す場合があります。 たとえば、UWP TxM (`uap10.0`) は、.NET のセキュリティ、外部からのアクセスと、UWP アプリケーションの Windows のセキュリティ、外部からのアクセスを表します。

lib 構造の例を以下に示します。

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

`lib` フォルダーには、実行時に使用されるアセンブリが含まれます。 ほとんどのパッケージでは、各ターゲット TxM の `lib` の下のフォルダーはすべて必要になります。

## <a name="ref"></a>Ref

場合によっては、コンパイル時に異なるアセンブリを使用する必要があります (現時点では、.NET 参照アセンブリでこれを行います)。 このような場合は、`ref` ("参照アセンブリ" の省略形) と呼ばれるトップ レベルのフォルダーを使用します。

ほとんどのパッケージの作成者には `ref` フォルダーは必要ありません。 これは、コンパイルや IntelliSense のために一貫性のあるセキュリティ、外部からのアクセスを提供する必要があるものの、TxM ごとに実装が異なるパッケージの場合に便利です。 この最大のユース ケースは、NuGet における .NET Core の配布の一環として生成される `System.*` パッケージです。 これらのパッケージには、一貫性のある ref アセンブリ セットで統合されているさまざまな実装があります。

機械的に、`ref` フォルダーに含まれるアセンブリはコンパイラに渡される参照アセンブリとなります。 csc.exe を使用している場合、これらは [C# /reference オプション](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) スイッチに渡されるアセンブリとなります。

`ref` フォルダーの構造は `lib` と同じです。たとえば、次のようになります。

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll

この例では、`ref` ディレクトリ内のアセンブリはすべて同じになります。

## <a name="runtimes"></a>Runtimes

runtimes フォルダーには、通常はオペレーティング システムおよび CPU アーキテクチャで定義される、特定の "ランタイム" で実行するために必要なアセンブリとネイティブ ライブラリが含まれます。 これらのランタイムは、`win`、`win-x86`、`win7-x86`、`win8-64` などの[ランタイム識別子 (RID)](/dotnet/core/rid-catalog) を使用して識別されます。

## <a name="native-helpers-to-use-platform-specific-apis"></a>プラットフォーム固有の API を使用するネイティブ ヘルパー

次の例では、いくつかのプラットフォームの単なるマネージドされた実装を持つものの、Windows 8 固有のネイティブ API を呼び出すことができる Windows 8 のネイティブ ヘルパーを使用するパッケージを示します。

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

上記のパッケージを指定する場合、次のようになります。

- Windows 8 でない場合は、`lib/net40/MyLibrary.dll` アセンブリが使用されます。

- Windows 8 の場合は、`runtimes/win8-<architecture>/lib/MyLibrary.dll` が使用され、`native/MyNativeHelper.dll` がビルドの出力にコピーされます。

上記の例では、`lib/net40` アセンブリは単なるマネージド コードであるのに対して、runtimes フォルダー内のアセンブリはネイティブ ヘルパー アセンブリの p/invoke を行って Windows 8 固有の API を呼び出します。

これまでは単一の `lib` フォルダーのみが選択されているため、ランタイム固有のフォルダーがある場合は、非ランタイム固有の `lib` より優先されます。 ネイティブ フォルダーが付加的なものであり、存在する場合はビルドの出力にコピーされます。

## <a name="managed-wrapper"></a>マネージド ラッパー

ランタイムを使用するもう 1 つの方法として、ネイティブ アセンブリではなく、単なるマネージド ラッパーであるパッケージを配布する方法があります。 このシナリオでは、次のようにパッケージを作成します。

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

この場合、対応するネイティブ アセンブリに依存しないこのパッケージの実装がない限り、トップレベルの `lib` フォルダーはありません。 マネージド アセンブリ `MyLibrary.dll` がこれらの両方のケースでまったく同じであった場合は、トップレベルの `lib` フォルダーに配置することはできます。ただし、win-x86 または win-x64 ではないプラットフォームにインストールされた場合、ネイティブ アセンブリがないとパッケージのインストールに失敗するため、トップレベルの lib は使用されますが、ネイティブ アセンブリはコピーされません。

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a>NuGet 2 および NuGet 3 のパッケージの作成

`packages.config` を使用するプロジェクトで利用できるパッケージと、`project.json` を使用するパッケージを作成する場合は、以下が適用されます。

- ref と runtimes は NuGet 3 のみで動作します。 NuGet 2 では両方とも無視されます。

- `install.ps1` や `uninstall.ps1` に依存して機能させることはできません。 これらのファイルは `packages.config` を使用する場合は実行されますが、`project.json` では無視されます。 したがって、実行せずにパッケージを使用できるようにする必要があります。 `init.ps1` は NuGet 3 で引き続き実行されます。

- ターゲットとプロパティのインストールは異なるため、両方のクライアントでパッケージが予期したとおりに動作することを確認してください。

- NuGet 3 では、lib のサブディレクトリは TxM である必要があります。 `lib` フォルダーのルートにライブラリを配置することはできません。

- NuGet 3 では、コンテンツは自動的にコピーされません。 パッケージのコンシューマーはファイル自体をコピーするか、タスク ランナーなどのツールを使用して、ファイルのコピーを自動化できます。

- NuGet 3 では、ソースと構成ファイルの変換は実行されません。

NuGet 2 と 3 をサポートする場合、`minClientVersion` は、パッケージが動作する最も古いバージョンの NuGet 2 クライアントである必要があります。 既存のパッケージの場合は、変更する必要はありません。
