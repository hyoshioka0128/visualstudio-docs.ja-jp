---
title: 'IDebugFunctionObject:: CreateArrayObject |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreateArrayObject
helpviewer_keywords:
- IDebugFunctionObject::CreateArrayObject method
ms.assetid: a380e53c-15f1-401f-927f-f366eea789e6
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 44d60c2f0573bf60d827737b2a54ff16b49d610c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99930004"
---
# <a name="idebugfunctionobjectcreatearrayobject"></a>IDebugFunctionObject::CreateArrayObject
配列オブジェクトを作成します。 この配列には、プリミティブまたはオブジェクトのインスタンス値を含めることができます。

## <a name="syntax"></a>構文

```cpp
HRESULT CreateArrayObject( 
   OBJECT_TYPE    ot,
   IDebugField*   pClassField,
   DWORD          dwRank,
   DWORD          dwDims[],
   DWORD          dwLowBounds[],
   IDebugObject** ppObject
);
```

```csharp
int CreateArrayObject(
   enum_OBJECT_TYPE ot,
   IDebugField      pClassField,
   uint             dwRank,
   uint[]           dwDims,
   uint[]           dwLowBounds,
   out IDebugObject ppObject
);
```

## <a name="parameters"></a>パラメーター
`ot`\
から新しい配列オブジェクトの型を示す [OBJECT_TYPE](../../../extensibility/debugger/reference/object-type.md) 列挙体の値を指定します。

`pClassField`\
からオブジェクトインスタンス値の配列を作成する場合は、オブジェクトのクラスを表す [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクト。 プリミティブオブジェクトの配列を作成する場合、このパラメーターは null 値になります。

`dwRank`\
から配列の次元のランクまたは数。

`dwDims`\
から配列の各次元のサイズ。

`dwLowBounds`\
から各次元の原点 (通常は0または 1)。

`ppObject`\
入出力新しく作成された配列を表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトを返します。 これは、実際には [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md) オブジェクトです。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)インターフェイスによって表される関数に対する配列パラメーターを表すオブジェクトを作成するには、このメソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
