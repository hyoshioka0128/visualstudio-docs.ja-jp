---
description: このオブジェクトが読み取り専用かどうかを判断します。
title: 'IDebugObject:: IsReadOnly |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::IsReadOnly
helpviewer_keywords:
- IDebugObject::IsReadOnly method
ms.assetid: c460f772-d08a-4b36-81f3-dff6a51a93fd
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d99cf51ba5415631b2e8e66c36b459297a8fcb6e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102161479"
---
# <a name="idebugobjectisreadonly"></a>IDebugObject::IsReadOnly
このオブジェクトが読み取り専用かどうかを判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT IsReadOnly( 
   BOOL* pfIsReadOnly
);
```

```csharp
int IsReadOnly(
   out int pfIsReadOnly
);
```

## <a name="parameters"></a>パラメーター
`pfIsReadOnly`\
入出力`TRUE`このオブジェクトが読み取り専用の場合は0以外 () を返します。それ以外の場合は 0 () を返し `FALSE` ます。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 読み取り専用オブジェクトの値は、作成後に変更することはできません。

## <a name="see-also"></a>関連項目
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
