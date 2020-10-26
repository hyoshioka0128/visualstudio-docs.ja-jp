---
title: EVALFLAGS |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- EVALFLAGS
helpviewer_keywords:
- EVALFLAGS enumeration
ms.assetid: 7b2cb14a-511a-4fef-9e4f-308139719fba
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9e6ee00402c13b2a79e4e6757a127211eda9c3c0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68149386"
---
# <a name="evalflags"></a>EVALFLAGS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

式の評価を制御するフラグを指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_EVALFLAGS {  
   EVAL_RETURNVALUE = 0x0002,  
   EVAL_NOSIDEEFFECTS = 0x0004,  
   EVAL_ALLOWBPS = 0x0008,  
   EVAL_ALLOWERRORREPORT = 0x0010,  
   EVAL_FUNCTION_AS_ADDRESS = 0x0040,  
   EVAL_NOFUNCEVAL = 0x0080,  
   EVAL_NOEVENTS = 0x1000  
};  
typedef DWORD EVALFLAGS;  
```  
  
```csharp  
public enum enum_EVALFLAGS {  
   EVAL_RETURNVALUE = 0x0002,  
   EVAL_NOSIDEEFFECTS = 0x0004,  
   EVAL_ALLOWBPS = 0x0008,  
   EVAL_ALLOWERRORREPORT = 0x0010,  
   EVAL_FUNCTION_AS_ADDRESS = 0x0040,  
   EVAL_NOFUNCEVAL = 0x0080,  
   EVAL_NOEVENTS = 0x1000  
}  
```  
  
## <a name="members"></a>メンバー  
 EVAL_RETURNVALUE  
 戻り値 (存在する場合) を評価することを指定します。  
  
 EVAL_NOSIDEEFFECTS  
 副作用を許可しないことを指定します。  
  
 EVAL_ALLOWBPS  
 ブレークポイントでの停止を指定します。  
  
 EVAL_ALLOWERRORREPORT  
 許可するホストへのエラー報告を指定します。 Internet Explorer のスクリプトでの式の評価に主に使用されます。  
  
 EVAL_FUNCTION_AS_ADDRESS  
 関数を呼び出す代わりに、関数をアドレスとして強制的に評価します。  
  
 EVAL_NOFUNCEVAL  
 関数が評価されないようにします。 たとえば、式に含まれるトークンを考えてみ `int` `myExpression(int) + 10` ます。 この関数は、アドレスとして正しく評価されますが、値としては評価できません。  
  
 EVAL_NOEVENTS  
 式の評価中に発生したイベントをセッションデバッグマネージャー (SDM) または IDE に送信しないことを示すフラグ。  
  
## <a name="remarks"></a>注釈  
 これらのフラグは、 [Evaluateasync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) メソッドと [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) メソッドに引数として渡されます。  
  
 これらのフラグは、ビットごとの OR と組み合わせることができます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)   
 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
