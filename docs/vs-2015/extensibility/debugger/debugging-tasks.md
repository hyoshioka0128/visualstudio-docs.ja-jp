---
title: タスクのデバッグ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], tasks
ms.assetid: 5d60e9e8-305e-4a48-829f-b9440fc8af7b
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f4a8a9879bce6d91448bb4f29b842328ab56bb97
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68200612"
---
# <a name="debugging-tasks"></a>タスクのデバッグ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

プログラムをデバッグするには、プログラムを起動し、デバッグエンジン (DE) をアタッチする必要があります。そうでない場合は、以前に起動されたプログラムに DE をアタッチする必要があります。 アタッチが完了すると、DE は特定のスタートアップイベントを生成する必要があります。 応答として、デバッグパッケージは IDE で設定されているブレークポイントをバインドしようとします。 プログラムは、バインドされたブレークポイントにヒットすると停止し、ユーザー入力を待機します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [セキュリティの問題](../../extensibility/debugger/security-issues.md)  
 プログラムのデバッグに必要なセキュリティ手順について説明します。  
  
 [プログラムの起動](../../extensibility/debugger/launching-a-program.md)  
 オペレーティングシステムを呼び出してプログラムを起動する DE を指定する手順について説明します。  
  
 [プログラムへ直接アタッチする](../../extensibility/debugger/attaching-directly-to-a-program.md)  
 既に実行されているプロセスでプログラムをデバッグするために使用されるプロセスについて説明します。  
  
 [起動の後のスタートアップ イベントの送信](../../extensibility/debugger/sending-startup-events-after-a-launch.md)  
 プログラムがメインエントリポイントにあり、デバッグできる状態になるまで、DE がプログラムにアタッチされた後に発生するイベントの一覧を表示します。  
  
 [実行の制御](../../extensibility/debugger/control-of-execution.md)  
 通常、DE が、状況に応じて、エントリポイントイベント、読み込み完了イベント、または停止イベントを送信する方法について説明します。  
  
 [ブレークポイントのバインド](../../extensibility/debugger/binding-breakpoints.md)  
 ユーザーがブレークポイントを設定した場合に、IDE が要求を使用しし、ブレークポイントを作成するようにデバッグセッションに要求する方法について説明します。  
  
 [式の評価](../../extensibility/debugger/evaluating-expressions.md)  
 式の作成方法と、式が評価されるときの動作について説明します。  
  
 [データの視覚化と表示](../../extensibility/debugger/visualizing-and-viewing-data.md)  
 型ビジュアライザーとカスタムビューアーが式エバリュエーター (EE) でどのようにサポートされるかについて説明します。  
  
## <a name="related-sections"></a>関連項目  
 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)  
 デバッグアーキテクチャの主要概念について説明します。  
  
 [デバッガーのコンポーネント](../../extensibility/debugger/debugger-components.md)  
 DE、EE、およびシンボルハンドラー (SH) を含む Visual Studio デバッグコンポーネントの概要について説明します。  
  
 [デバッガー コンテキスト](../../extensibility/debugger/debugger-contexts.md)  
 コード、ドキュメント、および式の評価コンテキスト内で、DE を同時に操作する方法について説明します。 3つのコンテキストのそれぞれについて、場所、位置、または評価に関連する評価について説明します。  
  
## <a name="see-also"></a>参照  
 [はじめに](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)
