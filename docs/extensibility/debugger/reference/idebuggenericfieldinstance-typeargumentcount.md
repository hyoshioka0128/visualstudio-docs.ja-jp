---
description: このインスタンスの型パラメーター引数の数を返します。
title: 'IDebugGenericFieldInstance:: TypeArgumentCount |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- TypeArgumentCount
- IDebugGenericFieldInstance::TypeArgumentCount
ms.assetid: e662c5ea-a5c1-478e-a268-5980dadffcd1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c7afd914b3880ca1004a319a66b3f4176e15789e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072872"
---
# <a name="idebuggenericfieldinstancetypeargumentcount"></a>IDebugGenericFieldInstance::TypeArgumentCount
このインスタンスの型パラメーター引数の数を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT TypeArgumentCount(
   ULONG32* pcArgs
);
```

```csharp
int TypeArgumentCount(
   ref uint pcArgs
);
```

## <a name="parameters"></a>パラメーター
`pcArgs`\
[入力、出力]このインスタンスの型パラメーター引数の数。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 たとえば、List の場合、このメソッドは \<int> 1 を返します。リストの場合、 \<int,float2> このメソッドは2を返します。 型引数がない場合、このメソッドは0を返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugGenericFieldInstance](../../../extensibility/debugger/reference/idebuggenericfieldinstance.md)
