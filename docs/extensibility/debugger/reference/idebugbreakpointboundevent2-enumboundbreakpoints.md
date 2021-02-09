---
title: 'IDebugBreakpointBoundEvent2:: EnumBoundBreakpoints ポイント |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointBoundEvent2::EnumBoundBreakpoints
helpviewer_keywords:
- IDebugBreakpointBoundEvent2::EnumBoundBreakpoints
ms.assetid: 1f588feb-522e-488d-be92-7bc19b9e3688
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e548f6c51372608b661ec85b80afeb535263cc6c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99921149"
---
# <a name="idebugbreakpointboundevent2enumboundbreakpoints"></a>IDebugBreakpointBoundEvent2::EnumBoundBreakpoints
このイベントにバインドされたブレークポイントの列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumBoundBreakpoints( 
    IEnumDebugBoundBreakpoints2** ppEnum
);
```

```csharp
int EnumBoundBreakpoints( 
    out IEnumDebugBoundBreakpoints2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\
入出力このイベントからバインドされたすべてのブレークポイントを列挙する [IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
正常に終了した場合は、`S_OK` を返します。 `S_FALSE`バインドされたブレークポイントがない場合はを返します。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
バインドされたブレークポイントの一覧は、このイベントにバインドされているブレークポイントの一覧であり、保留中のブレークポイントからバインドされたブレークポイントのリスト全体ではない可能性があります。 保留中のブレークポイントにバインドされているすべてのブレークポイントの一覧を取得するには、 [Getpendingbreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md) ポイントメソッドを呼び出して、関連付けられている [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) オブジェクトを取得し、 [enumboundbreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md) ポイントメソッドを呼び出して、保留中のブレークポイントのすべてのバインドされたブレークポイントを含む [IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md) オブジェクトを取得します。

## <a name="example"></a>例
次の例は、 [IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)インターフェイスを公開する **Cbreakpointsetdebugeventbase** オブジェクトに対してこのメソッドを実装する方法を示しています。

```cpp
STDMETHODIMP CBreakpointSetDebugEventBase::EnumBoundBreakpoints(
    IEnumDebugBoundBreakpoints2 **ppEnum)
{
    HRESULT hRes = E_FAIL;

    if ( ppEnum )
    {
        if ( m_pEnumBound )
        {
            hRes = m_pEnumBound->Clone(ppEnum);

            if ( EVAL(S_OK == hRes) )
                (*ppEnum)->Reset();
        }
        else
            hRes = E_FAIL;
    }
    else
        hRes = E_INVALIDARG;

    return ( hRes );
}
```

## <a name="see-also"></a>関連項目
- [IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)
- [IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)
- [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)
