---
ms.openlocfilehash: b615bcb78ad2eaf8524bfbf17864d4652e546ff1
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "80151265"
---
<span data-ttu-id="4e554-101">パッケージの NuGet.org ページに表示される、パッケージの省略可能な説明は、`<description></description>` ファイルで使用されている `.csproj` から取得されるか、または `$description`.nuspec ファイル[の ](../../reference/nuspec.md) を経由して取得されます。</span><span class="sxs-lookup"><span data-stu-id="4e554-101">The package's optional description, displayed on the package's NuGet.org page, is either pulled in from the `<description></description>` used in the `.csproj` file or pulled in via the `$description` in the [.nuspec file](../../reference/nuspec.md).</span></span>

<span data-ttu-id="4e554-102">"_description_" フィールドの例は、.NET パッケージ用の `.csproj` ファイルの次の XML テキストに示されています。</span><span class="sxs-lookup"><span data-stu-id="4e554-102">An example of a _description_ field is shown in the following XML text of the `.csproj` file for a .NET package:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <PackageId>Azure.Storage.Blobs</PackageId>
    <Version>12.4.0</Version>
    <PackageTags>Microsoft Azure Storage Blobs;Microsoft;Azure;Blobs;Blob;Storage;StorageScalable</PackageTags>
    <Description>
      This client library enables working with the Microsoft Azure Storage Blob service for storing binary and text data.
      For this release see notes - https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/storage/Azure.Storage.Blobs/README.md and https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/storage/Azure.Storage.Blobs/CHANGELOG.md
      in addition to the breaking changes https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/storage/Azure.Storage.Blobs/BreakingChanges.txt
      Microsoft Azure Storage quickstarts and tutorials - https://docs.microsoft.com/en-us/azure/storage/
      Microsoft Azure Storage REST API Reference - https://docs.microsoft.com/en-us/rest/api/storageservices/
      REST API Reference for Blob Service - https://docs.microsoft.com/en-us/rest/api/storageservices/blob-service-rest-api
    </Description>
  </PropertyGroup>
</PropertyGroup>
```
