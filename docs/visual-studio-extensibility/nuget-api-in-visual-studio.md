---
title: Visual Studio の NuGet API
description: Visual Studio で Managed Extensibility Framework を通じて NuGet がエクスポートする API のインターフェイス リファレンス
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: f1a11eb63c07a5d737a9474870f5653f6f7d850a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495911"
---
# <a name="nuget-api-in-visual-studio"></a><span data-ttu-id="55688-103">Visual Studio の NuGet API</span><span class="sxs-lookup"><span data-stu-id="55688-103">NuGet API in Visual Studio</span></span>

<span data-ttu-id="55688-104">Visual Studio のパッケージ マネージャー UI とコンソールに加え、NuGet は [Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index) を通じていくつかの便利なサービスもエクスポートします。</span><span class="sxs-lookup"><span data-stu-id="55688-104">In addition to the Package Manager UI and Console in Visual Studio, NuGet also exports some useful services through the [Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index).</span></span> <span data-ttu-id="55688-105">このインターフェイスでは、Visual Studio 内の他のコンポーネントが NuGet とやり取りできるるため、パッケージのインストールやアンインストール、インストールされているパッケージに関する情報の取得に使用することができます。</span><span class="sxs-lookup"><span data-stu-id="55688-105">This interface allows other components in Visual Studio to interact with NuGet, which can be used to install and uninstall packages, and to obtain information about installed packages.</span></span>

<span data-ttu-id="55688-106">NuGet 3.3 以降では、NuGet は次のサービスをエクスポートします。これらはすべて `NuGet.VisualStudio` アセンブリ内の `NuGet.VisualStudio.dll` 名前空間にあります。</span><span class="sxs-lookup"><span data-stu-id="55688-106">As of NuGet 3.3+, NuGet exports the following services all of which reside in the `NuGet.VisualStudio` namespace in the `NuGet.VisualStudio.dll` assembly:</span></span>

