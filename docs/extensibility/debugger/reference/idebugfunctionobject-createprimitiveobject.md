---
title: オブジェクトを作成します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreatePrimitiveObject
helpviewer_keywords:
- IDebugFunctionObject::CreatePrimitiveObject method
ms.assetid: 6e9dc8b6-b4e1-4abf-b6e0-e885910775bc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 24b26a072a3bebda2d01a89baaf2910de96e77d1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728531"
---
# <a name="idebugfunctionobjectcreateprimitiveobject"></a>IDebugFunctionObject::CreatePrimitiveObject
単純な整数などのプリミティブ データ オブジェクトを作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT CreatePrimitiveObject( 
   OBJECT_TYPE    ot,
   IDebugObject** ppObject
);
```

```csharp
int CreatePrimitiveObject(
   enum_OBJECT_TYPE ot,
   out IDebugObject ppObject
);
```

## <a name="parameters"></a>パラメーター
`ot`\
[in]作成するプリミティブの型を表す[OBJECT_TYPE](../../../extensibility/debugger/reference/object-type.md)列挙体の値。

`ppObject`\
[アウト]新しく作成されたオブジェクトを表す[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 [インターフェイス](../../../extensibility/debugger/reference/idebugfunctionobject.md)によって表される関数のパラメーターであるプリミティブ オブジェクトを表すオブジェクトを作成します。 たとえば、式の文字列が "myString(5)" の場合、このメソッドは整数 5 を表すオブジェクトを作成するために使用されます。

## <a name="see-also"></a>関連項目
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
