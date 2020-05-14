---
title: 起動後のスタートアップ イベントの送信 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], startup events
ms.assetid: 306ea0b4-6d9e-4871-8d8d-a4032d422940
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c71db002420a2b822bffd34f2ae05e712f6a4bb9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713010"
---
# <a name="send-startup-events-after-a-launch"></a>起動後にスタートアップ イベントを送信する
デバッグ エンジン (DE) がプログラムにアタッチされると、一連のスタートアップ イベントがデバッグ セッションに送り返されます。

 デバッグ セッションに返されるスタートアップ イベントには、次のものがあります。

- エンジン作成イベント。

- プログラム作成イベント。

- スレッドの作成とモジュールの読み込みイベント。

- ロード完了イベント。

  > [!NOTE]
  > このイベントが続くと、グローバル変数が初期化され、スタートアップ ルーチンが実行されます。

- 他のスレッド作成イベントおよびモジュールロードイベントが発生する可能性があります。

- Main**や**`WinMain`など、メイン エントリ ポイントに達したことを示すエントリ ポイント イベントです。 このイベントは、既に実行中のプログラムに DE がアタッチされている場合、通常は送信されません。

  プログラムを使用して、DE はまず、エンジン作成イベントを表すセッション デバッグ マネージャー (SDM) [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)インターフェイスを送信し、次にプログラム作成イベントを表す[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)を送信します。

  通常、これらのイベントの後には、1 つ以上[の IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)スレッド作成イベントと[IDebugModuleLoadEvent2](../../extensibility/debugger/reference/idebugmoduleloadevent2.md)モジュールの読み込みイベントが続きます。

  コードが読み込まれ、実行する準備が整っているとき、コードが実行される前に、DE は SDM を[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)読み込み完了イベントを送信します。 最後に、プログラムがまだ実行されていない場合、DE は[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)エントリ ポイント イベントを送信し、プログラムがメイン エントリ ポイントに到達し、デバッグの準備ができていることを示します。

## <a name="see-also"></a>関連項目
- [実行の制御](../../extensibility/debugger/control-of-execution.md)
- [デバッグ タスク](../../extensibility/debugger/debugging-tasks.md)
