---
title: LocationType |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- LocationType enumeration
ms.assetid: d3e1eedc-bfd3-4c91-881b-d69565138d0f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dc40cc6cc8e821db7c28a4647e36e7bad241b29f
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738646"
---
# <a name="locationtype"></a>LocationType
シンボルに含まれる位置情報の種類を示します。

## <a name="syntax"></a>構文

```C++
enum LocationType {
    LocIsNull,
    LocIsStatic,
    LocIsTLS,
    LocIsRegRel,
    LocIsThisRel,
    LocIsEnregistered,
    LocIsBitField,
    LocIsSlot,
    LocIsIlRel,
    LocInMetaData,
    LocIsConstant,
    LocTypeMax
};
```

## <a name="elements"></a>Elements
`LocIsNull` の場所情報は使用できません。

`LocIsStatic` の場所は静的です。

`LocIsTLS` の場所は、スレッドローカルストレージにあります。

`LocIsRegRel` の場所は、レジスタ相対です。

`LocIsThisRel` の場所は `this` 相対です。

`LocIsEnregistered` の場所は登録されています。

`LocIsBitField` の場所は、ビットフィールドにあります。

`LocIsSlot` の場所は、Microsoft 中間言語 (MSIL) スロットです。

`LocIsIlRel` の場所は MSIL 相対です。

`LocInMetaData` の場所はメタデータにあります。

`LocIsConstant` の場所は定数値です。

この列挙体の場所の種類の数を `LocTypeMax` します。

## <a name="remarks"></a>Remarks
[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)インターフェイスで使用できるプロパティは、イメージファイル内のシンボルの場所によって異なります。 詳細については、「[シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md)」を参照してください。

この列挙体の値は、 [IDiaSymbol:: get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)メソッドの呼び出しによって返されます。

## <a name="requirements"></a>［要件］
ヘッダー: cvconst. h

## <a name="see-also"></a>関連項目
- [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)
- [シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md)
