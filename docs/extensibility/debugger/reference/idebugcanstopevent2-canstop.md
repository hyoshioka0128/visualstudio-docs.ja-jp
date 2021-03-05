---
description: 現在のコードの場所で停止するか、実行を継続するかにかかわらず、デバッグエンジン (DE) に通知します。
title: 'IDebugCanStopEvent2:: CanStop |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2::CanStop
helpviewer_keywords:
- IDebugCanStopEvent2::CanStop
ms.assetid: 7d61adbe-6b3d-41f3-86a1-45d9cc01a7f8
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 38b4d528ae1aa5a89853dc4873a9c07aa051a14c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102173637"
---
# <a name="idebugcanstopevent2canstop"></a>IDebugCanStopEvent2::CanStop
現在のコードの場所で停止するか、実行を継続するかにかかわらず、デバッグエンジン (DE) に通知します。

## <a name="syntax"></a>構文

```cpp
HRESULT CanStop ( 
   BOOL fCanStop
);
```

```csharp
int CanStop ( 
   int fCanStop
);
```

## <a name="parameters"></a>パラメーター
`fCanStop`\
からDE を現在の `TRUE` コードの場所で停止する場合は0以外の値。それ以外の場合は 0 ( `FALSE` )。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このイベントの受信者は、通常、 [getreason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md) メソッドを呼び出して、DE が停止する理由を特定し、 `IDebugCanStopEvent2::CanStop` 適切な応答を使用してメソッドを呼び出します。

 DE が停止すると、停止の理由を説明するイベントが送信されます。 通常、送信されるイベント、 [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md) インターフェイスによって表されるユーザーまたはシグナル中断、および [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md) インターフェイスによって表されるブレークポイントイベントの2つがあります。

## <a name="see-also"></a>関連項目
- [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)
- [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md)
- [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)
- [GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)
