---
title: 'IDebugProgram2:: Attach |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgram2::Attach
helpviewer_keywords:
- IDebugProgram2::Attach
ms.assetid: de069fbf-a565-4905-b102-f5658c55aacd
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0e029c2e16d5eee1764b463b21fc0fd8a4032252
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62580405"
---
# <a name="idebugprogram2attach"></a>IDebugProgram2::Attach
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

プログラムにアタッチします。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Attach(   
   IDebugEventCallback2* pCallback  
);  
```  
  
```csharp  
int Attach(   
   IDebugEventCallback2 pCallback  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pCallback`  
 からデバッグイベント通知に使用される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) オブジェクト。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 次の表に、考えられるエラーコードを示します。  
  
|値|説明|  
|-----------|-----------------|  
|`E_ATTACH_DEBUGGER_ALREADY_ATTACHED`|指定されたプログラムは既にデバッガーにアタッチされています。|  
|`E_ATTACH_DEBUGGEE_PROCESS_SECURITY_VIOLATION`|Attach プロシージャの実行中にセキュリティ違反が発生しました。|  
|`E_ATTACH_CANNOT_ATTACH_TO_DESKTOP`|デスクトッププログラムをデバッガーにアタッチできません。|  
  
## <a name="remarks"></a>注釈  
 デバッグエンジン (DE) は、プログラムにアタッチするためにこのメソッドを呼び出すことはありません。 DE がプログラムのアドレス空間で実行されている場合は、 [Onattach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) メソッドが呼び出されます。 セッションデバッグマネージャーの (SDM) アドレス空間で DE を実行すると、 [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドが呼び出されます。  
  
## <a name="see-also"></a>参照  
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)   
 [OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)   
 [[アタッチ]](../../../extensibility/debugger/reference/idebugengine2-attach.md)
