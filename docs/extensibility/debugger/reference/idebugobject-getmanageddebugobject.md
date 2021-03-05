---
description: デバッグエンジンのアドレス空間にマネージオブジェクトのコピーを作成します。
title: 'IDebugObject:: GetManagedDebugObject |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::GetManagedDebugObject
helpviewer_keywords:
- IDebugObject::GetManagedDebugObject method
ms.assetid: cb89692e-7657-47ff-846d-311943521951
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 87956b3630f9d152ecdda7754623e7257cf0a01a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102164768"
---
# <a name="idebugobjectgetmanageddebugobject"></a>IDebugObject::GetManagedDebugObject
デバッグエンジンのアドレス空間にマネージオブジェクトのコピーを作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetManagedDebugObject( 
   IDebugManagedObject** ppObject
);
```

```csharp
int GetManagedDebugObject(
   out IDebugManagedObject ppObject
);
```

## <a name="parameters"></a>パラメーター
`ppObject`\
入出力新しく作成されたマネージオブジェクトを表す [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。 この [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) がマネージ値クラスのインスタンスを表していない場合は E_FAIL を返します。

## <a name="remarks"></a>解説
 この [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトは、インスタンスなどのマネージ値クラスのインスタンスを表す必要があり `System.Decimal` ます。 ローカルコピーを用意することで、 [Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md) 呼び出しのオーバーヘッドが解消されます。

## <a name="see-also"></a>関連項目
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)