- <span data-ttu-id="55688-107">[`IRegistryKey`](#iregistrykey-interface): レジストリ サブキーから値を取得するメソッド。</span><span class="sxs-lookup"><span data-stu-id="55688-107">[`IRegistryKey`](#iregistrykey-interface): Method to retrieve a value from a registry subkey.</span></span>
- <span data-ttu-id="55688-108">[`IVsPackageInstaller`](#ivspackageinstaller-interface): プロジェクトに NuGet パッケージをインストールするメソッド。</span><span class="sxs-lookup"><span data-stu-id="55688-108">[`IVsPackageInstaller`](#ivspackageinstaller-interface): Methods to install NuGet packages into projects.</span></span>
- <span data-ttu-id="55688-109">[`IVsPackageInstallerEvents`](#ivspackageinstallerevents-interface): パッケージのインストールまたはアンインストールのイベント。</span><span class="sxs-lookup"><span data-stu-id="55688-109">[`IVsPackageInstallerEvents`](#ivspackageinstallerevents-interface): Events for package install/uninstall.</span></span>
- <span data-ttu-id="55688-110">[`IVsPackageInstallerProjectEvents`](#ivspackageinstallerprojectevents-interface): パッケージのインストールまたはアンインストールのバッチ イベント。</span><span class="sxs-lookup"><span data-stu-id="55688-110">[`IVsPackageInstallerProjectEvents`](#ivspackageinstallerprojectevents-interface): Batch events for package install/uninstall.</span></span>
- <span data-ttu-id="55688-111">[`IVsPackageInstallerServices`](#ivspackageinstallerservices-interface): 現在のソリューションにインストールされているパッケージを取得し、プロジェクトで特定のパッケージがインストールされているかどうかを確認するメソッド。</span><span class="sxs-lookup"><span data-stu-id="55688-111">[`IVsPackageInstallerServices`](#ivspackageinstallerservices-interface): Methods to retrieve installed packages in the current solution and to check whether a given package is installed in a project.</span></span>
- <span data-ttu-id="55688-112">[`IVsPackageManagerProvider`](#ivspackagemanagerprovider-interface): NuGet パッケージの代替パッケージ マネージャー候補を提供するメソッド。</span><span class="sxs-lookup"><span data-stu-id="55688-112">[`IVsPackageManagerProvider`](#ivspackagemanagerprovider-interface): Methods to provide alternative Package Manager suggestions for a NuGet package.</span></span>
- <span data-ttu-id="55688-113">[`IVsPackageMetadata`](#ivspackagemetadata-interface): インストールされているパッケージに関する情報を取得するメソッド。</span><span class="sxs-lookup"><span data-stu-id="55688-113">[`IVsPackageMetadata`](#ivspackagemetadata-interface): Methods to retrieve information about an installed package.</span></span>
- <span data-ttu-id="55688-114">[`IVsPackageProjectMetadata`](#ivspackageprojectmetadata-interface): NuGet のアクションが実行されているプロジェクトに関する情報を取得するメソッド。</span><span class="sxs-lookup"><span data-stu-id="55688-114">[`IVsPackageProjectMetadata`](#ivspackageprojectmetadata-interface): Methods to retrieve information about a project where NuGet actions are being executed.</span></span>
- <span data-ttu-id="55688-115">[`IVsPackageRestorer`](#ivspackagerestorer-interface): プロジェクトにインストールされているパッケージを復元するメソッド。</span><span class="sxs-lookup"><span data-stu-id="55688-115">[`IVsPackageRestorer`](#ivspackagerestorer-interface): Methods to restore packages installed in a project.</span></span>
- <span data-ttu-id="55688-116">[`IVsPackageSourceProvider`](#ivspackagesourceprovider-interface): NuGet パッケージ ソースのリストを取得するメソッド。</span><span class="sxs-lookup"><span data-stu-id="55688-116">[`IVsPackageSourceProvider`](#ivspackagesourceprovider-interface): Methods to retrieve a list of NuGet package sources.</span></span>
- <span data-ttu-id="55688-117">[`IVsPackageUninstaller`](#ivspackageuninstaller-interface): プロジェクトから NuGet パッケージをアンインストールするメソッド。</span><span class="sxs-lookup"><span data-stu-id="55688-117">[`IVsPackageUninstaller`](#ivspackageuninstaller-interface): Methods to uninstall NuGet packages from projects.</span></span>
- <span data-ttu-id="55688-118">[`IVsTemplateWizard`](#ivstemplatewizard-interface): 事前インストールされているパッケージを含めるプロジェクト/項目テンプレート用に設計。このインターフェイスはコードから呼び出されることを意図して*いない*ため、パブリック メソッドはありません。</span><span class="sxs-lookup"><span data-stu-id="55688-118">[`IVsTemplateWizard`](#ivstemplatewizard-interface): Designed for project/item templates to include pre-installed packages; this interface is *not* meant to be invoked from code and has no public methods.</span></span>

## <a name="using-nuget-services"></a><span data-ttu-id="55688-119">NuGet サービスの使用</span><span class="sxs-lookup"><span data-stu-id="55688-119">Using NuGet services</span></span>

1. <span data-ttu-id="55688-120">[`NuGet.VisualStudio`](https://www.nuget.org/packages/NuGet.VisualStudio) パッケージを、`NuGet.VisualStudio.dll` アセンブリを含むプロジェクトにインストールします。</span><span class="sxs-lookup"><span data-stu-id="55688-120">Install the [`NuGet.VisualStudio`](https://www.nuget.org/packages/NuGet.VisualStudio) package into your project, which contains the `NuGet.VisualStudio.dll` assembly.</span></span>

    <span data-ttu-id="55688-121">インストールすると、パッケージがアセンブリ参照の **[相互運用機能型の埋め込み]** プロパティを **True** に自動的に設定します。</span><span class="sxs-lookup"><span data-stu-id="55688-121">When installed, the package automatically sets the **Embed Interop Types** property of the assembly reference to **True**.</span></span> <span data-ttu-id="55688-122">これにより、ユーザーが NuGet の新しいバージョンに更新するときに、バージョンの変更に対するコードの回復性を高めることができます。</span><span class="sxs-lookup"><span data-stu-id="55688-122">This makes your code  resilient against version changes when users update to newer versions of NuGet.</span></span>

> [!Warning]
> <span data-ttu-id="55688-123">コードでパブリック インターフェイス以外の型を使用しないでください。また、`NuGet.Core.dll` を含む他の NuGet アセンブリを参照しないでください。</span><span class="sxs-lookup"><span data-stu-id="55688-123">Do not use any other types besides the public interfaces in your code, and do not reference any other NuGet assemblies, including `NuGet.Core.dll`.</span></span>

1. <span data-ttu-id="55688-124">サービスを使用するには、[MEF インポート属性](/dotnet/framework/mef/index#imports-and-exports-with-attributes)または [IComponentModel サービス](/dotnet/api/microsoft.visualstudio.componentmodelhost.icomponentmodel?redirectedfrom=MSDN&view=visualstudiosdk-2017)を通じてそのサービスをインポートします。</span><span class="sxs-lookup"><span data-stu-id="55688-124">To use a service, import it through the [MEF Import attribute](/dotnet/framework/mef/index#imports-and-exports-with-attributes), or through the [IComponentModel service](/dotnet/api/microsoft.visualstudio.componentmodelhost.icomponentmodel?redirectedfrom=MSDN&view=visualstudiosdk-2017).</span></span>

    ```cs
    //Using the Import attribute
    [Import(typeof(IVsPackageInstaller2))]
    public IVsPackageInstaller2 packageInstaller;
    packageInstaller.InstallLatestPackage(null, currentProject,
        "Newtonsoft.Json", false, false);

    //Using the IComponentModel service
    var componentModel = (IComponentModel)GetService(typeof(SComponentModel));
    IVsPackageInstallerServices installerServices =
        componentModel.GetService<IVsPackageInstallerServices>();

    var installedPackages = installerServices.GetInstalledPackages();
    ```

<span data-ttu-id="55688-125">参考のため、NuGet.VisualStudio のソース コードは、[NuGet.Clients リポジトリ](https://github.com/NuGet/NuGet.Client/tree/dev/src/NuGet.Clients/NuGet.VisualStudio)に含まれています。</span><span class="sxs-lookup"><span data-stu-id="55688-125">For reference, the source code for NuGet.VisualStudio is contained within the [NuGet.Clients repository](https://github.com/NuGet/NuGet.Client/tree/dev/src/NuGet.Clients/NuGet.VisualStudio).</span></span>

## <a name="iregistrykey-interface"></a><span data-ttu-id="55688-126">IRegistryKey インターフェイス</span><span class="sxs-lookup"><span data-stu-id="55688-126">IRegistryKey interface</span></span>

```cs
/// <summary>
/// Specifies methods for manipulating a key in the Windows registry.
/// </summary>
public interface IRegistryKey
    {
    /// <summary>
    /// Retrieves the specified subkey for read or read/write access.
    /// </summary>
    /// <param name="name">The name or path of the subkey to create or open.</param>
    /// <returns>The subkey requested, or null if the operation failed.</returns>
    IRegistryKey OpenSubKey(string name);


    /// <summary>
    /// Retrieves the value associated with the specified name.
    /// </summary>
    /// <param name="name">The name of the value to retrieve. This string is not case-sensitive.</param>
    /// <returns>The value associated with name, or null if name is not found.</returns>
    object GetValue(string name);


    /// <summary>
    /// Closes the key and flushes it to disk if its contents have been modified.
    /// </summary>
    void Close();
}
```

## <a name="ivspackageinstaller-interface"></a><span data-ttu-id="55688-127">IVsPackageInstaller インターフェイス</span><span class="sxs-lookup"><span data-stu-id="55688-127">IVsPackageInstaller interface</span></span>

```cs
public interface IVsPackageInstaller
{
    /// <summary>
    /// Installs a single package from the specified package source.
    /// </summary>
    /// <param name="source">
    /// The package source to install the package from. This value can be <c>null</c>
    /// to indicate that the user's configured sources should be used. Otherwise,
    /// this should be the source path as a string. If the user has credentials
    /// configured for a source, this value must exactly match the configured source
    /// value.
    /// </param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageId">The package ID of the package to install.</param>
    /// <param name="version">
    /// The version of the package to install. <c>null</c> can be provided to
    /// install the latest version of the package.
    /// </param>
    /// <param name="ignoreDependencies">
    /// A boolean indicating whether or not to ignore the package's dependencies
    /// during installation.
    /// </param>
    void InstallPackage(string source, Project project, string packageId, Version version, bool ignoreDependencies);

    /// <summary>
    /// Installs a single package from the specified package source.
    /// </summary>
    /// <param name="source">
    /// The package source to install the package from. This value can be <c>null</c>
    /// to indicate that the user's configured sources should be used. Otherwise,
    /// this should be the source path as a string. If the user has credentials
    /// configured for a source, this value must exactly match the configured source
    /// value.
    /// </param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageId">The package ID of the package to install.</param>
    /// <param name="version">
    /// The version of the package to install. <c>null</c> can be provided to
    /// install the latest version of the package.
    /// </param>
    /// <param name="ignoreDependencies">
    /// A boolean indicating whether or not to ignore the package's dependencies
    /// during installation.
    /// </param>
    void InstallPackage(string source, Project project, string packageId, string version, bool ignoreDependencies);

    /// <summary>
    /// Installs a single package from the specified package source.
    /// </summary>
    /// <param name="repository">The package repository to install the package from.</param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageId">The package id of the package to install.</param>
    /// <param name="version">
    /// The version of the package to install. <c>null</c> can be provided to
    /// install the latest version of the package.
    /// </param>
    /// <param name="ignoreDependencies">
    /// A boolean indicating whether or not to ignore the package's dependencies
    /// during installation.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating if assembly references from the package should be
    /// skipped.
    /// </param>
    void InstallPackage(IPackageRepository repository, Project project, string packageId, string version, bool ignoreDependencies, bool skipAssemblyReferences);

    /// <summary>
    /// Installs one or more packages that exist on disk in a folder defined in the registry.
    /// </summary>
    /// <param name="keyName">
    /// The registry key name (under NuGet's repository key) that defines the folder on disk
    /// containing the packages.
    /// </param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// <para>
    /// Dependencies are always ignored.
    /// </para>
    /// </remarks>
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    /// <summary>
    /// Installs one or more packages that exist on disk in a folder defined in the registry.
    /// </summary>
    /// <param name="keyName">
    /// The registry key name (under NuGet's repository key) that defines the folder on disk
    /// containing the packages.
    /// </param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="ignoreDependencies">A boolean indicating whether the package's dependencies should be ignored</param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// </remarks>
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, bool ignoreDependencies, Project project, IDictionary<string, string> packageVersions);

    /// <summary>
    /// Installs one or more packages that are embedded in a Visual Studio Extension Package.
    /// </summary>
    /// <param name="extensionId">The Id of the Visual Studio Extension Package.</param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="project">The target project for package installation</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// <para>
    /// Dependencies are always ignored.
    /// </para>
    /// </remarks>
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    /// <summary>
    /// Installs one or more packages that are embedded in a Visual Studio Extension Package.
    /// </summary>
    /// <param name="extensionId">The Id of the Visual Studio Extension Package.</param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="ignoreDependencies">A boolean indicating whether the package's dependencies should be ignored</param>
    /// <param name="project">The target project for package installation</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// </remarks>
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, bool ignoreDependencies, Project project, IDictionary<string, string> packageVersions);
}
```

## <a name="ivspackageinstallerevents-interface"></a><span data-ttu-id="55688-128">IVsPackageInstallerEvents インターフェイス</span><span class="sxs-lookup"><span data-stu-id="55688-128">IVsPackageInstallerEvents interface</span></span>

```cs
public interface IVsPackageInstallerEvents
{
    /// <summary>
    /// Raised when a package is about to be installed into the current solution.
    /// </summary>
    event VsPackageEventHandler PackageInstalling;

    /// <summary>
    /// Raised after a package has been installed into the current solution.
    /// </summary>
    event VsPackageEventHandler PackageInstalled;

    /// <summary>
    /// Raised when a package is about to be uninstalled from the current solution.
    /// </summary>
    event VsPackageEventHandler PackageUninstalling;

    /// <summary>
    /// Raised after a package has been uninstalled from the current solution.
    /// </summary>
    event VsPackageEventHandler PackageUninstalled;

    /// <summary>
    /// Raised after a package has been installed into a project within the current solution.
    /// </summary>
    event VsPackageEventHandler PackageReferenceAdded;

    /// <summary>
    /// Raised after a package has been uninstalled from a project within the current solution.
    /// </summary>
    event VsPackageEventHandler PackageReferenceRemoved;
}
```

## <a name="ivspackageinstallerprojectevents-interface"></a><span data-ttu-id="55688-129">IVsPackageInstallerProjectEvents インターフェイス</span><span class="sxs-lookup"><span data-stu-id="55688-129">IVsPackageInstallerProjectEvents interface</span></span>

```cs
public interface IVsPackageInstallerProjectEvents
{
    /// <summary>
    /// Raised before any IVsPackageInstallerEvents events are raised for a project.
    /// </summary>
    event VsPackageProjectEventHandler BatchStart;

    /// <summary>
    /// Raised after all IVsPackageInstallerEvents events are raised for a project.
    /// </summary>
    event VsPackageProjectEventHandler BatchEnd;
}
```

## <a name="ivspackageinstallerservices-interface"></a><span data-ttu-id="55688-130">IVsPackageInstallerServices インターフェイス</span><span class="sxs-lookup"><span data-stu-id="55688-130">IVsPackageInstallerServices interface</span></span>

```cs
public interface IVsPackageInstallerServices
{
    // IMPORTANT: do NOT rearrange the methods here. The order is important to maintain
    // backwards compatibility with clients that were compiled against old versions of NuGet.

    /// <summary>
    /// Get the list of NuGet packages installed in the current solution.
    /// </summary>
    IEnumerable<IVsPackageMetadata> GetInstalledPackages();

    /// <summary>
    /// Checks if a NuGet package with the specified Id is installed in the specified project.
    /// </summary>
    /// <param name="project">The project to check for NuGet package.</param>
    /// <param name="id">The id of the package to check.</param>
    /// <returns><c>true</c> if the package is install. <c>false</c> otherwise.</returns>
    bool IsPackageInstalled(Project project, string id);

    /// <summary>
    /// Checks if a NuGet package with the specified Id and version is installed in the specified project.
    /// </summary>
    /// <param name="project">The project to check for NuGet package.</param>
    /// <param name="id">The id of the package to check.</param>
    /// <param name="version">The version of the package to check.</param>
    /// <returns><c>true</c> if the package is install. <c>false</c> otherwise.</returns>
    bool IsPackageInstalled(Project project, string id, SemanticVersion version);

    /// <summary>
    /// Checks if a NuGet package with the specified Id and version is installed in the specified project.
    /// </summary>
    /// <param name="project">The project to check for NuGet package.</param>
    /// <param name="id">The id of the package to check.</param>
    /// <param name="versionString">The version of the package to check.</param>
    /// <returns><c>true</c> if the package is install. <c>false</c> otherwise.</returns>
    /// <remarks>
    /// The reason this method is named IsPackageInstalledEx, instead of IsPackageInstalled, is that
    /// when client project compiles against this assembly, the compiler would attempt to bind against
    /// the other overload which accepts SemanticVersion and would require client project to reference NuGet.Core.
    /// </remarks>
    bool IsPackageInstalledEx(Project project, string id, string versionString);

    /// <summary>
    /// Get the list of NuGet packages installed in the specified project.
    /// </summary>
    /// <param name="project">The project to get NuGet packages from.</param>
    IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
}
```

## <a name="ivspackagemanagerprovider-interface"></a><span data-ttu-id="55688-131">IVsPackageManagerProvider インターフェイス</span><span class="sxs-lookup"><span data-stu-id="55688-131">IVsPackageManagerProvider interface</span></span>

```cs
public interface IVsPackageManagerProvider
{
    /// <summary>
    /// Localized display package manager name.
    /// </summary>
    string PackageManagerName { get; }

    /// <summary>
    /// Package manager unique id.
    /// </summary>
    string PackageManagerId { get; }

    /// <summary>
    /// The tool tip description for the package
    /// </summary>
    string Description { get; }

    /// <summary>
    /// Check if a recommendation should be surfaced for an alternate package manager.
    /// This code should not rely on slow network calls, and should return rapidly.
    /// </summary>
    /// <param name="packageId">Current package id</param>
    /// <param name="projectName">Unique project name for finding the project through VS dte</param>
    /// <param name="token">Cancellation Token</param>
    /// <returns>return true if need to direct to integrated package manager for this package</returns>
    Task<bool> CheckForPackageAsync(string packageId, string projectName, CancellationToken token);

    /// <summary>
    /// This Action should take the user to the other package manager.
    /// </summary>
    /// <param name="packageId">Current package id</param>
    /// <param name="projectName">Unique project name for finding the project through VS dte</param>
    void GoToPackage(string packageId, string projectName);
}
```

## <a name="ivspackagemetadata-interface"></a><span data-ttu-id="55688-132">IVsPackageMetadata インターフェイス</span><span class="sxs-lookup"><span data-stu-id="55688-132">IVsPackageMetadata interface</span></span>

```cs
public interface IVsPackageMetadata
{
    /// <summary>
    /// Id of the package.
    /// </summary>
    string Id { get; }

    /// <summary>
    /// Version of the package.
    /// </summary>
    /// <remarks>
    /// Do not use this property because it will require referencing NuGet.Core.dll assembly. Use the VersionString
    /// property instead.
    /// </remarks>
    [Obsolete("Do not use this property because it will require referencing NuGet.Core.dll assembly. Use the VersionString property instead.")]
    NuGet.SemanticVersion Version { get; }

    /// <summary>
    /// Title of the package.
    /// </summary>
    string Title { get; }

    /// <summary>
    /// Description of the package.
    /// </summary>
    string Description { get; }

    /// <summary>
    /// The authors of the package.
    /// </summary>
    IEnumerable<string> Authors { get; }

    /// <summary>
    /// The location where the package is installed on disk.
    /// </summary>
    string InstallPath { get; }

    // IMPORTANT: This property must come LAST, because it was added in 2.5. Having it declared
    // LAST will avoid breaking components that compiled against earlier versions which doesn't
    // have this property.
    /// <summary>
    /// The version of the package.
    /// </summary>
    /// <remarks>
    /// Use this property instead of the Version property becase with the type string,
    /// it doesn't require referencing NuGet.Core.dll assembly.
    /// </remarks>
    string VersionString { get; }
}
```

## <a name="ivspackageprojectmetadata-interface"></a><span data-ttu-id="55688-133">IVsPackageProjectMetadata インターフェイス</span><span class="sxs-lookup"><span data-stu-id="55688-133">IVsPackageProjectMetadata interface</span></span>

```cs
public interface IVsPackageProjectMetadata
{
    /// <summary>
    /// Unique batch id for batch start/end events of the project.
    /// </summary>
    string BatchId { get; }

    /// <summary>
    /// Name of the project.
    /// </summary>
    string ProjectName { get; }
}
```

## <a name="ivspackagerestorer-interface"></a><span data-ttu-id="55688-134">IVsPackageRestorer インターフェイス</span><span class="sxs-lookup"><span data-stu-id="55688-134">IVsPackageRestorer interface</span></span>

```cs
public interface IVsPackageRestorer
{
    /// <summary>
    /// Returns a value indicating whether the user consent to download NuGet packages
    /// has been granted.
    /// </summary>
    /// <returns>true if the user consent has been granted; otherwise, false.</returns>
    bool IsUserConsentGranted();

    /// <summary>
    /// Restores NuGet packages installed in the given project within the current solution.
    /// </summary>
    /// <param name="project">The project whose NuGet packages to restore.</param>
    void RestorePackages(Project project);
}
```

## <a name="ivspackagesourceprovider-interface"></a><span data-ttu-id="55688-135">IVsPackageSourceProvider インターフェイス</span><span class="sxs-lookup"><span data-stu-id="55688-135">IVsPackageSourceProvider interface</span></span>

```cs
public interface IVsPackageSourceProvider
{
    /// <summary>
    /// Provides the list of package sources.
    /// </summary>
    /// <param name="includeUnOfficial">Unofficial sources will be included in the results</param>
    /// <param name="includeDisabled">Disabled sources will be included in the results</param>
    /// <returns>Key: source name Value: source URI</returns>
    IEnumerable<KeyValuePair<string, string>> GetSources(bool includeUnOfficial, bool includeDisabled);

    /// <summary>
    /// Raised when sources are added, removed, disabled, or modified.
    /// </summary>
    event EventHandler SourcesChanged;
}
```

## <a name="ivspackageuninstaller-interface"></a><span data-ttu-id="55688-136">IVsPackageUninstaller インターフェイス</span><span class="sxs-lookup"><span data-stu-id="55688-136">IVsPackageUninstaller interface</span></span>

```cs
public interface IVsPackageUninstaller
{
    /// <summary>
    /// Uninstall the specified package from a project and specify whether to uninstall its dependency packages
    /// too.
    /// </summary>
    /// <param name="project">The project from which the package is uninstalled.</param>
    /// <param name="packageId">The package to be uninstalled</param>
    /// <param name="removeDependencies">
    /// A boolean to indicate whether the dependency packages should be
    /// uninstalled too.
    /// </param>
    void UninstallPackage(Project project, string packageId, bool removeDependencies);
}
```

## <a name="ivstemplatewizard-interface"></a><span data-ttu-id="55688-137">IVsTemplateWizard インターフェイス</span><span class="sxs-lookup"><span data-stu-id="55688-137">IVsTemplateWizard interface</span></span>

```cs
/// <summary>
/// Defines the logic for a template wizard extension.
/// </summary>

public interface IVsTemplateWizard : IWizard
{
}
```
