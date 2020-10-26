---
title: BPRESI_FIELDS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BPRESI_FIELDS
helpviewer_keywords:
- BPRESI_FIELDS enumeration
ms.assetid: 99f17b1e-3e67-4f85-89d6-5c6cf45c8008
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 837bb7d25ab8dea2b146a98cc65d320b58162685
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80737724"
---
# <a name="bpresi_fields"></a>BPRESI_FIELDS
ブレークポイントが正常に解決されたかどうかを取得するための情報を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_BPRESI_FIELDS {
    BPRESI_BPRESLOCATION = 0x0001,
    BPRESI_PROGRAM       = 0x0002,
    BPRESI_THREAD        = 0x0004,
    BPRESI_ALLFIELDS     = 0xffffffff
};
typedef DWORD BPRESI_FIELDS;
```

```csharp
public enum enum_BPRESI_FIELDS {
    BPRESI_BPRESLOCATION = 0x0001,
    BPRESI_PROGRAM       = 0x0002,
    BPRESI_THREAD        = 0x0004,
    BPRESI_ALLFIELDS     = 0xffffffff
};
```

## <a name="fields"></a>フィールド
`BPRESI_BPRESLOCATION`\
`bpResLocation` [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)構造体の (ブレークポイント解決の場所) フィールドを初期化または使用します。

`BPRESI_PROGRAM`\
構造体のフィールドを初期化/使用し `pProgram` `BP_RESOLUTION_INFO` ます。

`BPRESI_THREAD`\
構造体のフィールドを初期化/使用し `pThread` `BP_RESOLUTION_INFO` ます。

`BPRESI_ALLFIELDS`\
すべてのフィールドを指定します。

## <a name="remarks"></a>解説
[BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)構造体のどのフィールドを初期化するかを示すために[get解決情報](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)メソッドに渡されます。

これらのフラグは、構造体のどのフィールドが使用され、その構造が返されたときに有効であるかを示すためにも使用され `BP_RESOLUTION_INFO` ます。

これらの値は、ビットごとのを使用して組み合わせることができ `OR` ます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)
- [GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)
