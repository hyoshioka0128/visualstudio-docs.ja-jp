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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 226e8471d83208e9647578fca0fa16cc7b49e4eb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087640"
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

## <a name="remarks"></a>注釈
 が指すオブジェクトは、プリミティブ型、またはクラスや構造体などのより複雑な型にすることができます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)
