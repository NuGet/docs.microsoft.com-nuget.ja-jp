---
title: NuGet.org でのパッケージの readme
description: NuGet.org の readme ファイルがどのようにレンダリングされるか、および問題が発生した場合の対処方法について詳しく説明します。
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a5d68329128c9e9d047fe10e08ce41f1ae0895b4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2021
ms.locfileid: "107902228"
---
# <a name="package-readme-on-nugetorg"></a>NuGet.org でのパッケージの readme

[NuGet パッケージに readme ファイルを含める](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile)ことにより、パッケージの詳細を充実させ、ユーザーにとって有益なものにすることができます。

これは、おそらく、ユーザーが NuGet.org でパッケージの詳細ページを表示して最初の見る要素の 1 つであり、良い印象を与えるために不可欠です。

> [!IMPORTANT]
> NuGet.org でサポートされているのは、[Markdown](https://daringfireball.net/projects/markdown/) での readme ファイルと、限られたドメインのセットの画像のみです。 NuGet.org で readme が正しく表示されるように、[画像で許可されているドメイン](#allowed-domains-for-images-and-badges)と[サポートされている Markdown 機能](#supported-markdown-features)を確認してください。

## <a name="what-should-my-readme-include"></a>readme に含める必要があるもの

readme には次の項目を含めることを検討してください。
* パッケージの概要と動作についての説明 - どのような問題が解決されるか?
* パッケージの使用を開始する方法 - 特定の要件があるか?
* readme 自体に含まれていない場合に、より包括的なドキュメントへのリンク。
* 少なくともいくつかのコード スニペットやサンプルまたは画像の例。
* フィードバックを行う場所と方法。プロジェクトの問題、Twitter、バグ トラッカー、または他のプラットフォームへのリンクなど。
* 投稿方法 (該当する場合)。

高品質の readme は、さまざまな形式、形状、サイズで提供されることに注意してください。 NuGet.org で使用可能なパッケージが既にある場合は、リポジトリに `readme.md` や他のドキュメント ファイルが既に存在し、それが NuGet.org の詳細ページに追加するのに適している可能性があります。

## <a name="preview-your-readme"></a>readme をプレビューする

NuGet.org で公開される前に readme ファイルをプレビューするには、[NuGet.org のパッケージのアップロード Web ポータル](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg)を使用してパッケージをアップロードし、メタデータ プレビューの [Readme File]\(readme ファイル\) セクションまで下にスクロールします。 次のように表示されます。

![readme ファイルのプレビュー](media\readme-upload-preview.PNG)

時間をかけて、[画像のコンプライアンス](#allowed-domains-for-images-and-badges)と[サポートされている書式設定](#supported-markdown-features)について readme ファイルを繰り返しプレビューし、潜在的なユーザーに優れた印象を与えられることを確認することを検討してください。 NuGet.org に公開した後でパッケージの readme の誤りを修正するには、修正プログラムを使用して、更新されたパッケージのバージョンをプッシュする必要があります。 すべてに問題がないことを事前に確認することで、将来の頭痛の種を取り除くことができます。
## <a name="allowed-domains-for-images-and-badges"></a>画像とバッジに許可されているドメイン

セキュリティとプライバシーの問題により、NuGet.org では、画像やバッジをレンダリングできるドメインが、信頼されたホストに制限されています。 

NuGet.org によりレンダリングが許可されているのは、次の信頼されたドメインのバッジを含むすべての画像です。
* api.bintray.com
* api.codacy.com
* api.codeclimate.com
* api.dependabot.com
* api.travis-ci.com
* api.travis-ci.org
* app.fossa.io
* badge.fury.io
* badgen.net
* badges.gitter.im
* bettercodehub.com
* buildstats.info
* camo.githubusercontent.com
* ci.appveyor.com
* circleci.com
* codecov.io
* codefactor.io
* coveralls.io
* dev.azure.com
* github.com/.../workflows/.../badge.svg
* gitlab.com
* img.shields.io
* isitmaintained.com
* opencollective.com
* raw.github.com
* raw.githubusercontent.com
* snyk.io
* sonarcloud.io
* user-images.githubusercontent.com

別のドメインを許可リストに追加する必要があると思われる場合は、遠慮なく[問題を提出](https://github.com/NuGet/NuGetGallery/issues)してください。エンジニアリング チームによって、プライバシーとセキュリティのコンプライアンスに関するレビューが行われます。 相対ローカル パスで指定された画像と、サポートされていないドメインからホストされている画像はレンダリングされず、パッケージ所有者にのみ表示される readme ファイルのプレビューとパッケージ詳細ページで警告が発生します。

## <a name="supported-markdown-features"></a>サポートされている Markdown 機能
[Markdown](https://daringfireball.net/projects/markdown/) は、プレーン テキスト形式の構文を使用する軽量のマークアップ言語です。 NuGet.org の readme では、[Markdig](https://github.com/lunet-io/markdig) 解析エンジンによる [CommonMark](https://commonmark.org/) 準拠の Markdown がサポートされています。

現在、NuGet.org によってサポートされている Markdown の機能は次のとおりです。
* [ヘッダー](https://spec.commonmark.org/0.29/#atx-headings)
* [イメージ](https://spec.commonmark.org/0.29/#images)
* [追加の強調](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [リスト](https://spec.commonmark.org/0.29/#lists)
* [リンク](https://spec.commonmark.org/0.29/#links)
* [ブロック引用](https://spec.commonmark.org/0.29/#block-quotes)
* [円記号によるエスケープ](https://spec.commonmark.org/0.29/#backslash-escapes)
* [コード スパン](https://spec.commonmark.org/0.29/#code-spans)
* [タスク リスト](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [テーブル](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [絵文字](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [自動リンク](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

