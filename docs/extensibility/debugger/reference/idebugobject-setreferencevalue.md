---
description: このオブジェクトの参照値を設定します。
title: 'IDebugObject:: SetReferenceValue |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::SetReferenceValue
helpviewer_keywords:
- IDebugObject::SetReferenceValue method
ms.assetid: 08c78a4e-98eb-41cb-8b75-02a6a43d49f7
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bb376e4399157f9f9fe393086cca8fcf94c3b9de
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102161425"
---
# <a name="idebugobjectsetreferencevalue"></a>IDebugObject::SetReferenceValue
このオブジェクトの参照値を設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetReferenceValue( 
   IDebugObject* pObject
);
```

```csharp
int SetReferenceValue(
   [In] IDebugObject pObject
);
```

## <a name="parameters"></a>パラメーター
`pObject`\
から新しい参照値を表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドは、この [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトを、パラメーターに指定されたオブジェクトの値への参照として使用し `pObject` 、前の参照をすべて破棄します。 このオブジェクトは `IDebugObject` 、既に参照型である必要があることに注意してください。

## <a name="see-also"></a>関連項目
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)
