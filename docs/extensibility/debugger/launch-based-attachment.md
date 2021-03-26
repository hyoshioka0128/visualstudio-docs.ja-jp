---
title: 起動ベースの添付ファイル |Microsoft Docs
description: プログラムへの起動ベースの添付ファイルについて説明します。プログラムは自動で、手動添付ファイルのようなパスに従います。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, launching
- debug engines, attaching to programs
ms.assetid: 362f00ac-1909-4a3a-bacb-c0ceb5549816
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fe698d8d1b29f02ae3971fc95a66c4823f7252c7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059718"
---
# <a name="launch-based-attachment"></a>起動ベースの添付ファイル
プログラムへの起動に基づく添付ファイルは自動的に実行されます。 プログラムをホストするプロセスが SDM によって起動されると、起動ベースの添付ファイルは、手動添付メソッドと同様のパスに従います。 詳細については、「 [プログラムへのアタッチ](../../extensibility/debugger/attaching-to-the-program.md)」を参照してください。

## <a name="the-attaching-process"></a>アタッチプロセス
 主な違いは、次のように、 **アタッチ** 呼び出しの後のイベントのシーケンスです。

1. **IDebugEngineCreateEvent2** イベントオブジェクトを SDM に送信します。 詳細については、「 [イベントの送信](../../extensibility/debugger/sending-events.md)」を参照してください。

2. `IDebugProgram2::GetProgramId` **Attach** メソッドに渡された **IDebugProgram2** インターフェイスでメソッドを呼び出します。

3. **IDebugProgramCreateEvent2** イベントオブジェクトを送信して、ローカルの **IDebugProgram2** オブジェクトが作成されたことを SDM に通知します。

4. [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)イベントオブジェクトを送信して、起動したプロセスに対して新しいスレッドが作成されたことを SDM に通知します。

## <a name="see-also"></a>こちらもご覧ください
- [必要なイベントを送信する](../../extensibility/debugger/sending-the-required-events.md)
- [プログラムのデバッグを有効にする](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
