---
title: "NuGet のターゲット フレームワーク参照 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/11/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 4343a48e-f6df-4a44-9d66-4616c3caacf5
description: "NuGet ターゲット フレームワーク参照は、パッケージのフレームワーク依存コンポーネントを特定し、分離します。"
keywords: "NuGet パッケージのターゲット設定, .NET Framework のターゲット, .NET Framework のバージョン"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4d1d2e6850f22306d715b1c2071ee45b0eb050dc
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="target-frameworks"></a>ターゲット フレームワーク

NuGet は、多様な場所にあるターゲット フレームワーク参照を使用してパッケージのフレームワーク依存コンポーネントを特定し、分離します。

- [.nuspec マニフェスト](../schema/nuspec.md): パッケージは、プロジェクトのターゲット フレームワークに依存するプロジェクトに含めるパッケージを指定できます。
- [.nupkg フォルダー名](../create-packages/creating-a-package.md#from-a-convention-based-working-directory): パッケージの `lib` フォルダー内のフォルダーには、ターゲット フレームワークに従って名前を付けることができます。各フォルダーには、そのフレームワークに適した DLL や他のコンテンツが含まれます。
- [packages.config](../Schema/packages-config.md): 依存関係の `targetframework` 属性で、インストールするパッケージのバリエーションを指定します。
- [project.json](../Schema/project-json.md): `frameworks` ノードで、プロジェクトをコンパイルできるフレームワークのバージョンを指定します。

> [!Note]
> 以下の表を計算する NuGet クライアントのソース コードは、次の場所にあります。
> -  サポートされているフレームワーク名: [FrameworkConstants.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/FrameworkConstants.cs)
> -  フレームワークの優先順位とマッピング: [DefaultFrameworkMappings.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/DefaultFrameworkMappings.cs)

## <a name="supported-frameworks"></a>サポートされるフレームワーク

通常、フレームワークは、短いターゲット フレームワーク モニカー (TFM) で参照されます。 .NET Standard の場合、1 つの参照で複数のフレームワークを参照できるように、*TxM* に汎用化されています。

NuGet クライアントは以下の表のフレームワークをサポートしています。 同等のものがかっこ [] 内に示されています。 `dotnet` などの一部のツールは、一部のファイルで正規の TFM のバリエーションを使用することがあります。 たとえば、`dotnet pack` は `.nuspec` ファイルで `netcoreapp2.0` ではなく `.NETCoreApp2.0` を使用します。 さまざまな NuGet クライアント ツールがこれらのバリエーションを適切に処理しますが、ファイルを直接編集するときは常に正規の TFM を使用することをお勧めします。

| 名前           | 省略形 | TFM/TxM |
| -------------  | ------------ | --------- |
|.NET Framework  | net          | net11     |
|                |              | net20     |
|                |              | net35     |
|                |              | net40     |
|                |              | net403    |
|                |              | net45      |
|                |              | net451     |
|                |              | net452     |
|                |              | net46      |
|                |              | net461     |
|                |              | net462     |
|Windows ストア   | netcore      | netcore [netcore45] |
|                |              | netcore45 [win、win8] |
|                |              | netcore451 [win81] |
|                |              | netcore50 |
|.NET MicroFramework | netmf    | netmf |
|Windows         | win          | win [win8, netcore45] |
| | | win8 [netcore45, win] |
| | | win81 [netcore451] |
| | | win10 (Windows 10 プラットフォームではサポートされていません) |
Silverlight | sl | sl4 |
| | | sl5 |
Windows Phone (SL) | wp | wp [wp7] |
| | | wp7 |
| | | wp75 |
| | | wp8 |
| | | wp81 |
Windows Phone (UWP) | | wpa81 |
ユニバーサル Windows プラットフォーム | uap | uap [uap10.0] |
| | | uap10.0 |
.NET Standard | netstandard | netstandard1.0 |
| | | netstandard1.1 |
| | | netstandard1.2 |
| | | netstandard1.3 |
| | | netstandard1.4 |
| | | netstandard1.5 |
| | | netstandard1.6 |
| | | netstandard2.0 |
.NET Core アプリ | netcoreapp | netcoreapp1.0 |
| | | netcoreapp1.1 |
| | | netcoreapp2.0 |
Tizen | tizen | tizen3 |
| | | tizen4 |

## <a name="deprecated-frameworks"></a>使用されていないフレームワーク
次のフレームワークは使用されていません。 これらのフレームワークを対象とするパッケージは、指定されている代替のフレームワークに移行するようにしてください。

| 使用されていないフレームワーク | Replacement
| --- | ---
| aspnet50 | netcoreapp |
| aspnetcore50 |
| dnxcore50 |
| dnx |
| dnx45 |
| dnx451 |
| dnx452 |
| dotnet | netstandard |
| dotnet50 | |
| dotnet51 | |
| dotnet52 | |
| dotnet53 | |
| dotnet54 | |
| dotnet55 | |
| dotnet56 | |
| winrt | win |

## <a name="precedence"></a>優先順位

フレームワークの番号は相互の関連性や互換性を示していますが、必ずしも同一ではありません。

| フレームワーク | 使用可能 |
| --- | --- |
| uap (ユニバーサル Windows プラットフォーム) | win81 |
| | wpa81 |
| | netcore50 |
| win (Microsoft Store) | winrt |
| | | winrt45 |

## <a name="net-platform-standard"></a>.NET Platform Standard

[.NET Platform Standard](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/net-platform-standard.md) は、バイナリ互換フレームワーク間の参照を簡易化し、1 つのターゲット フレームワークで複数のフレームワークの組み合わせを参照できます (背景については、「[.NET のガイド](https://docs.microsoft.com/dotnet/articles/standard/index)」を参照してください。)。

[NuGet の Get Nearest Framework Tool](https://aka.ms/s2m3th) では、プロジェクトのフレームワークに基づいて、パッケージ内で使用できる複数のフレームワーク アセットから、1 つのフレームワークを選択するために使用する NuGet をシミュレートしています。

NuGet 3.3 以前には `dotnet` シリーズのモニカーを使用し、v3.4 以降には `netstandard` モニカー構文を使用することをお勧めします。

## <a name="portable-class-libraries"></a>ポータブル クラス ライブラリ

> [!Warning]
> **PCL はお勧めできません**。 PCL はサポートされていますが、パッケージ作成者は代わりに netstandard をサポートすることをお勧めします。 .NET Platform Standard は PCL が進化したものです。また、*portable-a+b+c* モニカーのような静的なものに関連付けられていない単一のモニカーを使用する、プラットフォームをまたぐバイナリ移植性を表します。

複数の子ターゲット フレームワークを参照するターゲット フレームワークを定義するには、参照されるフレームワークの一覧に接頭辞として `portable` キーワードを使用します。 このようなフレームワークでは意図しない副作用を招く可能性があるため、直接コンパイルされない余計なフレームワークは人為的に含めないようにしてださい。

第三者によって定義された追加のフレームワークは、この方法でアクセスできる他の環境との互換性を提供します。 さらに、これらの関連するフレームワークの組み合わせを `Profile#` として参照するために使用できる省略形のプロファイル番号がありますが、フォルダーと `.nuspec` の読みやすさが低下するため、このような番号を使用することは勧められません。

| プロファイル番号 | フレームワーク | 完全名 | .NET Standard |
 --- | --- | --- | ---
 Profile2 | .NETFramework 4.0 | portable-net40+win8+sl4+wp7 |
 | | Windows 8.0 | |
 | | Silverlight 4.0 |
 | | WindowsPhone 7.0|
 Profile3 | .NETFramework 4.0 | portable-net40+sl4
 | | Silverlight 4.0 |
 Profile4 | .NETFramework 4.5 | portable-net45+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile5 | .NETFramework 4.0 | portable-net40+win8
 | | Windows 8.0 |
 Profile6 | .NETFramework 4.0.3 | portable-net403+win8
 | | Windows 8.0 |
 Profile7 | .NETFramework 4.5 | portable-net45+win8 | netstandard1.1
 | | Windows 8.0 |
 Profile14 | .NETFramework 4.0 | portable-net40+sl5
 | | Silverlight 5.0 |
 Profile18 | .NETFramework 4.0.3 | portable-net403+sl4
 | | Silverlight 4.0 |
 Profile19 | .NETFramework 4.0.3 | portable-net403+sl5
 | | Silverlight 5.0 |
 Profile23 | .NETFramework 4.5 | portable-net45+sl4
 | | Silverlight 4.0 |
 Profile24 | .NETFramework 4.5 | portable-net45+sl5
 | | Silverlight 5.0 |
 Profile31 | Windows 8.1 | portable-win81+wp81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 Profile32 | Windows 8.1 | portable-win81+wpa81 | netstandard1.2
 | | WindowsPhone 8.1 (UWP) |
 Profile36 | .NETFramework 4.0 | portable-net40+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile37 | .NETFramework 4.0 | portable-net40+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile41 | .NETFramework 4.0.3 | portable-net403+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile42 | .NETFramework 4.0.3 | portable-net403+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile44 | .NETFramework 4.5.1 | portable-net451+win81 | netstandard1.2
 | | Windows 8.1 |
 Profile46 | .NETFramework 4.5 | portable-net45+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile47 | .NETFramework 4.5 | portable-net45+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile49 | .NETFramework 4.5 | portable-net45+wp8 | netstandard1.0
 | | WindowsPhone 8.0 (SL) |
 Profile78 | .NETFramework 4.5 | portable-net45+win8+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile84 | WindowsPhone 8.1 | portable-wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (UWP) |
 Profile88 | .NETFramework 4.0 | portable-net40+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile92 | .NETFramework 4.0 | portable-net40+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile95 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile96 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile102 | .NETFramework 4.0.3 | portable-net403+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile104 | .NETFramework 4.5 | portable-net45+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile111 | .NETFramework 4.5 | portable-net45+win8+wpa81 | netstandard1.1
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile136 | .NETFramework 4.0 | portable-net40+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile143 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile147 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile151 | NETFramework 4.5.1 | portable-net451+win81+wpa81 | netstandard1.2
 | | Windows 8.1 |
 | | WindowsPhone 8.1 (UWP) |
 Profile154 | .NETFramework 4.5 | portable-net45+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile157 | Windows 8.1 | portable-win81+wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 | | WindowsPhone 8.1 (UWP) |
 Profile158 | .NETFramework 4.5 | portable-net45+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile225 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile240 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile255 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile259 | .NETFramework 4.5 | portable-net45+win8+wpa81+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile328 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile336 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile344 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |

さらに、Xamarin をターゲットとする NuGet パッケージでは、Xamarin で定義された他のフレームワークも使用することができます。 [Xamarin 用の NuGet パッケージの作成](https://developer.xamarin.com/guides/cross-platform/advanced/nuget/)に関するページを参照してください。

| 名前 | 説明 | .NET Standard |
| --- | --- | ---
| monoandroid | Android OS の Mono サポート | netstandard1.4 |
| monotouch | iOS の Mono サポート | netstandard1.4 |
| monomac | OSX の Mono サポート | netstandard1.4 |
| xamarinios | Xamarin for iOS のサポート | netstandard1.4 |
| xamarinmac | Xamarin for Mac のサポート | netstandard1.4 |
| xamarinpsthree | Playstation 3 上の Xamarin のサポート | netstandard1.4 |
| xamarinpsfour | Playstation 4 上の Xamarin のサポート | netstandard1.4 |
| xamarinpsvita | PS Vita 上の Xamarin のサポート | netstandard1.4 |
| xamarinwatchos | Xamarin for Watch OS | netstandard1.4 |
| xamarintvos | Xamarin for TV OS | netstandard1.4 |
| xamarinxboxthreesixty | Xamarin for XBox 360 | netstandard1.4 |
| xamarinxboxone | Xamarin for XBox One | netstandard1.4 |

> [!Note]
> Stephen Cleary により、サポートされる PCL を一覧表示するツールが作成されました。このツールは、「[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html)」(.NET のフレームワーク プロファイル) の投稿に掲載されています。
