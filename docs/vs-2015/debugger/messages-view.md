---
title: メッセージ ビュー | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.externaltools.spyplus.messagesview
helpviewer_keywords:
- Messages view
ms.assetid: 14c2a786-c23a-4b2d-acad-8c32a856c70d
caps.latest.revision: 9
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3765b9804224549c98b57cd1b0a44f0330d278b5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157477"
---
# <a name="messages-view"></a>メッセージ ビュー
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

各ウィンドウには、メッセージ ストリームが関連付けられています。 メッセージ ビュー ウィンドウには、このメッセージ ストリームが表示されます。 ウィンドウ ハンドル、メッセージ コード、およびメッセージが表示されます。 スレッドまたはプロセスのメッセージ ビューも作成できます。 これにより、特定のプロセスまたはスレッドが所有するすべてのウィンドウに送信されたメッセージを表示できます。これは、ウィンドウ初期化メッセージをキャプチャする場合に特に便利です。  
  
 一般的なメッセージ ビュー ウィンドウは次のように表示されます。 最初の列にはウィンドウ ハンドルが含まれ、2 番目の列にはメッセージ コード (「[メッセージ コード](../debugger/message-codes.md)」で説明しています) が含まれていることを確認してください。 デコードされたメッセージ パラメーターと戻り値は、右側にあります。  
  
 ![Spy&#43;&#43; メッセージビュー](../debugger/media/spy-messagesview.png "Spy + + _MessagesView")  
Spy++ メッセージ ビュー  
  
## <a name="procedures"></a>プロシージャ  
  
#### <a name="to-open-a-messages-view-for-a-window-process-or-thread"></a>ウィンドウ、プロセス、スレッドのメッセージ ビューを開くには  
  
1. フォーカスを[ウィンドウ ビュー](../debugger/windows-view.md)、[プロセス ビュー](../debugger/processes-view.md)、または[スレッド ビュー](../debugger/threads-view.md)のウィンドウに移動します。  
  
2. 確認するメッセージが含まれている項目のノードを見つけ、選択します。  
  
3. **[Spy]** メニューから **[メッセージのログ出力]** を選択します。  
  
     [[メッセージ オプション] ダイアログ ボックス](../debugger/message-options-dialog-box.md)が開きます。  
  
4. 表示するメッセージのオプションを選択します。  
  
5. **[OK]** を押して、メッセージのログ記録を開始します。  
  
     メッセージ ビュー ウィンドウが開き、 **[メッセージ]** メニューが Spy++ ツールバーに追加されます。 選択したオプションに応じて、メッセージはアクティブなメッセージ ビュー ウィンドウへのストリーミングを開始します。  
  
6. 十分な数のメッセージが表示されたら、 **[メッセージ]** メニューから **[ログ記録の停止]** を選択します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [メッセージビューの制御](../debugger/how-to-control-messages-view.md)  
 メッセージビューを管理する方法について説明します。  
  
 [メッセージビューでのメッセージの検索](../debugger/how-to-search-for-a-message-in-messages-view.md)  
 メッセージビューで特定のメッセージを検索する方法について説明します。  
  
 [メッセージログの表示の開始と停止](../debugger/how-to-start-and-stop-the-message-log-display.md)  
 メッセージログを開始および停止する方法について説明します。  
  
 [メッセージ コード](../debugger/message-codes.md)  
 メッセージビューに表示されるメッセージのコードを定義します。  
  
 [メッセージのプロパティの表示](../debugger/how-to-display-message-properties.md)  
 メッセージに関する詳細情報を表示する方法。  
  
## <a name="related-sections"></a>関連項目  
 [Spy++ ビュー](../debugger/spy-increment-views.md)  
 Windows、メッセージ、プロセス、およびスレッドの Spy + + ツリービューについて説明します。  
  
 [Spy++ の使用](../debugger/using-spy-increment.md)  
 Spy + + ツールの概要と、その使用方法について説明します。  
  
 [[メッセージ オプション] ダイアログ ボックス](../debugger/message-options-dialog-box.md)  
 [アクティブなメッセージ] ビューに表示されるメッセージを選択するために使用します。  
  
 [[メッセージ検索] ダイアログ ボックス](../debugger/message-search-dialog-box.md)  
 メッセージビューで特定のメッセージのノードを検索するために使用します。  
  
 [[メッセージ プロパティ] ダイアログ ボックス](../debugger/message-properties-dialog-box.md)  
 メッセージビューで選択されたメッセージのプロパティを表示するために使用します。  
  
 [Spy++ リファレンス](../debugger/spy-increment-reference.md)  
 各 Spy + + メニューおよびダイアログボックスについて説明するセクションが含まれています。
