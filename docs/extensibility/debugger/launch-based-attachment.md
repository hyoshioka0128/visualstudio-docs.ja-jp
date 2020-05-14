---
title: 起動ベースの添付ファイル |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, launching
- debug engines, attaching to programs
ms.assetid: 362f00ac-1909-4a3a-bacb-c0ceb5549816
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4910a97350366500b56593ec0076fdf0990b6d8f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738459"
---
# <a name="launch-based-attachment"></a>起動ベースの添付ファイル
プログラムへの起動ベースの添付ファイルは自動的に行われます。 プログラムをホストするプロセスが SDM によって起動されると、起動ベースの添付ファイルは手動添付方式と同様のパスに従います。 詳細については、[プログラムへのアタッチを](../../extensibility/debugger/attaching-to-the-program.md)参照してください。

## <a name="the-attaching-process"></a>アタッチプロセス
 主な違いは、**次のように、Attach**呼び出しに続く一連のイベントです。

1. **イベント**オブジェクトを SDM に送信します。 詳細については、[イベントの送信](../../extensibility/debugger/sending-events.md)を参照してください。

2. メソッドを`IDebugProgram2::GetProgramId`呼び出す **、 IDebugProgram2**インターフェイスに**渡すメソッドに渡**します。

3. **イベント**オブジェクトを送信して、プログラムを DE に表すためにローカル**IDebugProgram2**オブジェクトが作成されたことを SDM に通知します。

4. イベント[オブジェクトを送信](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)して、起動したプロセスに対して新しいスレッドが作成されたことを SDM に通知します。

## <a name="see-also"></a>関連項目
- [必要なイベントを送信する](../../extensibility/debugger/sending-the-required-events.md)
- [プログラムのデバッグを有効にする](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
