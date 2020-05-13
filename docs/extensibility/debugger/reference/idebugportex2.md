---
title: をクリックして使用する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEx2
helpviewer_keywords:
- IDebugPortEx2 interface
ms.assetid: 144724d0-38ee-4c9b-87ca-8a504371182b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5789681b0da70f46dadac1e29d0d6bb9dc905d1a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725001"
---
# <a name="idebugportex2"></a>IDebugPortEx2
このインターフェイスを使用すると、セッション デバッグ マネージャー (SDM) がポートで実行されているプログラムとプロセスを制御できます。

## <a name="syntax"></a>構文

```
IDebugPortEx2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 カスタム ポート サプライヤーは[、IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)を実装するのと同じオブジェクトにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 SDM は[QueryInterface](/cpp/atl/queryinterface)、このインターフェイスを`IDebugPort2`取得するインターフェイスでクエリ インターフェイスを呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugPortEx2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)|実行可能ファイルを起動します。|
|[ResumeProcess](../../../extensibility/debugger/reference/idebugportex2-resumeprocess.md)|プロセスの実行を再開します。|
|[CanTerminateProcess](../../../extensibility/debugger/reference/idebugportex2-canterminateprocess.md)|プロセスを終了できるかどうかを決定します。|
|[TerminateProcess](../../../extensibility/debugger/reference/idebugportex2-terminateprocess.md)|プロセスを終了します。|
|[GetPortProcessId](../../../extensibility/debugger/reference/idebugportex2-getportprocessid.md)|ポート自体のプロセス ID を取得します。|
|[GetProgram](../../../extensibility/debugger/reference/idebugportex2-getprogram.md)|プログラム ノードに関連付けられているプログラムを取得します。|

## <a name="remarks"></a>Remarks
 このインターフェイスは、通常、SDM とカスタム ポート サプライヤー間でプライベートです。

 必要に応じて、デバッグ エンジン (DE) は[、起動中断](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)に渡される[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)インターフェイスでこのインターフェイスを検索し、プログラムを起動するのに[は、一時停止起動](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)を使用できます。 ただし、これは必須ではありません。

## <a name="requirements"></a>必要条件
 ヘッダー: ポートプリフ.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
