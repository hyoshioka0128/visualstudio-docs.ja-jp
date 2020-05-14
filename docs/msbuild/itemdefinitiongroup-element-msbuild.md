---
title: ItemDefinitionGroup 要素 (MSBuild) | Microsoft Docs
ms.date: 03/13/2017
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#ItemDefinitionGroup
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- ItemDefinitionGroup Element [MSBuild]
- <ItemDefinitionGroup> Element [MSBuild]
ms.assetid: 4e9fb04b-5148-4ae5-a394-42861dd62371
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 21e3b6554a9d6e0024cc21fd898962177acfffa7
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77633630"
---
# <a name="itemdefinitiongroup-element-msbuild"></a>ItemDefinitionGroup 要素 (MSBuild)

`ItemDefinitionGroup` 要素を使うと、一連の項目定義を定義できます。これは、プロジェクト内のすべての項目に既定で適用されるメタデータ値です。 ItemDefinitionGroup は、[CreateItem タスク](../msbuild/createitem-task.md)および [CreateProperty タスク](../msbuild/createproperty-task.md)を使う必要性より優先されます。 詳細については、「[項目定義](../msbuild/item-definitions.md)」を参照してください。

\<Project> \<ItemDefinitionGroup>

## <a name="syntax"></a>構文

```xml
<ItemDefinitionGroup Condition="'String A' == 'String B'">
    <Item1>... </Item1>
    <Item2>... </Item2>
</ItemDefinitionGroup>
```

## <a name="attributes-and-elements"></a>属性と要素

以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`Condition`|省略可能な属性です。 評価する条件です。 詳細については、「[条件](../msbuild/msbuild-conditions.md)」を参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[Item](../msbuild/item-element-msbuild.md)|ビルド プロセスの入力を定義します。 1 つの `ItemDefinitionGroup` に 0 個以上の `Item` 要素を含めることができます。|

### <a name="parent-elements"></a>親要素

| 要素 | 説明 |
| - | - |
| [プロジェクト](../msbuild/project-element-msbuild.md) | MSBuild プロジェクト ファイルの必須のルート要素です。 |

## <a name="example"></a>例

次のコード例では、ItemDefinitionGroup に 2 つのメタデータ項目 m と n を定義します。 この例では、項目 "i" ではメタデータ "m" が明示的に定義されていないため、既定のメタデータ "m" が項目 "i" に適用されます。 ただし、項目 "i" でメタデータ "n" が既に定義されているため、既定のメタデータ "n" は項目 "i" には適用されません。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemDefinitionGroup>
        <i>
            <m>m1</m>
            <n>n1</n>
        </i>
    </ItemDefinitionGroup>
    <ItemGroup>
        <i Include="a">
            <o>o1</o>
            <n>n2</n>
        </i>
    </ItemGroup>
    ...
</Project>
```

## <a name="see-also"></a>関連項目

- [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)
- [項目](../msbuild/msbuild-items.md)
