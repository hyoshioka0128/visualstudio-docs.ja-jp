---
description: ポートサプライヤー識別子を取得します。
title: 'IDebugPortSupplier2:: GetPortSupplierId 先 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::GetPortSupplierId
helpviewer_keywords:
- IDebugPortSupplier2::GetPortSupplierId
ms.assetid: 741d0829-0943-49bf-b56e-61e836043006
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a7fa298074f9942d2cf863a7e0e1e8ad71f86ed5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072105"
---
# <a name="idebugportsupplier2getportsupplierid"></a>IDebugPortSupplier2::GetPortSupplierId
ポートサプライヤー識別子を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetPortSupplierId( 
   GUID* pguidPortSupplier
);
```

```csharp
HRESULT GetPortSupplierId( 
   out Guid pguidPortSupplier
);
```

## <a name="parameters"></a>パラメーター
`pguidPortSupplier`\
入出力ポートサプライヤーの GUID を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
