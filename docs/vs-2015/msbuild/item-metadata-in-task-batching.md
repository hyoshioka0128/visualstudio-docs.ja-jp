---
title: タスクのバッチの項目メタデータ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- batching [MSBuild]
- MSBuild, batching
- task batching [MSBuild]
- MSBuild, task batching
ms.assetid: 31e480f8-fe4d-4633-8c54-8ec498e2306d
caps.latest.revision: 16
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 15a6eeea6ebf75513419cc763b2e29a6b6264391
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842132"
---
# <a name="item-metadata-in-task-batching"></a>タスクのバッチの項目メタデータ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] には、項目メタデータに基づき、項目リストをさまざまなカテゴリまたはバッチに分割し、各バッチで一度に 1 つのタスクを実行する機能があります。 厳密にどの項目がどのバッチで渡されるのかは少々複雑です。 このトピックでは、バッチ処理を伴う一般的なシナリオについて説明します。  
  
- 1 つの項目リストをバッチに分割する  
  
- 複数の項目リストをバッチに分割する  
  
- 一度に 1 つの項目をバッチ処理する  
  
- 項目リストをフィルター処理する  
  
  [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] によるバッチ処理については、「[バッチ処理](../msbuild/msbuild-batching.md)」を参照してください。  
  
## <a name="dividing-an-item-list-into-batches"></a>1 つの項目リストをバッチに分割する  
 バッチ処理では、項目メタデータに基づいて 1 つの項目リストを複数のバッチに分割し、各バッチを 1 つのタスクに個別に渡すことができます。 サテライト アセンブリのビルドに便利です。  
  
 次の例は、項目メタデータに基づいて 1 つの項目リストをバッチに分割する方法を示しています。 `ExampColl` 項目リストが `Number` 項目メタデータに基づいて 3 つのバッチに分割されます。 `Text` 属性に `%(ExampColl.Number)` があることで、バッチ処理の実行が [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] に通知されます。 `ExampColl` 項目リストは `Number` メタデータに基づいて 3 つのバッチに分割され、各バッチが個別にタスクに渡されます。  
  
```  
<Project  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <ExampColl Include="Item1">  
            <Number>1</Number>  
        </ExampColl>  
        <ExampColl Include="Item2">  
            <Number>2</Number>  
        </ExampColl>  
        <ExampColl Include="Item3">  
            <Number>3</Number>  
        </ExampColl>  
        <ExampColl Include="Item4">  
            <Number>1</Number>  
        </ExampColl>  
        <ExampColl Include="Item5">  
            <Number>2</Number>  
        </ExampColl>  
        <ExampColl Include="Item6">  
            <Number>3</Number>  
        </ExampColl>  
    </ItemGroup>  
  
    <Target Name="ShowMessage">  
        <Message  
            Text = "Number: %(ExampColl.Number) -- Items in ExampColl: @(ExampColl)"/>  
    </Target>  
  
</Project>  
```  
  
 [Message タスク](../msbuild/message-task.md) タスクには、次の情報が表示されます。  
  
 `Number: 1 -- Items in ExampColl: Item1;Item4`  
  
 `Number: 2 -- Items in ExampColl: Item2;Item5`  
  
 `Number: 3 -- Items in ExampColl: Item3;Item6`  
  
## <a name="dividing-several-item-lists-into-batches"></a>複数の項目リストをバッチに分割する  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] は、同じメタデータに基づいて複数の項目をバッチに分割できます。 異なる項目リストをバッチに分割し、複数のアセンブリをビルドする作業が簡単になります。 たとえば、.cs ファイルの項目リストをアプリケーション バッチとアセンブリ バッチに分割し、リソース ファイルの項目リストをアプリケーション バッチとアセンブリ バッチに分割します。 それからバッチ処理を利用し、これらの項目リストを 1 つのタスクに私、アプリケーションとアセンブリの両方をビルドできます。  
  
> [!NOTE]
> タスクに渡される項目リストにメタデータを参照する項目が含まれていない場合、その項目リストのすべての項目がすべてのバッチに渡されます。  
  
 次の例は、項目メタデータに基づいて複数の項目リストをバッチに分割する方法を示しています。 `ExampColl` と `ExampColl2` の項目リストが `Number` 項目メタデータに基づいてそれぞれ 3 つのバッチに分割されます。 `Text` 属性に `%(Number)` があることで、バッチ処理の実行が [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] に通知されます。 `ExampColl` と `ExampColl2` の項目リストは `Number` メタデータに基づいて 3 つのバッチに分割され、各バッチが個別にタスクに渡されます。  
  
