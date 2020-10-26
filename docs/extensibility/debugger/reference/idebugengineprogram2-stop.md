---
title: 'IDebugEngineProgram2:: Stop |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2::Stop
helpviewer_keywords:
- IDebugEngineProgram2::Stop
ms.assetid: 6e1c3d56-fb67-4a5b-80f9-8ee5131972bf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 286a448ee33f57d2e3a3282dc8d72b11a843a9c3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80730482"
---
# <a name="idebugengineprogram2stop"></a>IDebugEngineProgram2::Stop
このプログラムで実行されているすべてのスレッドを停止します。

## <a name="syntax"></a>構文

```cpp
HRESULT Stop( 
   void 
);
```

```csharp
int Stop();
```

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドは、このプログラムがマルチプログラム環境でデバッグされているときに呼び出されます。 他のプログラムからの停止イベントを受信すると、このメソッドがこのプログラムで呼び出されます。 このメソッドの実装は非同期である必要があります。つまり、このメソッドから制御が戻る前に、すべてのスレッドを停止する必要はありません。 このメソッドの実装は、このプログラムでの [Causebreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md) メソッドの呼び出しと同じように簡単に行うことができます。

 実装者は、プログラムが停止したときに [IDebugStopCompleteEvent2](../../../extensibility/debugger/reference/idebugstopcompleteevent2.md) を送信する必要があります。

## <a name="see-also"></a>関連項目
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)
