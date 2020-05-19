---
title: メッセージ ビュー | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.externaltools.spyplus.messagesview
helpviewer_keywords:
- Messages view
ms.assetid: 14c2a786-c23a-4b2d-acad-8c32a856c70d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6b20ed28518c9156e82c6fe75ecceda74c66615d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62845854"
---
# <a name="messages-view"></a>メッセージ ビュー
各ウィンドウには、メッセージ ストリームが関連付けられています。 メッセージ ビュー ウィンドウには、このメッセージ ストリームが表示されます。 ウィンドウ ハンドル、メッセージ コード、およびメッセージが表示されます。 スレッドまたはプロセスのメッセージ ビューも作成できます。 これにより、特定のプロセスまたはスレッドが所有するすべてのウィンドウに送信されたメッセージを表示できます。これは、ウィンドウ初期化メッセージをキャプチャする場合に特に便利です。

 一般的なメッセージ ビュー ウィンドウは次のように表示されます。 最初の列にはウィンドウ ハンドルが含まれ、2 番目の列にはメッセージ コード (「[メッセージ コード](../debugger/message-codes.md)」で説明しています) が含まれていることを確認してください。 デコードされたメッセージ パラメーターと戻り値は、右側にあります。

 ![Spy&#43;&#43; メッセージ ビュー](../debugger/media/spy--_messagesview.png "Spy++_MessagesView") Spy++ メッセージ ビュー

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
 [メッセージ ビューの制御](../debugger/how-to-control-messages-view.md) メッセージ ビューの管理方法について説明します。

 [[ウィンドウの検索] からメッセージ ビューを開く](../debugger/how-to-open-messages-view-from-find-window.md) [ウィンドウの検索] ダイアログ ボックスからメッセージ ビューを開く方法について説明します。

 [メッセージ ビューのメッセージの検索](../debugger/how-to-search-for-a-message-in-messages-view.md) メッセージ ビューで特定のメッセージを検索する方法について説明します。

 [メッセージ ログの表示を開始および停止する](../debugger/how-to-start-and-stop-the-message-log-display.md) メッセージ ログを開始および停止する方法について説明します。

 [メッセージ コード](../debugger/message-codes.md) メッセージ ビューに表示されているメッセージのコードを定義します。

 [[メッセージ プロパティ] の表示](../debugger/how-to-display-message-properties.md) メッセージに関する詳細を表示する方法です。

## <a name="related-sections"></a>関連項目
 [Spy++ ビュー](../debugger/spy-increment-views.md) ウィンドウ、メッセージ、プロセス、スレッドの Spy++ ツリー ビューについて説明します。

 [Spy++ の使用](../debugger/using-spy-increment.md) Spy++ ツールを紹介し、その使用方法について説明します。

 [[メッセージ オプション] ダイアログ ボックス](../debugger/message-options-dialog-box.md) アクティブなメッセージ ビューに一覧表示されるメッセージを選択するために使用されます。

 [[メッセージ検索] ダイアログ ボックス](../debugger/message-search-dialog-box.md) メッセージ ビューで特定のメッセージのノードを検索するために使用されます。

 [[メッセージ プロパティ] ダイアログ ボックス](../debugger/message-properties-dialog-box.md) メッセージ ビューで選択されたメッセージのプロパティを表示するために使用されます。

 [Spy++ リファレンス](../debugger/spy-increment-reference.md) Spy++ の各メニューとダイアログ ボックスについて説明するセクションが含まれています。