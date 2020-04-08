---
title: NuGet の project.json ファイル リファレンス
description: 一部のプロジェクト タイプでは、project.json で、プロジェクトで使用される NuGet パッケージの一覧が保守管理されます。
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: 5ecbcd4855de8ea7b6301a5e307779216baf96fc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488294"
---
# <a name="projectjson-reference"></a>project.json 参照

*NuGet 3.x 以降*

`project.json` ファイルは、パッケージ管理形式と呼ばれるプロジェクトで使用されるパッケージのリストを保持します。 これは `packages.config` に優先しますが、NuGet 4.0 以降では、[PackageReference](../consume-packages/package-references-in-project-files.md) によって置き換えられます。

[`project.lock.json`](#projectlockjson) ファイル (後述) も、`project.json` を使用するプロジェクトで使用されます。

`project.json` には次の基本構造があります。4 つの最上位レベルのオブジェクトのそれぞれが任意の数の子オブジェクトを持つことができます。

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }
}
```

## <a name="dependencies"></a>依存関係

プロジェクトの NuGet パッケージの依存関係を次の形式でリストします。

```json
"PackageID" : "version_constraint"
```

次に例を示します。

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

`dependencies` セクションは、NuGet パッケージ マネージャー ダイアログがプロジェクトにパッケージの依存関係を追加する場所です。

パッケージ ID は、nuget.org のパッケージ ID に対応しています。これはパッケージ マネージャー コンソールで使用される ID と同じです。`Install-Package Microsoft.NETCore`

パッケージを復元するときに、`"5.0.0"` のバージョンの制約は `>= 5.0.0` を意味します。 つまり、サーバーで 5.0.0 は使用できないが 5.0.1 は使用できる場合、NuGet は 5.0.1 をインストールし、アップグレードに関する警告を発します。 それ以外の場合は、NuGet は制約に一致するサーバー上で使用可能な最も低いバージョンを選択します。

解決ルールの詳細については、[依存関係の解決](../concepts/dependency-resolution.md)に関するページをご覧ください。

### <a name="managing-dependency-assets"></a>依存関係アセットの管理

依存関係からどのアセットを最上位レベルのプロジェクトにフローするかは、依存関係の参照の `include` プロパティと `exclude` プロパティでコンマ区切りのタグのセットを指定することで制御できます。 タグを次の表に一覧表示します。

| 包含/除外タグ | ターゲットの影響を受けるフォルダー |
| --- | --- |
| contentFiles | コンテンツ  |
| runtime | Runtime、Resources、FrameworkAssemblies  |
| compile | lib |
| build | build (MSBuild のプロパティとターゲット) |
| native | native |
| なし | フォルダーなし |
| すべて | すべてのフォルダー |

`exclude` で指定されているタグの方が、`include` で指定されているタグより優先されます。 たとえば、`include="runtime, compile" exclude="compile"` は `include="runtime"` と同じです。

たとえば、依存関係の `build` フォルダーと `native` フォルダーを含めるには、次を使用します。

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

依存関係の `content` フォルダーと `build` フォルダーを除外するには、次を使用します。

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a>フレームワーク

プロジェクトを実行するフレームワーク (`net45`、`netcoreapp`、`netstandard` など) をリストします。

```json
"frameworks": {
    "netcore50": {}
    }
 ```

`frameworks` セクションでは、1 つのエントリのみが許可されます (例外は、非推奨の DNX ツール チェーンでビルドされた ASP.NET プロジェクトの `project.json` ファイルで、これは複数のターゲットを許可します。)

## <a name="runtimes"></a>Runtimes

アプリを実行するオペレーティング システムとアーキテクチャ (`win10-arm`、`win8-x64`、`win8-x86`) をリストします。

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

任意のランタイムで実行できる PCL を含むパッケージは、ランタイムを指定する必要はありません。 これはどの依存関係にも当てはまります。それ以外の場合は、ランタイムを指定する必要があります。


## <a name="supports"></a>サポート

パッケージの依存関係のチェックのセットを定義します。 PCL またはアプリの実行を想定している場所を定義できます。 他の場所でもコードを実行できるように、定義は制限が緩くなっています。 しかしこれらのチェックを指定すると、NuGet はリストされている TxMs ですべての依存関係が満たされていることを確認します。 この値の例には、`net46.app`、`uwp.10.0.app` などがあります。

このセクションは、ポータブル クラス ライブラリのターゲット ダイアログでエントリを選択する際に、自動的に設定される必要があります。

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>インポートする

Imports は、`dotnet` TxM を使用するパッケージに、dotnet TxM を宣言しないパッケージで動作することを許可するように設計されています。 プロジェクトが `dotnet` TxM を使用している場合、以下を `dotnet` に追加して非 `project.json` プラットフォームを `dotnet` 対応にしない限り、依存するすべてのパッケージにも `dotnet` TxM が必要です。

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

`dotnet` TxM を使用している場合、PCL プロジェクト システムは、サポートされているターゲットに基づいて適切な `imports` ステートメントを追加します。

## <a name="differences-from-portable-apps-and-web-projects"></a>ポータブル アプリと Web プロジェクトとの違い

NuGet によって使用される `project.json` ファイルは、ASP.NET Core プロジェクト内にあるサブセットです。 ASP.NET Core では、`project.json` がプロジェクト メタデータ、コンパイルの情報、および依存関係のために使用されます。 他のプロジェクト システムで使用する場合は、これら 3 つが個別のファイルに分割され、`project.json` に含まれる情報が少なくなります。 重要な違いは次のとおりです。

- `frameworks` セクションには 1 つのフレームワークしか存在できません。

- ファイルには、DNX `project.json` ファイルで見られる、依存関係、コンパイル オプションなどを含めることはできません。 1 つのフレームワークしか存在できない場合は、フレームワーク固有の依存関係を入力する意味はありません。

- コンパイルは MSBuild によって処理されるため、コンパイル オプション、プリプロセッサ定義などはすべて、`project.json` ではなく、MSBuild プロジェクト ファイルの一部です。

NuGet 3 以降では、Visual Studio のパッケージ マネージャー UI がコンテンツを操作するため、開発者が手動で `project.json` を編集する必要はありません。 ただし、ファイルを編集することはできますが、プロジェクトをビルドしてパッケージの復元を開始するか、または別の方法で復元を呼び出す必要があります。 「[パッケージの復元](../consume-packages/package-restore.md)」を参照してください。


## <a name="projectlockjson"></a>project.lock.json

`project.lock.json` ファイルは、`project.json` を使用するプロジェクトで NuGet パッケージを復元する過程で生成されます。 このファイルには、NuGet がグラフ全体を処理する際に生成されたすべての情報のスナップショットが保持され、プロジェクトのすべてのパッケージのバージョン、コンテンツ、依存関係が含まれます。 ビルド システムはこれを使用して、プロジェクト自体のローカル パッケージ フォルダーに依存する代わりに、プロジェクトのビルド時に関連するグローバルな場所からパッケージを選択します。 この結果、多くの個別の `project.lock.json` ファイルの代わりに、`.nuspec` のみを読み取ればよいため、ビルド パフォーマンスが向上します。

`project.lock.json` はパッケージの復元で自動的に生成されるため、`.gitignore` ファイルと `.tfignore`ファイルに追加することで、ソース管理から省くことができます ([パッケージとソース管理](../consume-packages/packages-and-source-control.md)に関するページを参照してください)。 ただし、これをソース管理に含めると、変更履歴に時間の経過と共に解決された依存関係の変更が示されます。
