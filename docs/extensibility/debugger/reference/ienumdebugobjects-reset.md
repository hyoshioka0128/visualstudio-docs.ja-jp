---
title: 'IEnumDebugObjects:: Reset |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugObjects::Reset
helpviewer_keywords:
- IEnumDebugObjects::Reset method
ms.assetid: 4a245e47-cc39-4177-b83d-083ea0e3190f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9302330ac67cba4a9a68cacb7bc8f91aff7ad3ba
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80716332"
---
# <a name="ienumdebugobjectsreset"></a>IEnumDebugObjects::Reset
このメソッドは、列挙体を最初の要素にリセットします。

## <a name="syntax"></a>構文

```cpp
HRESULT Reset(void);
```

```csharp
int Reset();
```

## <a name="parameters"></a>パラメーター
 None

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドが呼び出された後、next を呼び出すと、列挙体の最初の要素が返さ[れます。](../../../extensibility/debugger/reference/ienumdebugobjects-next.md)

## <a name="see-also"></a>関連項目
- [IEnumDebugObjects](../../../extensibility/debugger/reference/ienumdebugobjects.md)
- [次へ](../../../extensibility/debugger/reference/ienumdebugobjects-next.md)
