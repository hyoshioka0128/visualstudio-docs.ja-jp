---
title: Notifycompletion の完了メソッド |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- NotifyDebuggerOfWaitCompletion method, Task class [.NET Framework debug engines]
ms.assetid: 841c5908-4f3f-400b-a7b0-96a95f362817
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8963e29a067754c0e8c89b9db336b239ac682ce1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738335"
---
# <a name="notifydebuggerofwaitcompletion-method"></a>Notifycompletion の Waitcompletion メソッド
デバッガーによってブレークポイントターゲットとして使用されるプレースホルダーメソッド。 このメソッドは、インライン化または最適化することはできません。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib ( *mscorlib.dll*)

## <a name="syntax"></a>構文

```vb
private void NotifyDebuggerOfWaitCompletion()
```

## <a name="remarks"></a>解説
 デバッガーの通知ビットが設定されている場合、タスクを使用するすべての結合操作は、このメソッドを呼び出す必要があります。

## <a name="requirements"></a>必要条件

## <a name="see-also"></a>関連項目
- [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
