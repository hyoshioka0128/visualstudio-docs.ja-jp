---
description: 配列の要素を取得します。
title: 'IDebugArrayObject:: GetElement |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetElement
helpviewer_keywords:
- IDebugArrayObject::GetElement method
ms.assetid: 08b44341-7bf1-4a8c-8b79-98ae5785b195
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ea10afac9f5503288d257833d6dd59f9ba56fc6f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158658"
---
# <a name="idebugarrayobjectgetelement"></a>IDebugArrayObject::GetElement
配列の要素を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetElement( 
   DWORD          dwIndex,
   IDebugObject** ppElement
);
```

```csharp
int GetElement(
   [In] uint dwIndex,
   out IDebugObject ppElement
);
```

## <a name="parameters"></a>パラメーター
`dwIndex`\
から要素のインデックス。

`ppElement`\
入出力要素を表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) インターフェイスを返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドは、配列オブジェクトが多次元であっても、配列オブジェクトのすべての要素を1次元配列として表示します。 たとえば、配列とパラメーター20が指定されている場合、 `myarray[3][2][6]` `dwIndex` このメソッドはから要素を返し、 `myarray[1][1][2]` `dwIndex` パラメーター21はから要素を返し `myarray[1][1][3]` ます。 [GetCount](../../../extensibility/debugger/reference/idebugarrayobject-getcount.md)メソッドを使用して、配列内の要素の合計数を確認します。

## <a name="see-also"></a>関連項目
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
