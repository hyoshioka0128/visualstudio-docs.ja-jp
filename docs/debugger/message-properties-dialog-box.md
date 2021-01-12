---
title: '[メッセージ プロパティ] ダイアログ ボックス | Microsoft Docs'
description: '[メッセージ プロパティ] を参照して、メッセージ ビューに表示されるメッセージよりも詳細な情報を確認します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- message options
- message options, General
ms.assetid: 58e9dc24-baf6-4ab8-916c-aea28b72e3b0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3f58ad7344c7de9a9486fcb3ccefbf263688926f
ms.sourcegitcommit: 620d30c60da8f9805fce524fe4951cf40f28297d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97903065"
---
# <a name="message-properties-dialog-box"></a>[メッセージ プロパティ] ダイアログ ボックス
このダイアログ ボックスを使用して、特定のメッセージの詳細を確認します。 このダイアログ ボックスを表示するには、[メッセージ ビュー](../debugger/messages-view.md) ウィンドウにフォーカスを移動します。 ツリーで任意のメッセージ ノードを選択し、 **[ビュー]** メニューから **[プロパティ]** を選択します。

 表示される唯一のタブが **[全般]** タブです。 次の設定を使用できます。

 **ウィンドウ ハンドル** このウィンドウの一意の ID です。 ウィンドウ ハンドル番号は再利用されます。ウィンドウの有効期間中にのみウィンドウを識別できます。 この値は、このウィンドウのプロパティを表示する場合にクリックします。

 **入れ子レベル** このメッセージの入れ子の深さです。0 の場合、入れ子になっていません。

 **メッセージ** 選択したウィンドウ メッセージの番号、状態、名前です。

 **lResult** *lResult* パラメーター (ある場合) の値です。

 **wParam** *wParam* パラメーター (ある場合) の値です。

 **lParam** *lParam* パラメーター (ある場合) の値です。 この値が文字列または構造体へのポインターである場合はデコードされます。

## <a name="related-sections"></a>関連項目
 [[メッセージ オプション] ダイアログ ボックス](../debugger/message-options-dialog-box.md) アクティブなメッセージ ビューに一覧表示されるメッセージを選択するために使用されます。

 [[メッセージ検索] ダイアログ ボックス](../debugger/message-search-dialog-box.md) メッセージ ビューで特定のメッセージのノードを検索するために使用されます。

 [Spy++ リファレンス](../debugger/spy-increment-reference.md) Spy++ の各メニューとダイアログ ボックスについて説明するセクションが含まれています。

 [[ウィンドウの検索] からメッセージ ビューを開く](../debugger/how-to-open-messages-view-from-find-window.md) [ウィンドウの検索] ダイアログ ボックスからメッセージ ビューを開く方法について説明します。

 [メッセージ ビューのメッセージの検索](../debugger/how-to-search-for-a-message-in-messages-view.md) メッセージ ビューで特定のメッセージを検索する方法について説明します。

 [メッセージ ビュー](../debugger/messages-view.md) ウィンドウ、プロセス、またはスレッドに関するメッセージ ストリームが表示されます。

 [Spy++ ビュー](../debugger/spy-increment-views.md) ウィンドウ、メッセージ、プロセス、およびスレッドの Spy++ ツリー ビューについて説明します。

 [Spy++ の使用](../debugger/using-spy-increment.md) Spy++ ツールを紹介し、その使用方法について説明します。