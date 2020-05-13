---
title: 'IDiaSymbol:: get_targetVirtualAddress |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_targetVirtualAddress method
ms.assetid: a0a5ce72-95f8-443e-bb4b-8c21194faad0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 838d0a16224ff6732e80b67593970dfa75807fe0
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739178"
---
# <a name="idiasymbolget_targetvirtualaddress"></a>IDiaSymbol::get_targetVirtualAddress
サンクターゲットの仮想アドレス (VA) を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_targetVirtualAddress ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

入出力サンクターゲットの VA を返します。

## <a name="return-value"></a>戻り値
 成功した場合は `S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラーコードを返します。

> [!NOTE]
> @No__t_0 の戻り値は、そのシンボルに対してプロパティを使用できないことを意味します。

## <a name="remarks"></a>Remarks
 このプロパティは、シンボルが[Symtagenum 列挙](../../debugger/debug-interface-access/symtagenum.md)値 `SymTagThunk` の場合にのみ有効です。

 "サンク" は、32ビットのメモリアドレス空間 (フラットアドレス空間とも呼ばれます) と16ビットのアドレス空間 (セグメント化されたアドレス空間と呼ばれます) の間で変換を行うコードの一部です。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)
