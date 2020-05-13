---
title: オブジェクトを作成します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreateArrayObject
helpviewer_keywords:
- IDebugFunctionObject::CreateArrayObject method
ms.assetid: a380e53c-15f1-401f-927f-f366eea789e6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bd4c07f2b95ff3077de79d4bc63f4fad19b0c6fa
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728607"
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
[in]新しい配列オブジェクトの型を示す[OBJECT_TYPE](../../../extensibility/debugger/reference/object-type.md)列挙体の値を指定します。

`pClassField`\
[in]オブジェクト インスタンス値の配列を作成する場合は、オブジェクトのクラスを表す[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)オブジェクト。 プリミティブオブジェクトの配列を作成する場合、このパラメータは null 値です。

`dwRank`\
[in]配列のランクまたは次元数。

`dwDims`\
[in]配列の各次元のサイズ。

`dwLowBounds`\
[in]各次元の原点 (通常は 0 または 1)。

`ppObject`\
[アウト]新しく作成された配列を表す[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)オブジェクトを返します。 これは実際には[オブジェクトです](../../../extensibility/debugger/reference/idebugarrayobject.md)。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 [インターフェイス](../../../extensibility/debugger/reference/idebugfunctionobject.md)によって表される関数の配列パラメーターを表すオブジェクトを作成します。

## <a name="see-also"></a>関連項目
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
