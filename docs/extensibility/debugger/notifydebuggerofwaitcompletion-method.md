---
title: Notifycompletion の完了メソッド |Microsoft Docs
description: デバッガーによってブレークポイントターゲットとして使用されるプレースホルダーである、Notifydebugger Ofwaitcompletion メソッドについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- NotifyDebuggerOfWaitCompletion method, Task class [.NET Framework debug engines]
ms.assetid: 841c5908-4f3f-400b-a7b0-96a95f362817
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b62b613950f9fd6c8ce18969c126a6e74a154b58
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99851297"
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

## <a name="requirements"></a>要件

## <a name="see-also"></a>関連項目
- [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
