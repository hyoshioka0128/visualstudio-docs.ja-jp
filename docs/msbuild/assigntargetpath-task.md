---
title: AssignTargetPath タスク | Microsoft Docs
description: MSBuild AssignTargetPath タスクを使用してファイルの一覧を受け入れ、まだ指定されていない場合は TargetPath 属性を追加します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
ms.assetid: 0e830e31-3bcf-4259-b2a8-a5df49b92d51
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9f3a46b16bc689e0753b806c4239544e1ddbd73f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99964941"
---
# <a name="assigntargetpath-task"></a>AssignTargetPath タスク

このタスクはファイルのリストを受け入れ、`<TargetPath>` 属性がまだ指定されていない場合は、この属性を追加します。

## <a name="task-parameters"></a>タスク パラメーター

`AssignTargetPath` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`RootFolder`|省略可能な `string` 型の入力パラメーターです。<br /><br /> ターゲット リンクを格納しているフォルダーのパスが格納されます。|
|`Files`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 入力パラメーターです。<br /><br /> ファイルの受信リストが格納されます。|
|`AssignedFiles`|省略可能<br /><br /> <xref:Microsoft.Build.Framework.ITaskItem> `[]` 出力パラメーターです。<br /><br /> ファイルの結果のリストが格納されます。|

## <a name="remarks"></a>Remarks

上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="example"></a>例

次の例では、`AssignTargetPath` タスクを実行してプロジェクトを構成しています。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Target Name="MyProject">
        <AssignTargetPath
RootFolder="Resources"
            Files="@(ResourceFiles)"
            <Output TaskParameter="AssignedFiles"
                ItemName="OutAssignedFiles"/>
        </AssignTargetPath>
    </Target>
</Project>
```

## <a name="see-also"></a>関連項目

- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
