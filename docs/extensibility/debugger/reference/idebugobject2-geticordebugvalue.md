---
description: このオブジェクトに関連付けられている値を表すマネージコードオブジェクトを取得します。
title: 'IDebugObject2:: Ge Ordebugvalue |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::GetICorDebugValue
helpviewer_keywords:
- IDebugObject2::GetICorDebugValue method
ms.assetid: bcd4355d-3fbe-483f-bb23-a44348323c6a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b25d5147283ad14b77e216a23a45f69516951908
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053751"
---
# <a name="idebugobject2geticordebugvalue"></a>IDebugObject2::GetICorDebugValue
このオブジェクトに関連付けられている値を表すマネージコードオブジェクトを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetICorDebugValue(
   IUnknown** ppUnk
);
```

```csharp
int GetICorDebugValue(
   out object ppUnk
);
```

## <a name="parameters"></a>パラメーター
`ppUnk`\
[出力] `IUnknown` このエイリアスを表すインターフェイス。 このインターフェイスは、インターフェイスに対してクエリを実行でき `ICorDebugValue` ます。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>注釈
 `ICorDebugValue`オブジェクトは、値を表す共通言語ランタイムインターフェイスです。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
