---
description: このメソッドは、列挙体の名前を表す IDebugField を返します。
title: 'IDebugEnumField:: GetUnderlyingSymbol |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField::GetUnderlyingSymbol
helpviewer_keywords:
- IDebugEnumField::GetUnderlyingSymbol method
ms.assetid: c3b8a117-6708-4cfd-8ffc-5f007d706bc5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9343c1b0908c6b132ea982a46623b8c1cf20efc9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092567"
---
# <a name="idebugenumfieldgetunderlyingsymbol"></a>IDebugEnumField::GetUnderlyingSymbol
このメソッドは、列挙体の名前を表す [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetUnderlyingSymbol(
   IDebugField** ppField
);
```

```csharp
int GetUnderlyingSymbol(
   out IDebugField ppField
);
```

## <a name="parameters"></a>パラメーター
`ppField`\
入出力この列挙体の名前を記述する [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 列挙体の名前には、 [Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)を使用してメモリ位置にバインドされる列挙型も含まれます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [束縛](../../../extensibility/debugger/reference/idebugbinder-bind.md)
