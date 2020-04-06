---
title: メソッドを通知する |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738335"
---
# <a name="notifydebuggerofwaitcompletion-method"></a>メソッドを通知します。
デバッガーによってブレークポイント ターゲットとして使用されるプレースホルダー メソッド。 このメソッドは、インライン化または最適化しないでください。

 **名前空間:**<xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib *(mscorlib.dll*内)

## <a name="syntax"></a>構文

```vb
private void NotifyDebuggerOfWaitCompletion()
```

## <a name="remarks"></a>Remarks
 タスクを使用するすべての結合操作は、デバッガー通知ビットが設定されている場合、このメソッドを呼び出す必要があります。

## <a name="requirements"></a>必要条件

## <a name="see-also"></a>関連項目
- [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
