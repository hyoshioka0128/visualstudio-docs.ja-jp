---
description: このメソッドは、オブジェクトに関連付けられている例外を取得します (存在する場合)。
title: 'IDebugBinder3:: GetExceptionObjectAndType |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::GetExceptionObjectAndType
helpviewer_keywords:
- IDebugBinder3::GetExceptionObjectAndType method
ms.assetid: 2a313fe1-4ee1-4f01-af86-382d6c661a8f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 67f6c146182546f83782a0299c0ea3e29f94a3b2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094251"
---
# <a name="idebugbinder3getexceptionobjectandtype"></a>IDebugBinder3::GetExceptionObjectAndType
このメソッドは、オブジェクトに関連付けられている例外を取得します (存在する場合)。

## <a name="syntax"></a>構文

```cpp
HRESULT GetExceptionObjectAndType(
   IDebugObject** ppException,
   IDebugField**  ppField
);
```

```csharp
int GetExceptionObjectAndType(
   out IDebugObject ppException,
   out IDebugField  ppField
);
```

## <a name="parameters"></a>パラメーター
`ppException`\
入出力例外を表すオブジェクトを返します。

`ppField`\
入出力例外の原因と考えられる特定のフィールドを表すオブジェクトを返します (これは null 値でもかまいません)。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

> [!NOTE]
> 例外があるかどうかを確認するには、によって返される値を確認し `ppException` ます。 null 値の場合、このオブジェクトには例外が関連付けられていません。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
