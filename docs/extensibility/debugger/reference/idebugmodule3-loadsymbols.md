---
title: 'IDebugModule3:: LoadSymbols |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule3::LoadSymbols
helpviewer_keywords:
- IDebugModule3::LoadSymbols
ms.assetid: 7548c8c1-cbc6-48aa-a845-19058d4a85bb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4c61339305200acc9a6c572a1a96595dc4cb6f50
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80726780"
---
# <a name="idebugmodule3loadsymbols"></a>IDebugModule3::LoadSymbols
現在のモジュールのシンボルを読み込みます。

## <a name="syntax"></a>構文

```cpp
HRESULT LoadSymbols(
   void
);
```

```csharp
int LoadSymbols();
```

## <a name="return-value"></a>戻り値
 メソッドが成功した場合は `S_OK` を返します。 失敗した場合はエラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドは、現在の検索パスからシンボルを読み込みます ( [setsymbols path](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md) メソッドを呼び出すことによって変更できます)。

 このメソッドは、 [ReloadSymbols_Deprecated](../../../extensibility/debugger/reference/idebugmodule2-reloadsymbols-deprecated.md) メソッドよりも優先されます。

## <a name="see-also"></a>関連項目
- [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)
- [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)
