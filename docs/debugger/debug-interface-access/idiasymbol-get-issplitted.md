---
title: 'IDiaSymbol:: get_isSplitted |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isSplitted method
ms.assetid: ff160cf6-003b-4ef5-a406-20a7b287b2bf
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9511551a2f3530adc14bee0f6eec3cf360b41c03
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740051"
---
# <a name="idiasymbolget_issplitted"></a>IDiaSymbol::get_isSplitted
データシンボルが集計または他のシンボルのコレクションに分割されているかどうかを指定するフラグを取得します。コンパイラは、シンボルを個別のエンティティとして処理しますが、これらは実際には大きなシンボルの一部でもあります。

## <a name="syntax"></a>構文

```C++
HRESULT get_isSplitted(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>パラメーター
 `pFlag`

入出力シンボルがシンボルの集計に分割されている場合は `TRUE` を返します。それ以外の場合は `FALSE` を返します。

## <a name="return-value"></a>戻り値
 成功した場合は `S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラーコードを返します。

> [!NOTE]
> @No__t_0 の戻り値は、そのシンボルに対してプロパティを使用できないことを意味します。

## <a name="remarks"></a>Remarks
 [IDiaSymbol:: get_isAggregated](../../debugger/debug-interface-access/idiasymbol-get-isaggregated.md)メソッドは、分割シンボルの一部であるすべてのシンボルに対して `TRUE` を返します。

## <a name="requirements"></a>［要件］

|必要条件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2|
|バージョン:|DIA SDK v1.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_isAggregated](../../debugger/debug-interface-access/idiasymbol-get-isaggregated.md)
