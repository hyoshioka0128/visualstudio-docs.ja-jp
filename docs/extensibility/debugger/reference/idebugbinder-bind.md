---
description: このメソッドは、シンボルの現在の値を格納しているメモリコンテキストまたはオブジェクトを取得します。
title: 'IDebugBinder:: Bind |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder::Bind
helpviewer_keywords:
- IDebugBinder::Bind method
ms.assetid: 15a11ad7-0fcc-4e80-ae34-8a7dd7bae3c3
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c373fbdae030de30544c67c1509eb812b746b7f1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143660"
---
# <a name="idebugbinderbind"></a>IDebugBinder::Bind
このメソッドは、シンボルの現在の値を格納しているメモリコンテキストまたはオブジェクトを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT Bind( 
   IDebugObject*  pContainer,
   IDebugField*   pField,
   IDebugObject** ppObject
);
```

```csharp
int Bind(
   IDebugObject     pContainer,
   IDebugField      pField,
   out IDebugObject ppObject
);
```

## <a name="parameters"></a>パラメーター
`pContainer`\
からによって参照される子を含む [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) `pField` 。

`pField`\
から記号を表す [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 。

`ppObject`\
入出力 `IDebugObject` シンボルのインスタンスを表すを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
