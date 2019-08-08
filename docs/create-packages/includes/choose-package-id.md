---
ms.openlocfilehash: e8949e9964ed19d342df53f08f59bb0f89e5feb0
ms.sourcegitcommit: 5aa49478dc466c67db5c3edda7c6ce8dcd8ae033
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68817485"
---
パッケージ識別子とバージョン番号は、パッケージに含まれる正確なコードを一意に識別するため、プロジェクトの中で最も重要な 2 つの値です。

**パッケージ識別子のベスト プラクティス:**

- **一意性**:この識別子は、nuget.org 全体で、あるいはパッケージをホストするギャラリー全体で一意になる必要があります。 識別子を決める前に、該当するギャラリーを検索し、その名前が既に使用されていないか確認してください。 競合を避けるために、`Contoso.` のように、識別子の最初の部分に会社の名前を使用することが適しているパターンです。
- **名前空間のような名前**:.NET の名前空間に似たパターンに従います。ハイフンの代わりにドット表記を使います。 たとえば、`Contoso-Utility-UsefulStuff` や `Contoso_Utility_UsefulStuff` ではなく `Contoso.Utility.UsefulStuff` を使用します。 パッケージ識別子がコードで使用される名前空間と一致すれば、利用者にとっても便利です。
- **サンプル パッケージ**:別のパッケージの使用方法を示すサンプル コードのパッケージを生成する場合、`Contoso.Utility.UsefulStuff.Sample` のように、識別子にサフィックスとして `.Sample` を付けます。 (サンプル パッケージは、もちろん、他のパッケージに依存します。)サンプル パッケージを作成する場合は、`<IncludeAssets>` 内で `contentFiles` 値を使用します。 `content` フォルダーで、`\Samples\Contoso.Utility.UsefulStuff.Sample` のように、`\Samples\<identifier>` という名前のフォルダーにサンプル コードを配置します。

**パッケージ バージョンのベスト プラクティス:**

- これは厳密には必須ではありませんが、一般的にはプロジェクト (またはアセンブリ) と一致するようにパッケージのバージョンを設定します。 パッケージを単一のアセンブリに限定する場合に、これはシンプルな方法です。 概して、NuGet 自体は依存関係の解決時、パッケージ バージョンを使います。アセンブリ バージョンではありません。
- 非標準のバージョン スキーマを使用するとき、「[パッケージのバージョン管理](../../reference/package-versioning.md)」で説明するように、NuGet バージョン管理ルールを検討してください。 NuGet は、ほぼ [semver 2 に準拠](../../reference/package-versioning.md#semantic-versioning-200)しています。

> 依存関係の解決については、「[PackageReference による依存関係の解決](../../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference)」をご覧ください。 バージョン管理の理解を深めるためにも役立つ可能性がある旧情報については、こちらの一連のブログ投稿を確認してください。
>
> - [第 1 部: DLL 地獄](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [第 2 部: コア アルゴリズム](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [第 3 部:バインド リダイレクトによる統合](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)