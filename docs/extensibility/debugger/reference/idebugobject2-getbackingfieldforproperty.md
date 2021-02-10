---
title: 'IDebugObject2:: GetBackingFieldForProperty |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::GetBackingFieldForProperty
helpviewer_keywords:
- IDebugObject2::GetBackingFieldForProperty method
ms.assetid: e72c6338-5573-4fad-8075-f3ade3435424
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f502479d4c74eb0b5cfa71db52698121830e66e6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99953475"
---
# <a name="idebugobject2getbackingfieldforproperty"></a>IDebugObject2::GetBackingFieldForProperty
このオブジェクトによって表されるプロパティをバッキングしている可能性のあるフィールドまたは変数 (存在する場合) を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetBackingFieldForProperty(
   IDebugObject2** ppObject
);
```

```csharp
int GetBackingFieldForProperty(
   out IDebugObject2 ppObject
);
```

## <a name="parameters"></a>パラメーター
`ppObject`\
入出力バッキングフィールドを記述する [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md) オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)オブジェクトは、マネージコードクラスのプロパティ、つまり get アクセサーまたは set アクセサーを持つメソッドを表します。 通常、このようなプロパティには、プロパティによって操作される値を格納する変数が必要です。 この変数はバッキングフィールドと呼ばれます。 オブジェクトのバッキングフィールドがない場合は、null 値が返されることを確認します。一部の呼び出し元では、戻り値には注意が払われず、では null 値が返されたかどうかが確認され `ppObject` ます。

## <a name="see-also"></a>関連項目
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
