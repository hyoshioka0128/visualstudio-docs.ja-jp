---
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
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fe87d5db40ce663d84c9561e89a84e6fcb1684ed
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80725564"
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
