---
title: CombinePath タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
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
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3b97714fc707d8f9174a01dcc1fe7b3b59176de2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68160386"
---
# <a name="combinepath-task"></a>CombinePath タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定されたパスを 1 つのパスに結合します。  
  
## <a name="task-parameters"></a>タスク パラメーター  
 次の表では、連結 [Epath タスク](../msbuild/combinepath-task.md)のパラメーターについて説明します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`BasePath`|必須の `String` 型のパラメーターです。<br /><br /> 他のパスと結合するベース パス。 相対パス、絶対パス、または空白を使用できます。|  
|`Paths`|必須の <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> BasePath と組み合わせて結合パスを形成する個々のパスのリスト。 パスは相対パスと絶対パスのどちらでも構いません。|  
|`CombinedPaths`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> このタスクによって作成される組み合わせたパス。|  
  
## <a name="remarks"></a>Remarks  
 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加パラメーターとその説明の一覧については、「 [Taskextension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [タスク](../msbuild/msbuild-tasks.md)   
 [タスクリファレンス](../msbuild/msbuild-task-reference.md)
