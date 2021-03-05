---
description: 逆アセンブリフィールドについて取得する情報を指定します。
title: DISASSEMBLY_STREAM_FIELDS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DISASSEMBLY_STREAM_FIELDS
helpviewer_keywords:
- DISASSEMBLY_STREAM_FIELDS enumeration
ms.assetid: cfc9b4de-c756-4844-bea7-d9f186a51d1b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8bb45f492a58bd079a1b73212fc9473041d10589
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102170472"
---
# <a name="disassembly_stream_fields"></a>DISASSEMBLY_STREAM_FIELDS
逆アセンブリフィールドについて取得する情報を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_DISASSEMBLY_STREAM_FIELDS {
    DSF_ADDRESS          = 0x00000001,
    DSF_ADDRESSOFFSET    = 0x00000002,
    DSF_CODEBYTES        = 0x00000004,
    DSF_OPCODE           = 0x00000008,
    DSF_OPERANDS         = 0x00000010,
    DSF_SYMBOL           = 0x00000020,
    DSF_CODELOCATIONID   = 0x00000040,
    DSF_POSITION         = 0x00000080,
    DSF_DOCUMENTURL      = 0x00000100,
    DSF_BYTEOFFSET       = 0x00000200,
    DSF_FLAGS            = 0x00000400,
    DSF_OPERANDS_SYMBOLS = 0x00010000,
    DSF_ALL              = 0x000107ff
};
typedef DWORD DISASSEMBLY_STREAM_FIELDS;
```

```csharp
public enum enum_DISASSEMBLY_STREAM_FIELDS {
    DSF_ADDRESS          = 0x00000001,
    DSF_ADDRESSOFFSET    = 0x00000002,
    DSF_CODEBYTES        = 0x00000004,
    DSF_OPCODE           = 0x00000008,
    DSF_OPERANDS         = 0x00000010,
    DSF_SYMBOL           = 0x00000020,
    DSF_CODELOCATIONID   = 0x00000040,
    DSF_POSITION         = 0x00000080,
    DSF_DOCUMENTURL      = 0x00000100,
    DSF_BYTEOFFSET       = 0x00000200,
    DSF_FLAGS            = 0x00000400,
    DSF_OPERANDS_SYMBOLS = 0x00010000,
    DSF_ALL              = 0x000107ff
};
```

## <a name="fields"></a>フィールド
`DSF_ADDRESS`\
フィールドを初期化/使用 `bstrAddress` します。

`DSF_ADDRESSOFFSET`\
フィールドを初期化/使用 `bstrAddressOffset` します。

`DSF_CODEBYTES`\
フィールドを初期化/使用 `bstrCodeBytes` します。

`DSF_OPCODE`\
フィールドを初期化/使用 `bstrOpCode` します。

`DSF_OPERANDS`\
フィールドを初期化/使用 `bstrOperands` します。

`DSF_SYMBOL`\
フィールドを初期化/使用 `bstrSymbol` します。

`DSF_CODELOCATIONID`\
フィールドを初期化/使用 `uCodeLocationId` します。

`DSF_POSITION`\
フィールドとフィールドを初期化/使用し `posBeg` `posEnd` ます。

`DSF_DOCUMENTURL`\
フィールドを初期化/使用 `bstrDocumentUrl` します。

`DSF_BYTEOFFSET`\
フィールドを初期化/使用 `dwByteOffset` します。

`DSF_FLAGS`\
`dwFlags`([DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)) フィールドを初期化/使用します。

`DSF_OPERANDS_SYMBOLS`\
フィールドにシンボル名を含め `bstrOperands` ます。

`DSF_ALL`\
逆アセンブリストリームのすべてのフィールドを指定します。

## <a name="remarks"></a>解説
[Disassemblydata](../../../extensibility/debugger/reference/disassemblydata.md)構造体内で初期化されるフィールドを示すために、 [Read](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)メソッドにパラメーターとして渡されます。

構造体 `dwFields` のメンバーに、 `DisassemblyData` 構造体が返されるときに使用されるフィールドと有効なフィールドを示すために使用されます。

これらの値は、ビットごとのを使用して組み合わせることができ `OR` ます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
- [読み取り](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)
- [DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)
