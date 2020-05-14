---
title: DISASSEMBLY_STREAM_FIELDS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DISASSEMBLY_STREAM_FIELDS
helpviewer_keywords:
- DISASSEMBLY_STREAM_FIELDS enumeration
ms.assetid: cfc9b4de-c756-4844-bea7-d9f186a51d1b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d10f2143cbefa86442e4087ac098020f5f2bd6ac
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737356"
---
# <a name="disassembly_stream_fields"></a>DISASSEMBLY_STREAM_FIELDS
逆アセンブリ フィールドについて取得する情報を指定します。

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
フィールドを初期化/`bstrAddress`使用します。

`DSF_ADDRESSOFFSET`\
フィールドを初期化/`bstrAddressOffset`使用します。

`DSF_CODEBYTES`\
フィールドを初期化/`bstrCodeBytes`使用します。

`DSF_OPCODE`\
フィールドを初期化/`bstrOpCode`使用します。

`DSF_OPERANDS`\
フィールドを初期化/`bstrOperands`使用します。

`DSF_SYMBOL`\
フィールドを初期化/`bstrSymbol`使用します。

`DSF_CODELOCATIONID`\
フィールドを初期化/`uCodeLocationId`使用します。

`DSF_POSITION`\
フィールドと`posEnd`フィールド`posBeg`を初期化/使用します。

`DSF_DOCUMENTURL`\
フィールドを初期化/`bstrDocumentUrl`使用します。

`DSF_BYTEOFFSET`\
フィールドを初期化/`dwByteOffset`使用します。

`DSF_FLAGS`\
[ ( `dwFlags` [DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)) ] フィールドを初期化/使用します。

`DSF_OPERANDS_SYMBOLS`\
フィールドにシンボル名を`bstrOperands`含めます。

`DSF_ALL`\
逆アセンブリ ストリームのすべてのフィールドを指定します。

## <a name="remarks"></a>Remarks
初期化する[DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)構造体のフィールドを示す Read[メソッドに](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)パラメーターとして渡されます。

構造体の`dwFields`メンバーに対して`DisassemblyData`、構造体が返されるときに使用され、有効なフィールドを示すために使用されます。

これらの値はビット単位`OR`で組み合わせることができる。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
- [Read](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)
- [DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)
