---
title: ID プレフィックス予約リファレンス |Microsoft ドキュメント
author: diverdan92
ms.author: diverdan92
manager: unniravindranathan
ms.date: 10/09/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: パッケージ ID プレフィックス予約機能の説明、作成者ガイドです。
keywords: NuGet パッケージ ID、プレフィックス、予約
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 7b1956612bd48a1c59503418f1a4d7d9dee900f5
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="package-id-prefix-reservation"></a>パッケージ ID のプレフィックスの予約

パッケージの所有者では、予約でき、ID のプレフィックスを予約して自身の id を保護することができます。 パッケージ使用者が追加情報をパッケージの使用時に消費しているか、パッケージは、識別プロパティの不正な提供されます。 

[nuget.org](https://www.nuget.org/)し、パッケージには予約済み ID が一致する限り、予約済みのパッケージ ID のプレフィックスの所有者から送信されたパッケージの名前付けパターンのプレフィックスの Visual Studio 2017 15.4 またはそれ以降のバージョンが視覚インジケータを表示します。 下方向へ ID プレフィックス予約任せます、ID のプレフィックスの所有者を適用する方法について説明します。

## <a name="id-prefix-reservation-details"></a>ID プレフィックス予約の詳細

パッケージ ID のプレフィックスは予約されていますがと、にいくつかの処理が行われます、 [nuget.org](https://www.nuget.org/)ギャラリーも Visual Studio と同様にします。 さらに、'public' として、複数の所有者にプレフィックスのサブセットを委任するプレフィックスを設定するなど、ID プレフィックス予約によってサポートされるシナリオ、上級です。

### <a name="id-prefix-reservation-on-nugetorg"></a>Nuget.org の ID のプレフィックスの予約

プレフィックスが予約されて[nuget.org](https://www.nuget.org/)次が発生します。

1. プレフィックス予約に関連付けられている所有者または所有者のセットで[nuget.org](https://www.nuget.org/)です。

1. パッケージを送信するたびに[nuget.org](https://www.nuget.org/) ID のプレフィックスを予約済みの所有者から発生しない限り、予約済み ID のプレフィックスに一致する ID を持つパッケージが拒否されました。

1. Visual Studio 2017 バージョン 15.4 以降で、予約済み ID のプレフィックスに一致し、ID のプレフィックスを予約されている所有者に由来するパッケージは視覚的になります[nuget.org](https://www.nuget.org/)パッケージがあることを示す予約済み ID プレフィックス。 これは新しいパッケージの送信と所有者の下にある既存のパッケージの両方に当てはまります。 **注:**単一フィードがパッケージのソースとして選択されている場合にのみ、Visual Studio でのインジケーターが表示されます。

1. 予約済み ID のプレフィックスに一致するすべての既存のパッケージが、*いない*予約済みの所有者によって所有されているプレフィックスは変更されません (、一覧にないことはできませんが、視覚インジケーターが付いていませんも)。 さらに、これらのパッケージの所有者は、パッケージに新しいバージョンを送信できます。

これらの変更は、次の条件に基づいており、いくつかの追加制限します。

- パッケージの 1 つだけの所有者には、(複数の所有者を持つパッケージ) 用に表示される視覚インジケータの予約済みのプレフィックスが必要です。

- 場所 1 つまたは複数の所有者には、予約済みのプレフィックスと、1 つまたは複数の所有者には、予約済みのプレフィックスはありません。 パッケージの 1 つ以上の所有者がある場合、予約済みのプレフィックスを持つ所有者だけは予約されたプレフィックスを持つ他の従属性を削除できます。 予約済みのプレフィックスを持たない所有者は、予約済みのプレフィックスを持つ所有者を削除できません。 ほかの所有者もない予約済みのプレフィックスを削除することもできます。

- パッケージが視覚インジケーターを持つ、*常に*視覚インジケーターがある (予約済みのプレフィックスを持つ、少なくとも 1 つその所有者の保証は常に、所有者)

### <a name="advanced-prefix-reservation-scenarios"></a>高度なプレフィックス予約シナリオ

Subprefix 委任、および public としてマーキング プレフィックスを含めて、次に示すいくつかのより高度なプレフィックス予約シナリオがあります。 可能なプレフィックスのより高度な予約を以下に示します。 

- プレフィックス予約中に、所有者は、その他の所有者にプレフィックスのサブセットの委任 (プレフィックス) を要求できます。 たとえば場合、'[Microsoft](https://www.nuget.org/profiles/microsoft)'を所有している' Microsoft\*'、が、'[aspnet](https://www.nuget.org/profiles/aspnet)'に予約する必要がある' Microsoft.AspNet。\*'、'[Microsoft](https://www.nuget.org/profiles/microsoft)' ことができます。デリゲートを ' Microsoft.AspNet です。\*' に、 [aspnet](https://www.nuget.org/profiles/aspnet)アカウント。

- プレフィックス予約中に、プレフィックスを公開して、所有者を選択できます。 これは許可することを示すこと、パッケージは、予約済みのプレフィックスから発生しますが、視覚インジケータ**いない**任意の所有者のプレフィックスに将来のパッケージの送信をブロックします。 これは、オープン ソース プロジェクトは、多くの共同作成者の場合に便利です - 上部または core の投稿者で予約されたプレフィックスを持つことができますが、すべてのコントリビューターに開いていることができます。 

### <a name="prefix-reservation-visual-indicator"></a>プレフィックスの予約の視覚インジケーター

表示、パッケージのソース予約済みのプレフィックスがの視覚インジケーターの下、 [nuget.org](https://www.nuget.org/)ギャラリーと Visual Studio 2017 15.4 またはそれ以降のバージョン。

**nuget.org ギャラリー**
![nuget.org ギャラリー](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>ID プレフィックスの予約アプリケーション プロセス

1. 確認して、受け入れ[プレフィックス ID 予約の条件](#id-prefix-reservation-criteria)です。

1. 他にも、予約する名前空間を決定[プレフィックス予約シナリオを高度な](#advanced-prefix-reservation-scenarios)が必要な場合があります。

1. 電子メールを送信[ account@nuget.org ](mailto:account@nuget.org)オーナーを使用して表示名で[nuget.org](https://www.nuget.org/)、要求している、予約済みのプレフィックスとします。 複数の所有者にプレフィックスのサブセットを委任する場合は、すべての所有者の表示名を説明し、サブセットのプレフィックスを確認します。

アプリケーションが送信されるへの同意または拒否の原因となった条件) (の却下の通知されます。 所有者の身元を識別する追加の質問を投稿する必要があります。

### <a name="id-prefix-reservation-criteria"></a>ID プレフィックス予約条件

ID プレフィックスの予約のすべてのアプリケーションを表示するときに、 [nuget.org](https://www.nuget.org/)チームに対してアプリケーションを評価する、条件の下。 プレフィックスを予約に満たす必要がないすべての条件が必要ですが、(後で指定された説明) が満たされている条件の大幅な証拠が存在しない場合、アプリケーションが拒否された可能性があります。

1. パッケージ ID プレフィックス適切かつ明確に識別パッケージの所有者ですか。

1. パッケージ ID のプレフィックスの所有者によって多数の送信済みのパッケージとは

1. パッケージ ID のプレフィックスを任意の所有者または組織に属する必要がありますいないを共通のものですか。

1. *いない*あいまいさとコミュニティの混乱が発生するパッケージ ID のプレフィックスを予約しますか?

1. パッケージ ID プレフィックス、はっきりと一貫性のある (特に、パッケージの作成者) に一致するパッケージの識別プロパティとは

## <a name="third-party-feed-provider-scenarios"></a>サード パーティ製のフィード プロバイダー シナリオ

サード パーティのフィード プロバイダーがプレフィックスの予約を提供する独自のサービスを実装する目的の場合は、NuGet V3 で search サービスのプロバイダーのフィードを変更してようにを行うことができます。 フィードの search サービスの追加は、追加する、*検証*V3 フィードを次の例のプロパティです。 NuGet クライアントは、フィード、V2 で追加されたプロパティをサポートしていません。

詳細については、次を参照してください。、 [API の search サービスに関するドキュメント](../api/search-query-service-resource.md)です。
