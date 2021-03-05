---
description: このブレークポイントを説明するブレークポイントの解決を取得します。
title: 'IDebugBoundBreakpoint2:: GetBreakpointResolution |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBoundBreakpoint2::GetBreakpointResolution
helpviewer_keywords:
- GetBreakpointResolution method
- IDebugBoundBreakpoint2::GetBreakpointResolution method
ms.assetid: 4479ac61-18a9-4a30-b213-9921c5af9a26
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: aa5f5e9aabbf96bc0dffb13e99b404c906384324
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102173726"
---
# <a name="idebugboundbreakpoint2getbreakpointresolution"></a>IDebugBoundBreakpoint2::GetBreakpointResolution
このブレークポイントを説明するブレークポイントの解決を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetBreakpointResolution( 
    IDebugBreakpointResolution2** ppBPResolution
);
```

```csharp
int GetBreakpointResolution( 
    out IDebugBreakpointResolution2 ppBPResolution
);
```

## <a name="parameters"></a>パラメーター
`ppBPResolution`\
入出力次のいずれかを表す [IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md) インターフェイスを返します。

- コードのブレークポイントがバインドされているコード内の場所を記述するブレークポイント解決オブジェクト。

- データブレークポイントがバインドされているデータの場所。

## <a name="return-value"></a>戻り値
成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 `E_BP_DELETED`バインドされたブレークポイントオブジェクトの状態が `BPS_DELETED` ( [BP_STATE](../../../extensibility/debugger/reference/bp-state.md)列挙体の一部) に設定されている場合は、を返します。

## <a name="remarks"></a>解説
[Getbreakpointtype](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getbreakpointtype.md)メソッドを呼び出して、ブレークポイントの解決がコードとデータのどちらであるかを判断します。

## <a name="example"></a>例
次の例は、IDebugBoundBreakpoint2 インターフェイスを公開する単純なオブジェクトに対してこのメソッドを実装する方法を示して `CBoundBreakpoint` います。 [](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)

```
HRESULT CBoundBreakpoint::GetBreakpointResolution(
    IDebugBreakpointResolution2** ppBPResolution)
{
    HRESULT hr;

    if (ppBPResolution)
    {
        // Verify that the bound breakpoint has not been deleted. If
        // deleted, then return hr = E_BP_DELETED.
        if (m_state != BPS_DELETED)
        {
            // Query for the IDebugBreakpointResolution2 interface.
            hr = m_pBPRes->QueryInterface(IID_IDebugBreakpointResolution2,
                                          (void **)ppBPResolution);
            assert(hr == S_OK);
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
- [IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)
- [GetBreakpointType](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getbreakpointtype.md)
