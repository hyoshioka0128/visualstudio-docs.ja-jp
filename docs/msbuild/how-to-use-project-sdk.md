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
ms.openlocfilehash: 74ccc29417cdee7a9f93c39509c0f7d06a5c72ff
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "76826472"
---
# <a name="how-to-use-msbuild-project-sdks"></a>方法: MSBuild プロジェクト SDK の使用

MSBuild 15.0 では、"プロジェクト SDK" という概念が導入されました。これによって、プロパティとターゲットをインポートする必要があるソフトウェア開発キットの使用が簡単になります。

```xml
<Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
        <TargetFramework>net46</TargetFramework>
    </PropertyGroup>
</Project>
```

プロジェクトの評価中に、MSBuild によってプロジェクト ファイルの先頭と末尾に暗黙的なインポートが追加されます。

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

- `Sdk` 要素の `<Project/>` 属性を使用する:

    ```xml
    <Project Sdk="My.Custom.Sdk">
        ...
    </Project>
    ```

    前述のように、暗黙的なインポートがプロジェクトの先頭と末尾に追加されます。
    
    特定のバージョンの SDK を指定するには、それを `Sdk` 属性に追加します。

    ```xml
    <Project Sdk="My.Custom.Sdk/1.2.3">
        ...
    </Project>
    ```

    > [!NOTE]
    > これは、現時点では、Visual Studio for Mac でプロジェクト SDK を参照するためにサポートされている唯一の方法です。

- 最上位の `<Sdk/>` 要素を使用する:

    ```xml
    <Project>
        <Sdk Name="My.Custom.Sdk" Version="1.2.3" />
        ...
    </Project>
   ```

   前述のように、暗黙的なインポートがプロジェクトの先頭と末尾に追加されます。
   
   `Version` 属性は必要ありません。

- `<Import/>` は、プロジェクトの任意の場所で使用できます。

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

   `<Import/>` 要素を使用する場合は、省略可能な `Version` 属性も指定できます。 たとえば、`<Import Project="Sdk.props" Sdk="My.Custom.Sdk" Version="1.2.3" />` を指定できます。

## <a name="how-project-sdks-are-resolved"></a>プロジェクト SDK の解決方法

インポートを評価すると、MSBuild では、指定した名前とバージョンに基づいてプロジェクト SDK へのパスが動的に解決されます。  また、MSBuild には、登録済み SDK リゾルバーの一覧もあります。SDK リゾルバーは、マシン上にあるプロジェクト SDK の場所を特定するプラグインです。 たとえば、次のプラグインがあります。

- NuGet ベースのリゾルバー。指定した SDK の ID とバージョンに一致する、NuGet パッケージ用に構成されたパッケージ フィードのクエリを実行します。

   このリゾルバーは、オプションのバージョンを指定した場合にのみアクティブになります。 任意のカスタム プロジェクト SDK に使用できます。
   
- .NET CLI リゾルバー。[.NET CLI](/dotnet/core/tools/) と共にインストールされた SDK を解決します。

   このリゾルバーにより、製品の一部である `Microsoft.NET.Sdk` や `Microsoft.NET.Sdk.Web` などのプロジェクト SDK の場所が特定されます。
   
- 既定のリゾルバー。MSBuild と共にインストールされた SDK を解決します。

NuGet ベースの SDK リゾルバーでは、[global.json](/dotnet/core/tools/global-json) ファイルでバージョンを指定することができます。これによって、個々のプロジェクトではなく、ある場所内のプロジェクト SDK のバージョンを制御できます。

```json
{
    "msbuild-sdks": {
        "My.Custom.Sdk": "5.0.0",
        "My.Other.Sdk": "1.0.0-beta"
    }
}
```

ビルド中には、各プロジェクト SDK の 1 つのバージョンのみを使用できます。 同じプロジェクト SDK の 2 つの異なるバージョンを参照すると、MSBuild から警告が生成されます。 **global.json** ファイルでバージョンが指定されている場合は、プロジェクトでバージョンを指定*しない*ことをお勧めします。

## <a name="see-also"></a>参照

- [MSBuild の概念](../msbuild/msbuild-concepts.md)
- [ビルドのカスタマイズ](../msbuild/customize-your-build.md)
- [パッケージ、メタデータ、フレームワーク](/dotnet/core/packages)
- [.NET Core の csproj 形式に追加されたもの](/dotnet/core/tools/csproj)
