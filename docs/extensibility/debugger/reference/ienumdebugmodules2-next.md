---
description: Modules 列挙体の次の要素セットを返します。
title: 'IEnumDebugModules2:: Next |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugModules2::Next
helpviewer_keywords:
- IEnumDebugModules2::Next
ms.assetid: 46b7ccad-b07b-4ec0-b3ce-13981ffab7e8
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a7c1d627579faea8bb4871feb310db79d6e5eea0
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102226398"
---
# <a name="ienumdebugmodules2next"></a>IEnumDebugModules2::Next
列挙体から次の要素のセットを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Next(
   ULONG           celt,
   IDebugModule2** rgelt,
   ULONG*          pceltFetched
);
```

```csharp
int Next(
   uint            celt,
   IDebugModule2[] rgelt,
   ref uint        pceltFetched
);
```

## <a name="parameters"></a>パラメーター
`celt`\
から取得する要素の数。 配列の最大サイズも指定し `rgelt` ます。

`rgelt`\
[入力、出力]入力する [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md) 要素の配列。

`pceltFetched`\
入出力で実際に返された要素の数を返し `rgelt` ます。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 要求された `S_FALSE` 数の要素を返すことができなかった場合は、を返します。それ以外の場合は、エラーコードを返します。

## <a name="see-also"></a>関連項目
- [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
