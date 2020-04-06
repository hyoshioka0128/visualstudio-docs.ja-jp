---
title: をクリックしてブレークポイントを設定します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBoundBreakpoint2::SetPassCount
helpviewer_keywords:
- SetPassCount method
- IDebugBoundBreakpoint2::SetPassCount method
ms.assetid: b32c12f9-b34d-43bd-a1b9-61af6cf8e51b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bcc7bd57ce0c392a2874f107c6e4d8d5753399d3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735435"
---
# <a name="idebugboundbreakpoint2setpasscount"></a>IDebugBoundBreakpoint2::SetPassCount
このバインドされたブレークポイントに関連付けられているパスカウントを設定または変更します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetPassCount( 
   BP_PASSCOUNT bpPassCount
);
```

```csharp
int SetPassCount( 
   BP_PASSCOUNT bpPassCount
);
```

## <a name="parameters"></a>パラメーター
`bpPassCount`\
[in]パスカウントを指定する[BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)構造体。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。 バインド`E_BP_DELETED`されたブレークポイント オブジェクトの状態が[(BP_STATE](../../../extensibility/debugger/reference/bp-state.md)列挙`BPS_DELETED`の一部) に設定されているかどうかを返します。

## <a name="remarks"></a>Remarks
 パスカウントは、ブレークポイントがいつ起動されるかを決定します。 現在のパスまたはヒット カウントは[、GetHitCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-gethitcount.md)メソッドを呼び出すことによって取得できます。

 このブレークポイントに以前に関連付けられていたパスカウントは失われます。

## <a name="see-also"></a>関連項目
- [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [GetHitCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-gethitcount.md)
- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)
- [BP_STATE](../../../extensibility/debugger/reference/bp-state.md)
