---
title: GetFrameworkPath タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#GetFrameworkPath
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- GetFrameworkPath task [MSBuild]
- MSBuild, GetFrameworkPath task
ms.assetid: 5b7bcdd7-d4a0-442d-af29-8aadb3b10598
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b907194c4818ff6b867e9d15b795506ef3b77476
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77634007"
---
# <a name="getframeworkpath-task"></a>GetFrameworkPath タスク

.NET Framework アセンブリのパスを取得します。
.NET Framework アセンブリのパスを取得します。

## <a name="task-parameters"></a>タスク パラメーター

`GetFrameworkPath` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`FrameworkVersion11Path`|省略可能な `String` 型の出力パラメーターです。<br /><br /> 存在する場合、フレームワーク バージョン 1.1 アセンブリのパスが含まれます。 それ以外の場合は、`null` を返します。|
|`FrameworkVersion20Path`|省略可能な `String` 型の出力パラメーターです。<br /><br /> 存在する場合、フレームワーク バージョン 2.0 アセンブリのパスが含まれます。 それ以外の場合は、`null` を返します。|
|`FrameworkVersion30Path`|省略可能な `String` 型の出力パラメーターです。<br /><br /> 存在する場合、フレームワーク バージョン 3.0 アセンブリのパスが含まれます。 それ以外の場合は、`null` を返します。|
|`FrameworkVersion35Path`|省略可能な `String` 型の出力パラメーターです。<br /><br /> 存在する場合、フレームワーク バージョン 3.5 アセンブリのパスが含まれます。 それ以外の場合は、`null` を返します。|
|`FrameworkVersion40Path`|省略可能な `String` 型の出力パラメーターです。<br /><br /> 存在する場合、フレームワーク バージョン 4.0 アセンブリのパスが含まれます。 それ以外の場合は、`null` を返します。|
|`Path`|省略可能な `String` 型の出力パラメーターです。<br /><br /> 利用できる場合、最新のフレームワーク アセンブリのパスが含まれます。 それ以外の場合は、`null` を返します。|

## <a name="remarks"></a>Remarks

.NET Framework のいくつかのバージョンがインストールされている場合、このタスクでは、MSBuild が実行されるように設計されているバージョンが返されます。

上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="example"></a>例

次の例では、`GetFrameworkPath` タスクを使用し、.NET Framework のパスを `FrameworkPath` プロパティに保存します。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Target Name="GetPath">
        <GetFrameworkPath>
            <Output
                TaskParameter="Path"
                PropertyName="FrameworkPath" />
        </GetFrameworkPath>
    </Target>
</Project>
```

## <a name="see-also"></a>関連項目

- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
