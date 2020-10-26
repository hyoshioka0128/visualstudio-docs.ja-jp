---
title: 'IDebugThread2:: GetLogicalThread |Microsoft Docs'
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80718838"
---
# <a name="idebugthread2getlogicalthread"></a>IDebugThread2::GetLogicalThread
デバッグエンジンは、このメソッドを実装しません。

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
からスタックフレームを表す [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) オブジェクト。

`ppLogicalThread`\
入出力 `IDebugLogicalThread2` 関連付けられている論理スレッドを表すインターフェイスを返します。 デバッグエンジンの実装では、これを null 値に設定する必要があります。

## <a name="return-value"></a>戻り値
 デバッグエンジンの実装は常に `E_NOTIMPL` を返します。

## <a name="see-also"></a>関連項目
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
