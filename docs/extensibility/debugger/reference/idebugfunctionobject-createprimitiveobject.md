---
title: 'IDebugFunctionObject:: CreatePrimitiveObject |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreatePrimitiveObject
helpviewer_keywords:
- IDebugFunctionObject::CreatePrimitiveObject method
ms.assetid: 6e9dc8b6-b4e1-4abf-b6e0-e885910775bc
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 69ad4328d2ae94a23ebaa9fb4fd0aa0d2cff7c74
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99929986"
---
# <a name="idebugfunctionobjectcreateprimitiveobject"></a>IDebugFunctionObject::CreatePrimitiveObject
単純な整数などのプリミティブデータオブジェクトを作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT CreatePrimitiveObject( 
   OBJECT_TYPE    ot,
   IDebugObject** ppObject
);
```

```csharp
int CreatePrimitiveObject(
   enum_OBJECT_TYPE ot,
   out IDebugObject ppObject
);
```

## <a name="parameters"></a>パラメーター
`ot`\
から作成するプリミティブの種類を表す [OBJECT_TYPE](../../../extensibility/debugger/reference/object-type.md) 列挙体の値。

`ppObject`\
入出力新しく作成されたオブジェクトを表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) を返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)インターフェイスによって表される関数のパラメーターであるプリミティブオブジェクトを表すオブジェクトを作成するには、このメソッドを呼び出します。 たとえば、式の文字列が "myString (5)" の場合、このメソッドを使用して、整数5を表すオブジェクトを作成します。

## <a name="see-also"></a>関連項目
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
