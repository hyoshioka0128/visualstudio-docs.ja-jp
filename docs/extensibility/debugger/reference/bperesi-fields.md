---
title: BPERESI_FIELDS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BPERESI_FIELDS
helpviewer_keywords:
- BPERESI_FIELDS enumeration
ms.assetid: dd7dd89c-1043-46a1-a929-099cc039c344
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: af2f20e7d3abd79261dc18753a7eb940666fc186
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737758"
---
# <a name="bperesi_fields"></a>BPERESI_FIELDS
ブレークポイントの解決に失敗した場合に取得する情報を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_BPERESI_FIELDS {
    PERESI_BPRESLOCATION = 0x0001,
    BPERESI_PROGRAM      = 0x0002,
    BPERESI_THREAD       = 0x0004,
    BPERESI_MESSAGE      = 0x0008,
    BPERESI_TYPE         = 0x0010,
    BPERESI_ALLFIELDS    = 0xffffffff
};
typedef DWORD BPERESI_FIELDS;
```

```csharp
public enum enum_BPERESI_FIELDS {
    PERESI_BPRESLOCATION = 0x0001,
    BPERESI_PROGRAM      = 0x0002,
    BPERESI_THREAD       = 0x0004,
    BPERESI_MESSAGE      = 0x0008,
    BPERESI_TYPE         = 0x0010,
    BPERESI_ALLFIELDS    = 0xffffffff
};
```

## <a name="fields"></a>フィールド
`PERESI_BPRESLOCATION`\
`bpResLocation` [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)構造の (ブレークポイント解決の場所) フィールドを初期化/使用します。

`BPERESI_PROGRAM`\
構造体のフィールドを`pProgram`初期化/使用`BP_ERROR_RESOLUTION_INFO`します。

`BPERESI_THREAD`\
構造体のフィールドを`pThread`初期化/使用`BP_ERROR_RESOLUTION_INFO`します。

`BPERESI_MESSAGE`\
構造体のフィールドを`bstrMessage`初期化/使用`BP_ERROR_RESOLUTION_INFO`します。

`BPERESI_TYPE`\
構造体の (`dwType`ブレークポイントの種類) フィールドを`BP_ERROR_RESOLUTION_INFO`初期化/使用します。

`BPERESI_ALLFIELDS`\
構造体のすべてのフィールドを初期化/使用`BP_ERROR_RESOLUTION_INFO`します。

## <a name="remarks"></a>Remarks
[初期化するBP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)構造体のフィールドを示すパラメーターとして[GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)メソッドに渡されます。

これらの値は、構造体のどのフィールドが`BP_ERROR_RESOLUTION_INFO`使用され、その構造体が返されたときに有効かを示すためにも使用されます。

これらの値はビット単位`OR`で組み合わせることができる。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
- [GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)
