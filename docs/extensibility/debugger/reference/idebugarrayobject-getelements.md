---
title: を返すオブジェクト::取得要素 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetElements
helpviewer_keywords:
- IDebugArrayObject::GetElements method
ms.assetid: f6a6262f-5183-46ce-8a45-33ef46088b98
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: be06acbef93d8858557fea5bd7563168be2d28aa
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736241"
---
# <a name="idebugarrayobjectgetelements"></a>IDebugArrayObject::GetElements
配列のすべての要素の列挙子を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetElements( 
   IEnumDebugObjects** ppEnum
);
```

```csharp
int GetElements(
   out IEnumDebugObjects ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\
[アウト]すべての要素[を列挙](../../../extensibility/debugger/reference/ienumdebugobjects.md)できるオブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 代わりに[、GetCount](../../../extensibility/debugger/reference/idebugarrayobject-getcount.md)メソッドと[GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)メソッドを使用して、要素を反復処理します。

## <a name="see-also"></a>関連項目
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
