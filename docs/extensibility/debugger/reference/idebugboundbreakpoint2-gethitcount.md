---
description: このバインドされたブレークポイントの現在のヒットカウントを取得します。
title: 'IDebugBoundBreakpoint2:: GetHitCount |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBoundBreakpoint2::GetHitCount
helpviewer_keywords:
- GetHitCount method
- IDebugBoundBreakpoint2::GetHitCount method
ms.assetid: 23481f37-047c-41d2-8286-4da1f4084961
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ca015a814956a0b6073e090d17751e623b557429
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088859"
---
# <a name="idebugboundbreakpoint2gethitcount"></a>IDebugBoundBreakpoint2::GetHitCount
このバインドされたブレークポイントの現在のヒットカウントを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetHitCount( 
   DWORD* pdwHitCount
);
```

```csharp
int GetHitCount( 
   out uint pdwHitCount
);
```

## <a name="parameters"></a>パラメーター
`pdwHitCount`\
入出力ヒットカウントを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 `E_BP_DELETED`バインドされたブレークポイントオブジェクトの状態が `BPS_DELETED` ( [BP_STATE](../../../extensibility/debugger/reference/bp-state.md)列挙体の一部) に設定されている場合は、を返します。

## <a name="remarks"></a>注釈
 ヒットカウントは、現在のセッションの実行中にこのブレークポイントが発生した回数です。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [BP_STATE](../../../extensibility/debugger/reference/bp-state.md)
