---
title: IDebugThread2::再開 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::Resume
helpviewer_keywords:
- IDebugThread2::Resume
ms.assetid: 36aad682-b0b9-40a2-b3fc-f0e61d41cdbc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3899dea7c33946588de4308f42b948ede703361a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718676"
---
# <a name="idebugthread2resume"></a>IDebugThread2::Resume
スレッドの実行を再開します。

## <a name="syntax"></a>構文

```cpp
HRESULT Resume ( 
   DWORD *pdwSuspendCount
);
```

```csharp
int Resume ( 
   out uint pdwSuspendCount
);
```

## <a name="parameters"></a>パラメーター
`pdwSuspendCount`\
[アウト]再開操作後の中断カウントを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドを呼び出すたびに、中断カウントが 0 に達するまで、実行が実際に再開されるまで、中断カウントが減ります。 この中断カウントは、**スレッド**デバッグ ウィンドウに表示されます。

 このメソッドを呼び出すたびに[、Suspend](../../../extensibility/debugger/reference/idebugthread2-suspend.md)メソッドを以前に呼び出す必要があります。 中断カウントは、メソッドが`IDebugThread2::Suspend`これまでに呼び出された回数を決定します。

## <a name="see-also"></a>関連項目
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [中断](../../../extensibility/debugger/reference/idebugthread2-suspend.md)
