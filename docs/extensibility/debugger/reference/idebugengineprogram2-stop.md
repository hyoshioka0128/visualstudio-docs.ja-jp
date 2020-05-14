---
title: プログラム2::ストップ |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730482"
---
# <a name="idebugengineprogram2stop"></a>IDebugEngineProgram2::Stop
このプログラムで実行中のすべてのスレッドを停止します。

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
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、このプログラムがマルチプログラム環境でデバッグ中のときに呼び出されます。 他のプログラムから停止イベントを受信すると、このプログラムでこのメソッドが呼び出されます。 このメソッドの実装は非同期である必要があります。つまり、このメソッドが返される前にすべてのスレッドを停止する必要はありません。 このメソッドの実装は、このプログラムで[CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)メソッドを呼び出すのと同じくらい簡単です。

 プログラムが停止したときに、実装者[は IDebugStopCompleteEvent2](../../../extensibility/debugger/reference/idebugstopcompleteevent2.md)を送信する必要があります。

## <a name="see-also"></a>関連項目
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)
