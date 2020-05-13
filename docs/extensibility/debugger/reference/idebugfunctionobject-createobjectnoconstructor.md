---
title: オブジェクトを作成します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreateObjectNoConstructor
helpviewer_keywords:
- IDebugFunctionObject::CreateObjectNoConstructor method
ms.assetid: 4e2bd6d5-f4bd-4c10-a998-3db451c9a0c8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ad95f9273276830b59ebc77214f3920a687d41ed
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728573"
---
# <a name="idebugfunctionobjectcreateobjectnoconstructor"></a>IDebugFunctionObject::CreateObjectNoConstructor
コンストラクターを持たないオブジェクトを作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT CreateObjectNoConstructor( 
   IDebugField*   pClassObject,
   IDebugObject** ppObject
);
```

```csharp
int CreateObjectNoConstructor(
   IDebugField      pClassField,
   out IDebugObject ppObject
);
```

## <a name="parameters"></a>パラメーター
`pClassObject`\
[in]作成するオブジェクトの型を表す[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)オブジェクト。

`ppObject`\
[アウト]新しく作成されたオブジェクトを表す[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドを呼び出して、構造体または複合型のインスタンスを表すオブジェクトを作成します (コンストラクターを必要としない) [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)インターフェイスによって表される関数へのパラメーターです。

 オブジェクト パラメーターにコンストラクターが必要な場合は[、CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject-createobject.md)メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
- [CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject-createobject.md)
