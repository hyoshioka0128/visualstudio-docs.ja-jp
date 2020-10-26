---
title: 'IDebugProcess3:: Step |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProcess3::Step
helpviewer_keywords:
- IDebugProcess3::Step
ms.assetid: 6ad9094c-27cc-4927-8a7c-1b4d97b2e436
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5069a40f4e3ea4b1fba74c8133a18b46f2b3f2d2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86386226"
---
# <a name="idebugprocess3step"></a>IDebugProcess3::Step
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

プロセスで1つの命令またはステートメントをステップ実行します。  
  
> [!NOTE]
> このメソッドは、 [ステップ](../../../extensibility/debugger/reference/idebugprogram2-step.md)の代わりに使用する必要があります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Step(  
   IDebugThread2* pThread,  
   STEPKIND       sk,  
   STEPUNIT       step,  
);  
```  
  
```csharp  
int Step(  
   IDebugThread2 pThread,   
   enum_STEPKIND sk,   
   enum_STEPUNIT step  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pThread`  
 からステップ処理中のスレッドを表す [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) オブジェクト。  
  
 `sk`  
 から [Stepkind](../../../extensibility/debugger/reference/stepkind.md) 値の1つ。  
  
 `step`  
 から [Stepunit](../../../extensibility/debugger/reference/stepunit.md) 値の1つ。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。  
  
## <a name="remarks"></a>解説  
 スレッド間の同期またはスレッド間の通信がある場合、プロセス内の他のスレッドは、特定のスレッドがステップ実行されているときに実行する必要があります。  
  
 **警告** この呼び出しの処理中に、停止イベントまたは即時 (同期) イベントを [イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) に送信しないでください。それ以外の場合、デバッガーは応答を停止する可能性があります。  
  
## <a name="see-also"></a>参照  
 [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)   
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [ステップの種類](../../../extensibility/debugger/reference/stepkind.md)   
 [ステップ単位](../../../extensibility/debugger/reference/stepunit.md)   
 [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
