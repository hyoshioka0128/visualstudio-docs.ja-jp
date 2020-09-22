---
title: 必要なイベントを送信する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], required events
ms.assetid: 08319157-43fb-44a9-9a63-50b919fe1377
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 457e2daf3e52c23ba9733d09d3aeb94750b5fab9
ms.sourcegitcommit: fb8babf5cd72f1fc2f97ffe4ad7b62d91f325f61
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2020
ms.locfileid: "90842217"
---
# <a name="sending-the-required-events"></a>必要なイベントの送信
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

必要なイベントを送信するには、次の手順に従います。  
  
## <a name="process-for-sending-required-events"></a>必要なイベントを送信するためのプロセス  
 デバッグエンジン (DE) を作成してプログラムにアタッチするときは、次のイベントがこの順序で必要になります。  
  
1. プロセス内の1つまたは複数のプログラムをデバッグするために DE を初期化するときに、 [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) イベントオブジェクトをセッションデバッグマネージャー (SDM) に送信します。  
  
2. デバッグ対象のプログラムがにアタッチされている場合は、 [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) イベントオブジェクトを SDM に送信します。 このイベントは、エンジンの設計によっては停止イベントである可能性があります。  
  
3. プロセスが起動されたときにプログラムがにアタッチされている場合は、 [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) イベントオブジェクトを SDM に送信して、新しいスレッドを IDE に通知します。 このイベントは、エンジンの設計によっては停止イベントである可能性があります。  
  
4. デバッグ中のプログラムの読み込みが終了したとき、またはプログラムへのアタッチが完了したときに、 [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) イベントオブジェクトを SDM に送信します。 このイベントは、停止イベントである必要があります。  
  
5. デバッグ対象のアプリケーションが起動された場合は、実行時アーキテクチャのコードの最初の命令が実行されるときに、 [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) イベントオブジェクトを SDM に送信します。 このイベントは、常に停止イベントです。 デバッグセッションにステップインすると、IDE はこのイベントを停止します。  
  
> [!NOTE]
> 多くの言語では、コードの先頭でグローバル初期化子または外部プリコンパイル済み関数 (CRT ライブラリまたは _Main) が使用されます。 デバッグしているプログラムの言語に、最初のエントリポイントの前にこれらの種類の要素のいずれかが含まれている場合は、このコードが実行され、 **main** やなどのユーザーエントリポイントに達したときに、エントリポイントイベントが送信され `WinMain` ます。  
  
## <a name="see-also"></a>参照  
 [デバッグするプログラムの有効化](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
