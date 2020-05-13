---
title: BPRESI_FIELDS |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737724"
---
# <a name="bpresi_fields"></a>BPRESI_FIELDS
ブレークポイントの正常な解決に関して取得する情報を指定します。

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
`bpResLocation` [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)構造の (ブレークポイント解決の場所) フィールドを初期化/使用します。

`BPRESI_PROGRAM`\
構造体のフィールドを`pProgram`初期化/使用`BP_RESOLUTION_INFO`します。

`BPRESI_THREAD`\
構造体のフィールドを`pThread`初期化/使用`BP_RESOLUTION_INFO`します。

`BPRESI_ALLFIELDS`\
すべてのフィールドを指定します。

## <a name="remarks"></a>Remarks
[BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)構造体のどのフィールドを初期化するかを示すために[GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)メソッドに渡されます。

これらのフラグは、構造体のどのフィールドが`BP_RESOLUTION_INFO`使用され、その構造体が返されたときに有効かを示すためにも使用されます。

これらの値はビット単位`OR`で組み合わせることができる。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)
- [GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)
