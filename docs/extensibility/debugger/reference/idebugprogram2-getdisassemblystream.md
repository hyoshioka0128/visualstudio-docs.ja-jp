---
description: このプログラムまたはこのプログラムの一部の逆アセンブリストリームを取得します。
title: 'IDebugProgram2:: GetDisassemblyStream |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetDisassemblyStream
helpviewer_keywords:
- IDebugProgram2::GetDisassemblyStream
ms.assetid: beda0da5-267e-4bf3-96c4-b659d29e2254
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c7016c003642b9ef2688390de7cdb39be412bded
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075901"
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

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [DISASSEMBLY_STREAM_SCOPE](../../../extensibility/debugger/reference/disassembly-stream-scope.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
