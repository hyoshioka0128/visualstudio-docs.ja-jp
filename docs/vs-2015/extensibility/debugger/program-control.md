---
title: プログラムの制御 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], control of execution
ms.assetid: 6be80904-e66c-4cae-8891-1113b799fb01
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8102bc488d5c74f751fb93584016aa6904fbe2d9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841677"
---
# <a name="program-control"></a>プログラムの制御
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio のデバッグでは、次のステップ実行ルーチンと続行ルーチンがすべてプログラムレベルで実行されます。  
  
- 次のステートメントを設定します。つまり、特定のフレーム環境で実行される次の命令にコンピューターを設定します。  
  
- を実行しています。つまり、ステップモードを終了し続けます。  
  
- 次の手順にステップインする  
  
- 現在のステップ実行モードを続行しています  
  
- プログラムに含まれるスレッドの中断  
  
- プログラムに含まれるスレッドの再開  
  
> [!NOTE]
> 呼び出し履歴の表示は、スレッドレベルで実装されます。 スレッドの呼び出し履歴を表示するときにフレーム情報を列挙するには、 [IEnumDebugFrameInfo2](../../extensibility/debugger/reference/ienumdebugframeinfo2.md) インターフェイスのすべてのメソッドを実装する必要があります。  
  
## <a name="methods-of-program-control"></a>プログラムコントロールのメソッド  
 次の表は、最小限の機能デバッグエンジン (DE) と実行制御のために実装する必要がある [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) のメソッドを示しています。  
  
|メソッド|説明|  
|------------|-----------------|  
|[IDebugProgram2::Execute](../../extensibility/debugger/reference/idebugprogram2-execute.md)|プログラムに含まれるすべてのスレッドの実行を停止状態から続行します。 実行コントロールに必要です。|  
|[IDebugProgram2::Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md)|プログラムに含まれるすべてのスレッドの実行を停止状態から続行します。 実行コントロールに必要です。|  
|[IDebugProgram2::Step](../../extensibility/debugger/reference/idebugprogram2-step.md)|指定されたスレッドでステップを実行します。 プログラムに含まれる他のすべてのスレッドの実行を続行します。 実行コントロールに必要です。|  
  
 マルチスレッドプログラムの場合は、 [IDebugProgram2:: EnumThreads](../../extensibility/debugger/reference/idebugprogram2-enumthreads.md) メソッドと [IEnumDebugThreads2](../../extensibility/debugger/reference/ienumdebugthreads2.md) インターフェイスのすべてのメソッドを実装する必要もあります。  
  
## <a name="see-also"></a>参照  
 [実行の制御と状態の評価](../../extensibility/debugger/execution-control-and-state-evaluation.md)
