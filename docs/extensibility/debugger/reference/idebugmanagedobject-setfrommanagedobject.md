---
title: 'IDebugManagedObject:: SetFromManagedObject |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugManagedObject::SetFromManagedObject
helpviewer_keywords:
- IDebugManagedObject::SetFromManagedObject method
ms.assetid: 8700ee8d-2704-4580-bccc-046837a24edd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4056befa0b5b053d480983901b24feb6b25cf538
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80727699"
---
# <a name="idebugmanagedobjectsetfrommanagedobject"></a>IDebugManagedObject::SetFromManagedObject
パラメーターとして指定された値クラスのインスタンスから、値クラスオブジェクトのインスタンスの値を設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetFromManagedObject( 
   IUnknown* pManagedObject
);
```

```csharp
int SetFromManagedObject(
   object pManagedObject
);
```

## <a name="parameters"></a>パラメーター
`pManagedObject`\
から新しい値を格納しているマネージオブジェクトを表すインターフェイス。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドは、 [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md) オブジェクトによって表されるマネージオブジェクトを変更するために使用されます。

## <a name="see-also"></a>関連項目
- [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)
