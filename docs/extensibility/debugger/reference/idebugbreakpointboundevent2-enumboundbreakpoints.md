---
title: Iデバッグブレークポイントバウンドイベント2::列挙型バウンドブレークポイント |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointBoundEvent2::EnumBoundBreakpoints
helpviewer_keywords:
- IDebugBreakpointBoundEvent2::EnumBoundBreakpoints
ms.assetid: 1f588feb-522e-488d-be92-7bc19b9e3688
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2f208c52bd45953aaad9efab9b6b65b15b3b759c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735360"
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
[アウト]このイベントからバインドされているすべてのブレークポイントを列挙する[IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)オブジェクトを返します。

## <a name="return-value"></a>戻り値
正常に終了した場合は、`S_OK` を返します。 バインド`S_FALSE`されたブレークポイントがない場合は返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
バインドされたブレークポイントのリストは、このイベントにバインドされているブレークポイント用であり、保留中のブレークポイントからバインドされたブレークポイントのリスト全体ではない可能性があります。 保留中のブレークポイントにバインドされているすべてのブレークポイントの一覧を取得するには、呼び出す[、 GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)に関連付けられている[IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)オブジェクトを取得し、保留中のブレークポイントのすべてのバインドされたブレークポイントを含む[IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)オブジェクトを取得する[列挙バインドブレークポイント](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)メソッドを呼び出します。

## <a name="example"></a>例
インターフェイスを公開する**オブジェクト**に対してこのメソッドを実装する方法を次の例[に](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)示します。

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
