---
title: CONTEXT_INFO_FIELDS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONTEXT_INFO_FIELDS
helpviewer_keywords:
- CONTEXT_INFO_FIELDS enumeration
ms.assetid: ef436bd3-738e-47e8-828c-8febce752439
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b398e7ee549026750cbdff7b7fede8522116f346
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737589"
---
# <a name="context_info_fields"></a>CONTEXT_INFO_FIELDS
メモリ コンテキストに関して取得する情報を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_CONTEXT_INFO_FIELDS {
    CIF_MODULEURL =       0x00000001,
    CIF_FUNCTION =        0x00000002,
    CIF_FUNCTIONOFFSET =  0x00000004,
    CIF_ADDRESS =         0x00000008,
    CIF_ADDRESSOFFSET =   0x00000010,
    CIF_ADDRESSABSOLUTE = 0x00000020,
    CIF_ALLFIELDS =       0x0000003f
};
typedef DWORD CONTEXT_INFO_FIELDS;
```

```csharp
public enum enum_CONTEXT_INFO_FIELDS {
    CIF_MODULEURL =       0x00000001,
    CIF_FUNCTION =        0x00000002,
    CIF_FUNCTIONOFFSET =  0x00000004,
    CIF_ADDRESS =         0x00000008,
    CIF_ADDRESSOFFSET =   0x00000010,
    CIF_ADDRESSABSOLUTE = 0x00000020,
    CIF_ALLFIELDS =       0x0000003f
};
```

## <a name="fields"></a>フィールド
`CIF_MODULEURL`\
CONTEXT_INFO構造体のフィールド`bstrModuleUrl`を初期化/[CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md)使用します。

`CIF_FUNCTION`\
構造体のフィールドを`bstrFunction`初期化/使用`CONTEXT_INFO`します。

`CIF_FUNCTIONOFFSET`\
構造体のフィールドを`posFunctionOffset`初期化/使用`CONTEXT_INFO`します。

`CIF_ADDRESS`\
構造体のフィールドを`bstrAddress`初期化/使用`CONTEXT_INFO`します。

`CIF_ADDRESSOFFSET`\
構造体のフィールドを`bstrAddressOffset`初期化/使用`CONTEXT_INFO`します。

`CIF_ALLFIELDS`\
構造体のすべてのフィールドを初期化/使用`CONTEXT_INFO`します。

## <a name="remarks"></a>Remarks
これらの値は、[初期化するCONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md)構造体のフィールドを示すパラメーターを[GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)メソッドに渡されます。

これらのフラグは、構造体のどのフィールドが使用され、`CONTEXT_INFO`構造体が返されるときに有効かを示すためにも使用されます。

これらの値はビット単位の OR と組み合わせられます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [Context_info](../../../extensibility/debugger/reference/context-info.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)
