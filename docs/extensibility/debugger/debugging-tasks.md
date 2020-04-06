---
title: デバッグ タスク |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], tasks
ms.assetid: 5d60e9e8-305e-4a48-829f-b9440fc8af7b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d41f53ab1392ea3c31908faf65a871fa100fbb3f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738957"
---
# <a name="debug-tasks"></a>デバッグ タスク
プログラムをデバッグするには、プログラムを起動し、デバッグ エンジン (DE) をアタッチする必要があります。 アタッチされると、DE は特定のスタートアップ イベントを生成する必要があります。 これに対して、デバッグ パッケージは、IDE に設定されたブレークポイントをバインドしようとします。 プログラムがバインドされたブレークポイントに達すると、停止してユーザー入力を待ちます。

## <a name="in-this-section"></a>このセクションの内容
 [セキュリティの問題](../../extensibility/debugger/security-issues.md)プログラムのデバッグに必要なセキュリティ手順について説明します。

 [プログラムを起動する](../../extensibility/debugger/launching-a-program.md)プログラムを起動するためにオペレーティング システムを呼び出す DE を指定する手順を説明します。

 [プログラムに直接アタッチする](../../extensibility/debugger/attaching-directly-to-a-program.md)既に実行中のプロセスでプログラムをデバッグするプロセスについて説明します。

 [起動後にスタートアップ イベントを送信する](../../extensibility/debugger/sending-startup-events-after-a-launch.md)プログラムがメイン エントリ ポイントにあり、デバッグの準備が整うまで、DE がプログラムにアタッチされた後に発生するイベントを一覧表示します。

 [実行の制御](../../extensibility/debugger/control-of-execution.md)デは、通常、状況に応じて、エントリ ポイント イベント、ロード完了イベント、または停止イベントを送信する方法について説明します。

 [ブレークポイントをバインドする](../../extensibility/debugger/binding-breakpoints.md)ユーザーがブレークポイントを設定した場合、IDE が要求を作成し、ブレークポイントを作成するデバッグ セッションを要求する方法について説明します。

 [式の評価](../../extensibility/debugger/evaluating-expressions.md)式の作成方法と、式の評価時の動作について説明します。

 [データの視覚化と表示](../../extensibility/debugger/visualizing-and-viewing-data.md)型ビジュアライザーとカスタム ビューアーが式エバリュエーター (EE) によってサポートされる方法について説明します。

## <a name="related-sections"></a>関連項目
 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)デバッグアーキテクチャの主要な概念について説明します。

 [デバッガー コンポーネント](../../extensibility/debugger/debugger-components.md)デ、EE、およびシンボル ハンドラー (SH) を含む Visual Studio のデバッグ コンポーネントの概要を説明します。

 [デバッガーのコンテキスト](../../extensibility/debugger/debugger-contexts.md)コード、ドキュメント、および式の評価コンテキスト内で DE が同時に動作する方法について説明します。 3 つのコンテキストのそれぞれについて、そのコンテキストに関連する場所、位置、または評価について説明します。

## <a name="see-also"></a>関連項目
 [はじめに](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)
