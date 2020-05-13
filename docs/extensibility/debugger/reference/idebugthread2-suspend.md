---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::Suspend
helpviewer_keywords:
- IDebugThread2::Suspend
ms.assetid: 1e20be85-aa12-48de-bb83-0bf0976e99ae
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 74a7dd5dc69effbd46986eff963de3e740d9aa8e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718645"
---
# <a name="idebugthread2suspend"></a>IDebugThread2::Suspend
スレッドを中断します。

## <a name="syntax"></a>構文

```cpp
HRESULT Suspend ( 
   DWORD *pdwSuspendCount
);
```

```csharp
HRESULT Suspend ( 
   out uint pdwSuspendCount
);
```

## <a name="parameters"></a>パラメーター
`pdwSuspendCount`\
[アウト]中断操作の後の中断カウントを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドを呼び出すたびに、中断カウントが 0 より大きくなります。 この中断カウントは、**スレッド**デバッグ ウィンドウに表示されます。

 このメソッドを呼び出すたびに[、Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md)メソッドを後で呼び出す必要があります。

## <a name="see-also"></a>関連項目
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md)
