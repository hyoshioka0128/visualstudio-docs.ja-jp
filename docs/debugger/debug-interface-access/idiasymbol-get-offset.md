---
title: 'IDiaSymbol:: get_offset |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_offset method
ms.assetid: 8292bb08-4dc8-4663-beb4-258f5d5a448d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: feb7620e507c5e57cf025211e42d541440af22f3
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739576"
---
# <a name="idiasymbolget_offset"></a>IDiaSymbol::get_offset
シンボルの場所のオフセットを取得します。 [LocationType 列挙](../../debugger/debug-interface-access/locationtype.md)が `LocIsRegRel` または `LocIsBitField` 場合に使用します。

## <a name="syntax"></a>構文

```C++
HRESULT get_offset ( 
   LONG* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

入出力シンボルの場所のオフセット (バイト単位) を返します。

## <a name="return-value"></a>戻り値
 成功した場合は `S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラーコードを返します。

> [!NOTE]
> @No__t_0 の戻り値は、そのシンボルに対してプロパティを使用できないことを意味します。

## <a name="remarks"></a>Remarks
 オフセットは、以前に特定された既知のポイントからのものです。 たとえば、`LocIsBitField` の場所の型のオフセットは、通常、含んでいるクラスの先頭からです。

## <a name="requirements"></a>［要件］

|必要条件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2|
|バージョン:|DIA SDK v1.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)
