---
title: RemoveDuplicates タスク | Microsoft Docs
description: MSBuild で RemoveDuplicates タスクを使用して、指定した項目コレクションから重複項目を削除する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 03/01/2018
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#RemoveDuplicates
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, RemoveDuplicates task
- RemoveDuplicates task [MSBuild]
ms.assetid: 481cbab6-73ff-488c-aba5-2c09f9eb1e04
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 269499153c4be228503d6bd5b22e91e63dd5b5dd
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93048668"
---
# <a name="removeduplicates-task"></a>RemoveDuplicates タスク

指定されたアイテム コレクションから、重複するアイテムを削除します。

## <a name="parameters"></a>パラメーター

 `RemoveDuplicates` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`Filtered`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> すべての重複する項目が削除された項目コレクションが含まれます。 入力項目の順序は保持され、重複する各項目は最初のインスタンスが保持されます。|
|`Inputs`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 重複した項目を削除する対象となる項目コレクションです。|

## <a name="remarks"></a>注釈

 このタスクでは大文字と小文字が区別されず、重複の判断時、項目メタデータは比較されません。

 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="example"></a>例

 次の例では、`RemoveDuplicates` タスクを使用し、`MyItems` 項目コレクションから重複項目を削除します。 タスクが完了すると、`FilteredItems` 項目コレクションに含まれる項目が 1 つになります。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <MyItems Include="MyFile.cs"/>
        <MyItems Include="MyFile.cs">
            <Culture>fr</Culture>
        </MyItems>
        <MyItems Include="myfile.cs"/>
    </ItemGroup>

    <Target Name="RemoveDuplicateItems">
        <RemoveDuplicates
            Inputs="@(MyItems)">
            <Output
                TaskParameter="Filtered"
                ItemName="FilteredItems"/>
        </RemoveDuplicates>
    </Target>
</Project>
```

 `RemoveDuplicates` タスクが入力順を保持する例を次に示します。 タスクが完了すると、`FilteredItems` 項目コレクションには、 *MyFile2.cs* *MyFile1.cs* および *MyFile3.cs* の順に項目が含まれます。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <MyItems Include="MyFile2.cs"/>
        <MyItems Include="MyFile1.cs" />
        <MyItems Include="MyFile3.cs" />
        <MyItems Include="myfile1.cs"/>
    </ItemGroup>

    <Target Name="RemoveDuplicateItems">
        <RemoveDuplicates
            Inputs="@(MyItems)">
            <Output
                TaskParameter="Filtered"
                ItemName="FilteredItems"/>
        </RemoveDuplicates>
    </Target>
</Project>
```

## <a name="see-also"></a>関連項目

- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
- [MSBuild の概念](../msbuild/msbuild-concepts.md)
- [タスク](../msbuild/msbuild-tasks.md)
