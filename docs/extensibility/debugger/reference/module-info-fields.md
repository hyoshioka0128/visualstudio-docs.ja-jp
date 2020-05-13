---
title: MODULE_INFO_FIELDS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_INFO_FIELDS
helpviewer_keywords:
- MODULE_INFO_FIELDS enumeration
ms.assetid: 8bed85f4-235f-4192-b58f-5fad7a4d7a78
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fa64147738a916d44b6924f193860f74bd10a855
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714329"
---
# <a name="module_info_fields"></a>MODULE_INFO_FIELDS
デバッグ モジュール情報のフラグを指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_MODULE_INFO_FIELDS { 
   MIF_NONE              = 0x0000,
   MIF_NAME              = 0x0001,
   MIF_URL               = 0x0002,
   MIF_VERSION           = 0x0004,
   MIF_DEBUGMESSAGE      = 0x0008,
   MIF_LOADADDRESS       = 0x0010,
   MIF_PREFFEREDADDRESS  = 0x0020,
   MIF_SIZE              = 0x0040,
   MIF_LOADORDER         = 0x0080,
   MIF_TIMESTAMP         = 0x0100,
   MIF_URLSYMBOLLOCATION = 0x0200,
   MIF_FLAGS             = 0x0400,
   MIF_ALLFIELDS         = 0x07ff
};
typedef DWORD MODULE_INFO_FIELDS;
```

```csharp
public enum enum_MODULE_INFO_FIELDS { 
   MIF_NONE              = 0x0000,
   MIF_NAME              = 0x0001,
   MIF_URL               = 0x0002,
   MIF_VERSION           = 0x0004,
   MIF_DEBUGMESSAGE      = 0x0008,
   MIF_LOADADDRESS       = 0x0010,
   MIF_PREFFEREDADDRESS  = 0x0020,
   MIF_SIZE              = 0x0040,
   MIF_LOADORDER         = 0x0080,
   MIF_TIMESTAMP         = 0x0100,
   MIF_URLSYMBOLLOCATION = 0x0200,
   MIF_FLAGS             = 0x0400,
   MIF_ALLFIELDS         = 0x07ff
};
```

## <a name="fields"></a>フィールド
 `MIF_NONE`\
 構造体のフィールドを初期化/使用しない。

 `MIF_NAME`\
 `m_bstrName` [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)構造体のフィールドを初期化/使用します。

 `MIF_URL`\
 構造体のフィールドを`m_bstrUrl`初期化/使用`MODULE_INFO`します。

 `MIF_VERSION`\
 構造体のフィールドを`m_bstrVersion`初期化/使用`MODULE_INFO`します。

 `MIF_DEBUGMESSAGE`\
 構造体のフィールドを`m_bstrDebugMessage`初期化/使用`MODULE_INFO`します。

 `MIF_LOADADDRESS`\
 構造体のフィールドを`m_addrLoadAddress`初期化/使用`MODULE_INFO`します。

 `MIF_PREFFEREDADDRESS`\
 構造体のフィールドを`m_addrPreferredLoadAddress`初期化/使用`MODULE_INFO`します。

 `MIF_SIZE`\
 構造体のフィールドを`m_dwSize`初期化/使用`MODULE_INFO`します。

 `MIF_LOADORDER`\
 構造体のフィールドを`m_dwLoadOrder`初期化/使用`MODULE_INFO`します。

 `MIF_TIMESTAMP`\
 構造体のフィールドを`m_TimeStamp`初期化/使用`MODULE_INFO`します。

 `MIF_URLSYMBOLLOCATION`\
 構造体のフィールドを`m_bstrUrlSymbolLocation`初期化/使用`MODULE_INFO`します。

 `MIF_FLAGS`\
 構造体のフィールドを`m_dwModuleFlags`初期化/使用`MODULE_INFO`します。

 `MIF_ALLFIELDS`\
 構造体のすべてのフィールドを初期化/使用します`MODULE_INFO`。

## <a name="remarks"></a>Remarks
 これらの値は、[初期化するMODULE_INFO](../../../extensibility/debugger/reference/module-info.md)構造体のフィールドを示す引数として[GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)メソッドに渡されます。

 これらの値は、使用されるフィールド`MODULE_INFO`と有効なフィールドを示すために、構造体でも使用されます。

 これらのフラグはビット単位`OR`で組み合わせることができる。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)
