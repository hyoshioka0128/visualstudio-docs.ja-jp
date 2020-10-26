---
title: 'IDebugPendingBreakpoint2:: Bind |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2::Bind
helpviewer_keywords:
- Bind method
- IDebugPendingBreakpoint2::Bind method
ms.assetid: 46e3f307-219d-40cd-a929-d41399c60ecf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 83d48e8df847620716b0f581be65ded48e2e5a13
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80725988"
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

## <a name="remarks"></a>解説
 このメソッドが呼び出されると、デバッグエンジン (DE) は、この保留中のブレークポイントを、一致するすべてのコードの場所にバインドしようとします。

 このメソッドが返された後、呼び出し元は、 [Enumboundbreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md) ポイントまたは [enumboundbreakpoints ポイント](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)の呼び出しを想定する前に、保留中のブレークポイントがバインドされているかエラーになっていることを示すイベントを待機する必要があります。メソッドは、バインドされたブレークポイントまたはエラーブレークポイントをそれぞれ列挙します

## <a name="see-also"></a>関連項目
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)
- [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)
- [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)
- [EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)
