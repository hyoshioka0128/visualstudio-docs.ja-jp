---
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
ms.openlocfilehash: 4e7d27e6a437c46d2ee72eb4fd5f79eaa9e912ac
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99953631"
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
