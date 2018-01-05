---
title: "NuGet の動作を構成する | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: c1e34826-d07d-4609-a0fd-123459ae89c5
description: "NuGet.Config ファイルは、グローバルとプロジェクト単位の両方で NuGet の動作を制御し、変更するには nuget config コマンドを使います。"
keywords: "NuGet 構成ファイル, NuGet の構成, NuGet の動作の設定, NuGet の設定, Nuget.Config, NuGetDefaults.Config, 既定値"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f9e56b68f70387435cdaa1537db503abb912fd2a
ms.sourcegitcommit: 122bf7ce308365ea45da018b0768f0536de76a1f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="configuring-nuget-behavior"></a>NuGet の動作を構成する

NuGet の動作は、1 つ以上の `NuGet.Config` (XML) ファイルの設定を総合して決まります。ファイルは、プロジェクト レベル、ユーザー レベル、およびコンピューター全体レベルで作成できます。 特にパッケージ ソースを構成するグローバルな `NuGetDefaults.Config` ファイル (2.7 以降) まありす。 設定は、CLI、パッケージ マネージャー コンソール、パッケージ マネージャー UI で発行されるすべてのコマンドに適用されます。

このトピックの内容

- [NuGet.Config ファイルの場所と使用](#config-file-locations-and-uses)
- [設定の変更](#changing-config-settings)
- [設定の適用方法](#how-settings-are-applied)
- [NuGetDefaults.Config ファイル](#nuget-defaults-file)

## <a name="config-file-locations-and-uses"></a>構成ファイルの場所と使用

| スコープ | NuGet.Config ファイルの場所 | 説明 |
| --- | --- | --- |
| プロジェクト | プロジェクト フォルダーまたはドライブのルートまでの任意のフォルダー | プロジェクト フォルダーにある場合は、設定はそのプロジェクトのみに適用されます。 複数のプロジェクト サブフォルダーを含む親フォルダーにある場合は、設定はそれらのサブフォルダーのすべてのプロジェクトに適用されます。 |
| ユーザー | Windows: %APPDATA%\NuGet\NuGet.Config<br/>Mac/Linux: ~/.nuget/NuGet.Config | 設定はすべての操作に適用されますが、プロジェクト レベルの設定によって上書きされます。 CLI コマンドの場合は、`-configFile` スイッチを使って別の構成ファイルを指定し、既定のユーザー レベルのファイルの設定を無視することができます。 |
| コンピューター | Windows: %ProgramFiles(x86)%\NuGet\Config<br/>Mac/Linux: $XDG_DATA_HOME (通常は ~/.local/share) | 設定はそのコンピューターでのすべての操作に適用されますが、ユーザー レベルまたはプロジェクト レベルの設定によって上書きされます。 |

以前のバージョンの NuGet に関する注意事項:
- NuGet 3.3 以前では、ソリューション全体の設定用に `.nuget` フォルダーが使われていました。 このファイルは、NuGet 3.4 以降では使われません。
- NuGet 2.6 から 3.x では、Windows でのコンピューター レベルの構成ファイルは %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config にありました。*{IDE}* には *VisualStudio* を使用でき、*{Version}* は Visual Studio のバージョン (*14.0* など)、*{SKU}* は *Community*、*Pro*、または *Enterprise* です。 設定を NuGet 4.0 以降に移行するには、単に構成ファイルを %ProgramFiles(x86)%\NuGet\Config にコピーします。Linux の以前の場所は /etc/opt、Mac の以前の場所は /Library/Application Support でした。

## <a name="changing-config-settings"></a>構成設定の変更

`NuGet.Config` ファイルは、[NuGet の構成設定](../Schema/nuget-config-file.md)に関するトピックで説明されているように、キーと値のペアを含む単純な XML テキスト ファイルです。

設定は、NuGet CLI の [config コマンド](../tools/cli-ref-config.md)を使って管理します。
- 既定では、変更はユーザー レベルの構成ファイルに対して行われます。
- 別のファイルの設定を変更するには、`-configFile` スイッチを使います。 その場合は、任意のファイル名を使うことができます。
- キーは常に大文字と小文字が区別されます。
- コンピューター レベルの設定ファイルの設定を変更するには、特権の昇格が必要です。

> [!Warning]
> 任意のテキスト エディターでファイルを変更できますが、NuGet (v3.4.3 以降) では、構成ファイルに正しくない形式の XML (タグの不一致、無効な引用符など) が含まれると、警告なしに構成ファイル全体が無視されます。 このため、設定の管理には `nuget config` を使うことをお勧めします。

### <a name="setting-a-value"></a>値の設定

Windows の場合:

```
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\NuGet.Config
```

Mac/Linux の場合:

```
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=/home/packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=/home/projects/packages -configfile /home/my.Config
nuget config -set repositoryPath=/home/packages -configfile home/myApp/NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=/home/packages -configfile $XDG_DATA_HOME/NuGet.Config
```

> [!Note]
> NuGet 3.4 以降では、`repositoryPath=%PACKAGEHOME%` (Windows) および `repositoryPath=%PACKAGEHOME` (Mac/Linux) のように、すべての値で環境変数を使うことができます。

### <a name="removing-a-value"></a>値の削除

値を削除するには、値を空にしてキーを指定します。

```
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>新しい構成ファイルの作成

次のテンプレートを新しいファイルにコピーした後、`nuget config --configFile <filename>` を使って値を設定します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

<br/>

## <a name="how-settings-are-applied"></a>設定の適用方法

複数の `NuGet.Config` ファイルを使って設定を異なる場所に格納することで、1 つのプロジェクト、プロジェクトのグループ、またはすべてのプロジェクトに設定を適用できます。 これらの設定は、コマンド ラインまたは Visual Studio から呼び出されるすべての NuGet 操作に集合的に適用され、プロジェクトまたは現在のフォルダーの "最も近く" に存在する設定が優先されます。

具体的には、NuGet は次の順序で異なる構成ファイルから設定を読み込みます。

1. [NuGetDefaults.Config ファイル](#nuget-defaults-file)。パッケージ ソースのみに関連する設定が含まれます。
1. コンピューター レベルのファイル。
1. ユーザー レベルのファイル。
1. `-configFile` で指定されたファイル。
1. ドライブ ルートから現在のフォルダー (nuget.exe が呼び出されたフォルダー、または Visual Studio プロジェクトを含むフォルダー) までの間のパスに存在するすべてのフォルダーで見つかったファイル。 たとえば、コマンドが c:\A\B\C で呼び出された場合、NuGet は c:\,、c:\A、c:\A\B、c:\A\B\C の順序で構成ファイルを探して読み込みます。

NuGet はこれらのファイルで設定を探すので、適用は次のようになります。

1. 単一項目の要素の場合は、前に検出された同じキーの値が置き換えられます。 つまり、現在のフォルダーまたはプロジェクトに "最も近い" 設定が、それより前に見つかった他の値を上書きします。 たとえば、`NuGetDefaults.Config` の設定 `defaultPushSource` は、他の構成ファイルにも存在する場合は上書きされます。

1. コレクション要素の場合は (`<packageSources>` など)、すべての構成ファイルの値が 1 つのコレクションに結合されます。

1. 指定されたノードに `<clear />` が存在すると、そのノードより前に定義された構成値は無視されます。

### <a name="settings-walkthrough"></a>設定のチュートリアル

2 つの異なるドライブに次のフォルダー構造があるものとします。

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

その場合、次の場所にそれぞれ指定された内容の `NuGet.Config` ファイルが 4 つ存在します  (コンピューター レベルのファイルはこの例には含まれませんが、ユーザー レベルのファイルと同じように動作します)。

ファイル A: ユーザー レベル ファイル (Windows では %APPDATA%\NuGet\NuGet.Config、Mac/Linux では ~/.nuget/NuGet.Config):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

ファイル B: disk_drive_2/NuGet.Config:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>        
        <add key="repositoryPath" value="disk_drive_2/tmp" />
    </config>
    <packageRestore>
        <add key="enabled" value="True" />
    </packageRestore>
</configuration>
```

ファイル C: disk_drive_2/Project1/NuGet.Config:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="External/Packages" />
        <add key="defaultPushSource" value="https://MyPrivateRepo/ES/api/v2/package" />
    </config>
    <packageSources>
        <clear /> <!-- ensure only the sources defined below are used -->
        <add key="MyPrivateRepo - ES" value="https://MyPrivateRepo/ES/nuget" />
    </packageSources>
</configuration>
```

ファイル D: disk_drive_2/Project2/NuGet.Config:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

NuGet は、呼び出された場所に応じて、次のように設定を読み込んで適用します。

- **disk_drive_1/users から呼び出された場合**: disk_drive_1 で検出されるのはユーザー レベルの構成ファイル (A) だけなので、(A) で指定されている既定のリポジトリのみが使われます。

- **disk_drive_2/ または disk_drive_/tmp から呼び出された場合**: NuGet は、最初にユーザー レベルのファイル (A) を読み込んだ後、disk_drive_2 のルートに移動して、ファイル (B) を検出します。 NuGet は /tmp でも構成ファイルを検索しますが、見つかりません。 その結果、nuget.org の既定のリポジトリが使われ、パッケージの復元が有効になり、パッケージが disk_drive_2/tmp に展開されます。

- **disk_drive_2/Project1 または disk_drive_2/Project1/Source から呼び出された場合**: NuGet は、最初にユーザー レベルのファイル (A) を読み込み、次に disk_drive_2 のルートからファイル (B) を読み込み、最後にファイル (C) を読み込みます。 (C) の設定で (B) および (A) の設定が上書きされるので、パッケージがインストールされる `repositoryPath` は、*disk_drive_2/tmp* ではなく disk_drive_2/Project1/External/Packages です。 また、(C) は `<packageSources>` をクリアするので、ソースは `https://MyPrivateRepo/ES/nuget` だけになり、nuget.org は使うことができなくなります。

- **disk_drive_2/Project2 または disk_drive_2/Project2/Source から呼び出された場合**: ユーザー レベルのファイル (A)、ファイル (B)、ファイル (D) の順に読み込まれます。 `packageSources` はクリアされないので、`nuget.org` と `https://MyPrivateRepo/DQ/nuget` の両方をソースとして使うことができます。 パッケージは、(B) で指定されている disk_drive_2/tmp に展開されます。

## <a name="nuget-defaults-file"></a>NuGet の既定のファイル

パッケージのインストール元および更新元であるパッケージ ソースを指定し、`nuget push` でパッケージを公開するときの既定のターゲットを制御するため、`NuGetDefaults.Config` ファイルが存在します。 管理者は開発用およびビルド用のコンピューターに整合性のある `NuGetDefaults.Config` ファイルを容易に (たとえば、グループ ポリシーを使って) 展開できるので、組織内のすべてのユーザーが nuget.org ではなく適切なパッケージ ソースを使うようにすることができます。

> [!Important]
> `NuGetDefaults.Config` ファイルにより、パッケージ ソースが開発者の NuGet 構成から削除されることはありません。 つまり、開発者が既に NuGet を使っていて、したがって nuget.org パッケージ ソースが登録されている場合、`NuGetDefaults.Config` ファイルの作成後に nuget.org は削除されません。
>
> さらに、`NuGetDefaults.Config` または NuGet の他のメカニズムのどちらでも、nuget.org などのパッケージ ソースへのアクセスを禁止することはできません。組織でこのようなアクセスをブロックする場合は、ファイアウォールなどの他の手段を使って行う必要があります。

### <a name="nugetdefaultsconfig-location"></a>NuGetDefaults.Config の場所

Windows: %ProgramFiles(x86)%\NuGet\Config (NuGet 2.7 から NuGet 3.x: %PROGRAMDATA%\NuGet\NuGetDefaults.Config)。Mac/Linux: $XDG_DATA_HOME (通常は ~/.local/share)。 

### <a name="nugetdefaultsconfig-settings"></a>NuGetDefaults.Config の設定

- `packageSources`: このコレクションは標準の構成ファイルの `packageSources` と同じ意味であり、望ましい順位で既定のソースを指定します。 この設定が `NuGetDefaults.Config` に存在する場合、NuGet は既定のパッケージ ソースとして nuget.org を使いません。 管理者はこれにより、このファイルを使うすべてのユーザーが同じソースを使うようにし、必要な場合は nuget.org の使用を禁止することができます。

- `disabledPackageSources`: このコレクションも `NuGet.Config` ファイルと同じ意味であり、影響を受ける各ソースの名前と、ソースが無効かどうかを示す true/false の値を列記します。 これにより、ソースの名前と URL を、既定で有効にしなくても、`packageSources` に残しておくことができます。 個々の開発者は、正しい URL を改めて調べなくても、他の `NuGet.Config` ファイルでソースの値を false に設定することにより、ソースを再び有効にできます。 これは、組織の内部ソースの URL の完全なリストを開発者に提供しながら、既定で個別のチームのソースのみを有効にする場合にも便利です。

- `defaultPushSource`: `nuget push` 操作の既定のターゲットを指定し、nuget.org の組み込みの既定値を上書きします。管理者がこの設定を展開すると、開発者は nuget.org に公開するには `nuget push -Source` を明示的に使う必要があるため、内部パッケージがパブリックの nuget.org に誤って公開されるのを防ぐことができます。

### <a name="example-nugetdefaultsconfig-and-application"></a>NuGetDefaults.Config とアプリケーションの例

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <!-- defaultPushSource key works like the 'defaultPushSource' key of NuGet.Config files. -->
    <!-- This can be used by administrators to prevent accidental publishing of packages to nuget.org. -->
    <config>
        <add key="defaultPushSource" value="https://contoso.com/packages/" />
    </config>

    <!-- Default Package Sources; works like the 'packageSources' section of NuGet.Config files. -->
    <!-- This collection cannot be deleted or modified but can be disabled/enabled by users. -->
    <packageSources>
        <add key="Contoso Package Source" value="https://contoso.com/packages/" />
        <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
    </packageSources>

    <!-- Default Package Sources that are disabled by default. -->
    <!-- Works like the 'disabledPackageSources' section of NuGet.Config files. -->
    <!-- Sources cannot be modified or deleted either but can be enabled/disabled by users. -->
    <disabledPackageSources>
        <add key="nuget.org" value="true" />
    </disabledPackageSources>
</configuration>
```
