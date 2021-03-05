---
description: オブジェクトとそのスコープ内またはコンテナー内の位置を記述する構造体を返します。
title: 'IDebugAddress:: GetAddress |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAddress::GetAddress
helpviewer_keywords:
- IDebugAddress:GetAddress method
ms.assetid: 2590387b-5d36-4116-9a75-737957b8898e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 52c52d12d8c357f4dbadeef673a3dc4474713ce9
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102145444"
---
# <a name="idebugaddressgetaddress"></a>IDebugAddress::GetAddress
オブジェクトとそのスコープ内またはコンテナー内の位置を記述する構造体を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetAddress (
   DEBUG_ADDRESS * pAddress
);
```

```csharp
int GetAddress(
   DEBUG_ADDRESS[] pAddress
);
```

## <a name="parameters"></a>パラメーター
`pAddress`\
[入力、出力]このメソッドによって格納される [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) 構造体。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)構造体がこのメソッドに渡され、その後、適切な情報が入力されます。 この情報の解釈方法は、返される情報の種類とシンボルハンドラー自体によって異なります。 詳細については、「 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) 」を参照してください。

## <a name="see-also"></a>関連項目
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
