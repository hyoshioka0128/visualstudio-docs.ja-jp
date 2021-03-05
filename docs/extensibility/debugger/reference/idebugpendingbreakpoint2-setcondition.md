---
description: 保留中のブレークポイントに関連付けられている条件を設定または変更します。
title: 'IDebugPendingBreakpoint2:: SetCondition |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2::SetCondition
helpviewer_keywords:
- SetCondition method
- IDebugPendingBreakpoint2::SetCondition method
ms.assetid: 0534224f-654f-4862-bc4d-a9a81a5f8899
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9ea2ce1a5a9ffdfb48e0190dc3399ceabf5cb052
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102142896"
---
# <a name="idebugpendingbreakpoint2setcondition"></a>IDebugPendingBreakpoint2::SetCondition
保留中のブレークポイントに関連付けられている条件を設定または変更します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetCondition( 
   BP_CONDITION bpCondition
);
```

```csharp
int SetCondition( 
   BP_CONDITION bpCondition
);
```

## <a name="parameters"></a>パラメーター
`bpCondition`\
から設定する条件を指定する [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md) 構造体。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 保留中のブレークポイントに関連付けられていたすべての条件は失われます。 この保留中のブレークポイントからバインドされたすべてのブレークポイントは、条件をパラメーターで指定された値に設定するために呼び出され `bpCondition` ます。

## <a name="see-also"></a>関連項目
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)
