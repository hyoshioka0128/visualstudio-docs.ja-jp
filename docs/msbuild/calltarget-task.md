---
title: CallTarget タスク | Microsoft Docs
description: MSBuild CallTarget タスクを使用して、プロジェクト ファイル内で指定されたターゲットを呼び出す方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- CallTarget task [MSBuild]
- MSBuild, CallTarget task
ms.assetid: bb1fe2c4-4383-436f-8326-c24cc4a46150
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3a2f124fa7e83e9f85e572276eed1851f42f7047
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99939553"
---
# <a name="calltarget-task"></a>CallTarget タスク

プロジェクト ファイル内で指定されたターゲットを呼び出します。

## <a name="task-parameters"></a>タスク パラメーター

 `CallTarget` タスクのパラメーターの説明を次の表に示します。

| パラメーター | 説明 |
|---------------------------| - |
| `RunEachTargetSeparately` | 省略可能な `Boolean` 型の入力パラメーターです。<br /><br /> `true` の場合は、MSBuild エンジンがターゲットごとに 1 回呼び出されます。 `false` の場合は、MSBuild エンジンがすべてのターゲットをビルドするために 1 回呼び出されます。 既定値は `false` です。 |
| `TargetOutputs` | 省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> ビルドされたすべてのターゲットの出力が含まれます。 |
| `Targets` | 省略可能な `String[]` 型のパラメーターです。<br /><br /> ビルドする 1 つまたは複数のターゲットを指定します。 |
| `UseResultsCache` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、キャッシュされた結果が返されます (存在する場合)。<br /><br /> **メモ** MSBuild タスクが実行された場合、その出力は、ビルド項目のリストとしてスコープ ((ProjectFileName, GlobalProperties)[TargetNames]) にキャッシュされます。 |

## <a name="remarks"></a>解説

 `Targets` に指定されたターゲットのビルドが失敗し、`RunEachTargetSeparately` が `true` に設定されている場合、タスクは残りのターゲットのビルドを続行します。

 既定のターゲットをビルドする場合は、[MSBuild タスク](../msbuild/msbuild-task.md)を使用して、`Projects` パラメーターを `$(MSBuildProjectFile)` と等しくなるように設定します。

`CallTarget` を使用すると、MSBuild によって、呼び出されたターゲットが呼び出し元の同じスコープではなく、新しいスコープで評価されます。 つまり、呼び出されたターゲットで項目やプロパティが変更された場合、それは呼び出し側のターゲットには表示されません。  呼び出し側のターゲットに情報を渡すには、`TargetOutputs` 出力パラメーターを使用します。

 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="example"></a>例

 次の例では、`CallOtherTargets` 内から `TargetA` を呼び出します。

```xml
<Project DefaultTargets="CallOtherTargets"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <Target Name="CallOtherTargets">
        <CallTarget Targets="TargetA"/>
    </Target>

    <Target Name="TargetA">
        <Message Text="Building TargetA..." />
    </Target>

</Project>
```

## <a name="see-also"></a>関連項目

- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
- [ターゲット](../msbuild/msbuild-targets.md)
