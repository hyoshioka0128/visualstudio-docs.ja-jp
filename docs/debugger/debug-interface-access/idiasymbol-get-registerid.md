---
title: IDiaSymbol::get_registerId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_registerId method
ms.assetid: f881e793-eb9e-48dc-a847-dd61d77174fc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6ffd349b56c4292de04d5d7a38e82eeafed6775e
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739461"
---
# <a name="idiasymbolget_registerid"></a>IDiaSymbol::get_registerId
[LocationType 列挙](../../debugger/debug-interface-access/locationtype.md)が `LocIsEnregistered` に設定されている場合に、その場所のレジスタ指定子を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_registerId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

入出力場所のレジスタ指定子を返します。

## <a name="return-value"></a>戻り値
 成功した場合は `S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラーコードを返します。

> [!NOTE]
> @No__t_0 の戻り値は、そのシンボルに対してプロパティを使用できないことを意味します。

## <a name="remarks"></a>Remarks
 シンボルがレジスタに対して相対的な場合、つまり、シンボルの[LocationType 列挙](../../debugger/debug-interface-access/locationtype.md)が `LocIsRegRel` に設定されている場合は、`get_registerId` メソッドを使用し、その後に[IDiaSymbol:: get_offset](../../debugger/debug-interface-access/idiasymbol-get-offset.md)メソッドを呼び出して、シンボルが格納されているレジスタからのオフセットを取得します。特定.

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)
