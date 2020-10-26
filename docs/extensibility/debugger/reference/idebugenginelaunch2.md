---
title: IDebugEngineLaunch2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineLaunch2
helpviewer_keywords:
- IDebugEngineLaunch2 interface
ms.assetid: 5eaf2ad8-3fbf-446e-b48b-5327ad3f5255
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ee77cbd680df2c851d53aac298605023227fa6f8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80730498"
---
# <a name="idebugenginelaunch2"></a>IDebugEngineLaunch2
デバッグエンジン (DE) がプログラムを起動して終了するために使用します。

## <a name="syntax"></a>構文

```
IDebugEngineLaunch2 : IDebugEngine2
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、カスタムポートで完全に処理できないプロセスを起動するための特別な要件がある場合に、カスタムの DE によって実装されます。 これは、通常、DE がインタープリターの一部で、デバッグ中のプロセスがスクリプトである場合に発生します。最初にインタープリターを起動してから、スクリプトを読み込んで起動する必要があります。 ポートはインタープリターを起動できますが、スクリプトでは特別な処理が必要になる場合があります (この場合、DE にはロールがあります)。 このインターフェイスは、カスタムポートが処理できないプログラムを起動するための固有の要件がある場合にのみ実装されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、SDM が (QueryInterface を使用して) [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) インターフェイスからこのインターフェイスを取得できる場合、セッションデバッグマネージャー (sdm) によって呼び出されます。 このインターフェイスを取得できる場合、SDM は、DE に特別な要件があることを認識し、ポートが起動するのではなく、このインターフェイスを呼び出してプログラムを起動します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugEngineLaunch2` ます。

|Method|説明|
|------------|-----------------|
|[LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)|DE を通じてプロセスを起動します。|
|[ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)|プロセスの実行を再開します。|
|[CanTerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-canterminateprocess.md)|プロセスを終了できるかどうかを決定します。|
|[TerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-terminateprocess.md)|プロセスを終了します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
