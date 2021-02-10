---
title: CombinePath タスク | Microsoft Docs
description: MSBuild CombinePath タスクを使用して、指定したパスを 1 つのパスに結合する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, CombinePath task
- CombinePath task [MSBuild]
ms.assetid: c20edbf4-3d4f-4f66-b1d5-753a0d858ed8
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f1eb27a311f1b61e3e36b4c9eaa65de7f3fd8f1c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99939501"
---
# <a name="combinepath-task"></a>CombinePath タスク

指定されたパスを 1 つのパスに結合します。
## <a name="task-parameters"></a>タスク パラメーター

 [CombinePath タスク](../msbuild/combinepath-task.md)のパラメーターの説明を次の表に示します。


|パラメーター|説明|
|---------------|-----------------|
|`BasePath`|必須の `String` 型のパラメーターです。<br /><br /> 他のパスと結合するベース パス。 相対パス、絶対パス、または空白を使用できます。|
|`Paths`|必須の <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> BasePath と組み合わせて結合パスを形成する個々のパスのリスト。 パスは相対パスと絶対パスのどちらでも構いません。|
|`CombinedPaths`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> このタスクによって作成される組み合わせたパス。|

## <a name="remarks"></a>Remarks

 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

 次の例は、`CombinePath` を使用して出力フォルダー構造を作成し、`$(ReleaseDirectory)` と連結されたルート パス `$(PublishRoot)` とサブフォルダー リスト `$(LangDirectories)` を組み合わせてプロパティ `$(OutputDirectory)` を作成する方法を示しています。

 ```xml
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp3.1</TargetFramework>
    <PublishRoot>C:\Site1\Release</PublishRoot>
  </PropertyGroup>

  <ItemGroup>
    <LangDirectories Include="en-us\;fr-fr\"/>
  </ItemGroup>

  <Target Name="CreateOutputDirectories" AfterTargets="Build">
    <CombinePath BasePath="$(PublishRoot)" Paths="@(LangDirectories)" >
      <Output TaskParameter="CombinedPaths" ItemName="OutputDirectories"/>
    </CombinePath>
    <MakeDir Directories="@(OutputDirectories)" />
  </Target>
```

`CombinePath` で、リストにすることができる唯一のプロパティは `Paths` です。この場合、出力もリストになります。 そのため、`$(PublishRoot)` が *C:\Site1\\* 、`$(ReleaseDirectory)` が *Release\\* 、`@(LangDirectories)` が *en-us\;fr-fr\\* である場合、この例では次のフォルダーが作成されます。

- C:\Site1\Release\en-us\
- C:\Site1\Release\fr-fr\

## <a name="see-also"></a>関連項目

- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
