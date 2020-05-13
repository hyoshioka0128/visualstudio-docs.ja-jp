---
title: 'IDiaSymbol:: get_udtKind |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_udtKind method
ms.assetid: 4002f887-aea6-4475-b302-67c57079fe0a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b1bd7e4963796858e7055667c1ae6a9557c77205
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739036"
---
# <a name="idiasymbolget_udtkind"></a>IDiaSymbol::get_udtKind
さまざまなユーザー定義型 (UDT) を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_udtKind ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

入出力UDT の種類 (構造体、クラス、または共用体) を指定する[Udtkind 列挙](../../debugger/debug-interface-access/udtkind.md)型の列挙体から値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は `S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラーコードを返します。

> [!NOTE]
> @No__t_0 の戻り値は、そのシンボルに対してプロパティを使用できないことを意味します。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [UdtKind 列挙型](../../debugger/debug-interface-access/udtkind.md)
