---
title: Choose 要素 (MSBuild) | Microsoft Docs
description: MSBuild Choose 要素を使用して子要素を評価し、評価する ItemGroup または PropertyGroup 要素の 1 つのセットを選択します。
ms.custom: SEO-VS-2020
ms.date: 03/13/2017
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Choose
dev_langs:
- VB
- CSharp
- C++
- jsharp
- xml
helpviewer_keywords:
- <Choose> Element [MSBuild]
- Choose Element [MSBuild]
ms.assetid: 7b8b025a-d944-4f5c-9018-c89fc2ef146d
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1ad83bc215c70389dbb9383e1cb9562b99be7106
ms.sourcegitcommit: bd9417123c6ef67aa2215307ba5eeec511e43e02
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2020
ms.locfileid: "92796629"
---
# <a name="choose-element-msbuild"></a>Choose 要素 (MSBuild)

子要素を評価して、`ItemGroup` 要素および/または `PropertyGroup` 要素の 1 つのセットを評価対象に選択します。

 \<Project> \<Choose>
 \<When>
 \<Choose>
... \<Otherwise>
 \<Choose>
...

## <a name="syntax"></a>構文

```xml
<Choose>
    <When Condition="'StringA'=='StringB'">... </When>
    <Otherwise>... </Otherwise>
</Choose>
```

## <a name="attributes-and-elements"></a>属性と要素

 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

 なし。

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[Otherwise](../msbuild/otherwise-element-msbuild.md)|省略可能な要素です。<br /><br /> すべての `When` 要素の条件が `false` と評価された場合に評価される `PropertyGroup` コードと `ItemGroup` 要素のブロックを指定します。 `Choose` 要素内で、最後の要素として、0 個または 1 個の `Otherwise` 要素を指定できます。|
|[When](../msbuild/when-element-msbuild.md)|必須の要素です。<br /><br /> `Choose` 要素で選ぶ対象のコード ブロックを指定します。 `Choose` 要素内で 1 個以上の `When` 要素を指定できます。|

### <a name="parent-elements"></a>親要素

| 要素 | 説明 |
| - | - |
| [Otherwise](../msbuild/otherwise-element-msbuild.md) | すべての `When` 要素の条件が `false` と評価された場合に実行するコードのブロックを指定します。 |
| [プロジェクト](../msbuild/project-element-msbuild.md) | MSBuild プロジェクト ファイルの必須のルート要素です。 |
| [When](../msbuild/when-element-msbuild.md) | `Choose` 要素で選ぶ対象のコード ブロックを指定します。 |

## <a name="remarks"></a>解説

 `Choose`、`When`、`Otherwise` 要素を組み合わせて使って、実行される可能性のある複数のコード セクションから 1 つを選びます。 詳細については、「[条件構造](../msbuild/msbuild-conditional-constructs.md)」を参照してください。

## <a name="example"></a>例

 次のプロジェクトでは、`Choose` 要素を使って、設定する `When` 要素のプロパティ値のセットを選んでいます。 両方の `When` 要素の `Condition` 属性が `false` と評価された場合、`Otherwise` 要素のプロパティ値が設定されます。

```xml
<Project
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >
    <PropertyGroup>
        <Configuration Condition="'$(Configuration)' == ''">Debug</Configuration>
        <OutputType>Exe</OutputType>
        <RootNamespace>ConsoleApplication1</RootNamespace>
        <AssemblyName>ConsoleApplication1</AssemblyName>
        <WarningLevel>4</WarningLevel>
    </PropertyGroup>
    <Choose>
        <When Condition=" '$(Configuration)'=='debug' ">
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
        <Otherwise>
            <PropertyGroup>
                <DebugSymbols>true</DebugSymbols>
                <Optimize>false</Optimize>
                <OutputPath>.\bin\$(Configuration)\</OutputPath>
                <DefineConstants>DEBUG;TRACE</DefineConstants>
            </PropertyGroup>
        </Otherwise>
    </Choose>
    <Import Project="$(MSBuildBinPath)\Microsoft.CSharp.targets" />
</Project>
```

## <a name="see-also"></a>関連項目

- [条件構造](../msbuild/msbuild-conditional-constructs.md)
- [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)
