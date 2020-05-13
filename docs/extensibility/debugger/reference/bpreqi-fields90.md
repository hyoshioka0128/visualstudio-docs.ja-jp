---
title: BPREQI_FIELDS90 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- BPREQI_FIELDS90 enumeration
ms.assetid: bf6f7efc-39f2-46a2-906d-c3647bf89995
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ea46939118ec48490280d6a85cc84e144d320d4e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737739"
---
# <a name="bpreqi_fields90"></a>BPREQI_FIELDS90
ブレークポイント要求に関して取得する情報を指定する有効な値を列挙します。 この列挙体は[、BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)列挙体を拡張します。

## <a name="syntax"></a>構文

```cpp
enum enum_BPREQI_FIELDS90
{
    // VS 8.0 values
    BPREQI90_BPLOCATION                = 0x0001,
    BPREQI90_LANGUAGE                  = 0x0002,
    BPREQI90_PROGRAM                   = 0x0004,
    BPREQI90_PROGRAMNAME               = 0x0008,
    BPREQI90_THREAD                    = 0x0010,
    BPREQI90_THREADNAME                = 0x0020,
    BPREQI90_PASSCOUNT                 = 0x0040,
    BPREQI90_CONDITION                 = 0x0080,
    BPREQI90_FLAGS                     = 0x0100,
    BPREQI90_ALLOLDFIELDS              = 0x01ff,
    BPREQI90_VENDOR                    = 0x0200,
    BPREQI90_CONSTRAINT                = 0x0400,
    BPREQI90_TRACEPOINT                = 0x0800,

    // Values added in VS 9.0
    BPREQI90_MACROTRACEPOINT           = 0x1000,

    BPREQI90_ALLFIELDS                 = 0xffff
};
typedef DWORD BPREQI_FIELDS90;
```

```csharp
public enum enum_BPREQI_FIELDS90
{
    // VS 8.0 values
    BPREQI90_BPLOCATION                = 0x0001,
    BPREQI90_LANGUAGE                  = 0x0002,
    BPREQI90_PROGRAM                   = 0x0004,
    BPREQI90_PROGRAMNAME               = 0x0008,
    BPREQI90_THREAD                    = 0x0010,
    BPREQI90_THREADNAME                = 0x0020,
    BPREQI90_PASSCOUNT                 = 0x0040,
    BPREQI90_CONDITION                 = 0x0080,
    BPREQI90_FLAGS                     = 0x0100,
    BPREQI90_ALLOLDFIELDS              = 0x01ff,
    BPREQI90_VENDOR                    = 0x0200,
    BPREQI90_CONSTRAINT                = 0x0400,
    BPREQI90_TRACEPOINT                = 0x0800,

    // Values added in VS 9.0
    BPREQI90_MACROTRACEPOINT           = 0x1000,

    BPREQI90_ALLFIELDS                 = 0xffff
};
```

## <a name="fields"></a>フィールド
`BPREQI90_BPLOCATION`\
[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)または[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)構造体`bpLocation`の (ブレークポイントの場所) フィールドを初期化または使用します。

`BPREQI90_LANGUAGE`\
または`BP_REQUEST_INFO2`構造体の`guidLanguage`フィールドを初期化`BP_REQUEST_INFO`または使用します。

`BPREQI90_PROGRAM`\
または`BP_REQUEST_INFO2`構造体の`pProgram`フィールドを初期化`BP_REQUEST_INFO`または使用します。

`BPREQI90_PROGRAMNAME`\
または`BP_REQUEST_INFO2`構造体の`bstrProgramName`フィールドを初期化`BP_REQUEST_INFO`または使用します。

`BPREQI90_THREAD`\
または`BP_REQUEST_INFO2`構造体の`pThread`フィールドを初期化`BP_REQUEST_INFO`または使用します。

`BPREQI90_THREADNAME`\
または`BP_REQUEST_INFO2`構造体の`bstrThreadName`フィールドを初期化`BP_REQUEST_INFO`または使用します。

`BPREQI90_PASSCOUNT`\
または`BP_REQUEST_INFO2`構造体の`bpPassCount`フィールドを初期化`BP_REQUEST_INFO`または使用します。

`BPREQI90_CONDITION`\
または`bpCondition``BP_REQUEST_INFO2`構造体の (ブレークポイント条件) フィールドを`BP_REQUEST_INFO`初期化または使用します。

`BPREQI90_FLAGS`\
または`BP_REQUEST_INFO2`構造体の`dwFlags`フィールドを初期化`BP_REQUEST_INFO`または使用します。

`BPREQI90_ALLOLDFIELDS`\
構造体の を初期化するか、すべてのフィールド`BP_REQUEST_INFO`を使用します。

`BPREQI90_VENDOR`\
構造体の`BP_REQUEST_INFO2`フィールドを`guidVendor`初期化または使用します。

`BPREQI90_CONSTRAINT`\
構造体の`BP_REQUEST_INFO2`フィールドを`bstrConstraint`初期化または使用します。

`BPREQI90_TRACEPOINT`\
構造体の`BP_REQUEST_INFO2`フィールドを`bstrTracepoint`初期化または使用します。

`BPREQI90_MACROTRACEPOINT`\
構造体の`BP_REQUEST_INFO2`フィールドを`bstrMacroTracepoint`初期化または使用します。 BPREQI_ALLFIELDSには、このフィールドは含まれません。

`BPREQI90_ALLFIELDS`\
構造体のすべてのフィールドを指定`BP_REQUEST_INFO2`します。

## <a name="requirements"></a>必要条件
ヘッダー: Msdbg90.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
