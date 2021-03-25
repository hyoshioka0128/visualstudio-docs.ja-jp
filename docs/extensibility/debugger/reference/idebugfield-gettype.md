---
description: このメソッドは、フィールドの型を取得します。
title: 'IDebugField:: GetType |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetType
helpviewer_keywords:
- IDebugField::GetType method
ms.assetid: b3cdec9f-ef7b-44d0-a775-d17ef7eae968
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fe4873286cebcb48d085a173d6be04d5123df80d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076954"
---
# <a name="idebugfieldgettype"></a>IDebugField::GetType
このメソッドは、フィールドの型を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetType( 
   IDebugField** ppType
);
```

```csharp
int GetType(
   out IDebugField ppType
);
```

## <a name="parameters"></a>パラメーター
`ppType`\
入出力フィールド型を別の [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトとして返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
