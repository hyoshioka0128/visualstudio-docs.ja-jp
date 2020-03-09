---
title: MSBuild の条件構造 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- <Choose> Element [MSBuild]
- Choose Element [MSBuild]
- conditional constructs [MSBuild]
- MSBuild, conditional constructs
- <When> Element [MSBuild]
- <Otherwise> Element [MSBuild]
- Otherwise Element [MSBuild]
- When Element [MSBuild]
ms.assetid: dd54258e-f4fb-448f-9da4-d1817e0cbaf2
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0a06849c2aa0f4ec0203a7209ffc78be438dba9e
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/26/2020
ms.locfileid: "77633383"
---
# <a name="msbuild-conditional-constructs"></a>MSBuild の条件構造

MSBuild には、[Choose](../msbuild/choose-element-msbuild.md)、[When](../msbuild/when-element-msbuild.md)、[Otherwise](../msbuild/otherwise-element-msbuild.md) 要素で either/or 処理を行うためのメカニズムが用意されています。

## <a name="use-the-choose-element"></a>Choose 要素を使用する

 `Choose` 要素には、`Condition` 属性を持つ一連の `When` 要素が含まれます。この要素は、いずれかの評価結果が `true` になるまで、上から下への順序でテストされます。 複数の `When` 要素が評価の結果、`true` になる場合、最初の要素だけが使用されます。 `Otherwise` 要素が存在する場合、`When` 要素の条件がいずれも評価の結果、`true` にならない場合にのみ評価されます。

 `Choose` 要素は、`Project`、`When`、`Otherwise` 要素の子要素として使用できます。 `When` 要素と `Otherwise` 要素には、子要素として `ItemGroup`、`PropertyGroup`、`Choose` を入れることができます。

## <a name="example"></a>例

 次の例では、either/or 処理に `Choose` 要素と `When` 要素が使用されています。 プロジェクトのプロパティと項目は、`Configuration` プロパティの値に基づいて設定されます。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >
    <PropertyGroup>
        <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
        <OutputType>Exe</OutputType>
        <RootNamespace>ConsoleApplication1</RootNamespace>
        <AssemblyName>ConsoleApplication1</AssemblyName>
        <WarningLevel>4</WarningLevel>
    </PropertyGroup>
    <Choose>
        <When Condition=" '$(Configuration)'=='Debug' ">
            <PropertyGroup>
                <DebugSymbols>true</DebugSymbols>
                <DebugType>full</DebugType>
                <Optimize>false</Optimize>
                <OutputPath>.\bin\Debug\</OutputPath>
                <DefineConstants>DEBUG;TRACE</DefineConstants>
            </PropertyGroup>
            <ItemGroup>
                <Compile Include="UnitTesting\*.cs" />
                <Reference Include="NUnit.dll" />
            </ItemGroup>
        </When>
        <When Condition=" '$(Configuration)'=='retail' ">
            <PropertyGroup>
                <DebugSymbols>false</DebugSymbols>
                <Optimize>true</Optimize>
                <OutputPath>.\bin\Release\</OutputPath>
                <DefineConstants>TRACE</DefineConstants>
            </PropertyGroup>
        </When>
    </Choose>
    <!-- Rest of Project -->
</Project>
```

## <a name="see-also"></a>関連項目

- [Choose 要素 (MSBuild)](../msbuild/choose-element-msbuild.md)
- [When 要素 (MSBuild)](../msbuild/when-element-msbuild.md)
- [Otherwise 要素 (MSBuild)](../msbuild/otherwise-element-msbuild.md)
- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
