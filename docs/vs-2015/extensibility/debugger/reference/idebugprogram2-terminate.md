---
title: 'IDebugProgram2:: Terminate |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgram2::Terminate
helpviewer_keywords:
- IDebugProgram2::Terminate
ms.assetid: 4d3127d3-b1e9-4b28-ac22-2f2eea255f86
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4673259e4a8ca0d4354037efbc35b63bedfcbc96
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68146347"
---
# <a name="idebugprogram2terminate"></a>IDebugProgram2::Terminate
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

プログラムを終了します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Terminate(   
   void   
);  
```  
  
```csharp  
int Terminate();  
```  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 可能であれば、プログラムは終了し、プロセスからアンロードされます。それ以外の場合は、デバッグエンジン (DE) によって必要なクリーンアップが実行されます。  
  
 このメソッドまたは [Terminate](../../../extensibility/debugger/reference/idebugprocess2-terminate.md) メソッドは、通常、ユーザーがすべてのデバッグを停止した場合に、IDE によって呼び出されます。 このメソッドを実装する場合は、プロセス内でプログラムを終了するのが理想的です。 これが不可能な場合は、このプロセスでプログラムが実行されないようにする必要があります (必要なクリーンアップを実行します)。 メソッドが `IDebugProcess2::Terminate` IDE によって呼び出された場合、メソッドが呼び出された後、プロセス全体が終了し `IDebugProgram2::Terminate` ます。  
  
## <a name="see-also"></a>参照  
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [Terminate](../../../extensibility/debugger/reference/idebugprocess2-terminate.md)
