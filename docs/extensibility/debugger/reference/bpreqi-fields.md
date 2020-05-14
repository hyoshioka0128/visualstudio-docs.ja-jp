---
title: BPREQI_FIELDS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BPREQI_FIELDS
helpviewer_keywords:
- BPREQI_FIELDS enumeration
ms.assetid: 679e771e-4a79-484e-af37-f962ef4aa245
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4c0e10b6c253c61a9e68e0cf161201f7d2520ae6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737752"
---
# <a name="bpreqi_fields"></a>BPREQI_FIELDS
ブレークポイント要求について取得する情報を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_BPREQI_FIELDS {
    BPREQI_BPLOCATION   = 0x0001,
    BPREQI_LANGUAGE     = 0x0002,
    BPREQI_PROGRAM      = 0x0004,
    BPREQI_PROGRAMNAME  = 0x0008,
    BPREQI_THREAD       = 0x0010,
    BPREQI_THREADNAME   = 0x0020,
    BPREQI_PASSCOUNT    = 0x0040,
    BPREQI_CONDITION    = 0x0080,
    BPREQI_FLAGS        = 0x0100,
    BPREQI_ALLOLDFIELDS = 0x01ff
    BPREQI_VENDOR       = 0x0200,   // BP_REQUEST_INFO2 only
    BPREQI_CONSTRAINT   = 0x0400,   // BP_REQUEST_INFO2 only
    BPREQI_TRACEPOINT   = 0x0800,   // BP_REQUEST_INFO2 only
    BPREQI_ALLFIELDS    = 0x0fff    // BP_REQUEST_INFO2 only
};
typedef DWORD BPREQI_FIELDS;
```

```csharp
public enum enum_BPREQI_FIELDS {
    BPREQI_BPLOCATION   = 0x0001,
    BPREQI_LANGUAGE     = 0x0002,
    BPREQI_PROGRAM      = 0x0004,
    BPREQI_PROGRAMNAME  = 0x0008,
    BPREQI_THREAD       = 0x0010,
    BPREQI_THREADNAME   = 0x0020,
    BPREQI_PASSCOUNT    = 0x0040,
    BPREQI_CONDITION    = 0x0080,
    BPREQI_FLAGS        = 0x0100,
    BPREQI_ALLOLDFIELDS = 0x01ff
    BPREQI_VENDOR       = 0x0200,   // BP_REQUEST_INFO2 only
    BPREQI_CONSTRAINT   = 0x0400,   // BP_REQUEST_INFO2 only
    BPREQI_TRACEPOINT   = 0x0800,   // BP_REQUEST_INFO2 only
    BPREQI_ALLFIELDS    = 0x0fff    // BP_REQUEST_INFO2 only
};
```

## <a name="fields"></a>フィールド
`BPREQI_BPLOCATION`\
[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)または[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)構造`bpLocation`の (ブレークポイントの場所) フィールドを初期化/使用します。

`BPREQI_LANGUAGE`\
または`BP_REQUEST_INFO2`構造体のフィールド`guidLanguage`を初期化/`BP_REQUEST_INFO`使用します。

`BPREQI_PROGRAM`\
または`BP_REQUEST_INFO2`構造体のフィールド`pProgram`を初期化/`BP_REQUEST_INFO`使用します。

`BPREQI_PROGRAMNAME`\
または`BP_REQUEST_INFO2`構造体のフィールド`bstrProgramName`を初期化/`BP_REQUEST_INFO`使用します。

`BPREQI_THREAD`\
または`BP_REQUEST_INFO2`構造体のフィールド`pThread`を初期化/`BP_REQUEST_INFO`使用します。

`BPREQI_THREADNAME`\
または`BP_REQUEST_INFO2`構造体のフィールド`bstrThreadName`を初期化/`BP_REQUEST_INFO`使用します。

`BPREQI_PASSCOUNT`\
または`BP_REQUEST_INFO2`構造体のフィールド`bpPassCount`を初期化/`BP_REQUEST_INFO`使用します。

`BPREQI_CONDITION`\
または構造体の`bpCondition`(ブレークポイント条件) フィールドを`BP_REQUEST_INFO`初期化`BP_REQUEST_INFO2`または使用します。

`BPREQI_FLAGS`\
または`BP_REQUEST_INFO2`構造体のフィールド`dwFlags`を初期化/`BP_REQUEST_INFO`使用します。

`BPREQI_ALLOLDFIELDS`\
構造体の全フィールドを初期化/使用します`BP_REQUEST_INFO`。

`BPREQI_VENDOR`\
構造体の`BP_REQUEST_INFO2`フィールドを`guidVendor`初期化/使用します。

`BPREQI_CONSTRAINT`\
構造体の`BP_REQUEST_INFO2`フィールドを`bstrConstraint`初期化/使用します。

`BPREQI_TRACEPOINT`\
構造体の`BP_REQUEST_INFO2`フィールドを`bstrTracepoint`初期化/使用します。

`BPREQI_ALLFIELDS`\
構造体のすべてのフィールドを指定`BP_REQUEST_INFO2`します。

## <a name="remarks"></a>Remarks
[getRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)メソッドと[BP_REQUEST_INFOメソッド](../../../extensibility/debugger/reference/bp-request-info.md)に引数として渡され[、BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)のフィールドと[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)構造体を初期化する方法を指定します。

これらのフラグは、 および`BP_REQUEST_INFO``BP_REQUEST_INFO2`構造体のどのフィールドが使用され、各構造体が戻されたときに有効かを示すためにも使用されます。

これらの値はビット単位`OR`で組み合わせることができる。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
