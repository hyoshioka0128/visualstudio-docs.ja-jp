---
title: REFERENCE_TYPE |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- REFERENCE_TYPE
helpviewer_keywords:
- REFERENCE_TYPE enumeration
ms.assetid: b1ffba10-eb9d-48ba-bf48-6d8b71d6f270
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 29ce6ad17aa32b98fd28914c422a49bd8bcc14b5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713656"
---
# <a name="reference_type"></a>REFERENCE_TYPE
参照の種類を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_REFERENCE_TYPE { 
   REF_TYPE_WEAK   = 0x0001,
   REF_TYPE_STRONG = 0x0002
};
typedef DWORD REFERENCE_TYPE;
```

```csharp
public enum enum_REFERENCE_TYPE { 
   REF_TYPE_WEAK   = 0x0001,
   REF_TYPE_STRONG = 0x0002
};
```

## <a name="fields"></a>フィールド
 `REF_TYPE_WEAK`\
 弱参照を指定します。 と`REF_TYPE_STRONG`組み合わせることはできません。

 `REF_TYPE_STRONG`\
 厳密な参照を指定します。 と`REF_TYPE_WEAK`組み合わせることはできません。

## <a name="remarks"></a>Remarks
 DEBUG_REFERENCE_INFO構造体の`dwRefType`メンバーとして使用[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)されます。

 メソッドにパラメーターとして渡[されます](../../../extensibility/debugger/reference/idebugreference2-setreferencetype.md)。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
- [SetReferenceType](../../../extensibility/debugger/reference/idebugreference2-setreferencetype.md)
