---
title: PropertyGroup 要素 (MSBuild) | Microsoft Docs
description: 一連のユーザー定義プロパティ要素を含む MSBuild PropertyGroup 要素について説明します。
ms.custom: SEO-VS-2020
ms.date: 03/13/2017
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#PropertyGroup
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- <PropertyGroup> element [MSBuild]
- PropertyGroup element [MSBuild]
ms.assetid: ff1e6c68-b9a1-4263-a1ce-dc3b829a64d4
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9d276cdfa997bb02cfa44037d8ebe758a4d2704e
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93048804"
---
# <a name="propertygroup-element-msbuild"></a>PropertyGroup 要素 (MSBuild)

ユーザー定義の [Property](../msbuild/property-element-msbuild.md) 要素のセットを格納します。 MSBuild プロジェクトで使用されるすべての `Property` 要素は、`PropertyGroup` 要素の子である必要があります。

 \<Project> \<PropertyGroup>

## <a name="syntax"></a>構文

```xml
<PropertyGroup Condition="'String A' == 'String B'">
    <Property1>...</Property1>
    <Property2>...</Property2>
</PropertyGroup>
```

## <a name="attributes-and-elements"></a>属性と要素

 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|条件|省略可能な属性です。<br /><br /> 評価する条件です。 詳細については、「[条件](../msbuild/msbuild-conditions.md)」を参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[プロパティ](../msbuild/property-element-msbuild.md)|省略可能な要素です。<br /><br /> プロパティ値を格納する、ユーザー定義のプロパティ名。 1 つの `PropertyGroup` 要素に 0 個以上の *Property* 要素を含めることができます。|

### <a name="parent-elements"></a>親要素

| 要素 | 説明 |
| - | - |
| [プロジェクト](../msbuild/project-element-msbuild.md) | MSBuild プロジェクト ファイルの必須のルート要素です。 |

## <a name="example"></a>例

 条件に基づいてプロパティを設定する方法を次のコード例に示します。 この例では、`CompileConfig` プロパティの値が `DEBUG` の場合に、`PropertyGroup` 要素内の `Optimization` プロパティ、`Obfuscate` プロパティ、`OutputPath` プロパティが設定されます。

```xml
<PropertyGroup Condition="'$(CompileConfig)' == 'DEBUG'" >
    <Optimization>false</Optimization>
    <Obfuscate>false</Obfuscate>
    <OutputPath>$(OutputPath)\debug</OutputPath>
</PropertyGroup>
```

## <a name="see-also"></a>関連項目

- [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)
- [MSBuild プロパティ](../msbuild/msbuild-properties.md)
