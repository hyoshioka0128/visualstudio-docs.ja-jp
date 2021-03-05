---
description: このメソッドは、このオブジェクトに関連付けられている引数の型のリストを取得します。
title: 'IDebugBinder3:: GetTypeArguments |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::GetTypeArguments
helpviewer_keywords:
- IDebugBinder3::GetTypeArguments method
ms.assetid: fa0c37a7-327f-463e-9a9d-bb3f534584cb
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 74cbd6e67a82113e43226ded8640630be50ba086
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102173898"
---
# <a name="idebugbinder3gettypearguments"></a>IDebugBinder3::GetTypeArguments
このメソッドは、このオブジェクトに関連付けられている引数の型のリストを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetTypeArguments(
   UINT          skip,
   UINT          count,
   IDebugField** ppFields,
   UINT*         pFetched
);
```

```csharp
int GetTypeArguments(
   uint          skip,
   uint          count,
   IDebugField[] ppFields,
   out uint      pFetched
);
```

## <a name="parameters"></a>パラメーター
`skip`\
から引数の型を取得する前にスキップするフィールドの数。

`count`\
から返される引数フィールドの数 (も配列のサイズを指定し `ppFields` ます)。

`ppFields`\
[入力、出力]このメソッドの戻り値として格納されるフィールドの配列。

`pFetched`\
[出力] \(省略可能) 実際に返された引数の型フィールドの数。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 引数の型の数は、 [Gettypeargumentcount](../../../extensibility/debugger/reference/idebugbinder3-gettypeargumentcount.md)で事前に取得できます。

## <a name="see-also"></a>関連項目
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
- [GetTypeArgumentCount](../../../extensibility/debugger/reference/idebugbinder3-gettypeargumentcount.md)
