---
title: デバッガーを起動しています |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], launching the debugger
- debugger [Debugging SDK], launching
ms.assetid: f24da1a1-f923-48b4-989f-18a22b581d1b
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e9c57079246dd52bd7fb44371999d0c3747dad40
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68149125"
---
# <a name="launching-the-debugger"></a>デバッガーの起動
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッガーを起動するには、適切な属性を使用してメソッドとイベントの正しいシーケンスを送信する必要があります。  
  
## <a name="sequences-of-methods-and-events"></a>メソッドとイベントのシーケンス  
  
1. セッションデバッグマネージャー (SDM) を呼び出すには、[ **デバッグ** ] メニューを選択し、[ **開始**] をクリックします。 詳細について [は、「プログラムの起動](../../extensibility/debugger/launching-a-program.md) 」を参照してください。  
  
2. SDM は [Onattach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) メソッドを呼び出します。  
  
3. デバッグエンジン (DE) プロセスモデルに基づいて、 `IDebugProgramNodeAttach2::OnAttach` メソッドは次のいずれかのメソッドを返します。これにより次の処理が決定されます。  
  
     が返された場合 `S_FALSE` 、デバッグエンジン (DE) は仮想マシンのプロセスで読み込まれます。  
  
     \- または -  
  
     が返された場合 `S_OK` 、DE は SDM のインプロセスで読み込まれます。 その後、SDM は次のタスクを実行します。  
  
    1. [GetEngineInfo](../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)を呼び出して、DE のエンジン情報を取得します。  
  
    2. DE を共同作成します。  
  
    3. [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md)を呼び出します。  
  
4. DE は、属性を使用して [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) を SDM に送信し `EVENT_SYNC` ます。  
  
5. DE は、属性を使用して [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) を SDM に送信し `EVENT_SYNC` ます。  
  
6. DE は、属性を使用して [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) を SDM に送信し `EVENT_SYNC` ます。  
  
7. DE は、属性を使用して [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) を SDM に送信し `EVENT_SYNC` ます。  
  
8. DE は、属性を使用して [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) を SDM に送信し `EVENT_SYNC` ます。  
  
## <a name="see-also"></a>参照  
 [呼び出し (デバッガーイベントを)](../../extensibility/debugger/calling-debugger-events.md)   
 [プログラムの起動](../../extensibility/debugger/launching-a-program.md)
