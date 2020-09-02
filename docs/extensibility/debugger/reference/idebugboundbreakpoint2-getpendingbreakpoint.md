---
title: 'IDebugBoundBreakpoint2:: GetPendingBreakpoint ポイント |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBoundBreakpoint2::GetPendingBreakpoint
helpviewer_keywords:
- IDebugBoundBreakpoint2::GetPendingBreakpoint method
- GetPendingBreakpoint method
ms.assetid: 22f94f81-f8d9-46de-96e9-fae6f3c24903
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4037cff1e080b4af97dbc56de4802f6f73504649
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80735484"
---
# <a name="idebugboundbreakpoint2getpendingbreakpoint"></a>IDebugBoundBreakpoint2::GetPendingBreakpoint
指定したバインドされたブレークポイントが作成された、保留中のブレークポイントを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetPendingBreakpoint( 
    IDebugPendingBreakpoint2** ppPendingBreakpoint
);
```

```csharp
int GetPendingBreakpoint( 
    out IDebugPendingBreakpoint2 ppPendingBreakpoint
);
```

## <a name="parameters"></a>パラメーター
`ppPendingBreakpoint`\
入出力このバインドされたブレークポイントの作成に使用された保留中のブレークポイントを表す [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
保留中のブレークポイントは、1つまたは複数のプログラムに適用できるコードにブレークポイントをバインドするために必要なすべての情報のコレクションと考えることができます。

## <a name="example"></a>例
次の例は、IDebugBoundBreakpoint2 インターフェイスを公開する単純なオブジェクトに対してこのメソッドを実装する方法を示して `CBoundBreakpoint` います。 [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)

```
HRESULT CBoundBreakpoint::GetPendingBreakpoint(
    IDebugPendingBreakpoint2** ppPendingBreakpoint)
{
    HRESULT hr;

    // Check for valid IDebugPendingBreakpoint2 interface pointer.
    if (ppPendingBreakpoint)
    {
        // Be sure that the bound breakpoint has not been deleted. If
        // deleted, then return hr = E_BP_DELETED.
        if (m_state != BPS_DELETED)
        {
            // Query for the IDebugPendingBreakpoint2 interface.
            hr = m_pPendingBP->QueryInterface(IID_IDebugPendingBreakpoint2,
                                              (void**)ppPendingBreakpoint);
        }
        else
        {
            hr = E_BP_DELETED;
        }
    }
    else
    {
        hr = E_INVALIDARG;
    }

    return hr;
}
```

## <a name="see-also"></a>関連項目
- [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
