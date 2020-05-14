---
title: THUNK_ORDINAL |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Thunk_Ordinal enumeration
ms.assetid: 026f98a9-36b8-41ef-8a72-12d7cbc2d362
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1de2d6c9700dcb7b1106c3693d855bb1d8ae2cfa
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738497"
---
# <a name="thunk_ordinal"></a>THUNK_ORDINAL
サンクの種類を指定します。

## <a name="syntax"></a>構文

```C++
typedef enum THUNK_ORDINAL {
    THUNK_ORDINAL_NOTYPE,
    THUNK_ORDINAL_ADJUSTOR,
    THUNK_ORDINAL_VCALL,
    THUNK_ORDINAL_PCODE,
    THUNK_ORDINAL_LOAD

    // trampoline thunk ordinals - only for use in Trampoline thunk symbols
    THUNK_ORDINAL_TRAMP_INCREMENTAL,
    THUNK_ORDINAL_TRAMP_BRANCHISLAND,
} THUNK_ORDINAL;
```

## <a name="elements"></a>Elements
THUNK_ORDINAL_NOTYPE 標準サンク。

THUNK_ORDINAL_ADJUSTOR A `this` ADJUSTOR サンク。

THUNK_ORDINAL_VCALL 仮想呼び出しサンク。

THUNK_ORDINAL_PCODE P-コードサンク。

THUNK_ORDINAL_LOAD 遅延読み込みサンク。

THUNK_ORDINAL_TRAMP_INCREMENTAL インクリメンタル trampoline サンク (trampoline サンクは、あるメモリ領域から別のメモリ領域への呼び出しをバウンスするために使用されます)。

THUNK_ORDINAL_TRAMP_BRANCHISLAND Branch point trampoline サンク。

## <a name="remarks"></a>Remarks
この列挙体の値は、 [IDiaSymbol:: get_thunkOrdinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md)メソッドの呼び出しから返されます。

## <a name="requirements"></a>［要件］
ヘッダー: cvconst. h

## <a name="see-also"></a>関連項目
- [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_thunkOrdinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md)
