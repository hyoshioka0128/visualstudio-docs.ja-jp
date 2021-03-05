---
description: カスタム属性がアタッチされているフィールドを取得します。
title: 'IDebugCustomAttribute:: GetParentField |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttribute::GetParentField
helpviewer_keywords:
- IDebugCustomAttribute::GetParentField
ms.assetid: bcdfdf37-bfcf-4988-a7b8-4c731d0af1b0
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a4af4569b64a41fc84a09c7e8f2ce0a8f6b42e86
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102154510"
---
# <a name="idebugcustomattributegetparentfield"></a>IDebugCustomAttribute::GetParentField
カスタム属性がアタッチされているフィールドを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetParentField( 
   IDebugField** ppField
);
```

```csharp
int GetParentField(
   out IDebugField ppField
);
```

## <a name="parameters"></a>パラメーター
`ppField`\
入出力カスタム属性がアタッチされているフィールドを表す [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 返された[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)オブジェクトに対して[getkind](../../../extensibility/debugger/reference/idebugfield-getkind.md)メソッドを呼び出し、親のフィールドの種類を判別します。

## <a name="see-also"></a>関連項目
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
