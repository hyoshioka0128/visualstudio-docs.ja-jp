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
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3b900817a5025b0d523f8d3bb3237a1b10cc3a6a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102152404"
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

## <a name="remarks"></a>解説
 指定されたレジストリルートは、通常、式エバリュエーターが最初にインスタンス化され、特定のバージョンの Visual Studio のレジストリキーを指している場合に設定されます (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudioの \\ *x* *. y* はバージョン番号です)。

## <a name="see-also"></a>関連項目
- [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)
