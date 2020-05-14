---
title: BP_LOCATION_CODE_CONTEXT |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_CODE_CONTEXT
helpviewer_keywords:
- BP_LOCATION_CODE_CONTEXT structure
ms.assetid: 37412896-021a-4f73-9bb7-4125502c2e18
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
ms.openlocfilehash: 4dcb8ffb1a1debcf6aeeca8dc4d21c1ab5f18b90
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738021"
---
# <a name="bp_location_code_context"></a>BP_LOCATION_CODE_CONTEXT
デバッグ中のプログラム内のアドレスに直接バインドされているブレークポイントの場所を記述します。

## <a name="syntax"></a>構文

```cpp
typedef struct _BP_LOCATION_CODE_CONTEXT {
    IDebugCodeContext2* pCodeContext;
} BP_LOCATION_CODE_CONTEXT;
```

## <a name="members"></a>メンバー
`pCodeContext`\
コード内のブレークポイントの位置を識別する[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)オブジェクト。

## <a name="remarks"></a>Remarks
この構造体は、共用体の一部として[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)構造のメンバーです。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
