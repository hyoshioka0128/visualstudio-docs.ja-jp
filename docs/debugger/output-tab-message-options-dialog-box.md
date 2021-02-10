---
title: '[出力] タブ ([メッセージ オプション] ダイアログ ボックス) | Microsoft Docs'
description: '[メッセージ ビュー] に表示されるメッセージ データを指定するには、[メッセージ オプション] の [出力] タブを使用します。 この記事では、使用可能な設定について説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- message options, Output
ms.assetid: 22dd48c2-6d17-41b1-b84c-9ddeaef68411
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d9cb48f061cfda78e3dec8ef515df82fdefb8193
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99891580"
---
# <a name="output-tab-message-options-dialog-box"></a>[出力] タブ ([メッセージ オプション] ダイアログ ボックス)
**[出力]** タブを使用し、各メッセージからどのデータを [[メッセージ ビュー]](../debugger/messages-view.md) に一覧表示するか指定します。 [[メッセージ オプション]](../debugger/message-options-dialog-box.md) ダイアログ ボックスを表示するには、 **[Spy]** メニューから **[ログ メッセージ]** を選択します。

 **[出力]** タブでは、次の設定を使用できます。

 **行番号** 行番号が表示されます。

 **メッセージの入れ子レベル** 入れ子になっているメッセージに接頭辞を付けます。レベルごとにピリオドが 1 つ付きます。

 **生のメッセージ パラメーター** 16 進数の **wParam** 値と **lParam** 値が表示されます。

 **デコードされたメッセージ パラメーター** **wParam** 値と **lParam** 値のメッセージ特定のデコード結果が表示されます。

 **生の戻り値** 16 進数 **lResult** 戻り値が表示されます。

 **デコードされた戻り値** **lResult** 戻り値のメッセージ固有のデコード結果が表示されます。

 **メッセージのポストされた時間** Windows システム開始から経過した時間 (ポストされたメッセージのみ)。

 **メッセージのマウスの位置** メッセージがポストされたときのマウスの画面座標 (ポストされたメッセージのみ)。

 **最大行数** 現在選択されているメッセージ ビューに保持される行数が制限されます。

 **メッセージのログもファイルに出力する** メッセージ ログの出力ファイルを指定します。 この出力ファイルは、メッセージ ログ ウィンドウと同期で書き込まれます。

 **設定を既定値として保存し** 新しいメッセージ ストリーム ウィンドウの前の設定を保存します。 これらの設定は Spy++ を終了したときに保存されます。