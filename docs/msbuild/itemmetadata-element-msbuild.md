---
title: ItemMetadata 要素 (MSBuild) | Microsoft Docs
ms.date: 03/13/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- ItemMetadata Element [MSBuild]
- <ItemMetadata> Element [MSBuild]
ms.assetid: e3db5122-202d-43a9-b2f4-3e0ec4ed3d08
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 66c19dbd74176babbf9e26030a68a6095992b660
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75589371"
---
# <a name="itemmetadata-element-msbuild"></a>ItemMetadata 要素 (MSBuild)
ユーザー定義の項目メタデータのキーを格納します。項目メタデータの値が含まれます。 1 つの項目が、任意の数のメタデータ キー/値ペアを含むことができます。

 \<Project> \<ItemGroup> \<Item>

## <a name="syntax"></a>構文

```xml
<ItemMetadataName> Item Metadata value</ItemMetadataName>
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
|[Item](../msbuild/item-element-msbuild.md)|ビルド プロセスに対する入力を定義するユーザー定義の要素。|

## <a name="text-value"></a>テキスト値
 テキスト値は省略可能です。

 このテキストは、項目メタデータの値を指定します。テキストまたは XML を使うことができます。

## <a name="example"></a>例
 次のコード例では、値が `fr` の `Culture` メタデータを項目 `CSFile` に追加する方法を示します。

```xml
<ItemGroup>
    <CSFile Include="main.cs" >
        <Culture>fr</Culture>
    </CSFile>
</ItemGroup>
```

## <a name="see-also"></a>関連項目
- [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)
- [項目](../msbuild/msbuild-items.md)
