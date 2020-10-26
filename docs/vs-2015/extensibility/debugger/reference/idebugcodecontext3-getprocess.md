---
title: 'IDebugCodeContext3:: GetProcess |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugCodeContext3::GetProcess
ms.assetid: e082e494-2255-4d9d-a5a9-6dadd904bea8
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6d72508dba0edd09b799f86a9ec04c6effa44b59
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68190924"
---
# <a name="idebugcodecontext3getprocess"></a>IDebugCodeContext3::GetProcess
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

デバッグプロセスのインターフェイスへの参照を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetProcess(   
   IDebugProcess2 **ppProcess  
);  
```  
  
```csharp  
public int GetProcess(   
   out IDebugProcess2 ppProcess  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppProcess`  
 入出力デバッグプロセスインターフェイスへの参照。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="example"></a>例  
 次の例は、 [IDebugBeforeSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugbeforesymbolsearchevent2.md)インターフェイスを公開する**CDebugCodeContext**オブジェクトに対してこのメソッドを実装する方法を示しています。  
  
```cpp#  
HRESULT CDebugCodeContext::GetProcess(IDebugProcess2** ppProcess)  
{  
    HRESULT hr = S_OK;  
    CComPtr<CDebugEngine> pEngine;  
    CComPtr<IDebugPort2> pPort2;  
  
    IfFalseGo( ppProcess, E_INVALIDARG );  
    *ppProcess = NULL;  
  
    IfFalseGo( m_pProgram, E_FAIL );  
    IfFailGo( ((CDebugProgram *)m_pProgram)->GetEngine(&pEngine) );  
    IfFailGo( pEngine->GetSDMProcess(ppProcess) );  
  
Error:  
  
    return hr;  
}  
```  
  
## <a name="see-also"></a>参照  
 [IDebugCodeContext3](../../../extensibility/debugger/reference/idebugcodecontext3.md)
