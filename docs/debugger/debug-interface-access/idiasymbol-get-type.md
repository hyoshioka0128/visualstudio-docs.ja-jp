---
title: 'IDiaSymbol:: get_type |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_type method
ms.assetid: 1c6a4176-dd4e-4c22-8b8f-0e559fc078ba
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 60f9b9fd91535cc16b96da530db8ab43c4eaabf2
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739097"
---
# <a name="idiasymbolget_type"></a>IDiaSymbol::get_type
この記号の型を表す記号を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_type (
    IDiaSymbol** pRetVal
);
```

#### <a name="parameters"></a>パラメーター
`pRetVal`

入出力この記号の型を表す[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)オブジェクトを返します。

## <a name="return-value"></a>戻り値
成功した場合は `S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラーコードを返します。

> [!NOTE]
> @No__t_0 の戻り値は、そのシンボルに対してプロパティを使用できないことを意味します。

## <a name="remarks"></a>Remarks
シンボルに含まれる型を特定するには、このメソッドを呼び出し、結果の[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)オブジェクトを確認する必要があります。 シンボルに型がない可能性があることに注意してください。 たとえば、構造体の名前に型はありませんが、子シンボルがある可能性があります ( [IDiaSymbol:: findchildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)メソッドを使用してこれらの子を確認します)。

## <a name="example"></a>例

```C++
IDiaSymbol*         pType;
CComPtr<IDiaSymbol> pBaseType;
if (SUCCEEDED(pType->get_type( &pBaseType ))) {
    BasicType btBaseType;
    if (SUCCEEDED(pBaseType->get_baseType((DWORD *)&btBaseType))) {
        // Do something with basic type.
    }
}
```

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_baseType](../../debugger/debug-interface-access/idiasymbol-get-basetype.md)
- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)
