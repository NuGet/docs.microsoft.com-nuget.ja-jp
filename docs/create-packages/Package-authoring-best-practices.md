---
title: パッケージ作成のベスト プラクティス
description: 高品質な NuGet パッケージを作成するためのベスト プラクティスに関する一般的なガイドです。
author: chgill-MSFT
ms.author: chgill
ms.date: 09/17/2020
ms.topic: conceptual
ms.openlocfilehash: aae05b63921f3494376b430186d3605eeff174c1
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387362"
---
# <a name="package-authoring-best-practices"></a>パッケージ作成のベスト プラクティス

このガイダンスの目的は、NuGet パッケージの作成者に対して、高品質なパッケージを作成および発行するための簡易なリファレンスを提供することです。 ここでは主に、メタデータやパックなどのパッケージ固有のベスト プラクティスに焦点を当てます。 高品質なライブラリを構築するためのより詳細な提案については、.NET の「[オープン ソース ライブラリのガイダンス](/dotnet/standard/library-guidance/)」を参照してください。

## <a name="types-of-recommendations"></a>推奨事項の種類

各記事で 4 種類の推奨事項 (**実施**、**検討**、**回避**、**実施しない**) が提示されます。 推奨事項の種類は、どの程度厳密に従うべきかを示しています。

**実施** の推奨事項にはほとんど常に従う必要があります。 次に例を示します。

✔️ パッケージの目的について説明する、パッケージの簡単な説明を含めてください。

その一方で、**検討** の推奨事項には一般に従うべきですが、その規則には正当な例外があります。

✔️ NuGet のプレフィックスの予約[条件](../nuget-org/id-prefix-reservation.md)を満たしているプレフィックスを持つ NuGet パッケージ名を選択することを検討してください。

**回避** の推奨事項は一般には良いアイデアではありませんが、規則に違反することが効果的である場合があります。

❌ 正確なバージョンを要求する NuGet パッケージ参照は回避してください。

最後に、**実施しない** の推奨事項は、ほとんどの場合でやってはいけないことを示しています。

❌ `LicenseUrl` メタデータ プロパティは使用しないでください。

## <a name="create-a-nuget-package"></a>NuGet パッケージの作成

