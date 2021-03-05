---
description: このデバッグエンジンによってデバッグされているすべてのモジュールのシンボルを (必要に応じて) 読み込みます。
title: 'IDebugEngine3:: LoadSymbols |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::LoadSymbols
helpviewer_keywords:
- IDebugEngine3::LoadSymbols
ms.assetid: c846a440-1d91-4d48-b8f1-82e902ae152b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f4b4f210ef07ad10b35251582dd8a3c0fe3b0685
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102153808"
---
# <a name="idebugengine3loadsymbols"></a>IDebugEngine3::LoadSymbols
このデバッグエンジンによってデバッグされているすべてのモジュールのシンボルを (必要に応じて) 読み込みます。

## <a name="syntax"></a>構文

```cpp
HRESULT LoadSymbols();
```

```csharp
int LoadSymbols();
```

## <a name="parameters"></a>パラメーター
 [なし] :

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 これにより、このデバッグエンジンによって参照されるすべてのモジュールのデバッグシンボルが読み込まれます。 シンボルは、まだ読み込まれていない場合にのみ読み込まれます。 [Setsymbols path](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)への呼び出しによって設定されたパスでシンボルが検索されます。

## <a name="see-also"></a>関連項目
- [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
