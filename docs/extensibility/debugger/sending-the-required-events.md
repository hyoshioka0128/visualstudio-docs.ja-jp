---
title: 必要なイベントを送信する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], required events
ms.assetid: 08319157-43fb-44a9-9a63-50b919fe1377
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cc83b47e53607fe1111ececbbf892c96f7bbb639
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712996"
---
# <a name="send-the-required-events"></a>必要なイベントを送信する
必要なイベントを送信するには、次の手順を使用します。

## <a name="process-for-sending-required-events"></a>必要なイベントを送信するプロセス
 デバッグ エンジン (DE) を作成し、プログラムにアタッチする場合は、次のイベントが、この順序で必要です。

1. DE がプロセス内の 1 つ以上のプログラムをデバッグするために初期化されている場合は、セッション デバッグ マネージャー (SDM) に[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)イベント オブジェクトを送信します。

2. デバッグ対象のプログラムがアタッチされている場合は、イベント[オブジェクトを](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)SDM に送信します。 このイベントは、エンジンの設計によっては停止イベントになる場合があります。

3. プロセスの起動時にプログラムがアタッチされている場合は、新しいスレッドを IDE に通知する[IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)イベント オブジェクトを SDM に送信します。 このイベントは、エンジンの設計によっては停止イベントになる場合があります。

4. デバッグ中のプログラムの読み込みが完了したとき、またはプログラムへのアタッチが完了したときに[、IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)イベント オブジェクトを SDM に送信します。 このイベントは停止イベントである必要があります。

5. デバッグ対象のアプリケーションが起動された場合は、ランタイム アーキテクチャ内のコードの最初の命令が実行されるときに[、IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)イベント オブジェクトを SDM に送信します。 このイベントは常に停止イベントです。 デバッグ セッションにステップ インすると、IDE はこのイベントで停止します。

> [!NOTE]
> 多くの言語では、コードの先頭にグローバル初期化子または外部のコンパイル済み関数 (CRT ライブラリまたは_Main) を使用します。 デバッグするプログラムの言語に、最初のエントリ ポイントの前にこれらの種類の要素のいずれかが含まれている場合、このコードが実行され、ユーザー エントリ ポイント **(main**または`WinMain`など) に達したときにエントリ ポイント イベントが送信されます。

## <a name="see-also"></a>関連項目
- [プログラムのデバッグの有効化](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
