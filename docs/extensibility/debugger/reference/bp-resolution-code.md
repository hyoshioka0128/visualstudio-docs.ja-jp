---
title: BP_RESOLUTION_CODE |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_RESOLUTION_CODE
helpviewer_keywords:
- BP_RESOLUTION_CODE structure
ms.assetid: ac103ec5-771c-4667-92de-b5abb53bbb52
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fbfd16025d338b54bec8e2e4276de62c8d00477e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737848"
---
# <a name="bp_resolution_code"></a>BP_RESOLUTION_CODE
コード ブレークポイントの場所を記述します。

## <a name="syntax"></a>構文

```cpp
typedef struct _BP_RESOLUTION_CODE {
    IDebugCodeContext2* pCodeContext;
} BP_RESOLUTION_CODE;
```

```csharp
public struct BP_RESOLUTION_CODE {
    public IDebugCodeContext2 pCodeContext;
};
```

## <a name="members"></a>メンバー
`pCodeContext`\
コード内のブレークポイントの位置を識別する[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)オブジェクト。

## <a name="remarks"></a>Remarks
この構造体は[、BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md)構造体のメンバーであり[、GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)メソッドによって返される[BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)構造体のメンバーになります。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md)
- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)
- [GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
