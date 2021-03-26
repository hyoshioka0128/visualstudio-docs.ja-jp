---
description: このメソッドは、addresses 列挙体を最初の要素にリセットします。
title: 'IEnumDebugAddresses:: Reset |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugAddresses::Reset
helpviewer_keywords:
- IEnumDebugAddresses::Reset method
ms.assetid: 3a9d7f20-5bc6-4e13-8e91-5af4092e092f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 385e650e908947288eafa6f3f2812db45f9721a3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083142"
---
# <a name="ienumdebugaddressesreset"></a>IEnumDebugAddresses::Reset
このメソッドは、列挙体を最初の要素にリセットします。

## <a name="syntax"></a>構文

```cpp
HRESULT Reset(void);
```

```csharp
int Reset();
```

## <a name="parameters"></a>パラメーター
 なし

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドが呼び出された後、next を呼び出すと、列挙体の最初の要素が返さ[れます。](../../../extensibility/debugger/reference/ienumdebugaddresses-next.md)

## <a name="see-also"></a>こちらもご覧ください
- [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)
- [次へ](../../../extensibility/debugger/reference/ienumdebugaddresses-next.md)
