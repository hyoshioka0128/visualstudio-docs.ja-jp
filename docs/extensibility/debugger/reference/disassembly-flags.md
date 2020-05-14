---
title: DISASSEMBLY_FLAGS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DISASSEMBLY_FLAGS
helpviewer_keywords:
- DISASSEMBLY_FLAGS enumeration
ms.assetid: c1ec5a4d-5d42-4660-932c-7348550140cb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ba6d9db3ad2cb1f9bbc9e3cea27aba939c6dd499
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737375"
---
# <a name="disassembly_flags"></a>DISASSEMBLY_FLAGS
逆アセンブリのフラグを指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_DISASSEMBLY_FLAGS {
    DF_DOCUMENTCHANGE     = 0x00000001,
    DF_DISABLED           = 0x00000002,
    DF_INSTRUCTION_ACTIVE = 0x00000004,
    DF_DATA               = 0x00000008,
    DF_HASSOURCE          = 0x00000010,
    DF_DOCUMENT_CHECKSUM  = 0x00000020
};
typedef DWORD DISASSEMBLY_FLAGS;
```

```csharp
public enum enum_DISASSEMBLY_FLAGS {
    DF_DOCUMENTCHANGE     = 0x00000001,
    DF_DISABLED           = 0x00000002,
    DF_INSTRUCTION_ACTIVE = 0x00000004,
    DF_DATA               = 0x00000008,
    DF_HASSOURCE          = 0x00000010,
    DF_DOCUMENT_CHECKSUM  = 0x00000020
};
```

## <a name="fields"></a>フィールド
`DF_DOCUMENTCHANGE`\
この命令が前のドキュメントとは異なるドキュメント内にあることを示します。

`DF_DISABLED`\
この命令が実行されないことを示します。

`DF_INSTRUCTION_ACTIVE`\
この命令が、次に実行される命令の 1 つであることを示します (複数の命令が存在する可能性があります)。

`DF_DATA`\
この命令が実際にはデータであることを示します (コードではありません)。

`DF_HASSOURCE`\
この命令にソースがあることを示します。 プロファイリングやガベージ コレクション コードなどの一部の命令には、対応するソースがありません。

`DF_DOCUMENT_CHECKSUM`\
ドキュメント`bstrDocumentUrl`URL の後にチェックサム データが含まれるフィールドを示します。 チェックサム データの格納方法については[、DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)構造体の「解説」セクションを参照してください。

## <a name="remarks"></a>Remarks
構造体の`dwFlags`メンバーとして使用[されます](../../../extensibility/debugger/reference/disassemblydata.md)。

これらのフラグはビット単位`OR`で組み合わせることができる。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
