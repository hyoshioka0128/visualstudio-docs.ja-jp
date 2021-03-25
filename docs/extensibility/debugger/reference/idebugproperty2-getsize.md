---
description: プロパティ値のサイズ (バイト単位) を取得します。
title: 'IDebugProperty2:: GetSize |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetSize
helpviewer_keywords:
- IDebugProperty2::GetSize
ms.assetid: 0deb8ec5-d6fb-4622-bb14-0c46b9459cc6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7db319a420dc63eaec8afcdcbeaa38fe861a4bea
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064788"
---
# <a name="idebugproperty2getsize"></a>IDebugProperty2::GetSize
プロパティ値のサイズ (バイト単位) を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetSize ( 
   DWORD* pdwSize
);
```

```csharp
int GetSize ( 
   out uint pdwSize
);
```

## <a name="parameters"></a>パラメーター
`pdwSize`\
入出力プロパティ値のサイズ (バイト単位) を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、を返します。それ以外の場合は `S_OK` エラーコードを返します。 `S_GETSIZE_NO_SIZE`プロパティのサイズが指定されていない場合は、を返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
