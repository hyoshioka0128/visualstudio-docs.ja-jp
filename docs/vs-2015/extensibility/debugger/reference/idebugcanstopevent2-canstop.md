---
title: 'IDebugCanStopEvent2:: CanStop |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2::CanStop
helpviewer_keywords:
- IDebugCanStopEvent2::CanStop
ms.assetid: 7d61adbe-6b3d-41f3-86a1-45d9cc01a7f8
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8167013489b3b37e254100f7547cd61d54529b95
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68191195"
---
# <a name="idebugcanstopevent2canstop"></a>IDebugCanStopEvent2::CanStop
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

現在のコードの場所で停止するか、実行を継続するかにかかわらず、デバッグエンジン (DE) に通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT CanStop (   
   BOOL fCanStop  
);  
```  
  
```csharp  
int CanStop (   
   int fCanStop  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `fCanStop`  
 からDE を現在の `TRUE` コードの場所で停止する場合は0以外の値。それ以外の場合は 0 ( `FALSE` )。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このイベントの受信者は、通常、 [getreason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md) メソッドを呼び出して、DE が停止する理由を特定し、 `IDebugCanStopEvent2::CanStop` 適切な応答を使用してメソッドを呼び出します。  
  
 DE が停止すると、停止の理由を説明するイベントが送信されます。 通常、送信されるイベント、 [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md) インターフェイスによって表されるユーザーまたはシグナル中断、および [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md) インターフェイスによって表されるブレークポイントイベントの2つがあります。  
  
## <a name="see-also"></a>参照  
 [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)   
 [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md)   
 [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)   
 [GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)