NuGet パッケージを作成するために推奨される最新の方法は、[SDK スタイルのプロジェクト](../resources/check-project-format.md)から作成することです。 [ターゲット フレームワーク](/dotnet/standard/frameworks)や[パッケージ メタデータ](#package-metadata)など、SDK スタイルのプロジェクトのプロパティは、[プロジェクト ファイル](/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file)に定義されています。

SDK スタイルのプロジェクトからパッケージを作成するには、必要なプロパティを定義し、[Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md?tabs=netcore-cli) または [dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) でパックします。

✔️ SDK スタイルのプロジェクトを作成し、Visual Studio または dotnet CLI を使用してパッケージを作成 (パック) してください。

必要なクライアント ツール、プロジェクト ファイルの例、コマンドなど、パッケージの作成に関するより詳細なガイダンスについては、「[dotnet CLI を使用して NuGet パッケージを作成する](./creating-a-package-dotnet-cli.md)」を参照してください。

どの .NET Framework をターゲットにするか決める際に、[クロス プラットフォーム ターゲットに関する最新のガイダンス](/dotnet/standard/library-guidance/cross-platform-targeting)を参照してください。

## <a name="package-metadata"></a>パッケージ メタデータ

メタデータは、すべての NuGet パッケージの基本コンポーネントです。 メタデータの品質は、パッケージの見つけやすさ、使いやすさ、および信頼性に大きな影響を与えます。

Visual Studio の場合、パッケージ メタデータを指定するお勧めの方法は、プロジェクト > [プロジェクト名] プロパティ > パッケージにアクセスすることです。

パッケージ メタデータ要素は、[プロジェクト ファイルで直接指定する](./creating-a-package-msbuild.md#set-properties)こともできます。

次の表に、使用可能なパッケージ メタデータ要素へのマッピングと説明を示します。

| Visual Studio のプロパティ名                       | [プロジェクト ファイルまたは MSBuild のプロパティ名](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                            | [Nuspec のプロパティ名](https://docs.microsoft.com/nuget/reference/nuspec#general-form-and-schema)     | 説明                                                                                                           |
|-----------------------------------------------    |-----------------------------------------------------------------------------------------------------------------------------------------  |---------------------------------------------------------------------------------------------------    |-------------------------------------------------------------------------------------------------------------------    |
| [`Package id`](#package-id)                       | [`PackageId`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageid)                                                              | [`id`](https://docs.microsoft.com/nuget/reference/nuspec#id)                                          | パッケージの名前または識別子。                                                                                       |
| [`Package version`](#package-version)             | [`PackageVersion`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageversion)                                                    | [`version`](https://docs.microsoft.com/nuget/reference/nuspec#version)                                | NuGet パッケージ バージョン。                                                                                                |
| [`Authors`](#authors)                             | [`Authors`](https://docs.microsoft.com/dotnet/core/tools/csproj#authors)                                                                  | [`authors`](https://docs.microsoft.com/nuget/reference/nuspec#authors)                                | パッケージ作成者のコンマ区切りのリスト。多くの場合、個人または組織の "わかりやすい名前" を使用します。           |
| [`Description`](#description)                     | [`Description`](https://docs.microsoft.com/dotnet/core/tools/csproj#description)                                                          | [`description`](https://docs.microsoft.com/nuget/reference/nuspec#description)                        | パッケージの説明。                                                                                         |
| [`Copyright`](#copyright)                         | [`Copyright`](https://docs.microsoft.com/dotnet/core/tools/csproj#copyright)                                                              | [`copyright`](https://docs.microsoft.com/nuget/reference/nuspec#copyright)                            | パッケージの著作権の詳細。                                                                                    |
| [`Licensing - Expression`](#licensing)            | [`PackageLicenseExpression`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)   | [`license type="expression"`](https://docs.microsoft.com/nuget/reference/nuspec#license)              | SPDX ライセンス式。                                                                                           |
| [`Licensing - File`](#licensing)                  | [`PackageLicenseFile`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)         | [`license type="file"`](https://docs.microsoft.com/nuget/reference/nuspec#license)                    | カスタム ライセンス ファイルへのパス。                                                                                        |
| [`Project URL`](#project-url)                     | `PackageProjectUrl`                                                                                                                       | [`projectUrl`](https://docs.microsoft.com/nuget/reference/nuspec#projecturl)                          | プロジェクトのホームページの URL。                                                                                       |
| [`Icon File`](#icon)                              | [`PackageIcon`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file)                                    | [`icon`](https://docs.microsoft.com/nuget/reference/nuspec#icon)                                      | パッケージのアイコン画像ファイルへのパス。                                                                                  |
| [`Repository URL`](#repository-type-and-url)      | [`RepositoryUrl`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositoryurl)                                                      | [`repository url`](https://docs.microsoft.com/nuget/reference/nuspec#repository)                      | パッケージのビルド元であるリポジトリの URL。                                                               |
| [`Repository type`](#repository-type-and-url)     | [`RespositoryType`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositorytype)                                                   | [`repository type`](https://docs.microsoft.com/nuget/reference/nuspec#repository)                     | リポジトリ URL が指しているリポジトリの種類 (つまり "git")。                                                    |
| [`Tags`](#tags)                                   | [`PackageTags`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagetags)                                                          | [`tags`](https://docs.microsoft.com/nuget/reference/nuspec#tags)                                      | パッケージを説明するタグとキーワードのスペース区切りの一覧。 タグは、パッケージを検索するときに使用されます。     |
| [`Release notes`](#release-notes)                 | [`PackageReleaseNotes`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                                          | [`releaseNotes`](https://docs.microsoft.com/nuget/reference/nuspec#releasenotes)                      | パッケージの今回のリリースで加えられた変更内容の説明。                                                     |
### <a name="package-id"></a>[パッケージ ID]

まったく新しいパッケージを発行する場合:

✔️ NuGet.org において一意かつ既存のパッケージと明確に区別されるパッケージ ID を選択してください。
> パッケージ ID が一意で区別可能かどうかを確認するには、NuGet.org でその ID を検索するか、次のリンクが存在するかどうかを確認します: https://www.nuget.org/packages/<package 名\> 。

✔️ NuGet の[プレフィックスの予約条件](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria)を満たしているプレフィックスを持つ NuGet パッケージ名を選択することを検討してください。
> パッケージのプレフィックス ID を予約すると、検証済みのチェック マークを取得できるようになります: ![画像](media/Verified-check-mark.png)
> 
> 詳細については、[「パッケージ ID プレフィックスの予約」に関するドキュメント](../nuget-org/id-prefix-reservation.md)を参照してください。

### <a name="package-version"></a>パッケージ バージョン

✔️ NuGet パッケージのバージョン管理に [SemVer](https://semver.org/) を使用することを検討してください。
> 基本的に、これは Major.Minor.Patch[-prerelease] の形式を使用することを意味します。

✔️ パッケージが非安定版またはプレビュー版の場合は、[プレリリース パッケージ](./prerelease-packages.md)として発行してください。

詳細なガイダンスについては、[.NET ライブラリのバージョン管理に関するガイド](/dotnet/standard/library-guidance/versioning)を参照してください。

### <a name="authors"></a>Authors

✔️ 作成者のフィールドは、ユーザーまたはユーザーの組織の "わかりやすい名前" のために使用してください。
> たとえば、NuGet.org のユーザー名が "jdoe" である場合、作成者のフィールドに "Jane Doe" を使用すると、コンシューマーがそのユーザーを作成者として認識しやすくなります。 組織の NuGet.org ユーザー名が "ContosoToolkit" である場合、"Contoso Corporation" を使用したほうが認識しやすく、コンシューマーの信頼性が高くなります。
### <a name="description"></a>説明

✔️ パッケージについて説明する、短い説明 (最大 4000 文字) を含めてください。
> パッケージの説明は、NuGet 検索に表示される最も目立つフィールドの 1 つであり、パッケージが適切かどうかを判断するために、潜在的なコンシューマーが最初に見るものになる可能性が高くなります。

### <a name="copyright"></a>Copyright

✔️ "Copyright (c) <名前/会社\> <年\>" を使用してパッケージを著作権で保護することを検討してください。
>基本的に、著作権表記によって、お客様の作業内容はお客様の許可がないとコピーできないということが示されます。 パッケージに著作権表記を含めることは簡単であり、何の害もありません。

例:Copyright (c) Contoso 2020

### <a name="licensing"></a>ライセンス

✔️ [ライセンス式またはライセンス ファイルをパッケージに含める](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file)ことを実施してください。
> [!IMPORTANT]
> ライセンスを持たないプロジェクトは、既定で[排他的な著作権](https://choosealicense.com/no-permission/)になります。これは、プロジェクトを使用する権限を誰にも付与していないことを意味します。

❌ 非推奨の `LicenseUrl` メタデータ プロパティは使用しないでください。
> URL でのライセンスの変更によって、以前のパッケージ バージョンに対して表示されたライセンスが遡及的に変更されるため、法的なあいまいさが生じます。

#### <a name="if-your-package-is-open-source"></a>パッケージが[オープンソース](https://opensource.org/osd)の場合

✔️ パッケージをオープンソースにするために、[オープンソース ライセンスを選択してください](https://choosealicense.com/)。
> *"オープンソース ライセンスは、オープンソースの定義に準拠するライセンスです。簡単に言うと、ソフトウェアの自由な使用、変更、および共有を許可するということです。"* - オープンソース イニシアチブ。 オープンソース ソフトウェアとオープンソース イニシアチブの詳細については、 https://opensource.org/ を参照してください。

✔️ [パッケージにライセンス式を含める](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file)ことを検討してください。
> ライセンス式は最も明確に表示され、コンシューマーに対して、パッケージを使用できるかどうか、またはライセンスが変更されたかどうかがより明確になります。 
> [!Note]
> NuGet.org で受け入れられるのは、オープンソース イニシアチブまたはフリー ソフトウェア財団によって承認されたライセンスのライセンス式のみです。

#### <a name="if-your-package-is-not-open-source"></a>パッケージがオープンソースでない場合

✔️ [ライセンス ファイルをパッケージに含める](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file)ことを実施してください。
> 標準以外のライセンスも含め、任意のライセンス ファイル (.txt または .md) をパッケージに追加できます。 

### <a name="project-url"></a>[プロジェクトの URL]

✔️ 関連付けられているプロジェクト、リポジトリ、または会社の Web サイトへのリンクを含めることを検討してください。
> プロジェクト サイトには、パッケージについてユーザーが知りたいすべてのことが含まれている必要があります。またおそらく、ユーザーがドキュメントを探す場所となります。

### <a name="icon"></a>アイコン

✔️ 視覚的に区別しやすくなるように、[パッケージにアイコンを含める](../reference/msbuild-targets.md#packing-an-icon-image-file)ことを検討してください。 これは、パッケージの品質に関する認識を向上させることができる、比較的小さな追加です。
> アイコンは、個々のパッケージに固有であるか、またはブランドのロゴであることがあります。

✔️ 最良な表示結果になるように、128 x 128 で透明な背景を持つ画像 (PNG) を使用してください。
> NuGet では、表示されるクライアントに合わせて画像が自動的にスケーリングされます。

❌ 非推奨の `IconUrl` メタデータ プロパティは使用しないでください。

### <a name="repository-type-and-url"></a>リポジトリの種類と URL

✔️ [ソース リンク](/dotnet/standard/library-guidance/sourcelink)を設定して、ソース管理メタデータが NuGet パッケージに自動的に追加され、ライブラリのデバッグが容易になるようにすることを検討してください。
> ソース リンクによって、`Repository URL` と `Repository Type` がパッケージ メタデータに自動的に追加されます。 また、パッケージのバージョンに関連付けられている特定のコミットも追加されます。

### <a name="tags"></a>タグ

✔️ 見つけやすさを向上させるために、パッケージに関連する重要な用語を含むいくつかのタグを追加してください。
> タグは NuGet.org の検索アルゴリズムにおいて考慮されます。また、パッケージ ID に含まれていないが重要である用語のために特に役立ちます。

たとえば、コンソールに対する文字列をログに記録するためのパッケージを発行した場合は、"ログ記録、ログ、コンソール、文字列、出力" などを含めます

### <a name="release-notes"></a>リリース ノート

✔️ 各更新に、どのような変更が実施されたかを説明するリリース ノートを含めることを検討してください。
> リリース ノートに必要な特定の形式はありませんが、以下を含めることをお勧めします。
>
> 1. 重大な変更
> 2. 新機能
> 3. バグの修正
> 
> リポジトリ内でリリース ノートまたは変更ログを既に追跡している場合は、関連するファイルへのリンクを含めることもできます。

## <a name="related-topics"></a>関連トピック

- [パッケージの作成と公開 (dotnet CLI)](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [パッケージの作成と公開 (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio.md?tabs=netcore-cli)