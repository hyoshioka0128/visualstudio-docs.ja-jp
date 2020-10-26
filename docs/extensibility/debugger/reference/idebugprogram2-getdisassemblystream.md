---
title: 'IDebugProgram2:: GetDisassemblyStream |Microsoft Docs'
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80722866"
---
# <a name="idebugprogram2getdisassemblystream"></a>IDebugProgram2::GetDisassemblyStream
このプログラムまたはこのプログラムの一部の逆アセンブリストリームを取得します。

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
から逆アセンブリストリームのスコープを定義する [DISASSEMBLY_STREAM_SCOPE](../../../extensibility/debugger/reference/disassembly-stream-scope.md) 列挙からの値を指定します。

`pCodeContext`\
から逆アセンブリストリームを開始する位置を表す [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) オブジェクト。

`ppDisassemblyStream`\
入出力逆アセンブリストリームを表す [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 `E_DISASM_NOTSUPPORTED`この特定のアーキテクチャで逆アセンブリがサポートされていない場合は、を返します。

## <a name="remarks"></a>注釈
 パラメーターに `dwScopes` `DSS_HUGE` [DISASSEMBLY_STREAM_SCOPE](../../../extensibility/debugger/reference/disassembly-stream-scope.md) 列挙セットのフラグが設定されている場合、逆アセンブリは、ファイルまたはモジュール全体に対して、たとえば、多数の逆アセンブリ命令を返すことが想定されます。 `DSS_HUGE`フラグが設定されていない場合、逆アセンブルは小さな領域 (通常は1つの関数) に限定されます。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [DISASSEMBLY_STREAM_SCOPE](../../../extensibility/debugger/reference/disassembly-stream-scope.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
