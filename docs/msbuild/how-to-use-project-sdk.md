---
title: '方法: MSBuild プロジェクト SDK の参照 | Microsoft Docs'
ms.date: 01/25/2018
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, SDKs, SDK
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d40e437763ba3eb75daa80a3a1bbf55ba9d896c9
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75574458"
---
# <a name="how-to-use-msbuild-project-sdks"></a>方法: MSBuild プロジェクト SDK の使用

[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 15.0 では、"プロジェクト SDK" という概念が導入されました。これによって、プロパティとターゲットをインポートする必要があるソフトウェア開発キットの使用が簡単になります。

```xml
<Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
        <TargetFramework>net46</TargetFramework>
    </PropertyGroup>
</Project>
```

プロジェクトの評価中に、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] によってプロジェクトの先頭と末尾に暗黙的なインポートが追加されます。

```xml
<Project>
    <!-- Implicit top import -->
    <Import Project="Sdk.props" Sdk="Microsoft.NET.Sdk" />

    <PropertyGroup>
        <TargetFramework>net46</TargetFramework>
    </PropertyGroup>

    <!-- Implicit bottom import -->
    <Import Project="Sdk.targets" Sdk="Microsoft.NET.Sdk" />
</Project>
```

## <a name="reference-a-project-sdk"></a>プロジェクト SDK を参照する

 プロジェクト SDK を参照するには、次の 3 つの方法があります。

1. `<Project/>` 要素の `Sdk` 属性を使用する:

    ```xml
    <Project Sdk="My.Custom.Sdk">
        ...
    </Project>
    ```

    前述のように、暗黙的なインポートがプロジェクトの先頭と末尾に追加されます。
    
    特定のバージョンの SDK を指定する場合は、それを `Sdk` 属性に追加できます。

    ```xml
    <Project Sdk="My.Custom.Sdk/1.2.3">
        ...
    </Project>
    ```

    > [!NOTE]
    > これは、現時点では、Visual Studio for Mac でプロジェクト SDK を参照するためにサポートされている唯一の方法です。

2. 最上位の `<Sdk/>` 要素を使用する:

    ```xml
    <Project>
        <Sdk Name="My.Custom.Sdk" Version="1.2.3" />
        ...
    </Project>
   ```

   前述のように、暗黙的なインポートがプロジェクトの先頭と末尾に追加されます。  `Version` 属性は必要ありません。

3. `<Import/>` は、プロジェクトの任意の場所で使用できます。

    ```xml
    <Project>
        <PropertyGroup>
            <MyProperty>Value</MyProperty>
        </PropertyGroup>
        <Import Project="Sdk.props" Sdk="My.Custom.Sdk" />
        ...
        <Import Project="Sdk.targets" Sdk="My.Custom.Sdk" />
    </Project>
   ```

   プロジェクトに明示的にインポートを含めることで、順序を完全に制御できます。

   `<Import/>` 要素を使用する場合は、省略可能な `Version` 属性も指定できます。  たとえば、`<Import Project="Sdk.props" Sdk="My.Custom.Sdk" Version="1.2.3" />` を指定できます。

## <a name="how-project-sdks-are-resolved"></a>プロジェクト SDK の解決方法

インポートを評価すると、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] では、指定した名前とバージョンに基づいて、プロジェクト SDK へのパスが動的に解決されます。  また、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] には、登録済み SDK リゾルバーの一覧もあります。SDK リゾルバーは、マシン上にあるプロジェクト SDK の場所を特定するプラグインです。  たとえば、次のプラグインがあります。

1. NuGet ベースのリゾルバー。指定した SDK の ID とバージョンに一致する、NuGet パッケージ用に構成されたパッケージ フィードのクエリを実行します。<br/>
   このリゾルバーは、省略可能なバージョンを指定した場合にのみ有効になります。任意のカスタム プロジェクト SDK に使用できます。
2. .NET CLI リゾルバー。 .NET CLI と共にインストールされた SDK を解決します。<br/>
   このリゾルバーは、製品の一部である `Microsoft.NET.Sdk` や `Microsoft.NET.Sdk.Web` などのプロジェクト SDK の場所を特定します。
3. 既定のリゾルバー。MSBuild と共にインストールされた SDK を解決します。

NuGet ベースの SDK リゾルバーでは、[global.json](/dotnet/core/tools/global-json) でバージョンを指定することができます。これによって、個々のプロジェクトではなく、ある場所内のプロジェクト SDK のバージョンを制御できます。

```json
{
    "msbuild-sdks": {
        "My.Custom.Sdk": "5.0.0",
        "My.Other.Sdk": "1.0.0-beta"
    }
}
```

ビルド中には、各プロジェクト SDK の 1 つのバージョンのみを使用できます。  同じプロジェクト SDK の 2 つの異なるバージョンを参照していると、MSBuild から警告が生成されます。  *global.json* でバージョンが指定されている場合は、プロジェクトでバージョンを指定**しない**ことをお勧めします。

## <a name="see-also"></a>関連項目

- [MSBuild の概念](../msbuild/msbuild-concepts.md)
- [ビルドのカスタマイズ](../msbuild/customize-your-build.md)
- [パッケージ、メタデータ、フレームワーク](/dotnet/core/packages)
- [.NET Core の csproj 形式に追加されたもの](/dotnet/core/tools/csproj)
