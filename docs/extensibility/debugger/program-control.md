---
title: プログラムコントロール |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], control of execution
ms.assetid: 6be80904-e66c-4cae-8891-1113b799fb01
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4e77e233050c5ce10aef5053f82c8d26cb984b85
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738230"
---
# <a name="program-control"></a>プログラム制御
Visual Studio のデバッグでは、次のステップ実行と継続ルーチンはすべてプログラム レベルで実行されます。

- 次のステートメントを設定する、つまり、特定のフレーム環境で実行される次の命令にコンピュータを設定する

- 実行、つまり、ステッピング・モードから終了し続ける

- 次の命令に進む

- 現在のステッピング モードを続行する

- プログラムに含まれるスレッドを中断する

- プログラムに含まれるスレッドの再開

> [!NOTE]
> 呼び出し履歴の表示は、スレッド レベルで実装されます。 スレッドの呼び出し履歴を表示するときにフレーム情報を列挙するには[、IEnumDebugFrameInfo2](../../extensibility/debugger/reference/ienumdebugframeinfo2.md)インターフェイスのすべてのメソッドを実装する必要があります。

## <a name="methods-of-program-control"></a>プログラム制御の方法
 次の表は、最小限の機能を持つデバッグ エンジン (DE) と実行制御に対して実装する必要がある[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)のメソッドを示しています。

|Method|説明|
|------------|-----------------|
|[IDebugProgram2::Execute](../../extensibility/debugger/reference/idebugprogram2-execute.md)|停止状態からプログラムに含まれるすべてのスレッドの実行を続行します。 実行制御に必要です。|
|[IDebugProgram2::Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md)|停止状態からプログラムに含まれるすべてのスレッドの実行を続行します。 実行制御に必要です。|
|[IDebugProgram2::Step](../../extensibility/debugger/reference/idebugprogram2-step.md)|指定したスレッドに対してステップを実行します。 プログラムに含まれる他のすべてのスレッドの実行を続行します。 実行制御に必要です。|

 マルチスレッド プログラムの場合は[、IDebugProgram2::EnumThreads](../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)メソッドと[IEnumDebugThreads2](../../extensibility/debugger/reference/ienumdebugthreads2.md)インターフェイスのすべてのメソッドも実装する必要があります。

## <a name="see-also"></a>関連項目
- [実行制御と状態評価](../../extensibility/debugger/execution-control-and-state-evaluation.md)
