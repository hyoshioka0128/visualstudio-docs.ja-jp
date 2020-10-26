---
title: m_stateFlags Field |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- m_stateFlags field, Task class [.NET Framework debug engines]
ms.assetid: 82b20efc-08f2-4cd2-91f6-4e01e3da906b
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 794ab8baac441fc14d41c2d30b9db4b0894e88e8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68149086"
---
# <a name="m_stateflags-field"></a>m_stateFlags フィールド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

オブジェクトの現在の状態に関する情報を格納 <xref:System.Threading.Tasks.Task> します。  
  
 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **アセンブリ:** mscorlib (mscorlib.dll)  
  
 .NET Framework からこの内部メンバーにアクセスすることはできないため、次の構文は、共通中間言語 (CIL) で提供されています。  
  
## <a name="syntax"></a>構文  
  
```  
.field assembly int32 modreq(System.Runtime.CompilerServices.IsVolatile) m_stateFlags  
```  
  
## <a name="remarks"></a>解説  
 通常、 <xref:System.Threading.Tasks.Task.Status%2A?displayProperty=fullName> この値にアクセスするにはプロパティを使用します。  
  
 このメンバーは、次の値の任意の組み合わせにすることができます。  
  
- [TASK_STATE_EXECUTED](../../extensibility/debugger/task-state-executed-field.md)  
  
- [TASK_STATE_FAULTED](../../extensibility/debugger/task-state-faulted-field.md)  
  
- [TASK_STATE_CANCELED](../../extensibility/debugger/task-state-canceled-field.md)  
  
- [TASK_STATE_WAITING_ON_CHILDREN](../../extensibility/debugger/task-state-waiting-on-children-field.md)  
  
- [TASK_STATE_RAN_TO_COMPLETION](../../extensibility/debugger/task-state-ran-to-completion-field.md)  
  
## <a name="see-also"></a>参照  
 [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
