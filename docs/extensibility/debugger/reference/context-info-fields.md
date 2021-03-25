---
description: メモリコンテキストについて取得する情報を指定します。
title: CONTEXT_INFO_FIELDS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONTEXT_INFO_FIELDS
helpviewer_keywords:
- CONTEXT_INFO_FIELDS enumeration
ms.assetid: ef436bd3-738e-47e8-828c-8febce752439
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 878dfb4e2f684b7a28b06820e110b22cdae962b9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096448"
---
# <a name="context_info_fields"></a>CONTEXT_INFO_FIELDS
メモリコンテキストについて取得する情報を指定します。

## <a name="syntax"></a>Syntax

```cpp
enum enum_CONTEXT_INFO_FIELDS {
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
`bstrModuleUrl` [CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md)構造体のフィールドを初期化/使用します。

`CIF_FUNCTION`\
構造体のフィールドを初期化/使用し `bstrFunction` `CONTEXT_INFO` ます。

`CIF_FUNCTIONOFFSET`\
構造体のフィールドを初期化/使用し `posFunctionOffset` `CONTEXT_INFO` ます。

`CIF_ADDRESS`\
構造体のフィールドを初期化/使用し `bstrAddress` `CONTEXT_INFO` ます。

`CIF_ADDRESSOFFSET`\
構造体のフィールドを初期化/使用し `bstrAddressOffset` `CONTEXT_INFO` ます。

`CIF_ALLFIELDS`\
構造体のすべてのフィールドを初期化/使用し `CONTEXT_INFO` ます。

## <a name="remarks"></a>注釈
これらの値は、 [CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md)構造体のどのフィールドを初期化するかを示すために、 [GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)メソッドにパラメーターを渡します。

これらのフラグは、構造体のどのフィールドが `CONTEXT_INFO` 使用され、構造体が返されたときに有効であるかを示すためにも使用されます。

これらの値は、ビットごとの OR と組み合わせることができます。

## <a name="requirements"></a>要件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)
