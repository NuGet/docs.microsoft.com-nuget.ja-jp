---
title: ユーザー データ要求
description: ユーザー データのエクスポートと削除を要求することに関する方針
author: karann-msft
ms.author: karann
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: ef054f741755bccf56eedfd462915b8e9fd6931a
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426987"
---
# <a name="user-data-requests"></a>ユーザー データ要求

nuget.org ユーザーは、[nuget.org](https://www.nuget.org) 経由で情報の削除要求とエクスポート要求を送信できます。いずれの要求もサポート要求として送信され、nuget.org 管理者が 30 日以内に実行します。

次のユーザー データには nuget.org から直接アクセスできます。

* メール アドレス、ログイン アカウント、プロファイルの写真、メール通知設定など、アカウント関連のデータ
* 所有している API キー
* 所有しているパッケージの一覧

このデータは、サポート要求でエクスポートされるデータに含まれません。

## <a name="identifying-customer-data"></a>顧客データを識別する

顧客データは nuget.org ユーザーアカウント名として識別できます。

## <a name="deleting-customer-data"></a>顧客データを削除する

nuget.org からユーザー データを削除することを要求するには:

1. ユーザーは [nuget.org](https://www.nuget.org) にサインインする必要があります
1. ユーザーはアカウントの削除要求を提出する必要があります [nuget.org/account/delete](https://www.nuget.org/account/delete)

ユーザーがパッケージの唯一の所有者である場合、アカウントの削除を要求する前に新しい所有者を探すことをお勧めします。 パッケージの所有権が譲渡されない場合、その NuGet パッケージは一覧から外れます。結果的に、Visual Studio や nuget.org Web サイトの検索クエリで利用できなくなります。 アカウントを削除する前に、nuget.org 管理者はユーザーと協力し、ユーザーが所有しているパッケージの新しい所有者を探します。

アカウントの削除アクションは、要求日から 30 日以内に nuget.org 管理者によって完了します。

アカウントの削除をもって、すべてのユーザー データが nuget.org システムから削除され、次のアクションが行われます。

* 削除したアカウントが nuget.org で登録解除になる
* 所有しているすべての API キーが削除される
* 予約されていたすべての名前空間が解放される
* あらゆるパッケージ所有権が削除される

所有しているパッケージは削除*されません*。 所有しているパッケージは検索結果の一覧からは外れますが、それに依存しているプロジェクトでは、パッケージの復元で引き続き利用できます。

## <a name="exporting-customer-data"></a>顧客データをエクスポートする

nuget.org にサインイン後、ユーザーは [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact) からエクスポート要求を提出できます。

ユーザーはエクスポートされたデータを Azure BLOB から 48 時間ダウンロードできます。 48 時間後にアクセスの有効期限が切れます。ユーザーは、必要であれば、新しいエクスポート要求を提出する必要があります。

次のデータがエクスポートされます。

* ユーザーのサポート要求
* 監査ログに残っているユーザーのアクション (パッケージの公開、アカウントの作成)
* IIS ログに残っているユーザー情報
