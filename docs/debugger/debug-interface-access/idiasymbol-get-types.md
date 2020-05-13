---
title: 'IDiaSymbol:: get_types |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_types method
ms.assetid: 5f056e0c-e15b-4e00-8f78-aadc8574f7ea
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6d23ea3c4d885b3f7575c998999814d0808d03bc
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739056"
---
# <a name="idiasymbolget_types"></a>IDiaSymbol::get_types
このシンボルのコンパイラ固有の型の配列を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_types ( 
   DWORD       cTypes,
   DWORD*      pcTypes,
   IDiaSymbol* types[]
);
```

#### <a name="parameters"></a>パラメーター
 `cTypes`

からデータを格納するバッファーのサイズ。

 `pcTypes`

入出力書き込まれた型の数を返します。 `types` パラメーターが `NULL` の場合は、使用可能な型の合計数を返します。

 `types[]`

入出力このシンボルのすべての型を表す[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)オブジェクトを使用して入力する配列。

## <a name="return-value"></a>戻り値
 成功した場合は `S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラーコードを返します。

> [!NOTE]
> @No__t_0 の戻り値は、そのシンボルに対してプロパティを使用できないことを意味します。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)