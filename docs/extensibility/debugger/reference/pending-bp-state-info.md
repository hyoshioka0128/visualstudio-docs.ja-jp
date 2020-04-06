---
title: PENDING_BP_STATE_INFO |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PENDING_BP_STATE_INFO
helpviewer_keywords:
- PENDING_BP_STATE_INFO structure
ms.assetid: 4d73ceff-43f9-4e95-8dba-88e1fab2def3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d66ecc63e133a75148f06b59b8f1ccf61fe2658d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714075"
---
# <a name="pending_bp_state_info"></a>PENDING_BP_STATE_INFO
コードの場所にバインドする準備が整っているブレークポイントの状態に関する情報が含まれます。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagPENDING_BP_STATE_INFO { 
   PENDING_BP_STATE       state;
   PENDING_BP_STATE_FLAGS flags;
} PENDING_BP_STATE_INFO;
```

```csharp
public struct PENDING_BP_STATE_INFO { 
   public uint state;
   public uint flags;
};
```

## <a name="members"></a>メンバー
 `state`\
 保留中のブレークポイントの状態を指定する[PENDING_BP_STATE](../../../extensibility/debugger/reference/pending-bp-state.md)列挙体の値。

 `flags`\
 ブレークポイントが仮想化されるかどうかを指定する[PENDING_BP_STATE_FLAGS](../../../extensibility/debugger/reference/pending-bp-state-flags.md)列挙体のフラグの組み合わせ。

## <a name="remarks"></a>Remarks
 この構造体は[、GetState](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)メソッドに渡され、そこで格納されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [Getstate](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)
- [PENDING_BP_STATE](../../../extensibility/debugger/reference/pending-bp-state.md)
- [PENDING_BP_STATE_FLAGS](../../../extensibility/debugger/reference/pending-bp-state-flags.md)
