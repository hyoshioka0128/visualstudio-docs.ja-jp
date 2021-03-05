---
description: 列挙シーケンス内の指定された数のカスタム属性をスキップします。
title: 'IEnumDebugCustomAttributes:: Skip |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumCustomAttributes::Skip
helpviewer_keywords:
- IEnumDebugCustomAttributes::Skip
ms.assetid: 54c72e23-cd4c-4746-935c-abea8057dd1b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c57ca47b8d5100ff9c9bf7451e07ad0924775475
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102226801"
---
# <a name="ienumdebugcustomattributesskip"></a>IEnumDebugCustomAttributes::Skip
列挙シーケンス内の指定された数のカスタム属性をスキップします。

## <a name="syntax"></a>構文

```cpp
HRESULT Skip ( 
   ULONG celt
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

## <a name="remarks"></a>解説
 が、 `celt` 残りの要素の数よりも大きい値を指定した場合、列挙は終了に設定され、 `S_FALSE` が返されます。

## <a name="see-also"></a>関連項目
- [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)
