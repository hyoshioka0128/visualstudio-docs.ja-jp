---
title: IDebugdisアセンブリストリーム2::読み取り |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::Read
helpviewer_keywords:
- IDebugDisassemblyStream2::Read
ms.assetid: 7db5f6bb-73ee-45bc-b187-c1b6aa2dfdd5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4a4f5c0250405c2e2a0314b52c4cbc64d749fc0a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732097"
---
# <a name="idebugdisassemblystream2read"></a>IDebugDisassemblyStream2::Read
逆アセンブリ ストリームの現在位置から開始する命令を読み取ります。

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
[in]分解する命令の数。 この値は`prgDisassembly`、配列の最大長でもあります。

`dwFields`\
[in]DISASSEMBLY_STREAM_FIELDS[列挙体](../../../extensibility/debugger/reference/disassembly-stream-fields.md)のフラグの組み合わせで、入力`prgDisassembly`するフィールドを示します。

`pdwInstructionsRead`\
[アウト]実際に逆アセンブルされた命令の数を返します。

`prgDisassembly`\
[アウト]逆アセンブルされたコードで埋め込まれた[DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)構造体の配列。 この配列の長さは`dwInstructions`、パラメーターによって決まります。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 GetSize メソッドを呼び出すことによって、現在のスコープで使用できる命令の[GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md)最大数を取得できます。

 次の命令が読み取られる現在の位置は[、Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)メソッドを呼び出すことによって変更できます。

 フラグ`DSF_OPERANDS_SYMBOLS`をパラメーターのフラグに追加`DSF_OPERANDS`して、命令`dwFields`を逆アセンブルするときにシンボル名を使用することを示すことができます。

## <a name="see-also"></a>関連項目
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
- [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
- [GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md)
- [Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)
