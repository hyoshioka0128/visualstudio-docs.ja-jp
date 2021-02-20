---
title: Property 要素 (MSBuild) | Microsoft Docs
description: PropertyGroup 要素の子として指定する必要があるユーザー定義プロパティの名前と値が含まれている MSBuild Property 要素について説明します。
ms.custom: SEO-VS-2020
ms.date: 03/13/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- <Property> Element [MSBuild]
- Property Element [MSBuild]
ms.assetid: 69ab08ab-3e76-41dd-a01b-49aa1d2e0cac
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 617a6d3712b137d76334d4063f36a1b8dde1d101
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99918848"
---
# <a name="property-element-msbuild"></a>Property 要素 (MSBuild)

ユーザー定義のプロパティ名と値を格納します。 MSBuild プロジェクトで使用されるすべてのプロパティは、`PropertyGroup` 要素の子として指定する必要があります。

 \<Project> \<PropertyGroup>

## <a name="syntax"></a>構文

```xml
<Property Condition="'String A' == 'String B'">
    Property Value
</Property>
```

## <a name="attributes-and-elements"></a>属性と要素

 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`Condition`|省略可能な属性です。<br /><br /> 評価する条件です。 詳細については、「[条件](../msbuild/msbuild-conditions.md)」を参照してください。|

### <a name="child-elements"></a>子要素

 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[PropertyGroup](../msbuild/propertygroup-element-msbuild.md)|プロパティのグループ化要素です。|

## <a name="text-value"></a>テキスト値

 テキスト値は省略可能です。

 このテキストはプロパティ値を指定します。これに XML を含めることができます。

## <a name="remarks"></a>注釈

 プロパティ名に使用できるのは ASCII 文字のみに制限されます。 プロパティ値は、"`$(`" と "`)`" の間にプロパティ名を入れることでプロジェクト内で参照されます。 たとえば、`builddir` プロパティの値が `build` の場合、`$(builddir)\classes` は *build\classes* に解決されます。 プロパティの詳細については、「[MSBuild プロパティ](../msbuild/msbuild-properties.md)」を参照してください。

## <a name="example"></a>例

 次のコードは、`Optimization` プロパティを `false` に設定します。さらに、`Version` プロパティが空の場合は `DefaultVersion` プロパティを `1.0` に設定します。

```xml
<PropertyGroup>
    <Optimization>false</Optimization>
    <DefaultVersion Condition="'$(Version)' == ''" >1.0</DefaultVersion>
</PropertyGroup>
```

## <a name="see-also"></a>関連項目

- [MSBuild プロパティ](../msbuild/msbuild-properties.md)
- [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)
