---
description: タスクは、実行状態に到達する前に取り消されたか、取り消しを確認し、例外なしで完了しました。
title: TASK_STATE_CANCELED Field |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- TASK_STATE_CANCELED field, Task class [.NET Framework debug engines]
ms.assetid: f4f5a96a-8230-493d-9696-8d2716bda261
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8e99148c223f86a0307a0588e7803a5fadf52d6a
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102223330"
---
# <a name="task_state_canceled-field"></a>TASK_STATE_CANCELED フィールド
タスクは、実行状態に到達する前に取り消されたか、取り消しを確認し、例外なしで完了しました。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib (mscorlib.dll)

 .NET Framework からこの内部メンバーにアクセスできないため、次の構文は、共通中間言語 (CIL) で提供されています。

## <a name="syntax"></a>構文

```csharp
.field static assembly literal int32 TASK_STATE_CANCELED = int32(0x00800000)
```

## <a name="remarks"></a>解説
 [M_stateFlags](../../extensibility/debugger/m-stateflags-field.md)フィールドにこの値が含まれている場合、 <xref:System.Threading.Tasks.Task.Status%2A> プロパティはを返し <xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName> ます。

## <a name="see-also"></a>関連項目
- [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
