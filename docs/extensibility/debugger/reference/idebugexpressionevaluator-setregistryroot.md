---
description: このメソッドは、レジストリのルートを設定します。
title: 'IDebugExpressionEvaluator:: SetRegistryRoot |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator::SetRegistryRoot
helpviewer_keywords:
- IDebugExpressionEvaluator::SetRegistryRoot method
ms.assetid: 790886d8-1975-4d3c-9a75-cd86c1faf4ca
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 14ce5d00dcfec9da4c6193398f62edbe4e1988d3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092047"
---
# <a name="idebugexpressionevaluatorsetregistryroot"></a>IDebugExpressionEvaluator::SetRegistryRoot
このメソッドは、レジストリのルートを設定します。 サイドバイサイドデバッグに使用されます。

## <a name="syntax"></a>構文

```cpp
HRESULT SetRegistryRoot ( 
   LPCOLESTR ustrRegistryRoot
);
```

```csharp
int SetRegistryRoot(
   string ustrRegistryRoot
);
```

## <a name="parameters"></a>パラメーター
`ustrRegistryRoot`\
から新しいレジストリルート。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 指定されたレジストリルートは、通常、式エバリュエーターが最初にインスタンス化され、特定のバージョンの Visual Studio のレジストリキーを指している場合に設定されます (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudioの \\ *x* *. y* はバージョン番号です)。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)
