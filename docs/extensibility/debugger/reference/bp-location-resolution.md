---
title: BP_LOCATION_RESOLUTION |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_RESOLUTION
helpviewer_keywords:
- BP_LOCATION_RESOLUTION structure
ms.assetid: 86ea2c8a-54a3-48e8-83c7-18a515273129
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
ms.openlocfilehash: 5f33f01d0c2b8465bbb417b56576118349234970
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737959"
---
# <a name="bp_location_resolution"></a>BP_LOCATION_RESOLUTION
特定の場所でのブレークポイントの解決方法を説明します。

## <a name="syntax"></a>構文

```cpp
typedef struct _BP_LOCATION_RESOLUTION {
    IDebugBreakpointResolution2* pResolution;
} BP_LOCATION_RESOLUTION;
```

## <a name="members"></a>メンバー
`pResolution`\
ブレークポイント[の種類](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)とその解決方法を決定するオブジェクト。

## <a name="remarks"></a>Remarks
この構造体は、共用体の一部として[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)構造のメンバーです。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)
