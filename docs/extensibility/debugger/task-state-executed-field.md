---
title: TASK_STATE_EXECUTED フィールド |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- TASK_STATE_EXECUTED field, Task class [.NET Framework debug engines]
ms.assetid: 75b8f9d0-b908-40d0-b109-70feaed2ab0c
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 9fc8e98bec78973fe1309f3521c5f95bd9b3f50e
ms.sourcegitcommit: 8d38d5d2f2b75fc1563952c0d6de0fe43af12766
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/26/2018
ms.locfileid: "39276859"
---
# <a name="taskstateexecuted-field"></a>TASK_STATE_EXECUTED フィールド
タスクは実行中で、まだ完了していません。  
  
 **Namespace:** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **アセンブリ:** mscorlib (mscorlib.dll 内)  
  
 .NET Framework からこの内部メンバーにアクセスできないため、次の構文には共通中間言語 (CIL) が提供されます。  
  
## <a name="syntax"></a>構文  
  
```csharp  
.field static assembly literal int32 TASK_STATE_EXECUTED = int32(0x00020000)  
```  
  
## <a name="remarks"></a>Remarks  
 場合、 [m_stateFlags](../../extensibility/debugger/m-stateflags-field.md)フィールドには、この値が含まれています、<xref:System.Threading.Tasks.Task.Status%2A>プロパティが返す<xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName>します。  
  
## <a name="see-also"></a>関連項目  
 [Task クラス](../../extensibility/debugger/task-class-internal-members.md)