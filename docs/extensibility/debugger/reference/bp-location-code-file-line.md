---
description: コードソースファイル内の特定の行にあるブレークポイントの場所のデータを格納します。
title: BP_LOCATION_CODE_FILE_LINE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_CODE_FILE_LINE
helpviewer_keywords:
- BP_LOCATION_CODE_FILE_LINE structure
ms.assetid: 3ff32032-d412-44d3-91bf-870cc354a09e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
ms.openlocfilehash: 3711123fd41a0c5cc4adc2e2d90791cf6fe483bf
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078228"
---
# <a name="bp_location_code_file_line"></a>BP_LOCATION_CODE_FILE_LINE
コードソースファイル内の特定の行にあるブレークポイントの場所のデータを格納します。

## <a name="syntax"></a>構文

```cpp
typedef struct _BP_LOCATION_CODE_FILE_LINE {
    BSTR                     bstrContext;
    IDebugDocumentPosition2* pDocPos;
} BP_LOCATION_CODE_FILE_LINE;
```

## <a name="members"></a>メンバー
`bstrContext`\
ブレークポイントのコンテキスト。通常は、呼び出し履歴に表示されるメソッドまたは関数の名前です。

`pDocPos`\
ブレークポイントのドキュメント位置を表す [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md) オブジェクト。

## <a name="remarks"></a>注釈
この構造体は、共用体の一部として [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) 構造体のメンバーになります。

## <a name="requirements"></a>要件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
