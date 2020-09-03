---
title: '[メッセージ] タブ ([メッセージ オプション] ダイアログ ボックス) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- message options, Messages
ms.assetid: fb9fa211-e82c-40a5-9e4b-ba8de07313c0
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a9eb1c88d935fa307e8b86a9a75da423bc08111c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68149437"
---
# <a name="messages-tab-message-options-dialog-box"></a>[メッセージ] タブ ([メッセージ オプション] ダイアログ ボックス)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**[メッセージ]** タブを使用し、[[メッセージ ビュー]](../debugger/messages-view.md) に一覧表示するメッセージの種類を選択し、メッセージ検索条件を指定します。 [[メッセージ オプション]](../debugger/message-options-dialog-box.md) ダイアログ ボックスを表示するには、 **[Spy]** メニューから **[ログ メッセージ]** を選択します。  
  
 一般的に、まず **[メッセージ グループ]** を選択し、それから個々の **[表示するメッセージ]** を選択して選択内容を微調整します。 **[すべて]** ボタンではメッセージの全種類が選択されます。 **[なし]** ボタンではすべての種類が消去されます。  
  
 **[メッセージ]** タブでは、次の設定を使用できます。  
  
 **表示するメッセージ**  
 表示する特定のメッセージを選択します。 [メッセージ] ウィンドウを新規作成すると、そのウィンドウにはすべてのメッセージが表示されることがあります。 **[メッセージ]** タブでメッセージにフィルターを適用すると、そのフィルターは、Windows ビューに既に表示されているメッセージではなく、新しいメッセージにのみ適用されます。  
  
 **メッセージグループ**  
 表示するメッセージグループを選択します。 利用できるグループ:  
  
- WM_USER: WM_USER より大きいか、それと等しいコードが含まれる  
  
- Registered: **RegisterWindowMessage** 呼び出しで登録されている  
  
- 不明: 0 ~ (WM_USER-1) の範囲内の不明なメッセージ  
  
  これらの**メッセージ グループ**は、 **[表示するメッセージ]** で特定のエントリにマッピングされないことにご注意ください。 グループを選択すると、選択内容はメッセージ ストリームに直接適用されます。  
  
  **[メッセージ グループ]** 内の灰色チェック ボックスは、そのグループで **[表示するメッセージ]** リスト ボックスが変更されていることを示します。そのグループのメッセージの種類については、一部が選択されていません。  
  
  **設定を既定値として保存**  
  現在の設定を保存して、後でメッセージ検索オプションとして使用します。 これらの設定は、Spy++ を終了したときにも保存されます。
