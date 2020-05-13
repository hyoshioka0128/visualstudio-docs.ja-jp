---
title: MemoryTypeEnum |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- MemoryTypeEnum enumeration
ms.assetid: 8778c047-edeb-4495-8f9f-3f8bbb297099
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e0710ec5cdfcfcb59407d18b43b885603f017fdb
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738630"
---
# <a name="memorytypeenum"></a>MemoryTypeEnum
アクセスするメモリの種類を指定します。

## <a name="syntax"></a>構文

```C++
enum MemoryTypeEnum {
    MemTypeCode,
    MemTypeData,
    MemTypeStack,
    MemTypeAny = -1
};
```

#### <a name="parameters"></a>パラメーター
`MemTypeCode` は、コードメモリにのみアクセスします。

`MemTypeData` は、データまたはスタックメモリにアクセスします。

`MemTypeStack` は、スタックメモリにのみアクセスします。

`MemTypeAny` は、あらゆる種類のメモリにアクセスします。

## <a name="remarks"></a>Remarks
この列挙体の値は、さまざまな種類のメモリへのアクセスを制限するために、 [IDiaStackWalkHelper:: readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md)メソッドに渡されます。

## <a name="requirements"></a>［要件］
ヘッダー: cvconst. h

## <a name="see-also"></a>関連項目
- [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaStackWalkHelper::readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md)
