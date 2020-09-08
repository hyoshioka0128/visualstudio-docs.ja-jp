---
title: タスクのデバッグ | Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85903561"
---
# <a name="debug-tasks"></a>タスクをデバッグする
プログラムをデバッグするには、起動してデバッグ エンジン (DE) をアタッチする必要があります。もしくは、以前に起動されたプログラムに DE をアタッチする必要があります。 アタッチが完了すると、DE で特定のスタートアップ イベントを生成する必要があります。 応答として、デバッグ パッケージは IDE で設定されているブレークポイントをバインドしようとします。 プログラムがバインドされたブレークポイントにヒットすると停止し、ユーザー入力を待機します。

## <a name="in-this-section"></a>このセクションの内容
 [セキュリティのイシュー](../../extensibility/debugger/security-issues.md) プログラムのデバッグに必要なセキュリティ手順について説明します。

 [プログラムを起動する](../../extensibility/debugger/launching-a-program.md) オペレーティング システムを呼び出してプログラムを起動する DE の指定方法について、手順に従って説明します。

 [プログラムに直接アタッチする](../../extensibility/debugger/attaching-directly-to-a-program.md) 既に実行されているプロセスでプログラムをデバッグするために使用されるプロセスについて説明します。

 [起動後にスタートアップ イベントを送信する](../../extensibility/debugger/sending-startup-events-after-a-launch.md) DE がプログラムにアタッチされてから、プログラムがそのメイン エントリ ポイントに移動し、デバッグの準備ができるまでに発生するイベントを一覧表示します。

 [実行の制御](../../extensibility/debugger/control-of-execution.md) DE が通常、エントリポイントのイベント、読み込み完了イベント、停止イベントをどのように送信するかを状況に応じて説明します。

 [ブレークポイントをバインドする](../../extensibility/debugger/binding-breakpoints.md) ユーザーがブレークポイントを設定している場合に、IDE がどのように要求を作成し、デバッグ セッションにブレークポイントの作成を促すかについて説明します。

 [式を評価する](../../extensibility/debugger/evaluating-expressions.md) 式がどのように作成され、式が評価されると何が起きるかについて説明します。

 [データの視覚化と表示](../../extensibility/debugger/visualizing-and-viewing-data.md) 型ビジュアライザーとカスタム ビューアーが式エバリュエーター (EE) によってどのようにサポートされるかについて説明します。

## <a name="related-sections"></a>関連項目
 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md) 主要なデバッグ アーキテクチャの概念について説明します。

 [デバッガー コンポーネント](../../extensibility/debugger/debugger-components.md) DE、EE、シンボル ハンドラー (SH) などの Visual Studio デバッグ コンポーネントの概要を示します。

 [デバッガー コンテキスト](../../extensibility/debugger/debugger-contexts.md) コード、ドキュメント、式の評価コンテキスト内で DE がどのように同時操作されるかについて説明します。 場所、位置、それに関連する評価の 3 つのコンテキストそれぞれについて説明します。

## <a name="see-also"></a>関連項目
 [開始するには](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)
