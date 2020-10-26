---
title: 'IDebugThread2:: SetNextStatement |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugThread2::SetNextStatement
helpviewer_keywords:
- IDebugThread2::SetNextStatement
ms.assetid: 9e2834dd-4ecf-45af-8e6c-f9318ebdac06
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 755044ec1d713075c1c1fd3165254ba192943288
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152961"
---
# <a name="idebugthread2setnextstatement"></a>IDebugThread2::SetNextStatement
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

現在の命令ポインターを指定されたコードコンテキストに設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
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
 将来使用するために予約されています。を null 値に設定します。  
  
 `pCodeContext`  
 から実行されるコードの場所とそのコンテキストを記述する [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) オブジェクト。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 次の表に、その他の使用可能な値を示します。  
  
|値|説明|  
|-----------|-----------------|  
|E_CANNOT_SET_NEXT_STATEMENT_ON_NONLEAF_FRAME|次のステートメントは、フレームスタックを深く掘り下げたスタックフレーム内に存在することはできません。|  
|E_CANNOT_SETIP_TO_DIFFERENT_FUNCTION|次のステートメントは、スタック内のどのフレームにも関連付けられていません。|  
|E_CANNOT_SET_NEXT_STATEMENT_ON_EXCEPTION|一部のデバッグエンジンでは、例外の後に次のステートメントを設定することはできません。|  
  
## <a name="remarks"></a>注釈  
 命令ポインターは、次に実行する命令またはステートメントを示します。 このメソッドは、ソースコードの行を再試行したり、別の関数で実行を強制するために使用されます。たとえば、のようになります。  
  
## <a name="see-also"></a>参照  
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)   
 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
