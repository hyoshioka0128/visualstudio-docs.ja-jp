---
description: コンパイラによって内部的に生成されたものも含め、メソッドのすべてのローカル変数の列挙子を作成します。
title: 'IDebugMethodField:: EnumAllLocals |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumAllLocals
helpviewer_keywords:
- IDebugMethodField::EnumAllLocals method
ms.assetid: 0bc7cc13-2628-4bd8-8c06-4d2aa6755ea8
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 38f14ba2d520974b9f8f567c7840737ed2763080
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102172169"
---
# <a name="idebugmethodfieldenumalllocals"></a>IDebugMethodField::EnumAllLocals
コンパイラによって内部的に生成されたものも含め、メソッドのすべてのローカル変数の列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumAllLocals( 
   IDebugAddress*     pAddress,
   IEnumDebugFields** ppLocals
);
```

```csharp
int EnumAllLocals(
   IDebugAddress        pAddress,
   out IEnumDebugFields ppLocals
);
```

## <a name="parameters"></a>パラメーター
`pAddress`\
から特定のスコープまたはコンテキストを指すメソッド内のデバッグアドレスを表す [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) オブジェクト。

`ppLocals`\
入出力指定されたスコープ内のすべてのローカルのリストを表す [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) オブジェクトを返します。それ以外の場合、は、ローカルがないことを示す null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合、は S_OK を返します。ローカルがない場合は S_FALSE を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 指定されたデバッグアドレスを含むブロック内で定義されている変数のみが列挙されます。 このメソッドには、コンパイラによって生成されるローカル変数が含まれます。 必要なものがすべてソースで明示的に定義されている場合は、 [enumlocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md) メソッドを呼び出します。

 メソッドには、複数のスコープコンテキストまたはブロックを含めることができます。

## <a name="see-also"></a>関連項目
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)
