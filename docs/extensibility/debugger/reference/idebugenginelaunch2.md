---
title: IDebugエンジンの打ち上げ2 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730498"
---
# <a name="idebugenginelaunch2"></a>IDebugEngineLaunch2
プログラムを起動および終了するためにデバッグ エンジン (DE) によって使用されます。

## <a name="syntax"></a>構文

```
IDebugEngineLaunch2 : IDebugEngine2
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 このインターフェイスは、カスタム ポートで完全に処理できないプロセスを起動するための特別な要件がある場合、カスタム DE によって実装されます。 これは、通常、DE がインタープリターの一部であり、デバッグ中のプロセスがスクリプトである場合に、インタプリタを最初に起動してから、スクリプトをロードして開始します。 ポートはインタプリタを起動できますが、スクリプトは特別な処理を必要とするかもしれません(DE が役割を持つ場所)。 このインターフェイスは、カスタム ポートで処理できないプログラムを起動するための固有の要件がある場合にのみ実装されます。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスは、SDM が (クエリ インターフェイスを使用して) [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)インターフェイスからこのインターフェイスを取得できる場合、セッション デバッグ マネージャー (SDM) によって呼び出されます。 このインターフェイスを取得できる場合、SDM は DE に特別な要件があることを認識し、このインターフェイスを呼び出して、ポートで起動するのではなく、プログラムを起動します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugEngineLaunch2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)|DE を使用してプロセスを起動します。|
|[ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)|プロセスの実行を再開します。|
|[CanTerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-canterminateprocess.md)|プロセスを終了できるかどうかを判断します。|
|[TerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-terminateprocess.md)|プロセスを終了します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
