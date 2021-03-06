---
title: NuGet パッケージ名の争いを解決する
description: ブランド、商標、その他の競合状況に関連する、NuGet パッケージ発行元間の争いを解決するためのプロセス。
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: d9ed7de95a1f38ea2c288b28958519b1dff0e595
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775656"
---
# <a name="resolving-disputes-over-nuget-package-names"></a>NuGet パッケージ名に関する争いを解決する

この記事では、他の NuGet 発行元との争いの解決を求めるコミュニティ メンバーに推奨される解決プロセスについて説明します。

たとえば、Northwind Traders がその Web サイトからダウンロードできる MSI としてドライバーをクライアントに提供する CRM システムを作るとします。 個人開発者の Nancy は Northwind のクライアント ライブラリを使いやすくしたいため、`NorthwindTraders.Client` という名前の NuGet パッケージに変えます。 その後、Northwind はそのクライアント ライブラリに独自の公式 NuGet パッケージを作りたくなり、パッケージ名に対する Nancy の所有権と争いになります。

このシナリオでは、Nancy には悪意がないように見え、それどころか、自分の時間を使ってコードを作り、Northwind のツールや顧客をサポートしています。 とは言え、Northwind 名の正当な所有者は Northwind です。

以下のプロセスに従うことで、Northwind と Nancy はしかるべき解決に向かい協力し合うことができます。いずれの当事者も開発者コミュニティに貢献することが目的であるからです。 一般的に、NuGet チームが関与する必要はありません。通常、当事者同士、互いの協力があれば問題なく解決します。

## <a name="process"></a>プロセス

1. パッケージ詳細ページの **[Contact Owners]\(所有者に問い合わせ\)** リンクを使い、争いの元になっているパッケージの所有者に連絡を取ります。 問題についてはっきりと、ただし穏やかに説明します。
2. [support@nuget.org](mailto:support@nuget.org) にメッセージのコピーを送信し、NuGet と .NET Foundation に争いについて知らせます。
3. 解決まで最大 30 日待ちます。それが過ぎたら、[support@nuget.org](mailto:support@nuget.org) に再度通知します。 nuget.org サポート チームが関与し、両当事者と共に解決に努めます。
