---
title: Team Foundation ビルドでの NuGet パッケージの復元のチュートリアル
description: Team Foundation ビルド (TFS と Visual Studio Team Services の両方) で NuGet パッケージを復元する方法について説明します。
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: a86a58f8afb4b0f1affeddd47d6c5606fb465757
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "73611003"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a>Team Foundation ビルドでのパッケージの復元の設定

この記事では、Git と Team Services バージョン管理の両方における [Team Services ビルド](/vsts/build-release/index)の一環としてパッケージを復元する方法に関する詳細なチュートリアルを提供します。

このチュートリアルは、Visual Studio Team Service の使用のシナリオに固有ですが、概念は他のバージョン管理およびビルドシステムにも適用されます。

適用先:

- TFS の任意のバージョンで実行されているカスタム MSBuild プロジェクト
- Team Foundation Server 2012 またはそれ以前
- TFS 2013 以降に移行されたカスタム Team Foundation ビルド プロセス テンプレート
- Nuget の復元機能が削除されたビルド プロセス テンプレート

ビルド プロセス テンプレートを含む Visual Studio Team Services または Team Foundation Server 2013 を使用している場合は、パッケージの自動復元がビルド プロセスの一環として発生します。

## <a name="the-general-approach"></a>一般的な方法

NuGet を使用する利点は、バージョン管理システムへのバイナリのチェックインを回避できることです。

