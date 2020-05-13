---
title: BP_LOCATION_DATA_STRING |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_DATA_STRING
helpviewer_keywords:
- BP_LOCATION_DATA_STRING structure
ms.assetid: 445d6f3f-95b0-47ac-85e2-51b778240687
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
ms.openlocfilehash: 75f881feaaa2068abd98d771a63024f20435d98f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737971"
---
# <a name="bp_location_data_string"></a>BP_LOCATION_DATA_STRING
統合開発環境 (IDE) からユーザーが入力できる文字列に基づくデータ ブレークポイントを設定するために使用します。

## <a name="syntax"></a>構文

```cpp
typedef struct _BP_LOCATION_DATA_STRING {
    IDebugThread2* pThread;
    BSTR           bstrContext;
    BSTR           bstrDataExpr;
    DWORD          dwNumElements;
} BP_LOCATION_DATA_STRING;
```

## <a name="members"></a>メンバー
`pThread`\
ブレークポイントが発生するスレッドを表す[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)オブジェクト。

`bstrContext`\
コード内のブレークポイントのコンテキスト (通常は呼び出し履歴に表示されるメソッドまたは関数名)。

`bstrDataExpr`\
ブレークポイントを設定するためにユーザーが入力するデータ文字列。

`dwNumElements`\
ブレークポイントが発生するデータ文字列内の要素の数。

## <a name="remarks"></a>Remarks
この構造体は、共用体の一部として[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)構造のメンバーです。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
