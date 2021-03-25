---
description: 指定されたコードの場所の識別子に対応するコードコンテキストオブジェクトを返します。
title: 'IDebugDisassemblyStream2:: GetCodeContext |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::GetCodeContext
helpviewer_keywords:
- IDebugDisassemblyStream2::GetCodeContext
ms.assetid: a6d0ae82-7617-4915-9713-369abe3e2e53
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c532c68435d1eaabdb03f8acae571ac4b71a5a7b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067076"
---
# <a name="idebugdisassemblystream2getcodecontext"></a>IDebugDisassemblyStream2::GetCodeContext
指定されたコードの場所の識別子に対応するコードコンテキストオブジェクトを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCodeContext( 
   UINT64               uCodeLocationId,
   IDebugCodeContext2** ppCodeContext
);
```

```csharp
int GetCodeContext( 
   ulong                  uCodeLocationId,
   out IDebugCodeContext2 ppCodeContext
);
```

## <a name="parameters"></a>パラメーター
`uCodeLocationId`\
からコードの場所の識別子を指定します。 コードの場所の識別子の説明については、「 [Getcodelocationid](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md) メソッド」の「解説」を参照してください。

`ppCodeContext`\
入出力関連付けられているコードコンテキストを表す [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 コードの場所の識別子は、 [Getcurrentlocation](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcurrentlocation.md) メソッドの呼び出しから返され、 [disassemblydata](../../../extensibility/debugger/reference/disassemblydata.md) 構造に含めることができます。

 コードコンテキストをコードロケーション識別子に変換するには、 [Getcodelocationid](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md) メソッドを呼び出します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)
- [GetCurrentLocation](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcurrentlocation.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
