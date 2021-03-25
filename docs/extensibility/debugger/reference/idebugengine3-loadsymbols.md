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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 43651baac29b3904b9bc12d8d4b965ca1cd8e3ee
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066180"
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

## <a name="remarks"></a>注釈
 これにより、このデバッグエンジンによって参照されるすべてのモジュールのデバッグシンボルが読み込まれます。 シンボルは、まだ読み込まれていない場合にのみ読み込まれます。 [Setsymbols path](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)への呼び出しによって設定されたパスでシンボルが検索されます。

## <a name="see-also"></a>こちらもご覧ください
- [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
