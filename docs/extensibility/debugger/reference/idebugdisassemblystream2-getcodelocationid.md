---
description: 特定のコードコンテキストのコード位置識別子を返します。
title: 'IDebugDisassemblyStream2:: GetCodeLocationId |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::GetCodeLocationId
helpviewer_keywords:
- IDebugDisassemblyStream2::GetCodeLocationId
ms.assetid: 567adfb8-2f54-499a-a027-e4ecb82277ef
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8c1c3a6f7a9f2e2a0617f1322d17073a9dcc7c32
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102162928"
---
# <a name="idebugdisassemblystream2getcodelocationid"></a>IDebugDisassemblyStream2::GetCodeLocationId
特定のコードコンテキストのコード位置識別子を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCodeLocationId( 
   IDebugCodeContext2* pCodeContext,
   UINT64*             puCodeLocationId
);
```

```csharp
int GetCodeLocationId( 
   IDebugCodeContext2 pCodeContext,
   out ulong          puCodeLocationId
);
```

## <a name="parameters"></a>パラメーター
`pCodeContext`\
から識別子に変換される [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) オブジェクト。

`puCodeLocationId` 入出力コードの場所の識別子を返します。 「解説」を参照してください。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 `E_CODE_CONTEXT_OUT_OF_SCOPE`コードコンテキストが有効であってもスコープ外にある場合は、を返します。

## <a name="remarks"></a>解説
 コードの場所の識別子は、逆アセンブリをサポートするデバッグエンジン (DE) に固有です。 この場所識別子は、コード内の位置を追跡するために、DE によって内部的に使用されます。通常は、何らかの種類のアドレスまたはオフセットです。 唯一の要件は、ある場所のコードコンテキストが別の場所のコードコンテキストよりも小さい場合、最初のコードコンテキストの対応するコードの場所の識別子も、2番目のコードコンテキストのコードの場所の識別子よりも小さくなければならないということです。

 コードの場所の識別子のコードコンテキストを取得するには、 [GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md) メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md)
