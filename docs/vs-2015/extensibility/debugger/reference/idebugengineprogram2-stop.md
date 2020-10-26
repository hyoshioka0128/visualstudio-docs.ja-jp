---
title: 'IDebugEngineProgram2:: Stop |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2::Stop
helpviewer_keywords:
- IDebugEngineProgram2::Stop
ms.assetid: 6e1c3d56-fb67-4a5b-80f9-8ee5131972bf
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cb74cb2940a91bbc64fa4a06f28d07a828357fc6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62431486"
---
# <a name="idebugengineprogram2stop"></a>IDebugEngineProgram2::Stop
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このプログラムで実行されているすべてのスレッドを停止します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Stop(   
   void   
);  
```  
  
```csharp  
int Stop();  
```  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドは、このプログラムがマルチプログラム環境でデバッグされているときに呼び出されます。 他のプログラムからの停止イベントを受信すると、このメソッドがこのプログラムで呼び出されます。 このメソッドの実装は非同期である必要があります。つまり、このメソッドから制御が戻る前に、すべてのスレッドを停止する必要はありません。 このメソッドの実装は、このプログラムでの [Causebreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md) メソッドの呼び出しと同じように簡単に行うことができます。  
  
 このメソッドへの応答として、デバッグイベントは送信されません。  
  
## <a name="see-also"></a>参照  
 [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)   
 [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)
