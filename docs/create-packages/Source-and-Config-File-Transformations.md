---
title: NuGet パッケージのソースと config ファイルの変換
description: インストール時にソース コードと構成 (XML) ファイルを変換する NuGet パッケージの機能について説明します。
author: JonDouglas
ms.author: jodou
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 76c589b5ad034127675fb2bbf79ea97992883ebe
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859110"
---
# <a name="transforming-source-code-and-configuration-files"></a>ソース コードと構成ファイルの変換

**ソース コード変換** は、パッケージがインストールされるときに、パッケージの `content` または `contentFiles` フォルダー (`packages.config` を使用している場合は `content`、`PackageReference` を使用している場合は `contentFiles`) のファイルに一方向トークンの置き換えを適用します。この場合、トークンは、Visual Studio [プロジェクトのプロパティ](/dotnet/api/vslangproj.projectproperties)を参照します。 これにより、プロジェクトの名前空間にファイルを挿入したり、ASP.NET プロジェクトで通常は `global.asax` に置かれるコードをカスタマイズしたりすることができます。

**構成ファイルの変換** を使用して、`web.config` や `app.config` などのターゲット プロジェクトに既に存在するファイルを変更することができます。 たとえば、場合によっては、パッケージで構成ファイルの `modules` セクションに項目を追加する必要があります。 この変換は、構成ファイルに追加するセクションを記述するパッケージ内の特別なファイルを含めることで行われます。 パッケージがアンインストールされるときには、同じ変更が、逆に行われ、これを双方向の変換にします。

## <a name="specifying-source-code-transformations"></a>変換のソース コードを指定する

1. パッケージからプロジェクトに挿入するファイルは、パッケージ内の `content` および `contentFiles` フォルダーに配置する必要があります。 たとえば、`ContosoData.cs` という名前のファイルをターゲット プロジェクトの `Models` フォルダーにインストールする場合は、パッケージの `content\Models` および `contentFiles\{lang}\{tfm}\Models` フォルダー内にファイルが置かれている必要があります。

1. インストール時にトークンの置換を適用するように NuGet に指示するには、`.pp` をソース コード ファイル名に追加します。 インストール後、ファイルには `.pp` 拡張子は付きません。

    たとえば、`ContosoData.cs` で変換を行うには、パッケージ内のファイルに `ContosoData.cs.pp` という名前を付けます。 インストール後には、`ContosoData.cs` として表示されます。

1. ソース コード ファイル内では、`$token$` 形式の大文字と小文字が区別されないトークンを使用し、NuGet でプロジェクトのプロパティと置き換える必要がある値を示します。

    ```cs
    namespace $rootnamespace$.Models
    {
        public struct CategoryInfo
        {
            public string categoryid;
            public string description;
            public string htmlUrl;
            public string rssUrl;
            public string title;
        }
    }
    ```

    インストール時に、NuGet が、ターゲット プロジェクトのルート名前空間が `Fabrikam` であると仮定して、`$rootnamespace$` を `Fabrikam` に置き換えます。

`$rootnamespace$` トークンは、最もよく使用されるプロジェクト プロパティです。他のすべてのトークンは、[プロジェクト プロパティ](/dotnet/api/vslangproj.projectproperties)に関するページに一覧表示されています。 当然ながら、一部のプロパティはプロジェクトの種類に固有である可能性があります。

## <a name="specifying-config-file-transformations"></a>構成ファイルの変換を指定する

以降のセクションで後述するように、2 つの方法で構成ファイルの変換を実行できます。

- `app.config.transform` および `web.config.transform` ファイルをパッケージの `content` フォルダーに含めます。`.transform` 拡張子は、パッケージがインストールされるときに、これらのファイルが既存の構成ファイルにマージする XML を含んでいることを NuGet に指示します。 パッケージがアンインストールされると、その同じ XML が削除されます。
- `app.config.install.xdt` および `web.config.install.xdt` ファイルをパッケージの `content` フォルダーに含めるときに、[XDT 構文](/previous-versions/aspnet/dd465326(v=vs.110))を使用して、目的の変更を記述します。 このオプションを使用して、`.uninstall.xdt` ファイルも含め、プロジェクトからパッケージが削除されるときに変更を逆に実行することもできます。

> [!Note]
> 変換は、Visual Studio でリンクとして参照されている `.config` ファイルには適用されません。

