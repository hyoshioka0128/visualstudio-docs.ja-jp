---
title: を処理する保留中のブレークポイント2::GetState |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2::GetState
helpviewer_keywords:
- GetState method
- IDebugPendingBreakpoint2::GetState method
ms.assetid: e88d543f-2e83-4ba7-86ca-f874e39955ff
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4ad65ff6fcebb18ac1b8852c08195e9a8b062749
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725756"
---
# <a name="idebugpendingbreakpoint2getstate"></a>IDebugPendingBreakpoint2::GetState
保留中のブレークポイントの状態を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetState( 
   PENDING_BP_STATE_INFO* pState
);
```

```csharp
int GetState( 
   PENDING_BP_STATE_INFO[] pState
);
```

## <a name="parameters"></a>パラメーター
`pState`\
[イン、アウト]この保留中のブレークポイントの説明が格納されている[PENDING_BP_STATE_INFO](../../../extensibility/debugger/reference/pending-bp-state-info.md)構造体。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [PENDING_BP_STATE_INFO](../../../extensibility/debugger/reference/pending-bp-state-info.md)
