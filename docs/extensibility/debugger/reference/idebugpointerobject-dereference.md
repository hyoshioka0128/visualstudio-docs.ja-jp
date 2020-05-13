---
title: オブジェクトを:Dします。マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725564"
---
# <a name="idebugpointerobjectdereference"></a>IDebugPointerObject::Dereference
指すオブジェクトを取得します。

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
[in]指すオブジェクトの先頭からの単純なバイト オフセット。

`ppObject`\
[アウト]指し付けられたオブジェクトにオフセットを加えた場合は[、IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。 このオブジェクトが別のオブジェクトを指していない場合は、E_FAILを返します。

## <a name="remarks"></a>Remarks
 参照先のオブジェクトは、プリミティブまたはクラスや構造体などのより複雑な型にすることができます。

## <a name="see-also"></a>関連項目
- [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)
