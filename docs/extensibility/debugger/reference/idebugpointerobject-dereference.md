---
description: ポイントされているオブジェクトを取得します。
title: IDebugPointerObject::D ereference |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerObject::Dereference
helpviewer_keywords:
- IDebugPointerObject::Dereference method
ms.assetid: 196ec2cc-8569-4780-b217-23b24e7f50ca
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e4aa96f726ec18e84aceba159fe9be6128456ce0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102169692"
---
# <a name="idebugpointerobjectdereference"></a>IDebugPointerObject::Dereference
ポイントされているオブジェクトを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT DeReference( 
   DWORD          dwIndex,
   IDebugObject** ppObject
);
```

```csharp
int Dereference(
   uint             dwIndex,
   out IDebugObject ppObject
);
```

## <a name="parameters"></a>パラメーター
`dwIndex`\
からが指すオブジェクトの先頭からの単純なバイトオフセット。

`ppObject`\
入出力が指すオブジェクトを表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクト、およびオフセットがある場合は、それを返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。 このオブジェクトが別のオブジェクトを指していない場合は E_FAIL を返します。

## <a name="remarks"></a>解説
 が指すオブジェクトは、プリミティブ型、またはクラスや構造体などのより複雑な型にすることができます。

## <a name="see-also"></a>関連項目
- [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)
