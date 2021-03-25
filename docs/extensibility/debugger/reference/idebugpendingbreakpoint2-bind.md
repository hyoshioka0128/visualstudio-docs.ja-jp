---
description: この保留中のブレークポイントを1つまたは複数のコードの場所にバインドします。
title: 'IDebugPendingBreakpoint2:: Bind |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2::Bind
helpviewer_keywords:
- Bind method
- IDebugPendingBreakpoint2::Bind method
ms.assetid: 46e3f307-219d-40cd-a929-d41399c60ecf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3a99319aa4269a1f17032a30ea8df02b4f08836a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084533"
---
# <a name="idebugpendingbreakpoint2bind"></a>IDebugPendingBreakpoint2::Bind
この保留中のブレークポイントを1つまたは複数のコードの場所にバインドします。

## <a name="syntax"></a>構文

```cpp
HRESULT Bind( 
   void 
);
```

```csharp
int Bind();
```

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 `E_BP_DELETED`ブレークポイントが削除されている場合は、を返します。

## <a name="remarks"></a>注釈
 このメソッドが呼び出されると、デバッグエンジン (DE) は、この保留中のブレークポイントを、一致するすべてのコードの場所にバインドしようとします。

 このメソッドが返された後、呼び出し元は、 [Enumboundbreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md) ポイントまたは [enumboundbreakpoints ポイント](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)の呼び出しを想定する前に、保留中のブレークポイントがバインドされているかエラーになっていることを示すイベントを待機する必要があります。メソッドは、バインドされたブレークポイントまたはエラーブレークポイントをそれぞれ列挙します

## <a name="see-also"></a>こちらもご覧ください
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)
- [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)
- [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)
- [EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)
