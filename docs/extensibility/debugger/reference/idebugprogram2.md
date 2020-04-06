---
title: Iデバッグプログラム2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2
helpviewer_keywords:
- IDebugProgram2 interface
ms.assetid: 8d73df73-cfff-4b8b-b426-d6051edb1939
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 150746197be4945b012717bef08e18ea57168177
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722724"
---
# <a name="idebugprogram2"></a>IDebugProgram2
このインターフェイスは、プロセスで実行されているプログラムを表します。

## <a name="syntax"></a>構文

```
IDebugProgram2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) とカスタム ポート サプライヤーは、プロセス内のプログラムを表すために、このインターフェイスを実装します。 セッション デバッグ マネージャー (SDM) も、このインターフェイスを実装して[、Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md)に情報を提供します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 イベント[は](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)、新しいプログラムのこのインターフェイスを返します。 このインターフェイスは、複数のインターフェイスで多くのメソッドのパラメーターとしても使用されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugProgram2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)|このプログラムで実行されているスレッドを列挙します。|
|[GetName](../../../extensibility/debugger/reference/idebugprogram2-getname.md)|プログラムの名前を取得します。|
|[プロセスを取得します。](../../../extensibility/debugger/reference/idebugprogram2-getprocess.md)|このプログラムが実行されているプロセスを取得します。|
|[Terminate](../../../extensibility/debugger/reference/idebugprogram2-terminate.md)|このプログラムを終了します。|
|[Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md)|このプログラムにアタッチします。|
|[CanDetach](../../../extensibility/debugger/reference/idebugprogram2-candetach.md)|デバッグ エンジン (DE) がプログラムからデタッチできるかどうかを判断します。|
|[Detach](../../../extensibility/debugger/reference/idebugprogram2-detach.md)|このプログラムからデバッガをデタッチします。|
|[GetProgramId](../../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)|このプログラムのグローバル一意識別子を取得します。|
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugprogram2-getdebugproperty.md)|プログラムのプロパティを取得します。|
|[実行](../../../extensibility/debugger/reference/idebugprogram2-execute.md)|停止状態からこのプログラムを実行し続けます。 以前の実行状態はすべてクリアされます。|
|[続行](../../../extensibility/debugger/reference/idebugprogram2-continue.md)|停止状態からこのプログラムを実行し続けます。 以前の実行状態は保持されます。|
|[Step](../../../extensibility/debugger/reference/idebugprogram2-step.md)|ステップを実行します。|
|[CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)|このプログラムが、次にそのスレッドの 1 つがコードを実行する時に実行を停止することを要求します。|
|[GetEngineInfo](../../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md)|このプログラムを実行しているデバッグ エンジン (DE) の名前と識別子を取得します。|
|[EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)|ソース ファイル内の指定した位置のコード コンテキストを列挙します。|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)|このプログラムのメモリ バイトを取得します。|
|[GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)|このプログラムまたはこのプログラムの一部の逆アセンブリ ストリームを取得します。|
|[EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)|このプログラムが読み込んで実行しているモジュールを列挙します。|
|[GetENCUpdate](../../../extensibility/debugger/reference/idebugprogram2-getencupdate.md)|このプログラムのエディット コンティニュ (ENC) 更新プログラムを取得します。<br /><br /> カスタム デバッグ エンジンは、このメソッドを実装しません (`E_NOTIMPL`常に返す必要があります)。|
|[EnumCodePaths](../../../extensibility/debugger/reference/idebugprogram2-enumcodepaths.md)|このプログラムのコード パスを列挙します。|
|[WriteDump](../../../extensibility/debugger/reference/idebugprogram2-writedump.md)|ダンプをファイルに書き込みます。|

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="remarks"></a>Remarks
 プログラムは、特定のランタイム アーキテクチャで実行されるスレッド コンテナーであり、プロセスは 1 つ以上のプログラムで構成されます。

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)
- [次へ](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)
- [Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)
