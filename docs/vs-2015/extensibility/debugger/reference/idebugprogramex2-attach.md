---
title: 'IDebugProgramEx2:: Attach |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramEx2::Attach
helpviewer_keywords:
- IDebugProgramEx2::Attach
ms.assetid: 33b22b2f-431e-4205-9441-d28a9c928c97
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4fe729f2fc196380a3db1a60d1c32f62bbd70998
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841989"
---
# <a name="idebugprogramex2attach"></a>IDebugProgramEx2::Attach
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

プログラムにセッションをアタッチします。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Attach(   
   IDebugEventCallback2* pCallback,  
   DWORD                 dwReason,  
   IDebugSession2*       pSession  
);  
```  
  
```  
[C#]  
int Attach(   
   IDebugEventCallback2 pCallback,  
   uint                 dwReason,  
   IDebugSession2       pSession  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pCallback`  
 からアタッチされたデバッグエンジンがイベントを送信するコールバック関数を表す [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) オブジェクト。  
  
 `dwReason`  
 からアタッチ操作の理由を説明する [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md) 列挙の値。  
  
 `pSession`  
 からプログラムにアタッチしているセッションを一意に識別する値。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返します。それ以外の場合は `S_OK` エラーコードを返します。 `E_ATTACH_DEBUGGER_ALREADY_ATTACHED`プログラムが既にアタッチされている場合、このメソッドはを返します。  
  
## <a name="remarks"></a>注釈  
 プログラムを含むポートは、の値を使用して、 `pSession` どのセッションがプログラムにアタッチしようとしているかを判断できます。 たとえば、ポートで一度に1つのデバッグセッションだけをプロセスにアタッチできる場合、ポートでは、同じセッションがプロセス内の他のプログラムに既にアタッチされているかどうかを判断できます。  
  
> [!NOTE]
> 渡されるインターフェイスは、 `pSession` クッキーとしてのみ扱われます。これは、このプログラムにアタッチするセッションデバッグマネージャーを一意に識別する値です。指定されたインターフェイスのメソッドは機能しません。  
  
## <a name="see-also"></a>参照  
 [IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)
