---
title: オブジェクトの取得マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::GetManagedDebugObject
helpviewer_keywords:
- IDebugObject::GetManagedDebugObject method
ms.assetid: cb89692e-7657-47ff-846d-311943521951
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 67d0d7a8642c9dd90067b0e197f420d4cc821faa
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726687"
---
# <a name="idebugobjectgetmanageddebugobject"></a>IDebugObject::GetManagedDebugObject
デバッグ エンジンのアドレス空間にマネージ オブジェクトのコピーを作成します。

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
[アウト]新しく作成された[マネージ オブジェクト](../../../extensibility/debugger/reference/idebugmanagedobject.md)を表すオブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。 この[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)がマネージ値クラスのインスタンスを表していない場合は、E_FAILを返します。

## <a name="remarks"></a>Remarks
 この[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)オブジェクトは、インスタンスなどのマネージ値クラスのインスタンス`System.Decimal`を表す必要があります。 ローカル コピーを作成することで[、Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)を呼び出すオーバーヘッドがなくなります。

## <a name="see-also"></a>関連項目
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)
