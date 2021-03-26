---
description: 保留中のブレークポイントの有効化状態を切り替えます。
title: 'IDebugPendingBreakpoint2:: Enable |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2::Enable
helpviewer_keywords:
- IDebugPendingBreakpoint2::Enable method
- Enable method
ms.assetid: 09e32d05-464b-40a6-a41d-76f2759cf2cd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bd3539d7be7930ecc04958c9a005ed873f8282d4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087757"
---
# <a name="idebugpendingbreakpoint2enable"></a>IDebugPendingBreakpoint2::Enable
保留中のブレークポイントの有効化状態を切り替えます。

## <a name="syntax"></a>構文

```cpp
HRESULT Enable(
    BOOL fEnable
);
```

```csharp
int Enable(
    int fEnable
);
```

## <a name="parameters"></a>パラメーター
`fEnable`\
から`TRUE`保留中のブレークポイントを有効にする場合は0以外の値に設定し、無効にする場合は 0 () に設定し `FALSE` ます。

## <a name="return-value"></a>戻り値
成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 `E_BP_DELETED`ブレークポイントが削除されている場合は、を返します。

## <a name="remarks"></a>注釈
保留中のブレークポイントを有効または無効にすると、それにバインドされているすべてのブレークポイントは同じ状態に設定されます。

このメソッドは、ブレークポイントが既に有効または無効になっている場合でも、必要な回数だけ呼び出すことができます。

## <a name="example"></a>例
次の例は、IDebugPendingBreakpoint2 インターフェイスを公開する単純なオブジェクトに対してこのメソッドを実装する方法を示して `CPendingBreakpoint` います。 [](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)

```cpp
HRESULT CPendingBreakpoint::Enable(BOOL fEnable)
{
    HRESULT hr;

    // Verify that the pending breakpoint has not been deleted. If deleted,
    // then return hr = E_BP_DELETED.
    if (m_state.state != PBPS_DELETED)
    {
        // If the bound breakpoint member variable is valid, then enable or
        // disable the bound breakpoint.
        if (m_pBoundBP)
        {
            m_pBoundBP->Enable(fEnable);
        }
        // Set the PENDING_BP_STATE in the PENDING_BP_STATE_INFO structure
        // to enabled or disabled depending on the passed BOOL condition.
        m_state.state = fEnable ? PBPS_ENABLED : PBPS_DISABLED;
        hr = S_OK;

    }
    else
    {
        hr = E_BP_DELETED;
    }

    return hr;
}
```

## <a name="see-also"></a>こちらもご覧ください
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