これは、git などの[分散バージョン管理](https://en.wikipedia.org/wiki/Distributed_revision_control)システムを使用している場合に特に有効です。これは、開発者が、ローカルで作業を始める前に、完全な履歴を含めた全体のリポジトリを複製する必要があるためです。 バイナリ ファイルは一般的に差分圧縮なしで保存されるので、バイナリ ファイルをチェックインすると、大幅なリポジトリの肥大化を招く可能性があります。

NuGet は、現在まで長期にわたってビルドの一部としての[パッケージ復元](../consume-packages/package-restore.md)をサポートしています。 以前の実装では、NuGet は、プロジェクトのビルド中にパッケージを復元したので、ビルド プロセスを拡張する必要があるパッケージの場合に、卵が先か鶏が先かという問題がありました。 しかし、MSBuild では、ビルド中のビルドの拡張は許可されないので、これは MSBuild の問題だと主張されることがありますが、私はこれが固有の問題であると主張します。 拡張する必要がある局面によっては、パッケージが復元されるときには登録するのに遅すぎることがあります。

この問題の解決策として、ビルド プロセスの最初の手順としてパッケージが復元されることを確認します。

```cli
nuget restore path\to\solution.sln
```

ビルド プロセスでコードをビルドする前にパッケージを復元する場合、`.targets` ファイルをチェックインする必要はありません。

> [!Note]
> Visual Studio での読み込みを許可するようにパッケージを作成する必要があります。 そのようになっていない場合、他の開発者も、パッケージを最初に復元しなくともソリューションを単純に開くことができるようにするために、引き続き `.targets` ファイルもチェックインする必要があります。

次のデモ プロジェクトは、`packages` フォルダーと `.targets` ファイルをチェックインする必要がないような方法でビルドを設定する方法を示しています。 このサンプル プロジェクト用の Team Foundation Service で自動ビルドを設定する方法も示しています。

## <a name="repository-structure"></a>リポジトリの構造

デモのプロジェクトは、Bing のクエリにコマンドライン引数を使用しているシンプルなコマンド ライン ツールです。 .NET Framework 4 を対象とし、多くの [BCL パッケージ](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](https://www.nuget.org/packages/Microsoft.Net.Http)、[Microsoft.Bcl](https://www.nuget.org/packages/Microsoft.Bcl)、[Microsoft.Bcl.Async](https://www.nuget.org/packages/Microsoft.Bcl.Async)、[Microsoft.Bcl.Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)) を使用しています。

リポジトリの構造は次のようになります。

    <Project>
        │   .gitignore
        │   .tfignore
        │   build.proj
        │
        ├───src
        │   │   BingSearcher.sln
        │   │
        │   └───BingSearcher
        │       │   App.config
        │       │   BingSearcher.csproj
        │       │   packages.config
        │       │   Program.cs
        │       │
        │       └───Properties
        │               AssemblyInfo.cs
        │
        └───tools
            └───NuGet
                    nuget.exe

`packages` フォルダーも、どの `.targets` ファイルもチェックインしていないことがわかります。

ただし、`nuget.exe` はビルド時に必要なのでチェックインしました。 広く使用されている規則に従って、共有 `tools` フォルダーの下にチェックインしました。

ソース コードは `src` フォルダーの下にあります。 このデモでは、1 つのソリューションのみを使用しますが、このフォルダーに複数のソリューションが含まれていることは容易に想像できます。

### <a name="ignore-files"></a>ファイルを無視

> [!Note]
> 現在、[NuGet クライアントに既知のバグ](https://nuget.codeplex.com/workitem/4072)があり、そのためにクライアントが依然として `packages` フォルダーをバージョン管理に追加します。 回避策は、ソース管理の統合を無効にすることです。 そのためには、ソリューションと並列な `.nuget` フォルダーに `Nuget.Config ` ファイルが必要です。 このフォルダーがまだ存在しない場合は、それを作成する必要があります。 [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md) に次のコンテンツを追加します。

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

**packages** フォルダーをチェックインしないことをバージョン管理に伝達するために、git (`.gitignore`) および TF バージョン管理 (`.tfignore`) の両方の無視ファイルも追加しました。 これらのファイルは、チェックインしたくないファイルのパターンについて記述します。

`.gitignore` ファイルは次のようになります。

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

`.gitignore` ファイルは[非常に強力](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html)です。 たとえば、`packages` フォルダーの内容を一般的にチェックインしなくとも、`.targets` ファイルのチェックインに関する前のガイドに従う場合、代わりに次のコマンドを使用できます。

    packages
    !packages/**/*.targets

これはすべての `packages` フォルダーを除外しますが、すべての含まれる `.targets` ファイルを再び含めます。 ところで、Visual Studio 開発者のニーズに合わせて特別にカスタマイズされた `.gitignore` ファイルのテンプレートを[ここ](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)で見つけることができます。

TF バージョン管理は、[.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) ファイルを使用してよく似たメカニズムをサポートします。 構文はほぼ同じです。

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a>build.proj

このデモでは、非常にシンプルなビルド プロセスを維持しています。 ソリューションをビルドする前にパッケージを復元することを確認しながらすべてのソリューションをビルドする MSBuild プロジェクトを作成します。

このプロジェクトには、従来の 3 つのターゲット `Clean`、`Build`、`Rebuild` だけでなく、新しいターゲット `RestorePackages` があります。

- `Build` と `Rebuild` のターゲットはどちらも `RestorePackages` に依存します。 これにより、`Build` と `Rebuild` の両方を実行できることを確認し、パッケージが復元されていることに依存できます。
- `Clean`、`Build`、および `Rebuild` は、すべてソリューション ファイルの対応する MSBuild ターゲットを呼び出します。
- `RestorePackages` ターゲットは、各ソリューション ファイルの `nuget.exe` を呼び出します。 これは、[MSBuild のバッチ機能](/visualstudio/msbuild/msbuild-batching)を使用して実行されます。

この結果は次のようになります。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0"
            DefaultTargets="Build"
            xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
    <OutDir Condition=" '$(OutDir)'=='' ">$(MSBuildThisFileDirectory)bin\</OutDir>
    <Configuration Condition=" '$(Configuration)'=='' ">Release</Configuration>
    <SourceHome Condition=" '$(SourceHome)'=='' ">$(MSBuildThisFileDirectory)src\</SourceHome>
    <ToolsHome Condition=" '$(ToolsHome)'=='' ">$(MSBuildThisFileDirectory)tools\</ToolsHome>
    </PropertyGroup>

    <ItemGroup>
    <Solution Include="$(SourceHome)*.sln">
        <AdditionalProperties>OutDir=$(OutDir);Configuration=$(Configuration)</AdditionalProperties>
    </Solution>
    </ItemGroup>

    <Target Name="RestorePackages">
    <Exec Command="&quot;$(ToolsHome)NuGet\nuget.exe&quot; restore &quot;%(Solution.Identity)&quot;" />
    </Target>

    <Target Name="Clean">
    <MSBuild Targets="Clean"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Build" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Build"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Rebuild" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Rebuild"
                Projects="@(Solution)" />
    </Target>
</Project>
```

## <a name="configuring-team-build"></a>チーム ビルドを構成する

チーム ビルドは、さまざまなプロセス テンプレートを提供します。 このデモでは、Team Foundation Service を使用しています。 TFS のオンプレミス インストールはよく似ています。

Git および TF バージョン管理には異なるチーム ビルド テンプレートがあるので、次の手順は、使用しているバージョン管理システムによって異なります。 どちらの場合でも、必要なのは、ビルドするプロジェクトとして build.proj を選択することだけです。

最初に、git のプロセス テンプレートを見てみましょう。 git ベースのテンプレートで、プロパティ `Solution to build` を介してビルドが選択されています。

![git のビルド プロセス](media/PackageRestoreTeamBuildGit.png)

このプロパティは、リポジトリ内の場所であることに注意してください。 `build.proj` はルートにあるので、単純に `build.proj` を使用します。 ビルド ファイルを `tools` というフォルダーの下に置いた場合、値は `tools\build.proj` になります。

TF バージョン管理テンプレートでは、プロパティ `Projects` を介してプロジェクトが選択されます。

![TFVC のビルド プロセス](media/PackageRestoreTeamBuildTFVC.png)

Git ベースのテンプレートとは対照的に、TF バージョン管理は、ピッカー (右側にある 3 つのドット付きのボタン) をサポートします。 したがって、入力エラーを回避するために、それらを使用してプロジェクトを選択することをお勧めします。
