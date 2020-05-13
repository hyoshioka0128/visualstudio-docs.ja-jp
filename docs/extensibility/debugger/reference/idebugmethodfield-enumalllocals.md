---
title: フィールド::列挙体のローカルマイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumAllLocals
helpviewer_keywords:
- IDebugMethodField::EnumAllLocals method
ms.assetid: 0bc7cc13-2628-4bd8-8c06-4d2aa6755ea8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 50da5af616c56276a0299a0d08e6eeb0b88181cc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727331"
---
# <a name="idebugmethodfieldenumalllocals"></a>IDebugMethodField::EnumAllLocals
コンパイラによって内部的に生成された変数を含め、メソッドのすべてのローカル変数の列挙子を作成します。

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
[in]特定のスコープまたはコンテキストを指すメソッド内のデバッグ アドレスを表す[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)オブジェクト。

`ppLocals`\
[アウト]指定した[スコープ](../../../extensibility/debugger/reference/ienumdebugfields.md)内のすべてのローカルのリストを表すオブジェクトを返します。それ以外の場合は、ローカルを示さないことを示す null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OKを返すか、ローカルがない場合はS_FALSEを返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>Remarks
 指定されたデバッグ アドレスを含むブロック内で定義されている変数のみが列挙されます。 このメソッドには、コンパイラによって生成されたローカルが含まれます。 必要なのがソースで明示的に定義されたローカルである場合は[、EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)メソッドを呼び出します。

 メソッドには、複数のスコープ コンテキストまたはブロックを含めることができます。

## <a name="see-also"></a>関連項目
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)
