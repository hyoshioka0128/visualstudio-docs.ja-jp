---
description: 逆アセンブリストリームの現在位置から指示を読み取ります。
title: 'IDebugDisassemblyStream2:: Read |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::Read
helpviewer_keywords:
- IDebugDisassemblyStream2::Read
ms.assetid: 7db5f6bb-73ee-45bc-b187-c1b6aa2dfdd5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bcabd0cc42f013b579ee32deeb33d68cd9d45f5d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066920"
---
# <a name="idebugdisassemblystream2read"></a>IDebugDisassemblyStream2::Read
逆アセンブリストリームの現在位置から指示を読み取ります。

## <a name="syntax"></a>構文

```cpp
HRESULT Read( 
   DWORD                     dwInstructions,
   DISASSEMBLY_STREAM_FIELDS dwFields,
   DWORD*                    pdwInstructionsRead,
   DisassemblyData*          prgDisassembly
);
```

```csharp
int Read( 
   uint                           dwInstructions,
   enum_DISASSEMBLY_STREAM_FIELDS dwFields,
   out uint                       pdwInstructionsRead,
   DisassemblyData[]              prgDisassembly
);
```

## <a name="parameters"></a>パラメーター
`dwInstructions`\
から逆アセンブルする命令の数。 この値は、配列の最大長でも `prgDisassembly` あります。

`dwFields`\
からどのフィールドを入力するかを示す、 [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md) 列挙のフラグの組み合わせ `prgDisassembly` 。

`pdwInstructionsRead`\
入出力実際に逆アセンブルされた命令の数を返します。

`prgDisassembly`\
入出力逆アセンブルされたコードで埋め込まれる [Disassemblydata](../../../extensibility/debugger/reference/disassemblydata.md) 構造体の配列。逆アセンブル命令ごとに1つの構造体。 この配列の長さは、パラメーターによって指定され `dwInstructions` ます。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 現在のスコープで使用可能な命令の最大数は、 [GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md) メソッドを呼び出すことによって取得できます。

 次の命令が読み込まれる現在位置は、 [Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md) メソッドを呼び出すことによって変更できます。

 フラグは、 `DSF_OPERANDS_SYMBOLS` `DSF_OPERANDS` 命令を `dwFields` 逆アセンブルするときにシンボル名を使用することを示すために、パラメーターのフラグに追加できます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
- [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
- [GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md)
- [Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)
