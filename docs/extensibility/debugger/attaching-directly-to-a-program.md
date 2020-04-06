---
title: プログラムに直接アタッチする |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: ad2b7db8-821c-440c-ba07-c55c6a395e0f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8a9a5699ee81b8c8ae36bcf492e93467615a9e89
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739254"
---
# <a name="attach-directly-to-a-program"></a>プログラムに直接アタッチする
既に実行されているプロセスでプログラムをデバッグするユーザーは、通常、次のプロセスに従います。

1. IDE で、[ツール] メニューの [**プロセスのデバッグ**] を**クリック**します。

    **[プロセス]** ダイアログ ボックスが表示されます。

2. プロセスを選択し、[**アタッチ**]ボタンをクリックします。

    [**プロセスにアタッチ]** ダイアログ ボックスが表示され、コンピュータにインストールされているすべてのデバッグ エンジン (D) が一覧表示されます。

3. 選択したプロセスのデバッグに使用する DEs を指定し **、[OK]** をクリックします。

   デバッグ パッケージはデバッグ セッションを開始し、DEs のリストをそのセッションに渡します。 デバッグ セッションは、コールバック関数と共にこのリストを選択したプロセスに渡し、実行中のプログラムを列挙するようにプロセスに要求します。

   プログラムを使用して、ユーザーの要求に応答して、デバッグ パッケージはセッション デバッグ マネージャー (SDM) をインスタンス化し、選択した DEs の一覧を渡します。 リストと共に、デバッグ パッケージは SDM を[IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md)インターフェイスに渡します。 デバッグ パッケージは[、IDebugProcess2::Attach](../../extensibility/debugger/reference/idebugprocess2-attach.md)を呼び出すことによって、選択したプロセスに DEs の一覧を渡します。 SDM は、次に、ポート上で[IDebugProcess2::EnumPrograms を](../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)呼び出して、プロセスで実行されているプログラムを列挙します。

   この時点から、各デバッグ エンジンは、2 つの例外を除き、[起動後のアタッチ](../../extensibility/debugger/attaching-after-a-launch.md)で詳しく説明されているプログラムにアタッチされます。

   効率を高めるために、アドレス・スペースを SDM と共有するために実装された DE は、各 DE が接続先のプログラムのセットを持つようにグループ化されます。 この場合[、IDebugProcess2 は](../../extensibility/debugger/reference/idebugprocess2.md) [IDebugEngine2:::Attach](../../extensibility/debugger/reference/idebugengine2-attach.md)を呼び出し、アタッチするプログラムの配列を渡します。

   2 つ目の例外は、既に実行中のプログラムにアタッチする DE によって送信されるスタートアップ イベントには、通常はエントリ ポイント イベントが含まれていないことです。

## <a name="see-also"></a>関連項目
- [起動後のスタートアップ イベントの送信](../../extensibility/debugger/sending-startup-events-after-a-launch.md)
- [デバッグ タスク](../../extensibility/debugger/debugging-tasks.md)
