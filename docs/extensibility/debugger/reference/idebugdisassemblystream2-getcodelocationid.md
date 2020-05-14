---
title: を使用します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::GetCodeLocationId
helpviewer_keywords:
- IDebugDisassemblyStream2::GetCodeLocationId
ms.assetid: 567adfb8-2f54-499a-a027-e4ecb82277ef
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 32be70e11776177a0e68f09689c2262497703ab1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732256"
---
# <a name="idebugdisassemblystream2getcodelocationid"></a>IDebugDisassemblyStream2::GetCodeLocationId
特定のコード コンテキストのコードの場所識別子を返します。

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
[in]識別子に変換される[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)オブジェクト。

`puCodeLocationId`[アウト]コードの場所の識別子を返します。 「解説」を参照してください。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。 コード`E_CODE_CONTEXT_OUT_OF_SCOPE`コンテキストが有効であるがスコープ外である場合に返します。

## <a name="remarks"></a>Remarks
 コードの場所の識別子は、逆アセンブルをサポートするデバッグ エンジン (DE) に固有です。 この場所識別子は、コード内の位置を追跡するために DE によって内部的に使用され、通常はアドレスまたは何らかのオフセットです。 唯一の要件は、ある場所のコード コンテキストが別の場所のコード コンテキストよりも小さい場合、最初のコード コンテキストの対応するコードの場所識別子も、2 番目のコード コンテキストのコードの場所識別子よりも小さくする必要があります。

 コードの場所の識別子のコード コンテキストを取得するには、呼び出します、 [GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md)メソッドです。

## <a name="see-also"></a>関連項目
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md)
