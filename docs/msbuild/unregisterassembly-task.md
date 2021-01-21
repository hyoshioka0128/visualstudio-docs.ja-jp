---
title: UnregisterAssembly タスク | Microsoft Docs
description: MSBuild で UnregisterAssembly タスクを使用して、COM 相互運用のために指定されたアセンブリの登録を解除する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#UnregisterAssembly
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, UnregisterAssembly task
- UnregisterAssembly task [MSBuild]
ms.assetid: 04f549dd-3591-4dda-9c3a-cf6ede9df2c3
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 068073b2d84d95ad3d86abe582691be0dd4af895
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93046913"
---
# <a name="unregisterassembly-task"></a>UnregisterAssembly タスク

COM 相互運用のために、指定されたアセンブリの登録を解除します。 [RegisterAssembly タスク](../msbuild/registerassembly-task.md)とは逆の処理になります。

## <a name="parameters"></a>パラメーター

 `UnregisterAssembly` タスクのパラメーターの説明を次の表に示します。

|パラメーター|[説明]|
|---------------|-----------------|
|`Assemblies`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 登録解除するアセンブリを指定します。|
|`AssemblyListFile`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> `RegisterAssembly` タスクと `UnregisterAssembly` タスクの間の状態に関する情報が含まれます。 これにより、`RegisterAssembly` タスクで登録に失敗したアセンブリの登録をタスクが解除しないようにできます。<br /><br /> このパラメーターが指定されている場合、`Assemblies` と `TypeLibFiles` のパラメーターは無視されます。|
|`TypeLibFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> 指定したアセンブリから指定したタイプ アセンブリを登録解除します。 **注:** このパラメーターは、タイプ ライブラリのファイル名がアセンブリ名と異なる場合にのみ必要です。|

## <a name="remarks"></a>注釈

 アセンブリが存在していなくても、このタスクは正常に終了します。 存在しないアセンブリの登録を解除しようとした場合、タスクは警告を発行して正常終了します。 これは、アセンブリ登録をレジストリから削除することが、このタスクのジョブであるためです。 アセンブリが存在しない場合、アセンブリはレジストリに登録されていないため、タスクは正常に終了します。

 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.AppDomainIsolatedTaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:System.MarshalByRefObject> クラスから継承されます。 `MarshalByRefObject` クラスは <xref:Microsoft.Build.Utilities.Task> クラスと同じ機能を提供しますが、独自のアプリケーション ドメインでインスタンス化できます。

## <a name="example"></a>例

 次の例では `UnregisterAssembly` タスクを使用して、`OutputPath` と `FileName` のプロパティで指定されたパスにあるアセンブリ (存在する場合) を登録解除します。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <OutputPath>\Output\</OutputPath>
        <FileName>MyFile.dll</FileName>
    </PropertyGroup>
    <Target Name="UnregisterAssemblies">
        <UnregisterAssembly
            Condition="Exists('$(OutputPath)$(FileName)')"
            Assemblies="$(OutputPath)$(FileName)" />
    </Target>

</Project>
```

## <a name="see-also"></a>関連項目

- [RegisterAssembly タスク](../msbuild/registerassembly-task.md)
- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)