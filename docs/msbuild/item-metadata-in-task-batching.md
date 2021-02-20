---
title: タスクのバッチの項目メタデータ | Microsoft Docs
description: MSBuild により、タスクのバッチの項目メタデータを使用して、項目リストがさまざまなカテゴリまたはバッチに分割され、各バッチでタスクが 1 回実行される方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- batching [MSBuild]
- MSBuild, batching
- task batching [MSBuild]
- MSBuild, task batching
ms.assetid: 31e480f8-fe4d-4633-8c54-8ec498e2306d
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 28451b9bf317c33e1aff52a62247374ea2b6871e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99913887"
---
# <a name="item-metadata-in-task-batching"></a>タスクのバッチの項目メタデータ

MSBuild には、項目メタデータに基づき、項目リストをさまざまなカテゴリまたはバッチに分割し、各バッチで一度に 1 つのタスクを実行する機能があります。 厳密にどの項目がどのバッチで渡されるのかは少々複雑です。 このトピックでは、バッチ処理を伴う一般的なシナリオについて説明します。

- 1 つの項目リストをバッチに分割する

- 複数の項目リストをバッチに分割する

- 一度に 1 つの項目をバッチ処理する

- 項目リストをフィルター処理する

MSBuild でのバッチ処理については、[バッチ処理](../msbuild/msbuild-batching.md)に関する記事をご覧ください。

## <a name="divide-an-item-list-into-batches"></a>1 つの項目リストをバッチに分割する

バッチ処理では、項目メタデータに基づいて 1 つの項目リストを複数のバッチに分割し、各バッチを 1 つのタスクに個別に渡すことができます。 サテライト アセンブリのビルドに便利です。

次の例は、項目メタデータに基づいて 1 つの項目リストをバッチに分割する方法を示しています。 `ExampColl` 項目リストが `Number` 項目メタデータに基づいて 3 つのバッチに分割されます。 `Text` 属性に `%(ExampColl.Number)` があることで、バッチ処理を実行する必要があることが MSBuild に通知されます。 `ExampColl` 項目リストは `Number` メタデータに基づいて 3 つのバッチに分割され、各バッチが個別にタスクに渡されます。

```xml
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

[Message タスク](../msbuild/message-task.md) には、次の情報が表示されます。

`Number: 1 -- Items in ExampColl: Item1;Item4`

`Number: 2 -- Items in ExampColl: Item2;Item5`

`Number: 3 -- Items in ExampColl: Item3;Item6`

## <a name="divide-several-item-lists-into-batches"></a>複数の項目リストをバッチに分割する

MSBuild では、同じメタデータに基づいて複数の項目リストをバッチに分割できます。 異なる項目リストをバッチに分割し、複数のアセンブリをビルドする作業が簡単になります。 たとえば、 *.cs* ファイルの項目リストをアプリケーション バッチとアセンブリ バッチに分割し、リソース ファイルの項目リストをアプリケーション バッチとアセンブリ バッチに分割します。 それからバッチ処理を利用し、これらの項目リストを 1 つのタスクに私、アプリケーションとアセンブリの両方をビルドできます。

> [!NOTE]
> タスクに渡される項目リストにメタデータを参照する項目が含まれていない場合、その項目リストのすべての項目がすべてのバッチに渡されます。

次の例は、項目メタデータに基づいて複数の項目リストをバッチに分割する方法を示しています。 `ExampColl` と `ExampColl2` の項目リストが `Number` 項目メタデータに基づいてそれぞれ 3 つのバッチに分割されます。 `Text` 属性に `%(Number)` があることで、バッチ処理を実行する必要があることが MSBuild に通知されます。 `ExampColl` と `ExampColl2` の項目リストは `Number` メタデータに基づいて 3 つのバッチに分割され、各バッチが個別にタスクに渡されます。

```xml
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

[Message タスク](../msbuild/message-task.md) には、次の情報が表示されます。

`Number: 1 -- Items in ExampColl: Item1 ExampColl2: Item4`

`Number: 2 -- Items in ExampColl: Item2 ExampColl2: Item5`

`Number: 3 -- Items in ExampColl: Item3 ExampColl2: Item6`

## <a name="batch-one-item-at-a-time"></a>一度に 1 つの項目をバッチ処理する

バッチ処理は、作成時にすべての項目に割り当てられる既知の項目メタデータでも実行できます。 それにより、コレクション内のすべての項目にバッチ処理に使用するメタデータが与えられます。 `Identity` メタデータ値はすべての項目に固有のものであり、1 つの項目リスト内のすべての項目を 1 つの個別バッチに分割するときに役立ちます。 既知の項目メタデータの一覧については、「[既知の項目メタデータ](../msbuild/msbuild-well-known-item-metadata.md)」をご覧ください。

次の例では、項目リストの各項目を 1 つずつバッチ処理する方法を示しています。 すべての項目の `Identity` メタデータ値が固有であるため、`ExampColl` 項目リストは 6 つのバッチに分割されます。各バッチに項目リストの 1 つの項目が含まれています。 `Text` 属性に `%(Identity)` があることで、バッチ処理を実行する必要があることが MSBuild に通知されます。

```xml
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
            Text = "Identity: '%(Identity)' -- Items in ExampColl: @(ExampColl)"/>
    </Target>

</Project>
```

[Message タスク](../msbuild/message-task.md) には、次の情報が表示されます。

```output
Identity: 'Item1' -- Items in ExampColl: Item1
Identity: 'Item2' -- Items in ExampColl: Item2
Identity: 'Item3' -- Items in ExampColl: Item3
Identity: 'Item4' -- Items in ExampColl: Item4
Identity: 'Item5' -- Items in ExampColl: Item5
Identity: 'Item6' -- Items in ExampColl: Item6
```

## <a name="filter-item-lists"></a>項目リストをフィルター処理する

バッチ処理を利用すれば、1 つの項目リストをタスクに渡す前に特定の項目をフィルター処理できます。 たとえば、既知の項目メタデータ `Extension` でフィルター処理すると、特定の拡張子を持つファイルのみでタスクが実行されます。

次の例は、項目メタデータに基づいて項目リストをバッチに分割し、タスクに渡すときにバッチをフィルター処理する方法を示しています。 `ExampColl` 項目リストが `Number` 項目メタデータに基づいて 3 つのバッチに分割されます。 タスクの `Condition` 属性は、`Number` 項目メタデータ値が `2` のバッチのみをタスクに渡すことを指定します。

```xml
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

[Message タスク](../msbuild/message-task.md) には、次の情報が表示されます。

```
Items in ExampColl: Item2;Item5
```

## <a name="see-also"></a>関連項目

- [既知の項目メタデータ](../msbuild/msbuild-well-known-item-metadata.md)
- [Item 要素 (MSBuild)](../msbuild/item-element-msbuild.md)
- [ItemMetadata 要素 (MSBuild)](../msbuild/itemmetadata-element-msbuild.md)
- [バッチ処理](../msbuild/msbuild-batching.md)
- [MSBuild の概念](../msbuild/msbuild-concepts.md)
- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
