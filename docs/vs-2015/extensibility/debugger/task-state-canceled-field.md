---
title: TASK_STATE_CANCELED Field |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- TASK_STATE_CANCELED field, Task class [.NET Framework debug engines]
ms.assetid: f4f5a96a-8230-493d-9696-8d2716bda261
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 54e0b95084bd685d5bc4b025f777c82b0ab1381f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68162234"
---
# <a name="task_state_canceled-field"></a>TASK_STATE_CANCELED フィールド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

タスクは、実行状態に到達する前に取り消されたか、取り消しを確認し、例外なしで完了しました。  
  
 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **アセンブリ:** mscorlib (mscorlib.dll)  
  
 .NET Framework からこの内部メンバーにアクセスすることはできないため、次の構文は、共通中間言語 (CIL) で提供されています。  
  
## <a name="syntax"></a>構文  
  
```  
.field static assembly literal int32 TASK_STATE_CANCELED = int32(0x00800000)  
```  
  
## <a name="remarks"></a>解説  
 [M_stateFlags](../../extensibility/debugger/m-stateflags-field.md)フィールドにこの値が含まれている場合、 <xref:System.Threading.Tasks.Task.Status%2A> プロパティはを返し <xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName> ます。  
  
## <a name="see-also"></a>参照  
 [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
