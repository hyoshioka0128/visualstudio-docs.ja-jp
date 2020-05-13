---
title: を使用します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::GetLogicalThread
helpviewer_keywords:
- IDebugThread2::GetLogicalThread
ms.assetid: bce6230e-41d4-49b7-a050-2dde5efb6805
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e148fb0b9b043fc1717effca00d698ee14beb2f1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718838"
---
# <a name="idebugthread2getlogicalthread"></a>IDebugThread2::GetLogicalThread
デバッグ エンジンでは、このメソッドは実装されません。

## <a name="syntax"></a>構文

```cpp
HRESULT GetLogicalThread( 
   IDebugStackFrame2*     pStackFrame,
   IDebugLogicalThread2** ppLogicalThread
);
```

```csharp
int GetLogicalThread( 
   IDebugStackFrame2        pStackFrame,
   out IDebugLogicalThread2 ppLogicalThread
);
```

## <a name="parameters"></a>パラメーター
`pStackFrame`\
[in]スタック フレームを表す[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)オブジェクト。

`ppLogicalThread`\
[アウト]関連付`IDebugLogicalThread2`けられた論理スレッドを表すインターフェイスを返します。 デバッグ エンジンの実装では、これを null 値に設定する必要があります。

## <a name="return-value"></a>戻り値
 デバッグ エンジンの実装は`E_NOTIMPL`常に を返します。

## <a name="see-also"></a>関連項目
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
