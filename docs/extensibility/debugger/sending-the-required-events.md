---
title: 必要なイベントを送信する |Microsoft Docs
description: デバッグエンジンを作成し、Visual Studio のデバッグでプログラムにアタッチするときに必要な順序付けされたイベントについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], required events
ms.assetid: 08319157-43fb-44a9-9a63-50b919fe1377
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a53f4d7a89b1f5902f576490d827148e9fb816bf
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070376"
---
# <a name="send-the-required-events"></a>必要なイベントを送信する
必要なイベントを送信するには、次の手順に従います。

## <a name="process-for-sending-required-events"></a>必要なイベントを送信するためのプロセス
 デバッグエンジン (DE) を作成してプログラムにアタッチするときは、次のイベントがこの順序で必要になります。

1. プロセス内の1つまたは複数のプログラムをデバッグするために DE を初期化するときに、 [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) イベントオブジェクトをセッションデバッグマネージャー (SDM) に送信します。

2. デバッグ対象のプログラムがにアタッチされている場合は、 [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) イベントオブジェクトを SDM に送信します。 このイベントは、エンジンの設計によっては停止イベントである可能性があります。

3. プロセスが起動されたときにプログラムがにアタッチされている場合は、 [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) イベントオブジェクトを SDM に送信して、新しいスレッドを IDE に通知します。 このイベントは、エンジンの設計によっては停止イベントである可能性があります。

4. デバッグ中のプログラムの読み込みが終了したとき、またはプログラムへのアタッチが完了したときに、 [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) イベントオブジェクトを SDM に送信します。 このイベントは、停止イベントである必要があります。

5. デバッグ対象のアプリケーションが起動された場合は、実行時アーキテクチャのコードの最初の命令が実行されるときに、 [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) イベントオブジェクトを SDM に送信します。 このイベントは、常に停止イベントです。 デバッグセッションにステップインすると、IDE はこのイベントを停止します。

> [!NOTE]
> 多くの言語では、コードの先頭でグローバル初期化子または外部プリコンパイル済み関数 (CRT ライブラリまたは _Main) が使用されます。 デバッグ中のプログラムの言語に、初期エントリポイントの前にこれらの種類の要素のいずれかが含まれている場合、このコードが実行され、 **main** やなどのユーザーエントリポイントに到達すると、エントリポイントイベントが送信され `WinMain` ます。

## <a name="see-also"></a>関連項目
- [プログラムのデバッグを有効にする](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
