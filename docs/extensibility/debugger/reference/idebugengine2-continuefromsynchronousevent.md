---
title: 同期イベントを続行するマイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::ContinueFromSynchronousEvent
helpviewer_keywords:
- IDebugEngine2::ContinueFromSynchronousEvent
ms.assetid: 9a57dfcd-df8e-4be5-b1fe-bd853e3c6bb2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: da059b6efe137092d46241977a98b22b1eb66c44
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731148"
---
# <a name="idebugengine2continuefromsynchronousevent"></a>IDebugEngine2::ContinueFromSynchronousEvent
セッション デバッグ マネージャー (SDM) によって呼び出され、以前にデバッグ エンジン (DE) によって SDM に送信された同期デバッグ イベントが受信され、処理されたことを示します。

## <a name="syntax"></a>構文

```cpp
HRESULT ContinueFromSynchronousEvent(
    IDebugEvent2* pEvent
);
```

```csharp
HRESULT ContinueFromSynchronousEvent(
    IDebugEvent2 pEvent
);
```

## <a name="parameters"></a>パラメーター
`pEvent`\
[in]デバッガーを続行する前に送信された同期イベントを表す[IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)オブジェクト。

## <a name="return-value"></a>戻り値
成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
DE は、それがパラメータによって表されるイベントのソースであることを確認する`pEvent`必要があります。

## <a name="example"></a>例
`CEngine` [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)インターフェイスを実装する単純なオブジェクトに対してこのメソッドを実装する方法を次の例に示します。

```cpp
HRESULT CEngine::ContinueFromSynchronousEvent(IDebugEvent2* pEvent)
{
    HRESULT hr;

    // Create a pointer to a unique event interface defined for batch file
    // breaks.
    IAmABatchFileEvent *pBatEvent;
    // Check for successful query for the unique batch file event
    // interface.
    if (SUCCEEDED(pEvent->QueryInterface(IID_IAmABatchFileEvent,
                                        (void **)&pBatEvent)))
    {
        // Release the result of the QI.
        pBatEvent->Release();
        // Check thread message for notification to continue.
        if (PostThreadMessage(GetCurrentThreadId(),
                              WM_CONTINUE_SYNC_EVENT,
                              0,
                              0))
        {
            hr = S_OK;
        }
        else
        {
            hr = HRESULT_FROM_WIN32(GetLastError());
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
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
