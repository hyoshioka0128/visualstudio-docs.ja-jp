---
title: マネージオブジェクトを取得します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugManagedObject::GetManagedObject
helpviewer_keywords:
- IDebugManagedObject::GetManagedObject method
ms.assetid: 6abe1402-6aad-41e6-8ec1-ae12d5945992
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b7080760b174c51d62c44cd2757944948e0104ca
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727742"
---
# <a name="idebugmanagedobjectgetmanagedobject"></a>IDebugManagedObject::GetManagedObject
マネージ オブジェクトを表すインターフェイスを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetManagedObject( 
   IUnknown** ppManagedObject
);
```

```cpp
int GetManagedObject(
   out object ppManagedObject
);
```

## <a name="parameters"></a>パラメーター
`ppManagedObject`\
[アウト]マネージ オブジェクトを表すインターフェイスを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドから返されるインターフェイスは、マネージ クラスによって実装されるインターフェイスに対してクエリを実行でき、メソッドを呼び出すことができます。

## <a name="see-also"></a>関連項目
- [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)
