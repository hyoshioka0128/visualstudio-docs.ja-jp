---
title: IDebugThread2::SetNextStatement |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugThread2::SetNextStatement
helpviewer_keywords:
- IDebugThread2::SetNextStatement
ms.assetid: 9e2834dd-4ecf-45af-8e6c-f9318ebdac06
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: bfc2afb15dbacde1eb0a96178d2769365deb4e31
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49893794"
---
# <a name="idebugthread2setnextstatement"></a>IDebugThread2::SetNextStatement
現在の命令ポインターを指定したコードのコンテキストに設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetNextStatement (   
   IDebugStackFrame2*  pStackFrame,  
   IDebugCodeContext2* pCodeContext  
);  
```  
  
```csharp  
int SetNextStatement (   
   IDebugStackFrame2  pStackFrame,  
   IDebugCodeContext2 pCodeContext  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pStackFrame`  
 今後使用するために予約されていますnull 値に設定します。  
  
 `pCodeContext`  
 [in][IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)実行されるコードの場所を記述するオブジェクトとそのコンテキスト。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。 次の表では、使用可能なその他の値を示します。  
  
|[値]|説明|  
|-----------|-----------------|  
|E_CANNOT_SET_NEXT_STATEMENT_ON_NONLEAF_FRAME|次のステートメントは、フレームのスタックにスタック フレームにすることはできません。|  
|E_CANNOT_SETIP_TO_DIFFERENT_FUNCTION|次のステートメントは、スタック内の任意のフレームに関連付けられていません。|  
|E_CANNOT_SET_NEXT_STATEMENT_ON_EXCEPTION|いくつかのデバッグ エンジンでは、例外の後に次のステートメントを設定できません。|  
  
## <a name="remarks"></a>Remarks  
 命令ポインターでは、実行する次の命令またはステートメントを示します。 このメソッドは、ソース コードの行を再試行するか、たとえば、別の関数で引き続き実行を強制的に使用されます。  
  
## <a name="see-also"></a>関連項目  
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)   
 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)