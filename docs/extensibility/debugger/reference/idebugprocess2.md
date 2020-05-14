---
title: をクリックして作業を開始する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2
helpviewer_keywords:
- IDebugProcess2 interface
ms.assetid: 99f6cd06-4076-45ee-b2ae-fa2ad627fd18
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c72659491ec6718397a4fbb494175eea0896c7f7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723801"
---
# <a name="idebugprocess2"></a>IDebugProcess2
このインターフェイスは、ポートで実行されているプロセスを表します。 ポートがローカル ポートの場合、`IDebugProcess2`通常はローカル マシン上の物理プロセスを表します。

## <a name="syntax"></a>構文

```
IDebugProcess2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 このインターフェイスは、グループとしてプログラムを管理するカスタム ポート サプライヤーによって実装されます。 このインターフェイスは、ポート サプライヤーによって実装されている必要があります。

 デバッグ エンジンは[、LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)を使用したプログラムの起動をサポートしている場合にも、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスは、このプロセスで識別されたプログラムのグループと対話するために、主にセッション デバッグ マネージャー (SDM) によって呼び出されます。

 このインターフェイス[を取得するには、GetProcess](../../../extensibility/debugger/reference/idebugprogram2-getprocess.md)または[GetProcess](../../../extensibility/debugger/reference/idebugport2-getprocess.md)を呼び出します。 このインターフェイスも を呼び`IDebugEngineLaunch2::LaunchSuspended`出すことによって返されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugProcess2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md)|プロセスの説明を取得します。|
|[EnumPrograms](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)|このプロセスに含まれるプログラムを列挙します。|
|[GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md)|プロセスのタイトル、フレンドリ名、またはファイル名を取得します。|
|[GetServer](../../../extensibility/debugger/reference/idebugprocess2-getserver.md)|このプロセスが実行されているマシン サーバーのインスタンスを取得します。|
|[Terminate](../../../extensibility/debugger/reference/idebugprocess2-terminate.md)|プロセスを終了します。|
|[Attach](../../../extensibility/debugger/reference/idebugprocess2-attach.md)|プロセスにアタッチします。|
|[CanDetach](../../../extensibility/debugger/reference/idebugprocess2-candetach.md)|SDM がプロセスをデタッチできるかどうかを判断します。|
|[Detach](../../../extensibility/debugger/reference/idebugprocess2-detach.md)|プロセスからデバッガーをデタッチします。|
|[GetPhysicalProcessId](../../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)|システム プロセス識別子を取得します。|
|[プロセス ID を取得します。](../../../extensibility/debugger/reference/idebugprocess2-getprocessid.md)|このプロセスのグローバル一意識別子を取得します。|
|[GetAttachedSessionName](../../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md)<br /><br /> [非推奨]|プロセスをデバッグしているセッションの名前を取得します。<br /><br /> [非推奨。 常に返`E_NOTIMPL`す必要があります。|
|[EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md)|プロセスで実行されているスレッドを列挙します。|
|[CauseBreak](../../../extensibility/debugger/reference/idebugprocess2-causebreak.md)|このプロセスで次のコードを実行しているプログラムが停止することを要求します。|
|[GetPort](../../../extensibility/debugger/reference/idebugprocess2-getport.md)|このプロセスが実行されているポートを取得します。|

## <a name="remarks"></a>Remarks
 1`IDebugProcess2`つまたは複数の[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)インターフェイスが含まれています。

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [プロセスを取得します。](../../../extensibility/debugger/reference/idebugport2-getprocess.md)
- [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [プロセスを取得します。](../../../extensibility/debugger/reference/idebugprogram2-getprocess.md)
- [次へ](../../../extensibility/debugger/reference/ienumdebugprocesses2-next.md)
- [Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
