---
title: NuGet packages.config ファイル参照
description: 一部のプロジェクト タイプでは、packages.config で、プロジェクトで使用される NuGet パッケージの一覧が保守管理されます。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 2019ce5961a8237fbda855cd7d5b42948808be3a
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817838"
---
# <a name="packagesconfig-reference"></a>packages.config 参照

`packages.config` ファイルは、プロジェクトで参照されるパッケージの一覧を保守管理するために、一部のプロジェクト タイプで使用されます。 それにより、NuGet は、ビルド サーバーなど、別のコンピューターにプロジェクトを転送するとき、一部のパッケージだけでプロジェクトの依存関係を簡単に復元できます。

このオプションを使用すると場合、`packages.config`は通常、プロジェクトのルートに配置します。 最初の NuGet 操作が実行すると、作成することも手動でなど、どのようなコマンドを実行する前にときに自動的に作成された`nuget restore`です。

使用するプロジェクト[PackageReference](../consume-packages/Package-References-in-Project-Files.md)を使わない`packages.config`です。

## <a name="schema"></a>Schema

このスキーマは単純です。標準の XML ヘッダーは、1 つまたは複数の `<packages>` 要素を含むシングル `<package>` ノードです。要素は参照ごとに 1 つになります。 各 `<package>` 要素に次の属性を指定できます。

| 属性 | 必須 | 説明 |
| --- | --- | --- |
| ID | [はい] | Newtonsoft.json や Microsoft.AspNet.Mvc など、パッケージの識別子。 | 
| version | [はい] | 3.1.1 や 4.2.5.11-beta など、インストールするパッケージの正確なバージョン。 バージョン文字列には少なくとも 3 つの数字を含める必要があります。4 番目はプレリリース サフィックスであり、任意です。 範囲は許可されません。 | 
| targetFramework | いいえ | [ターゲット フレームワーク モニカー (TFM)](target-frameworks.md) はパッケージのインストール時に適用されます。 パッケージのインストール時、これは最初、プロジェクトのターゲットに設定されます。 結果的に、異なる `<package>` 要素に異なる TFM が与えられます。 たとえば、.NET 4.5.2 を対象とするプロジェクトを作成する場合、そのポイントでインストールされたパッケージは net452 の TFM を使用します。 後でプロジェクトのターゲットを .NET 4.6 に変更し、パッケージを追加する場合、net46 の TFM が使用されます。 プロジェクトのターゲットと `targetFramework` 属性に不一致があると警告が出ます。その場合、影響が出たパッケージを再インストールできます。 | 
| allowedVersions | いいえ | パッケージ更新中に適用された、このパッケージの許可されるバージョンの範囲 ([アップグレード バージョンの制約](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)ページをご覧ください)。 インストール操作中または復元操作中にインストールされるパッケージには影響を*与えません*。 構文については、「[Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards)」(パッケージのバージョン管理) を参照してください。 PackageManager UI も、許可される範囲外のすべてのバージョンを無効にします。 | 
| developmentDependency | いいえ | コンシューミング プロジェクト自体で NuGet パッケージが作成される場合、依存関係に対してこれを `true` に設定すると、そのパッケージがコンシューミング パッケージの作成時に含まれません。 既定値は、`false` です。 | 

## <a name="examples"></a>使用例

次の `packages.config` は 2 つの依存関係を参照します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

次の `packages.config` は 9 つのパッケージを参照しますが、`developmentDependency` 属性に起因し、`Microsoft.Net.Compilers` はコンシューミング パッケージのビルド時に含まれません。 Newtonsoft.Json の参照はまた、更新を 8.x バージョンと 9.x バージョンのみに制限します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
