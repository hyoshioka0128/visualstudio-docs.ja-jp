---
title: 起動後のスタートアップイベントの送信 |Microsoft Docs
description: デバッグエンジンがプログラムにアタッチされた後にデバッグエンジンからデバッグセッションに送信される一連のスタートアップイベントについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], startup events
ms.assetid: 306ea0b4-6d9e-4871-8d8d-a4032d422940
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 227d863df1e3318d2df6be6a24aaf05b5033e92d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070401"
---
# <a name="send-startup-events-after-a-launch"></a>起動後にスタートアップイベントを送信する
デバッグエンジン (DE) がプログラムにアタッチされると、一連のスタートアップイベントがデバッグセッションに返されます。

 デバッグセッションに返されるスタートアップイベントには次のものがあります。

- エンジン作成イベント。

- プログラム作成イベント。

- スレッド作成イベントとモジュール読み込みイベント。

- 読み込み完了イベント。コードが読み込まれ、実行の準備ができたときに、コードが実行される前に送信されます。

  > [!NOTE]
  > このイベントが続行されると、グローバル変数が初期化され、スタートアップルーチンが実行されます。

- 他のスレッド作成イベントとモジュール読み込みイベント。

- エントリポイントイベント。プログラム **がメインの** エントリポイントに到達したことを通知し `WinMain` ます。 このイベントは、通常、既に実行されているプログラムに DE をアタッチした場合には送信されません。

  プログラムによって、DE は最初にセッションデバッグマネージャー (SDM) の [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) インターフェイスを送信します。このインターフェイスはエンジン作成イベントを表し、その後にプログラム作成イベントを表す [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)が続きます。

  これらのイベントの後には、通常、1つ以上の [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) thread 作成イベントと [IDebugModuleLoadEvent2](../../extensibility/debugger/reference/idebugmoduleloadevent2.md) モジュール読み込みイベントが続きます。

  コードが読み込まれ、実行の準備が整うと、コードが実行される前に、DE は SDM a [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) load complete イベントを送信します。 最後に、プログラムがまだ実行されていない場合、DE は [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) entry point イベントを送信し、プログラムがメインエントリポイントに到達し、デバッグの準備ができたことを通知します。

## <a name="see-also"></a>こちらもご覧ください
- [実行の制御](../../extensibility/debugger/control-of-execution.md)
- [デバッグタスク](../../extensibility/debugger/debugging-tasks.md)
