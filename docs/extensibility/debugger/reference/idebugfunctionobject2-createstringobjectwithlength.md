---
description: 指定された長さの文字列オブジェクトを作成します。
title: 'IDebugFunctionObject2:: CreateStringObjectWithLength |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- CreateStringObjectWithLength
- IDebugFunctionObject2::CreateStringObjectWithLength
ms.assetid: 1f43ec66-1615-4a4c-8b9d-e933f549f96d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5314bf6d06f291ce7128b3b6ccebd520ef2eafca
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072833"
---
# <a name="idebugfunctionobject2createstringobjectwithlength"></a>IDebugFunctionObject2::CreateStringObjectWithLength
指定された長さの文字列オブジェクトを作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT CreateStringObjectWithLength (
   LPCOLESTR      pcstrString,
   UINT           uiLength,
   IDebugObject** ppObject
);
```

```csharp
int CreateStringObjectWithLength (
   string           pcstrString,
   uint             uiLength,
   out IDebugObject ppObject
);
```

## <a name="parameters"></a>パラメーター
`pcstrString`\
から文字列オブジェクトの文字列値。

`uiLength`\
から文字列の長さ (バイト単位)。

`ppObject`\
入出力新しく作成された文字列オブジェクトを表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)
