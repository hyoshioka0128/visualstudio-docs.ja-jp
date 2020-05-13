---
title: IDebug バウンドブレークポイント2::Dエレテ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBoundBreakpoint2::Delete
helpviewer_keywords:
- Delete method
- IDebugBoundBreakpoint2::Delete method
ms.assetid: 7088dc66-f24a-446f-a52a-397d02457a41
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a480a97c14b568565fee9b1b82d672db11f4ebab
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735660"
---
# <a name="idebugboundbreakpoint2delete"></a>IDebugBoundBreakpoint2::Delete
ブレークポイントを削除します。

## <a name="syntax"></a>構文

```cpp
HRESULT Delete( 
    void 
);
```

```csharp
int Delete();
```

## <a name="return-value"></a>戻り値
成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。 バインド`E_BP_DELETED`されたブレークポイント オブジェクトの状態が[(BP_STATE](../../../extensibility/debugger/reference/bp-state.md)列挙`BPS_DELETED`の一部) に設定されているかどうかを返します。

## <a name="example"></a>例
[IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)インターフェイスを公開する単純な`CBoundBreakpoint`オブジェクトに対してこのメソッドを実装する方法を次の例に示します。

```
HRESULT CBoundBreakpoint::Delete(void)
{
    HRESULT hr;

    // Verify that the bound breakpoint has not been
    // deleted. If deleted, then return hr = E_BP_DELETED.
    if (m_state != BPS_DELETED)
    {
        m_pInterp->RemoveBreakpoint(m_sbstrDoc, this);

        // Change the state of the breakpoint to BPS_DELETED.
        m_state = BPS_DELETED;
        hr = S_OK;
    }
    else
    {
        hr = E_BP_DELETED;
    }

    return hr;
}
```

## <a name="see-also"></a>関連項目
- [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [BP_STATE](../../../extensibility/debugger/reference/bp-state.md)
