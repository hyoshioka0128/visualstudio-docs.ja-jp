---
title: 'IDiaSymbol:: get_typeIds |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_typeIds method
ms.assetid: 5166e647-fde5-4efe-92bf-77f8ae3fbc9b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4db7c1d7e3ed19268d94b28a7f0500788f7d21f5
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739070"
---
# <a name="idiasymbolget_typeids"></a>IDiaSymbol::get_typeIds
このシンボルのコンパイラ固有の型識別子の値の配列を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_typeIds ( 
   DWORD  cTypeIds,
   DWORD* pcTypeIds,
   DWORD  typeIds[]
);
```

#### <a name="parameters"></a>パラメーター
 `cTypeIds`

からデータを格納するバッファーのサイズ。

 `pcTypeIds`

入出力書き込まれた `typeIds` の数を返します。 `typeIds` が `NULL` の場合は、使用可能な型識別子の合計数を返します。

 `typeIds[]`

入出力型識別子を使用して入力する配列。

## <a name="return-value"></a>戻り値
 成功した場合は `S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラーコードを返します。

> [!NOTE]
> @No__t_0 の戻り値は、そのシンボルに対してプロパティを使用できないことを意味します。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)