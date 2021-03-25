---
title: 操作モード |Microsoft Docs
description: IDE が動作する3つのモード (デザインモード、実行モード、中断モード) について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, modes
ms.assetid: f69972d0-809d-40df-9da3-04738791391c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 563db644069731c5d74088dadf296933c36b0cc1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067843"
---
# <a name="operational-modes"></a>操作モード
IDE が動作できるモードには、次の3つがあります。

- [デザインモード](#vsconoperationalmodesanchor1)

- [実行モード](#vsconoperationalmodesanchor2)

- [中断モード](#vsconoperationalmodesanchor3)

  これらのモード間でのカスタムデバッグエンジン (DE) の遷移方法は、移行メカニズムについて理解しておく必要がある実装上の決定です。 これらのモードは、DE によって直接実装される場合とない場合があります。 これらのモードは、ユーザーの操作または DE からのイベントに基づいて切り替える、実際にデバッグするパッケージモードです。 たとえば、実行モードから中断モードへの切り替えは、DE からの停止イベントによって指定されます。 中断から実行モードまたはステップモードへの移行は、ステップ実行や実行などの操作を実行するユーザーによって指定されます。 逆遷移の詳細については、「 [実行の制御](../../extensibility/debugger/control-of-execution.md)」を参照してください。

## <a name="design-mode"></a><a name="vsconoperationalmodesanchor1"></a> デザインモード
 デザインモードは、Visual Studio のデバッグの実行されていない状態です。その間、アプリケーションでデバッグ機能を設定できます。

 デザインモードでは、いくつかのデバッグ機能しか使用されません。 開発者は、ブレークポイントを設定するか、ウォッチ式を作成することができます。 IDE がデザインモードの間は、DE が読み込まれたり呼び出されたりすることはありません。 実行モードと中断モードでの相互作用は、実行モードと中断モードでのみ行われます。

## <a name="run-mode"></a><a name="vsconoperationalmodesanchor2"></a> 実行モード
 実行モードは、IDE のデバッグセッションでプログラムが実行されたときに発生します。 アプリケーションは、終了するまで、ブレークポイントがヒットするまで、または例外がスローされるまで実行されます。 アプリケーションが終了すると、デザインモードに切り替えます。 ブレークポイントにヒットしたとき、または例外がスローされた場合、DE は中断モードに遷移します。

## <a name="break-mode"></a><a name="vsconoperationalmodesanchor3"></a> 中断モード
 中断モードは、デバッグプログラムの実行が中断されたときに発生します。 中断モードでは、開発者は中断時にアプリケーションのスナップショットを提供し、開発者はアプリケーションの状態を分析し、アプリケーションの実行方法を変更できます。 開発者は、コードの表示と編集、データの検査または変更、アプリケーションの再起動、実行の終了、または同じポイントからの実行の継続を行うことができます。

 中断モードは、DE が同期停止イベントを送信するときに入力されます。 同期停止イベントは、イベントの停止とも呼ばれ、セッションデバッグマネージャー (SDM) に通知し、デバッグ中のアプリケーションがコードの実行を停止したことを IDE に通知します。 [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)インターフェイスと[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)インターフェイスは、イベントを停止する例です。

 停止イベントは、次のいずれかのメソッドを呼び出すことで継続されます。これにより、デバッガーが中断モードから実行モードまたはステップモードに遷移します。

- [実行](../../extensibility/debugger/reference/idebugprocess3-execute.md)

- [Step](../../extensibility/debugger/reference/idebugprocess3-step.md)

- [続行](../../extensibility/debugger/reference/idebugprocess3-continue.md)

### <a name="step-mode"></a><a name="vsconoperationalmodesanchor4"></a> ステップモード
 ステップモードは、プログラムが次のコード行、または関数の内外にステップインするときに発生します。 ステップは、メソッドの [ステップ](../../extensibility/debugger/reference/idebugprocess3-step.md)を呼び出すことによって実行されます。 このメソッド `DWORD` には、入力パラメーターとして [stepunit](../../extensibility/debugger/reference/stepunit.md) および [stepunit](../../extensibility/debugger/reference/stepkind.md) 列挙体を指定するが必要です。

 プログラムが次のコード行または関数にステップインした場合、またはカーソルまたは設定されたブレークポイントまで実行された場合、DE は自動的に中断モードに戻ります。

## <a name="see-also"></a>こちらもご覧ください
- [実行の制御](../../extensibility/debugger/control-of-execution.md)
