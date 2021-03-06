---
description: このメソッドは、fields 列挙から次の要素のセットを返します。
title: 'IEnumDebugFields:: Next |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFields::Next
helpviewer_keywords:
- IEnumDebugFields::Next method
ms.assetid: 22c177a2-af81-4234-812b-f9b47be245a2
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cb60dcf991c1a3002612b6779ef179c1571f3244
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102226658"
---
# <a name="ienumdebugfieldsnext"></a>IEnumDebugFields::Next
このメソッドは、列挙体から次の要素のセットを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Next(
   ULONG         celt,
   IDebugField** rgelt,
   ULONG*        pceltFetched
);
```

```csharp
int Next(
   uint          celt,
   IDebugField[] rgelt,
   ref uint      pceltFetched
);
```

## <a name="parameters"></a>パラメーター
`celt`\
から取得する要素の数。 配列の最大サイズも指定し `rgelt` ます。

`rgelt`\
[入力、出力]入力する [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 要素の配列。

`pceltFetched`\
入出力で実際に返された要素の数を返し `rgelt` ます。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 要求された `S_FALSE` 数の要素を返すことができなかった場合は、を返します。それ以外の場合は、エラーコードを返します。

## <a name="see-also"></a>関連項目
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
