---
description: 初期化中に、デバッグエンジンがコールバックを式エバリュエーターに渡すことができるようにします。
title: 'IDebugExpressionEvaluator2:: SetIDebugIDECallback |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugExpressionEvaluator2::SetIDebugIDECallback
- SetIDebugIDECallback
ms.assetid: f01c40ad-ef4b-477b-8304-602c6972bc88
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3793fbcf19b87d6aed1df81d6739ae6529c2ba14
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077331"
---
# <a name="idebugexpressionevaluator2setidebugidecallback"></a>IDebugExpressionEvaluator2::SetIDebugIDECallback
初期化中に、デバッグエンジンがコールバックを式エバリュエーターに渡すことができるようにします。

## <a name="syntax"></a>構文

```cpp
HRESULT SetIDebugIDECallback (
   IDebugIDECallback * pCallback
);
```

```csharp
int SetIDebugIDECallback (
   IDebugIDECallback pCallback
);
```

## <a name="parameters"></a>パラメーター
`pCallback`\
からコールバックのインターフェイス。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md)
