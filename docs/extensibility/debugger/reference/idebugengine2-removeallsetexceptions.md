---
description: IDE が特定のランタイムアーキテクチャまたは言語に対して設定した例外の一覧を削除します。
title: 'IDebugEngine2:: RemoveAllSetExceptions |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::RemoveAllSetExceptions
helpviewer_keywords:
- IDebugEngine2::RemoveAllSetExceptions
ms.assetid: 165fbe89-802d-4d99-85ca-c10fd6cccc09
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b40da7391fc360b68da70f02f4d32afb92e83a58
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087939"
---
# <a name="idebugengine2removeallsetexceptions"></a>IDebugEngine2::RemoveAllSetExceptions
IDE が特定のランタイムアーキテクチャまたは言語に対して設定した例外の一覧を削除します。

## <a name="syntax"></a>構文

```cpp
HRESULT RemoveAllSetExceptions( 
   REFGUID guidType
);
```

```csharp
int RemoveAllSetExceptions( 
   ref Guid guidType
);
```

## <a name="parameters"></a>パラメーター
`guidType`\
から言語の GUID、または実行時アーキテクチャに固有のデバッグエンジンの GUID のいずれかです。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドによって削除された例外は、 [Setexception](../../../extensibility/debugger/reference/idebugengine2-setexception.md) メソッドの以前の呼び出しによって設定されています。

 特定の例外を削除するには、 [Removesetexception](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md) メソッドを呼び出します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)
