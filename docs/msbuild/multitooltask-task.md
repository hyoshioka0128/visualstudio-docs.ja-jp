---
title: MultiToolTask タスク | Microsoft Docs
ms.date: 03/10/2019
ms.topic: reference
f1_keywords:
- vc.task.multitooltask
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (C++), MultiToolTask task
- MultiToolTask task (MSBuild (C++))
author: ghogen
ms.author: ghogen
ms.workload:
- multiple
ms.openlocfilehash: d9e8b23492f23d39977b4eb26f8ee633b8463f27
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75565215"
---
# <a name="multitooltask-task"></a>MultiToolTask タスク

説明はありません。

## <a name="parameters"></a>パラメーター

以下の表では、**MultiToolTask** タスクのパラメーターについて説明します。

|パラメーター|説明|
|---------------|-----------------|
|**EnvironmentVariablesToSet**|省略可能な **string[]** 型のパラメーターです。|
|**SemaphoreProcCount**|省略可能な **string** 型のパラメーターです。|
|**SchedulerFunction**|省略可能な **string** 型のパラメーターです。|
|**SchedulerVerbose**|省略可能な **bool** 型のパラメーターです。|
|**Sources**|必須の **ITaskItem[]** 型のパラメーターです。|
|**TaskAssemblyName**|省略可能な **string** 型のパラメーターです。|
|**TaskName**|必須の **String** 型のパラメーターです。|
|**TrackerLogDirectory**|必須の **String** 型のパラメーターです。|

## <a name="see-also"></a>関連項目

[タスク リファレンス](../msbuild/msbuild-task-reference.md)
