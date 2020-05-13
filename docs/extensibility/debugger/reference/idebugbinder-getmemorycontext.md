---
title: バインダーを使用します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder::GetMemoryContext
helpviewer_keywords:
- IDebugBinder::GetMemoryContext method
ms.assetid: 801c5b60-acff-4822-b23d-e9c7bbca8a0f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8d50126e26b836f7b53ee1abeb5c4988b74a2eed
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735998"
---
# <a name="idebugbindergetmemorycontext"></a>IDebugBinder::GetMemoryContext
このメソッドは、オブジェクトの場所またはメモリ アドレスをメモリ コンテキストに変換します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetMemoryContext( 
   IDebugField*           pField,
   DWORD                  dwConstant,
   IDebugMemoryContext2** ppMemCxt
);
```

```csharp
int GetMemoryContext(
   IDebugField              pField,
   uint                     dwConstant,
   out IDebugMemoryContext2 ppMemCxt
);
```

## <a name="parameters"></a>パラメーター
`pField`\
[in]検索するオブジェクトを記述する[IDebug フィールド](../../../extensibility/debugger/reference/idebugfield.md)。 の`NULL`場合は、`dwConstant`代わりにを使用します。

`dwConstant`\
[in]0x5000 などの定数メモリ アドレス。

`ppMemCxt`\
[アウト]オブジェクトのアドレスまたはメモリ内のアドレスを表す[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)インターフェイスを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
