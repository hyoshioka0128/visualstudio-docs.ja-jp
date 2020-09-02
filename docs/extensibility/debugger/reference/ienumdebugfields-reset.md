---
title: 'IEnumDebugFields:: Reset |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFields::Reset
helpviewer_keywords:
- IEnumDebugFields::Reset method
ms.assetid: 38ff61e4-0120-42e8-971a-16be6050b425
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: be33249ef583776f613c6716143249e3ce31bc8d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80716851"
---
# <a name="ienumdebugfieldsreset"></a>IEnumDebugFields::Reset
このメソッドは、列挙体を最初の要素にリセットします。

## <a name="syntax"></a>構文

```cpp
HRESULT Reset(void);
```

```csharp
int Reset();
```

#### <a name="parameters"></a>パラメーター
 None

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドが呼び出された後、next を呼び出すと、列挙体の最初の要素が返さ[れます。](../../../extensibility/debugger/reference/ienumdebugfields-next.md)

## <a name="see-also"></a>関連項目
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [次へ](../../../extensibility/debugger/reference/ienumdebugfields-next.md)
