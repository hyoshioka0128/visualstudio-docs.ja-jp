---
title: Stackフレーム Typeenum |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- StackFrameTypeEnum enumeration
ms.assetid: 61e40163-eee0-4c1f-af47-cef3771bdc41
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 20b0c9dd106e5744a369ddaa6cb870788f7464d3
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738550"
---
# <a name="stackframetypeenum"></a>StackFrameTypeEnum
スタックフレームの種類を指定します。

## <a name="syntax"></a>構文

```C++
enum StackFrameTypeEnum {
    FrameTypeFPO,
    FrameTypeTrap,
    FrameTypeTSS,
    FrameTypeStandard,
    FrameTypeFrameData,
    FrameTypeUnknown = -1
};
```

## <a name="elements"></a>Elements
`FrameTypeFPO` フレームポインターを省略します。FPO info を利用できます。

`FrameTypeTrap` カーネルトラップフレーム。

`FrameTypeTSS` カーネルトラップフレーム。

`FrameTypeStandard` 標準の EBP スタックフレームです。

`FrameTypeFrameData` フレームポインターを省略します。使用可能なフレームデータ情報です。

デバッグ情報が含まれていないフレームを `FrameTypeUnknown` します。

## <a name="remarks"></a>Remarks
この列挙体の値は、 [IDiaStackFrame:: get_type](../../debugger/debug-interface-access/idiastackframe-get-type.md)メソッドの呼び出しによって返されます。

## <a name="requirements"></a>［要件］
ヘッダー: cvconst. h

## <a name="see-also"></a>関連項目
- [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaStackFrame::get_type](../../debugger/debug-interface-access/idiastackframe-get-type.md)
