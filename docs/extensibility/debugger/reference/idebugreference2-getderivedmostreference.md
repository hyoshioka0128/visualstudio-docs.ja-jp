---
description: 参照の最も派生した参照を取得します。
title: 'IDebugReference2:: GetDerivedMostReference |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::GetDerivedMostReference
helpviewer_keywords:
- IDebugReference2::GetDerivedMostReference
ms.assetid: 07253b74-7d39-48e0-8e85-ac8dfd919f6e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9c482b05620f280b2948aefe7e95eb38682268c6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071442"
---
# <a name="idebugreference2getderivedmostreference"></a>IDebugReference2::GetDerivedMostReference
参照の最も派生した参照を取得します。 将来使用するために予約されています。

## <a name="syntax"></a>構文

```cpp
HRESULT GetDerivedMostReference( 
   IDebugReference2** ppDerivedMost
);
```

```csharp
int GetDerivedMostReference( 
   out IDebugReference2 ppDerivedMost
);
```

## <a name="parameters"></a>パラメーター
`ppDerivedMost`\
入出力最派生のプロパティを表す [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 常に `E_NOTIMPL` を返します。

## <a name="remarks"></a>注釈
 たとえば、このプロパティがを実装するオブジェクトを表し、 `ClassRoot` 実際にから派生したのインスタンス化である場合、 `ClassDerived` このメソッドは、 `ClassRoot` オブジェクトへの参照を表す [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) オブジェクトを返し `ClassDerived` ます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
