---
title: ItemDefinitionGroup 要素 (MSBuild) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
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
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b5aea9c7c7868dfdd9726b86bb344456ebe707d8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68162449"
---
# <a name="itemdefinitiongroup-element-msbuild"></a>ItemDefinitionGroup 要素 (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`ItemDefinitionGroup` 要素を使うと、一連の項目定義を定義できます。これは、プロジェクト内のすべての項目に既定で適用されるメタデータ値です。 ItemDefinitionGroup は、 [CreateItem タスク](../msbuild/createitem-task.md) と [CreateProperty タスク](../msbuild/createproperty-task.md)を使用する必要があることよりも優先されます。 詳細については、「[項目定義](../msbuild/item-definitions.md)」を参照してください。  
  
 \<Project>  
 \<ItemDefinitionGroup>  
  
## <a name="syntax"></a>構文  
  
```  
<ItemGroup Condition="'String A' == 'String B'">  
    <Item1>... </Item1>  
    <Item2>... </Item2>  
</ItemGroup>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
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
  
|要素|説明|  
|-------------|-----------------|  
|[プロジェクト](../msbuild/project-element-msbuild.md)|[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクト ファイルの必須のルート要素です。|  
  
## <a name="example"></a>例  
 次のコード例では、ItemDefinitionGroup に 2 つのメタデータ項目 m と n を定義します。 この例では、項目 "i" ではメタデータ "m" が明示的に定義されていないため、既定のメタデータ "m" が項目 "i" に適用されます。 ただし、項目 "i" でメタデータ "n" が既に定義されているため、既定のメタデータ "n" は項目 "i" には適用されません。  
  
```  
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
  
## <a name="see-also"></a>参照  
 [プロジェクトファイルスキーマリファレンス](../msbuild/msbuild-project-file-schema-reference.md)   
 [項目](../msbuild/msbuild-items.md)
