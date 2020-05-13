---
title: を待ってブレークポイント2::セット条件 |マイクロソフトドキュメント
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
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4683d944f2489b8b21ff545c86e3d867283d644a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725722"
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
[in]設定する条件を指定する[BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)構造体。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 以前に保留中のブレークポイントに関連付けられていた条件は失われます。 この保留中のブレークポイントからバインドされたすべてのブレークポイントが呼び出され、パラメーターで指定された値に`bpCondition`条件が設定されます。

## <a name="see-also"></a>関連項目
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)
