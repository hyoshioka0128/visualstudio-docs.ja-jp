---
title: 'IDebugEnumField:: GetUnderlyingSymbol |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField::GetUnderlyingSymbol
helpviewer_keywords:
- IDebugEnumField::GetUnderlyingSymbol method
ms.assetid: c3b8a117-6708-4cfd-8ffc-5f007d706bc5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 14cac9d3f761e95b821179137f2efc23ef61b91b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80730274"
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

## <a name="remarks"></a>解説
 列挙体の名前には、 [Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)を使用してメモリ位置にバインドされる列挙型も含まれます。

## <a name="see-also"></a>関連項目
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)
