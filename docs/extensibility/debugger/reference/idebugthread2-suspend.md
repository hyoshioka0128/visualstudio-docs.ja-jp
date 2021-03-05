---
description: スレッドを中断します。
title: 'IDebugThread2:: Suspend |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::Suspend
helpviewer_keywords:
- IDebugThread2::Suspend
ms.assetid: 1e20be85-aa12-48de-bb83-0bf0976e99ae
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0f80799961ccce4b3492b46801b1917055742666
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102164449"
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
入出力中断操作後の中断回数を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドを呼び出すたびに、中断回数が0を超えて増加します。 この中断回数は、[ **スレッド** デバッグ] ウィンドウに表示されます。

 このメソッドを呼び出すたびに、後で [Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md) メソッドを呼び出す必要があります。

## <a name="see-also"></a>関連項目
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md)
