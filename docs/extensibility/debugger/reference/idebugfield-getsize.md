---
description: このメソッドは、フィールドのサイズ (バイト単位) を取得します。
title: 'IDebugField:: GetSize |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetSize
helpviewer_keywords:
- IDebugField::GetSize method
ms.assetid: 73329924-3751-4f44-af54-5986b7943374
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 471b6dce3c4795f8059e64aff5e7522b3ba91842
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077032"
---
# <a name="idebugfieldgetsize"></a>IDebugField::GetSize
このメソッドは、フィールドのサイズ (バイト単位) を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetSize( 
   DWORD* pdwSize
);
```

```csharp
int GetSize(
   out uint pdwSize
);
```

## <a name="parameters"></a>パラメーター
`pdwSize`\
入出力サイズを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 すべてのフィールドには型があり、すべての型にサイズが設定されています。 たとえば、byte 型のフィールドのサイズは1バイトです。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
