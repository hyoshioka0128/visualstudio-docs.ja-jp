---
title: Iデバッグプログラム2::ゲットディスアセンブリストリーム |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetDisassemblyStream
helpviewer_keywords:
- IDebugProgram2::GetDisassemblyStream
ms.assetid: beda0da5-267e-4bf3-96c4-b659d29e2254
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2160f963ad1f3f37291519ced30b8096e33a6116
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722866"
---
# <a name="idebugprogram2getdisassemblystream"></a>IDebugProgram2::GetDisassemblyStream
このプログラムまたはこのプログラムの一部の逆アセンブリ ストリームを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetDisassemblyStream( 
   DISASSEMBLY_STREAM_SCOPE   dwScope,
   IDebugCodeContext2*        pCodeContext,
   IDebugDisassemblyStream2** ppDisassemblyStream
);
```

```csharp
int GetDisassemblyStream( 
   enum_DISASSEMBLY_STREAM_SCOPE  dwScope,
   IDebugCodeContext2             pCodeContext,
   out IDebugDisassemblyStream2   ppDisassemblyStream
);
```

## <a name="parameters"></a>パラメーター
`dwScope`\
[in]逆アセンブリ ストリームのスコープを定義する[DISASSEMBLY_STREAM_SCOPE](../../../extensibility/debugger/reference/disassembly-stream-scope.md)列挙体の値を指定します。

`pCodeContext`\
[in]逆アセンブル ストリームを開始する位置を表す[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)オブジェクト。

`ppDisassemblyStream`\
[アウト]逆アセンブリ ストリームを表す[IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。 この`E_DISASM_NOTSUPPORTED`特定のアーキテクチャで逆アセンブリがサポートされていない場合に返します。

## <a name="remarks"></a>Remarks
 パラメーターに`dwScopes`DISASSEMBLY_STREAM_SCOPE列挙型`DSS_HUGE`セットのフラグ[DISASSEMBLY_STREAM_SCOPE](../../../extensibility/debugger/reference/disassembly-stream-scope.md)がある場合、逆アセンブリは、ファイル全体またはモジュール全体など、多数の逆アセンブリ命令を返す必要があります。 フラグが`DSS_HUGE`設定されていない場合、逆アセンブリは小さな領域(通常は単一の関数の領域)に限定されると予想されます。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [DISASSEMBLY_STREAM_SCOPE](../../../extensibility/debugger/reference/disassembly-stream-scope.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
