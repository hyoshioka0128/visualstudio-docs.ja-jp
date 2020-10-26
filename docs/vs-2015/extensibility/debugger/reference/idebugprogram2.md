---
title: IDebugProgram2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgram2
helpviewer_keywords:
- IDebugProgram2 interface
ms.assetid: 8d73df73-cfff-4b8b-b426-d6051edb1939
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 372c119b6a841d7d4b349e85548914f7641b53d1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148640"
---
# <a name="idebugprogram2"></a>IDebugProgram2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、プロセスで実行されているプログラムを表します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugProgram2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 デバッグエンジン (DE) とカスタムポート供給業者は、プロセス内のプログラムを表すために、このインターフェイスを実装します。 また、セッションデバッグマネージャー (SDM) は、このインターフェイスを実装して、 [アタッチ](../../../extensibility/debugger/reference/idebugprogram2-attach.md)する情報を提供します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)イベントは、新しいプログラムに対してこのインターフェイスを返します。 このインターフェイスは、複数のインターフェイスの多くのメソッドのパラメーターとしても使用されます。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDebugProgram2` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)|このプログラムで実行されているスレッドを列挙します。|  
|[GetName](../../../extensibility/debugger/reference/idebugprogram2-getname.md)|プログラムの名前を取得します。|  
|[GetProcess](../../../extensibility/debugger/reference/idebugprogram2-getprocess.md)|このプログラムが実行されているプロセスを取得します。|  
|[Terminate](../../../extensibility/debugger/reference/idebugprogram2-terminate.md)|このプログラムを終了します。|  
|[[アタッチ]](../../../extensibility/debugger/reference/idebugprogram2-attach.md)|このプログラムにアタッチします。|  
|[CanDetach](../../../extensibility/debugger/reference/idebugprogram2-candetach.md)|デバッグエンジン (DE) をプログラムからデタッチできるかどうかを決定します。|  
|[[デタッチ]](../../../extensibility/debugger/reference/idebugprogram2-detach.md)|このプログラムからデバッガーをデタッチします。|  
|[GetProgramId](../../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)|このプログラムのグローバル一意識別子を取得します。|  
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugprogram2-getdebugproperty.md)|プログラムのプロパティを取得します。|  
|[実行](../../../extensibility/debugger/reference/idebugprogram2-execute.md)|このプログラムの実行を停止状態から続行します。 以前の実行状態はすべて消去されます。|  
|[続行](../../../extensibility/debugger/reference/idebugprogram2-continue.md)|このプログラムの実行を停止状態から続行します。 以前の実行状態は保持されます。|  
|[Step](../../../extensibility/debugger/reference/idebugprogram2-step.md)|ステップを実行します。|  
|[CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)|次にそのスレッドの1つがコードを実行したときに、このプログラムの実行を停止するように要求します。|  
|[GetEngineInfo](../../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md)|このプログラムを実行しているデバッグエンジン (DE) の名前と識別子を取得します。|  
|[EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)|ソースファイル内の指定された位置のコードコンテキストを列挙します。|  
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)|このプログラムのメモリのバイト数を取得します。|  
|[GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)|このプログラムまたはこのプログラムの一部の逆アセンブリストリームを取得します。|  
|[EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)|このプログラムによって読み込まれ、実行されているモジュールを列挙します。|  
|[GetENCUpdate](../../../extensibility/debugger/reference/idebugprogram2-getencupdate.md)|このプログラムのエディットコンティニュ (ENC) 更新プログラムを取得します。<br /><br /> カスタムデバッグエンジンは、このメソッドを実装しません (常にを返す必要があり `E_NOTIMPL` ます)。|  
|[EnumCodePaths](../../../extensibility/debugger/reference/idebugprogram2-enumcodepaths.md)|このプログラムのコードパスを列挙します。|  
|[WriteDump](../../../extensibility/debugger/reference/idebugprogram2-writedump.md)|ダンプをファイルに書き込みます。|  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="remarks"></a>注釈  
 プログラムは、特定の実行時アーキテクチャで実行されるスレッドコンテナーであり、プロセスは1つ以上のプログラムで構成されます。  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)   
 [次に](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)   
 [場合](../../../extensibility/debugger/reference/idebugportevents2-event.md)   
 [外付け](../../../extensibility/debugger/reference/idebugengine2-attach.md)   
 [DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)   
 [場合](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)   
 [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)
