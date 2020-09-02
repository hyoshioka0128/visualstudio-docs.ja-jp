---
title: 'IDebugProcess3:: Continue |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProcess3::Continue
helpviewer_keywords:
- IDebugProcess3::Continue
ms.assetid: 57506242-5763-4c08-adb9-8a78ce02cebb
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 92a36bb7e89d8afaa6d76f7d7b3772bd1714ffa7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86386239"
---
# <a name="idebugprocess3continue"></a>IDebugProcess3::Continue
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このプロセスの実行を停止状態から続行します。 前の実行状態 (ステップなど) はすべて保持され、プロセスは再度実行を開始します。  
  
> [!NOTE]
> このメソッドは、 [Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md)の代わりに使用する必要があります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Continue(  
   IDebugThread2* pThread  
);  
```  
  
```csharp  
int Continue(  
   IDebugThread2 pThread  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pThread`  
 から続行するスレッドを表す [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) オブジェクト。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>解説  
 このメソッドは、デバッグされているプロセスの数や、停止イベントを生成したプロセスに関係なく、このプロセスで呼び出されます。 の実装では、前の実行状態 (ステップなど) を保持し、以前の実行を完了する前に停止していないかのように実行を継続する必要があります。 つまり、このプロセス内のスレッドがステップオーバー操作を行っていて、他のプロセスが停止したために停止された場合は、 `Continue` 指定されたスレッドが元のステップオーバー操作を完了する必要があります。  
  
 **警告** この呼び出しの処理中に、停止イベントまたは即時 (同期) イベントを [イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) に送信しないでください。それ以外の場合、デバッガーは応答を停止する可能性があります。  
  
## <a name="see-also"></a>参照  
 [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)   
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
