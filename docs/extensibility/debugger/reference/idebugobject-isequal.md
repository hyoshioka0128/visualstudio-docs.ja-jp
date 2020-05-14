---
title: オブジェクト::IsEqual |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::IsEqual
helpviewer_keywords:
- IDebugObject::IsEqual method
ms.assetid: 4b76e663-ef2e-41ff-9be1-bf26d666a34a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 13018e31fb5f8bed89a0a290d687360a605a855d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726502"
---
# <a name="idebugobjectisequal"></a>IDebugObject::IsEqual
オブジェクトをこのオブジェクトと比較します。

## <a name="syntax"></a>構文

```cpp
HRESULT IsEqual( 
   IDebugObject* pObject,
   BOOL*         pfIsEqual
);
```

```csharp
int IsEqual(
   IDebugObject pObject,
   out int      pfIsEqual
);
```

## <a name="parameters"></a>パラメーター
`pObject`\
[in]比較対象のオブジェクトを表す[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)オブジェクト。

`pfIsEqual`\
[アウト]オブジェクトの値が等`TRUE`しい場合は、ゼロ以外の値 ( ) を返します。それ以外の場合は`FALSE`、ゼロ ( ) を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 通常、このメソッドは、パラメーターとこの[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) `pObject`オブジェクトによって表される値のアドレスを比較できます。アドレスが等しい場合、オブジェクトは等しいと見なすことができます。

## <a name="see-also"></a>関連項目
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
