---
title: 'IDebugBinder3:: GetTypeArgumentCount |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::GetTypeArgumentCount
helpviewer_keywords:
- IDebugBinder3::GetTypeArgumentCount method
ms.assetid: caf68de6-6f7c-4efd-b803-121347a5032e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: db43ed4dc178cf5080822e2dc387b5faa4bc5cd1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80735714"
---
# <a name="idebugbinder3gettypeargumentcount"></a>IDebugBinder3::GetTypeArgumentCount
このメソッドは、このオブジェクトに関連付けられている引数の型の数を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetTypeArgumentCount(
   UINT* uCount
);
```

```csharp
int GetTypeArgumentCount(
   out uint uCount
);
```

## <a name="parameters"></a>パラメーター
`uCount`\
入出力このオブジェクトに関連付けられている引数の型の数。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドによって返される値を使用して、 [GetTypeArguments](../../../extensibility/debugger/reference/idebugbinder3-gettypearguments.md) メソッドで使用する配列を割り当てることができます。

## <a name="see-also"></a>関連項目
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
- [GetTypeArguments](../../../extensibility/debugger/reference/idebugbinder3-gettypearguments.md)
