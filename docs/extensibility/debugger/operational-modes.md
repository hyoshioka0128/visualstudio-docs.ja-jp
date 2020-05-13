---
title: 操作モード |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, modes
ms.assetid: f69972d0-809d-40df-9da3-04738791391c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 027152b2b2fc18b509a687220e5d963ea1b7e721
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738287"
---
# <a name="operational-modes"></a>運用モード
IDE が動作するモードは、次の 3 種類あります。

- [デザインモード](#vsconoperationalmodesanchor1)

- [実行モード](#vsconoperationalmodesanchor2)

- [ブレークモード](#vsconoperationalmodesanchor3)

  カスタム デバッグ エンジン (DE) がこれらのモード間で移行する方法は、移行メカニズムに精通する必要がある実装の決定です。 DE はこれらのモードを直接実装する場合と実装しない場合があります。 これらのモードは、ユーザーアクションまたは DE からのイベントに基づいて切り替える実際のデバッグ パッケージ モードです。 たとえば、実行モードから中断モードへの移行は、DE からの停止イベントによって起動されます。 中断モードから実行モードまたはステップ モードへの移行は、ステップや実行などの操作を実行するユーザーによって起動されます。 DE 遷移の詳細については、「[実行の制御](../../extensibility/debugger/control-of-execution.md)」を参照してください。

## <a name="design-mode"></a><a name="vsconoperationalmodesanchor1"></a>デザインモード
 デザイン モードは Visual Studio デバッグの実行されていない状態で、その間、アプリケーションでデバッグ機能を設定できます。

 デザイン モードでは、いくつかのデバッグ機能しか使用されません。 開発者は、ブレークポイントを設定するか、ウォッチ式を作成するかを選択できます。 IDE がデザイン モードの間、DE が読み込まれたり呼び出されたりすることはありません。 DE との相互作用は、実行モードとブレーク モードの間のみ行われます。

## <a name="run-mode"></a><a name="vsconoperationalmodesanchor2"></a>実行モード
 実行モードは、プログラムが IDE のデバッグ セッションで実行されるときに発生します。 アプリケーションは、ブレークポイントがヒットするまで、または例外がスローされるまで、終了するまで実行されます。 アプリケーションが終了に実行されると、DE はデザイン モードに移行します。 ブレークポイントにヒットするか、例外がスローされると、DE はブレーク モードに移行します。

## <a name="break-mode"></a><a name="vsconoperationalmodesanchor3"></a>ブレークモード
 中断モードは、デバッグプログラムの実行が中断されたときに発生します。 中断モードは、中断時のアプリケーションのスナップショットを開発者に提供し、開発者はアプリケーションの状態を分析し、アプリケーションの実行方法を変更できるようにします。 開発者は、コードの表示と編集、データの検査または変更、アプリケーションの再起動、実行の終了、または同じポイントからの実行の継続を行うことができます。

 DE が同期停止イベントを送信すると、中断モードが入力されます。 同期停止イベント (停止イベントとも呼ばれます) は、デバッグ中のアプリケーションがコードの実行を停止したことをセッションデバッグ マネージャー (SDM) と IDE に通知します。 イベントを停止する例として[、IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)および[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)インターフェイスが表示されます。

 停止イベントは、次のいずれかのメソッドの呼び出しによって継続され、デバッガーが中断モードから実行またはステップ モードに移行します。

- [実行](../../extensibility/debugger/reference/idebugprocess3-execute.md)

- [Step](../../extensibility/debugger/reference/idebugprocess3-step.md)

- [続行](../../extensibility/debugger/reference/idebugprocess3-continue.md)

### <a name="step-mode"></a><a name="vsconoperationalmodesanchor4"></a>ステップモード
 ステップ モードは、プログラムが次のコード行に進むか、関数の中に入るか、関数から抜け出すかを示すときに発生します。 ステップは、メソッド[Step](../../extensibility/debugger/reference/idebugprocess3-step.md)を呼び出して実行されます。 このメソッドでは`DWORD`、入力パラメーターとして[STEPUNIT](../../extensibility/debugger/reference/stepunit.md)列挙体と[STEPKIND](../../extensibility/debugger/reference/stepkind.md)列挙体を指定する s が必要です。

 プログラムが正常にコードの次の行または関数にステップインするか、またはカーソルまたは設定されたブレークポイントに実行されると、DE は自動的にブレーク モードに戻ります。

## <a name="see-also"></a>関連項目
- [実行の制御](../../extensibility/debugger/control-of-execution.md)
