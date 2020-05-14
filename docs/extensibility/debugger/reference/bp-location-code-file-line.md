---
title: BP_LOCATION_CODE_FILE_LINE |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_CODE_FILE_LINE
helpviewer_keywords:
- BP_LOCATION_CODE_FILE_LINE structure
ms.assetid: 3ff32032-d412-44d3-91bf-870cc354a09e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
ms.openlocfilehash: e338c3b24ade2cf7663b77abea64f58425d3a068
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738004"
---
# <a name="bp_location_code_file_line"></a>BP_LOCATION_CODE_FILE_LINE
コード ソース ファイル内の特定の行にブレークポイントの位置のデータが格納されます。

## <a name="syntax"></a>構文

```cpp
typedef struct _BP_LOCATION_CODE_FILE_LINE {
    BSTR                     bstrContext;
    IDebugDocumentPosition2* pDocPos;
} BP_LOCATION_CODE_FILE_LINE;
```

## <a name="members"></a>メンバー
`bstrContext`\
ブレークポイントのコンテキスト (通常は呼び出し履歴に表示されるメソッドまたは関数名)。

`pDocPos`\
ブレークポイント[のドキュメント](../../../extensibility/debugger/reference/idebugdocumentposition2.md)の位置を表すオブジェクト。

## <a name="remarks"></a>Remarks
この構造体は、共用体の一部として[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)構造のメンバーです。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
