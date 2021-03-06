---
description: タスクは実行中で、まだ完了していません。
title: TASK_STATE_EXECUTED Field |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- TASK_STATE_EXECUTED field, Task class [.NET Framework debug engines]
ms.assetid: 75b8f9d0-b908-40d0-b109-70feaed2ab0c
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6bdc6344c3257611664fc792658dcf6508e91bfd
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102223291"
---
# <a name="task_state_executed-field"></a>TASK_STATE_EXECUTED フィールド
タスクは実行中で、まだ完了していません。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib (mscorlib.dll)

 .NET Framework からこの内部メンバーにアクセスできないため、次の構文は、共通中間言語 (CIL) で提供されています。

## <a name="syntax"></a>構文

```csharp
.field static assembly literal int32 TASK_STATE_EXECUTED = int32(0x00020000)
```

## <a name="remarks"></a>解説
 [M_stateFlags](../../extensibility/debugger/m-stateflags-field.md)フィールドにこの値が含まれている場合、 <xref:System.Threading.Tasks.Task.Status%2A> プロパティはを返し <xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName> ます。

## <a name="see-also"></a>関連項目
- [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