XDT を使用することの利点は、2 つの静的なファイルを単純にマージする代わりに、XPath が完全にサポートされる要素と属性のマッチングを使用して XML DOM の構造を操作するための構文を提供することです。 XDT はその後で、要素の追加、更新、削除、指定した場所での新しい要素の配置、要素の置換/削除 (子ノードを含む) を行うことができます。 これにより、パッケージのインストール中に実行されたすべての変換を元に戻すアンインストール変換を簡単に作成できるようになります。

### <a name="xml-transforms"></a>XML 変換

パッケージの `content` フォルダーの `app.config.transform` と `web.config.transform` は、プロジェクトの既存の `app.config` および `web.config` ファイルにマージする要素のみを含んでいます。

例のように、プロジェクトが最初に `web.config` 内に次のコンテンツを含んでいると仮定します。

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

パッケージのインストール中に `MyNuModule` 要素を `modules` セクションに追加するには、次のような `web.config.transform` ファイルをパッケージの `content` フォルダー内に作成します。

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

NuGet がパッケージをインストールした後に、`web.config` は次のように表示されます。

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

NuGet が `modules` セクションを置き換えずに、新しい要素と特性のみを追加することによって単純に新しいエントリをその中にマージしています。 NuGet は、どの既存の要素または属性も変更しません。

パッケージがアンインストールされるときに、NuGet は、`.transform` ファイルをもう一度調べ、含まれている要素を適切な `.config` ファイルから削除します。 このプロセスは、パッケージのインストール後に変更する `.config` ファイルのどの行にも影響しません。

広範な例として、[Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) パッケージは、多くのエントリを `web.config` に追加し、それらもパッケージがアンインストールされるときに削除されます。

その `web.config.transform` ファイルを調べるには、ELMAH パッケージを上記のリンクからダウンロードし、パッケージの拡張子を `.nupkg` から `.zip` に変更して、`content\web.config.transform` をその ZIP ファイル内から開きます。

パッケージのインストールおよびアンインストールの影響を確認するには、新しい ASP.NET プロジェクトを Visual Studio で作成し (テンプレートは、[新しいプロジェクト] ダイアログ ボックスの **[Visual C#] > [Web]** にあります)、空の ASP.NET アプリケーションを選択します。 `web.config` を開いて初期状態を確認します。 プロジェクトを右クリックし、**[NuGet パッケージの管理]** を選択し、nuget.org で ELMAH を見つけて、最新バージョンをインストールします。 `web.config` のすべての変更に注意してください。 次に、パッケージをアンインストールすると、`web.config` が前の状態に戻ります。

### <a name="xdt-transforms"></a>XDT 変換

> [!Note]
> [`packages.config` から `PackageReference` への移行に関するドキュメントのパッケージの互換性の問題に関するセクション](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues)で説明したように、XDT 変換は、以下で説明するように、`packages.config` でのみサポートされています。 次のファイルをパッケージに追加すると、`PackageReference` でパッケージを使用しているコンシューマーには変換が適用されません (XDT 変換を `PackageReference` で動作するようにするには、[このサンプル](https://github.com/NuGet/Samples/tree/main/XDTransformExample)を参照してください)。

[XDT 構文](/previous-versions/aspnet/dd465326(v=vs.110))を使用して構成ファイルを変更することができます。 `$` 区切り文字 (大文字と小文字は区別されません) 内にプロパティ名を含めることにより、NuGet でトークンを[プロジェクト プロパティ](/dotnet/api/vslangproj.projectproperties)に置き換えることもできます。

たとえば、次の `app.config.install.xdt` ファイルは、プロジェクトの `FullPath`、`FileName`、`ActiveConfigurationSettings` 値を含む `app.config` に `appSettings` 要素を挿入します。

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <appSettings xdt:Transform="Insert">
        <add key="FullPath" value="$FullPath$" />
        <add key="FileName" value="$filename$" />
        <add key="ActiveConfigurationSettings " value="$ActiveConfigurationSettings$" />
    </appSettings>
</configuration>
```

別の例で、プロジェクトが最初に `web.config` 内に次のコンテンツを含んでいると仮定します。

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

パッケージのインストール中に `MyNuModule` 要素を `modules` セクションに追加するために、パッケージの `web.config.install.xdt` は次を含んでいます。

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" xdt:Transform="Insert" />
        </modules>
    </system.webServer>
</configuration>
```

パッケージをインストールした後、`web.config` は次のようになります。

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

パッケージのアンインストール中に `MyNuModule` 要素のみを削除するには、`web.config.uninstall.xdt` ファイルは、次を含む必要があります。

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" xdt:Transform="Remove" xdt:Locator="Match(name)" />
        </modules>
    </system.webServer>
</configuration>
```