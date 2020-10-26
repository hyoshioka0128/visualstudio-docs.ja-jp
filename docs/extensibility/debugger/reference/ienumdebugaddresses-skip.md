---
title: 'IEnumDebugAddresses:: Skip |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugAddresses::Skip
helpviewer_keywords:
- IEnumDebugAddresses::Skip method
ms.assetid: ed9a8e71-30ef-414b-9da5-c9a2a251b84e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b4803b447ba049fd934d60a41adb5403335029a9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80717594"
---
# <a name="ienumdebugaddressesskip"></a>IEnumDebugAddresses::Skip
このメソッドは、指定された数の要素をスキップします。

## <a name="syntax"></a>構文

```cpp
HRESULT Skip(
   [in] ULONG celt
);
```

```csharp
int Skip(
   uint celt
);
```

## <a name="parameters"></a>パラメーター
`celt`\
からスキップする要素の数。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 `S_FALSE` `celt` が残りの要素の数より大きい場合はを返します。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 が、 `celt` 残りの要素の数よりも大きい値を指定した場合、列挙は終了に設定され、 `S_FALSE` が返されます。

## <a name="see-also"></a>関連項目
- [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)
