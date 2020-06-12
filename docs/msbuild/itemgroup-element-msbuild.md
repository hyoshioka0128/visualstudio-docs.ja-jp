---
title: ItemGroup 要素 (MSBuild) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#ItemGroup
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- ItemGroup element [MSBuild]
- <ItemGroup> element [MSBuild]
ms.assetid: aac894e3-a9f1-4bbc-a796-6ef07001f35b
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c058a5986f72192a86d0e554d9e0d0b9bdce1b42
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84173513"
---
# <a name="itemgroup-element-msbuild"></a>ItemGroup 要素 (MSBuild)

ユーザー定義 [Item](../msbuild/item-element-msbuild.md) 要素のセットが含まれます。 MSBuild プロジェクトで使用されるすべての項目が、`ItemGroup` 要素の子として指定されている必要があります。

\<Project>
\<ItemGroup>

## <a name="syntax"></a>構文

```xml
<ItemGroup Condition="'String A' == 'String B'"
           Label="Label">
    <Item1>... </Item1>
    <Item2>... </Item2>
</ItemGroup>
```

## <a name="attributes-and-elements"></a>属性と要素

以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`Condition`|省略可能な属性です。 評価する条件です。 詳細については、「[条件](../msbuild/msbuild-conditions.md)」を参照してください。|
|`Label`|省略可能な属性です。 `ItemGroup` を識別します。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[Item](../msbuild/item-element-msbuild.md)|ビルド プロセスの入力を定義します。 1 つの `ItemGroup` に 0 個以上の `Item` 要素を含めることができます。|

### <a name="parent-elements"></a>親要素

| 要素 | 説明 |
| - | - |
| [プロジェクト](../msbuild/project-element-msbuild.md) | MSBuild プロジェクト ファイルの必須のルート要素です。 |
| [Target](../msbuild/target-element-msbuild.md) | .NET Framework 3.5 以降、`Target` 要素の中に `ItemGroup` 要素を使用できるようになりました。 詳細については、[ターゲット](../msbuild/msbuild-targets.md) を参照してください。 |

## <a name="example"></a>例

次のコード例は、`ItemGroup` 要素の中で宣言されたユーザー定義の項目コレクション `Res` および `CodeFiles` を示しています。 `Res` 項目コレクション内のそれぞれの項目には、ユーザー定義の子要素 [ItemMetadata](../msbuild/itemmetadata-element-msbuild.md) が含まれています。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup>
        <Res Include = "Strings.fr.resources" >
            <Culture>fr</Culture>
        </Res>
        <Res Include = "Dialogs.fr.resources" >
            <Culture>fr</Culture>
        </Res>

        <CodeFiles Include="**\*.cs" Exclude="**\generated\*.cs" />
        <CodeFiles Include="..\..\Resources\Constants.cs" />
    </ItemGroup>
...
</Project>
```

単純なプロジェクト ファイルでは、通常 1 つの `ItemGroup` 要素を使用しますが、複数の `ItemGroup` 要素を使用することもできます。 複数の `ItemGroup` 要素が使用されている場合、項目は 1 つの `ItemGroup` に結合されます。 たとえば、インポートされたファイルで定義されている個別の `ItemGroup` 要素によって、いくつかの項目が含められる場合があります。

ItemGroups には、`Condition` 属性を使用して条件を適用できます。 その場合、条件が満たされた場合にのみ項目が項目リストに追加されます。 「[MSBuild の条件](msbuild-conditions.md)」を参照してください

## <a name="see-also"></a>関連項目

- [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)
- [項目](../msbuild/msbuild-items.md)
- [MSBuild プロジェクトの共通項目](../msbuild/common-msbuild-project-items.md)
