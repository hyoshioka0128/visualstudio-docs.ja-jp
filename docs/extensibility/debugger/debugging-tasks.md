---
title: タスクのデバッグ |Microsoft Docs
ms.date: 11/04/2016
ms.topic: overview
helpviewer_keywords:
- debugging [Debugging SDK], tasks
ms.assetid: 5d60e9e8-305e-4a48-829f-b9440fc8af7b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 070068853d962bdf9b209edb9410d33d46ccf853
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903561"
---
# <a name="debug-tasks"></a>デバッグタスク
プログラムをデバッグするには、プログラムを起動し、デバッグエンジン (DE) をアタッチする必要があります。そうでない場合は、以前に起動されたプログラムに DE をアタッチする必要があります。 アタッチが完了すると、DE は特定のスタートアップイベントを生成する必要があります。 応答として、デバッグパッケージは IDE で設定されているブレークポイントをバインドしようとします。 プログラムは、バインドされたブレークポイントにヒットすると停止し、ユーザー入力を待機します。

## <a name="in-this-section"></a>このセクションの内容
 [セキュリティの問題](../../extensibility/debugger/security-issues.md)プログラムのデバッグに必要なセキュリティ手順について説明します。

 [プログラムを起動する](../../extensibility/debugger/launching-a-program.md)オペレーティングシステムを呼び出してプログラムを起動する DE を指定する手順について説明します。

 [プログラムに直接アタッチする](../../extensibility/debugger/attaching-directly-to-a-program.md)既に実行されているプロセスでプログラムをデバッグするために使用されるプロセスについて説明します。

 [起動後にスタートアップイベントを送信する](../../extensibility/debugger/sending-startup-events-after-a-launch.md)プログラムがメインエントリポイントにあり、デバッグできる状態になるまで、DE がプログラムにアタッチされた後に発生するイベントの一覧を表示します。

 [実行の制御](../../extensibility/debugger/control-of-execution.md)通常、DE が、状況に応じて、エントリポイントイベント、読み込み完了イベント、または停止イベントを送信する方法について説明します。

 [ブレークポイントのバインド](../../extensibility/debugger/binding-breakpoints.md)ユーザーがブレークポイントを設定した場合に、IDE が要求を使用しし、ブレークポイントを作成するようにデバッグセッションに要求する方法について説明します。

 [式の評価](../../extensibility/debugger/evaluating-expressions.md)式の作成方法と、式が評価されるときの動作について説明します。

 [データの視覚化と表示](../../extensibility/debugger/visualizing-and-viewing-data.md)型ビジュアライザーとカスタムビューアーが式エバリュエーター (EE) でどのようにサポートされるかについて説明します。

## <a name="related-sections"></a>関連項目
 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)デバッグアーキテクチャの主要概念について説明します。

 [デバッガーコンポーネント](../../extensibility/debugger/debugger-components.md)DE、EE、およびシンボルハンドラー (SH) を含む Visual Studio デバッグコンポーネントの概要について説明します。

 [デバッガーコンテキスト](../../extensibility/debugger/debugger-contexts.md)コード、ドキュメント、および式の評価コンテキスト内で、DE を同時に操作する方法について説明します。 3つのコンテキストのそれぞれについて、場所、位置、または評価に関連する評価について説明します。

## <a name="see-also"></a>関連項目
 [開始するには](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)
