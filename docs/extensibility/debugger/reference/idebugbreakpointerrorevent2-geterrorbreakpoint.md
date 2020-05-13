---
title: イベントイベント 2::エラーブレークポイントを取得する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointErrorEvent2::GetErrorBreakpoint
helpviewer_keywords:
- IDebugBreakpointErrorEvent2::GetErrorBreakpoint
ms.assetid: e5acfd19-ac17-47f3-a31a-b2aa8baca36d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fe22f18d4574ffde48cea975bff8d8f5801ca465
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735074"
---
# <a name="idebugbreakpointerrorevent2geterrorbreakpoint"></a>IDebugBreakpointErrorEvent2::GetErrorBreakpoint
ブレークポイントがバインドされなかった理由を説明する[IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)オブジェクトを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetErrorBreakpoint( 
    IDebugErrorBreakpoint2** ppErrorBP
);
```

```csharp
int GetErrorBreakpoint( 
    out IDebugErrorBreakpoint2 ppErrorBP
);
```

## <a name="parameters"></a>パラメーター
`ppErrorBP`\
[アウト]警告またはエラー[を](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)記述するオブジェクトを返します。

## <a name="return-value"></a>戻り値
成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
インターフェイスが`IDebugErrorBreakpoint2`取得されたら[、メソッドを](../../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)呼び出して[、IDebugError ブレークポイントResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)オブジェクトを取得します。 次に[、GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)メソッドを使用して、無効な場所、無効な式、または保留中のブレークポイントがバインドされていない理由 (コードがまだ読み込まれていないなど) を特定できます。

## <a name="example"></a>例
インターフェイスを公開する**オブジェクト**に対してこのメソッドを実装する方法を次の例[に](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)示します。

```cpp
STDMETHODIMP CBreakpointErrorDebugEventBase::GetErrorBreakpoint(
    IDebugErrorBreakpoint2 **ppbp)
{
    HRESULT hRes = E_FAIL;

    if ( ppbp )
    {
        if ( m_pError )
        {
            *ppbp = m_pError;

            m_pError->AddRef();

            hRes = S_OK;
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
- [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)
- [IDebugErrorBreakpointResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)
- [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
