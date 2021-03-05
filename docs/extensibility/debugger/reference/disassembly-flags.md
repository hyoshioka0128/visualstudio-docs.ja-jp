---
description: 逆アセンブリのフラグを指定します。
title: DISASSEMBLY_FLAGS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DISASSEMBLY_FLAGS
helpviewer_keywords:
- DISASSEMBLY_FLAGS enumeration
ms.assetid: c1ec5a4d-5d42-4660-932c-7348550140cb
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3aeaf00e7073cd1146dcc5856684ed7209e7d800
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102170485"
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
この命令が前のドキュメントとは異なるドキュメントにあることを示します。

`DF_DISABLED`\
この命令が実行されないことを示します。

`DF_INSTRUCTION_ACTIVE`\
この命令が、次に実行される命令の1つであることを示します (複数存在する場合もあります)。

`DF_DATA`\
この命令が (コードではなく) 実際のデータであることを示します。

`DF_HASSOURCE`\
この命令にソースがあることを示します。 プロファイルやガベージコレクションコードなどの一部の命令には、対応するソースがありません。

`DF_DOCUMENT_CHECKSUM`\
フィールドに `bstrDocumentUrl` 、ドキュメントの URL の後にチェックサムデータが格納されていることを示します。 チェックサムデータの格納方法については、 [Disassemblydata](../../../extensibility/debugger/reference/disassemblydata.md) 構造体の「解説」を参照してください。

## <a name="remarks"></a>解説
`dwFlags` [Disassemblydata](../../../extensibility/debugger/reference/disassemblydata.md)構造体のメンバーとして使用されます。

これらのフラグは、ビットごとのを使用して組み合わせることができ `OR` ます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
