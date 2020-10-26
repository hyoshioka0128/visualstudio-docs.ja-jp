---
title: 'IDebugBreakpointResolution2:: GetBreakpointType |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointResolution2::GetBreakpointType
helpviewer_keywords:
- IDebugBreakpointResolution2::GetBreakpointType
ms.assetid: 2b707fb9-f703-4c78-91bf-7434f57790a0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2949366eeb3e79a732e94a4a8f8e9912048c6452
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80734811"
---
# <a name="idebugbreakpointresolution2getbreakpointtype"></a>IDebugBreakpointResolution2::GetBreakpointType
この解像度によって表されるブレークポイントの型を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetBreakpointType( 
    BP_TYPE* pBPType
);
```

```csharp
int GetBreakpointType( 
    out enum_ BP_TYPE pBPType
);
```

## <a name="parameters"></a>パラメーター
`pBPType`\
入出力このブレークポイントの種類を指定する [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md) 列挙から値を返します。

## <a name="return-value"></a>戻り値
成功した場合は、を返します。それ以外の場合は `S_OK` エラーコードを返します。 `bpResLocation`関連付けられた[BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)構造のフィールドが有効でない場合は E_FAIL を返します。

## <a name="remarks"></a>解説
ブレークポイントには、コードまたはデータのブレークポイントを指定できます。たとえば、のようになります。

## <a name="example"></a>例
次の例は、IDebugBreakpointResolution2 インターフェイスを公開する単純なオブジェクトに対してこのメソッドを実装する方法を示して `CDebugBreakpointResolution` います。 [IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)

```
HRESULT CDebugBreakpointResolution::GetBreakpointType(BP_TYPE* pBPType)
{
    HRESULT hr;

    if (pBPType)
    {
        // Set default BP_TYPE.
        *pBPType = BPT_NONE;

        // Check if the BPRESI_BPRESLOCATION flag is set in BPRESI_FIELDS.
        if (IsFlagSet(m_bpResolutionInfo.dwFields, BPRESI_BPRESLOCATION))
        {
            // Set the new BP_TYPE.
            *pBPType = m_bpResolutionInfo.bpResLocation.bpType;
            hr = S_OK;
        }
        else
        {
            hr = E_FAIL;
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
- [IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)
- [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md)
- [BPRESI_FIELDS](../../../extensibility/debugger/reference/bpresi-fields.md)
- [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md)
- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)
