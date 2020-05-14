---
title: BP_LOCATION_CODE_FUNC_OFFSET |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_CODE_FUNC_OFFSET
helpviewer_keywords:
- BP_LOCATION_CODE_FUNC_OFFSET structure
ms.assetid: ab38f7ca-fa01-4cf3-a06c-56cbb7207617
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
ms.openlocfilehash: 32331a5b628c27dc79d6a2e5919c8d268c96a3aa
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737998"
---
# <a name="bp_location_code_func_offset"></a>BP_LOCATION_CODE_FUNC_OFFSET
コード内の関数内のブレークポイントのオフセット位置を記述します。

## <a name="syntax"></a>構文

```cpp
typedef struct _BP_LOCATION_CODE_FUNC_OFFSET {
    BSTR                     bstrContext;
    IDebugFunctionPosition2* pFuncPos;
} BP_LOCATION_CODE_FUNC_OFFSET;
```

## <a name="members"></a>メンバー
`bstrContext`\
ブレークポイントのコンテキスト (通常は呼び出し履歴に表示されるメソッドまたは関数名)。

`pFuncPos`\
関数の名前と関数の先頭からの相対位置を記述する[IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md)オブジェクト。

## <a name="remarks"></a>Remarks
この構造体は、共用体の一部として[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)構造のメンバーです。

この`pFuncPos`メンバーは、関数ブレークポイントの設定場所を示します。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md)
