---
title: Notifycompletion の完了メソッド |Microsoft Docs
description: デバッガーによってブレークポイントターゲットとして使用されるプレースホルダーである、Notifydebugger Ofwaitcompletion メソッドについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- NotifyDebuggerOfWaitCompletion method, Task class [.NET Framework debug engines]
ms.assetid: 841c5908-4f3f-400b-a7b0-96a95f362817
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d58bb7a5e3a3395b534e5679ec303e5d93d5dc85
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054739"
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