```  
<Project  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
  
        <ExampColl Include="Item1">  
            <Number>1</Number>  
        </ExampColl>  
        <ExampColl Include="Item2">  
            <Number>2</Number>  
        </ExampColl>  
        <ExampColl Include="Item3">  
            <Number>3</Number>  
        </ExampColl>  
  
        <ExampColl2 Include="Item4">  
            <Number>1</Number>  
        </ExampColl2>  
        <ExampColl2 Include="Item5">  
            <Number>2</Number>  
        </ExampColl2>  
        <ExampColl2 Include="Item6">  
            <Number>3</Number>  
        </ExampColl2>  
  
    </ItemGroup>  
  
    <Target Name="ShowMessage">  
        <Message  
            Text = "Number: %(Number) -- Items in ExampColl: @(ExampColl) ExampColl2: @(ExampColl2)"/>  
    </Target>  
  
</Project>  
```  
  
 [Message タスク](../msbuild/message-task.md) タスクには、次の情報が表示されます。  
  
 `Number: 1 -- Items in ExampColl: Item1 ExampColl2: Item4`  
  
 `Number: 2 -- Items in ExampColl: Item2 ExampColl2: Item5`  
  
 `Number: 3 -- Items in ExampColl: Item3 ExampColl2: Item6`  
  
## <a name="batching-one-item-at-a-time"></a>一度に 1 つの項目をバッチ処理する  
 バッチ処理は、作成時にすべての項目に割り当てられる既知の項目メタデータでも実行できます。 それにより、コレクション内のすべての項目にバッチ処理に使用するメタデータが与えられます。 `Identity` メタデータ値はすべての項目に固有のものであり、1 つの項目リスト内のすべての項目を 1 つの個別バッチに分割するときに役立ちます。 既知の項目メタデータの完全な一覧については、「 [既知の項目メタデータ](../msbuild/msbuild-well-known-item-metadata.md)」を参照してください。  
  
 次の例では、項目リストの各項目を 1 つずつバッチ処理する方法を示しています。 すべての項目の `Identity` メタデータ値が固有であるため、`ExampColl` 項目リストは 6 つのバッチに分割されます。各バッチに項目リストの 1 つの項目が含まれています。 `Text` 属性に `%(Identity)` があることで、バッチ処理の実行が [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] に通知されます。  
  
```  
<Project  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
  
        <ExampColl Include="Item1"/>  
        <ExampColl Include="Item2"/>  
        <ExampColl Include="Item3"/>  
        <ExampColl Include="Item4"/>  
        <ExampColl Include="Item5"/>  
        <ExampColl Include="Item6"/>  
  
    </ItemGroup>  
  
    <Target Name="ShowMessage">  
        <Message  
            Text = "Identity: "%(Identity)" -- Items in ExampColl: @(ExampColl)"/>  
    </Target>  
  
</Project>  
```  
  
 [Message タスク](../msbuild/message-task.md) タスクには、次の情報が表示されます。  
  
```  
Identity: "Item1" -- Items in ExampColl: Item1  
Identity: "Item2" -- Items in ExampColl: Item2  
Identity: "Item3" -- Items in ExampColl: Item3  
Identity: "Item4" -- Items in ExampColl: Item4  
Identity: "Item5" -- Items in ExampColl: Item5  
Identity: "Item6" -- Items in ExampColl: Item6  
```  
  
## <a name="filtering-item-lists"></a>項目リストをフィルター処理する  
 バッチ処理を利用すれば、1 つの項目リストをタスクに渡す前に特定の項目をフィルター処理できます。 たとえば、既知の項目メタデータ `Extension` でフィルター処理すると、特定の拡張子を持つファイルのみでタスクが実行されます。  
  
 次の例は、項目メタデータに基づいて項目リストをバッチに分割し、タスクに渡すときにバッチをフィルター処理する方法を示しています。 `ExampColl` 項目リストが `Number` 項目メタデータに基づいて 3 つのバッチに分割されます。 タスクの `Condition` 属性は、`Number` 項目メタデータ値が `2` のバッチのみをタスクに渡すことを指定します。  
  
```  
<Project  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
  
        <ExampColl Include="Item1">  
            <Number>1</Number>  
        </ExampColl>  
        <ExampColl Include="Item2">  
            <Number>2</Number>  
        </ExampColl>  
        <ExampColl Include="Item3">  
            <Number>3</Number>  
        </ExampColl>  
        <ExampColl Include="Item4">  
            <Number>1</Number>  
        </ExampColl>  
        <ExampColl Include="Item5">  
            <Number>2</Number>  
        </ExampColl>  
        <ExampColl Include="Item6">  
            <Number>3</Number>  
        </ExampColl>  
  
    </ItemGroup>  
  
    <Target Name="Exec">  
        <Message  
            Text = "Items in ExampColl: @(ExampColl)"  
            Condition="'%(Number)'=='2'"/>  
    </Target>  
  
</Project>  
```  
  
 [Message タスク](../msbuild/message-task.md) タスクには、次の情報が表示されます。  
  
```  
Items in ExampColl: Item2;Item5  
```  
  
## <a name="see-also"></a>参照  
 [既知の項目メタデータ](../msbuild/msbuild-well-known-item-metadata.md)   
 [Item 要素 (MSBuild)](../msbuild/item-element-msbuild.md)   
 [ItemMetadata 要素 (MSBuild)](../msbuild/itemmetadata-element-msbuild.md)   
 [バッチ](../msbuild/msbuild-batching.md)   
 [MSBuild の概念](../msbuild/msbuild-concepts.md)   
 [MSBuild リファレンス](../msbuild/msbuild-reference.md)
