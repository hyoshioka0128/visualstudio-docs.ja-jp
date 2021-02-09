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
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 731b13b823fd1ad1666d3578c7f0475c2e00b789
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99929733"
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
