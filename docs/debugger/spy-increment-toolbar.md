---
title: Spy++ ツールバー | Microsoft Docs
description: メニュー バーの下に表示される Spy++ ツール バーのインターフェイス要素について説明します。 ツールバーを表示または非表示にするには、 [表示] メニューの [ツールバー] をクリックします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Spy++ toolbar
ms.assetid: 949c18fb-bb25-42ed-9130-c4a47869f24d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: af6db0f367c73804197ef35d0b3734d68f15a332
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99903529"
---
# <a name="spy-toolbar"></a>Spy++ ツール バー
このツールバーは、Spy++ のメニュー バーの下に表示されます。 ツールバーを表示または非表示にするには、 **[表示]** メニューの **[ツールバー]** をクリックします。

 ツール バーで使用できるコントロールは次のとおりです。

## <a name="uielement-list"></a>UIElement の一覧

|Button|効果|
|------------|------------|
|![Spy&#43;&#43; の [ウィンドウ] ボタン](../debugger/media/icon_spy--_windows.gif "Icon_Spy++_Windows")|システム内のウィンドウとコントロールのツリー ビューを表示します。 詳細については、「[ウィンドウ ビュー](../debugger/windows-view.md)」を参照してください。|
|![Spy&#43;&#43; の [プロセス] ボタン](../debugger/media/icon_spy--_processes.gif "Icon_Spy++_Processes")|システム内のプロセスのツリー ビューを表示します。 詳細については、「[プロセス ビュー](../debugger/processes-view.md)」を参照してください。|
|![Spy&#43;&#43; の [スレッド] ボタン](../debugger/media/icon_spy--_threads.gif "Icon_Spy++_Threads")|システム内のスレッドのツリー ビューを表示します。 詳細については、「[スレッド ビュー](../debugger/threads-view.md)」を参照してください。|
|![Spy&#43;&#43; の [メッセージ] ボタン](../debugger/media/icon_spy--_messages.gif "Icon_Spy++_Messages")|ウィンドウ メッセージを表示するウィンドウを作成し、 **[メッセージ オプション]** ダイアログ ボックスを開いて、メッセージを表示するウィンドウを選択したり、他のオプションを選択したりできるようにします。 詳細については、「[メッセージ ビュー](../debugger/messages-view.md)」を参照してください。|
|![Spy&#43;&#43; の [ログの開始] ボタン](../debugger/media/icon_spy--_startlog.gif "Icon_Spy++_StartLog")|メッセージのログ記録を開始し、メッセージ ストリームを表示します。 このコントロールは、 **[メッセージ]** ウィンドウがアクティブ ウィンドウである場合にのみ使用できます。 詳細については、[メッセージ ログの表示を開始および終了する](../debugger/how-to-start-and-stop-the-message-log-display.md)」を参照してください。|
|![Spy&#43;&#43; の [ログの停止] ボタン](../debugger/media/icon_spy--_stoplog.gif "Icon_Spy++_StopLog")|メッセージのログ記録を停止し、メッセージ ストリームを表示します。 このコントロールは、 **[メッセージ]** ウィンドウがアクティブ ウィンドウである場合にのみ使用できます。 詳細については、[メッセージ ログの表示を開始および終了する](../debugger/how-to-start-and-stop-the-message-log-display.md)」を参照してください。|
|Spy&#43;&#43; の ![[ログ オプション]](../debugger/media/icon_spy--_logoptions.gif "Icon_Spy++_LogOptions") ボタン|[[メッセージ オプション]](../debugger/message-options-dialog-box.md) ダイアログ ボックスを表示します。 このダイアログ ボックスを使用して、表示するウィンドウとメッセージの種類を選択します。 このコントロールは、 **[メッセージ]** ウィンドウがアクティブ ウィンドウである場合にのみ使用できます。|
|Spy&#43;&#43; の ![[ログのクリア]](../debugger/media/spy--_clearlog.gif "Spy++_ClearLog") ボタン|アクティブな **メッセージ** ウィンドウの内容がクリアされます。 このコントロールは、 **[メッセージ]** ウィンドウがアクティブ ウィンドウである場合にのみ使用できます。|
|![Spy&#43;&#43; の [ウィンドウ検索] ボタン](../debugger/media/icon_spy--_findwindow.gif "Icon_Spy++_FindWindow")|[[ウィンドウ検索]](../debugger/find-window-dialog-box.md) ダイアログ ボックスを開きます。このダイアログ ボックスで、ウィンドウの検索条件を設定したり、プロパティやメッセージを表示したりできます。 詳細については、[ファインダー ツールを使用する](../debugger/how-to-use-the-finder-tool.md)」を参照してください。|
|![Spy&#43;&#43; の [最初のウィンドウを検索] ボタン](../debugger/media/icon_spy--_window.gif "Icon_Spy++_Window")|現在のビューで、一致するウィンドウ、プロセス、スレッド、またはメッセージを検索します。|
|![Spy&#43;&#43; の [次のウィンドウを検索] ボタン](../debugger/media/icon_spy--_nextwindow.gif "Icon_Spy++_NextWindow")|現在のビューで、次に一致するウィンドウ、プロセス、スレッド、またはメッセージを検索します。 このコントロール (および関連するメニュー コマンド) は、一意ではない有効な検索結果がある場合にのみ使用できます。 たとえば、ウィンドウ ツリーの検索条件としてウィンドウ ハンドルを使用すると、そのハンドルを持つウィンドウはウィンドウ ツリー内に 1 つしかないため、一意の結果が生成されます。この場合、 **[次を検索]** を使用することはできません。|
|![Spy&#43;&#43; の [前のウィンドウを検索] ボタン](../debugger/media/icon_spy--_prevwindow.gif "Icon_Spy++_PrevWindow")|現在のビューで、前の一致するウィンドウ、プロセス、スレッド、またはメッセージを検索します。 このコントロール (および関連するメニュー コマンド) は、一意ではない有効な検索結果がある場合にのみ使用できます。 たとえば、ウィンドウ ツリーの検索条件としてウィンドウ ハンドルを使用すると、そのハンドルを持つウィンドウはウィンドウ ツリー内に 1 つしかないため、一意の結果が生成されます。この場合、 **[前を検索]** を使用することはできません。|
|![Spy&#43;&#43; の [プロパティ エクスプローラー] ボタン](../debugger/media/icon_spy--_propexp.gif "Icon_Spy++_PropExp")|ウィンドウ ビューで選択されているウィンドウのプロパティを表示します。|
|![Spy&#43;&#43; の [更新] ボタン](../debugger/media/icon_spy--_refresh.gif "Icon_Spy + + _Refresh")|システム ビューを更新します。|

## <a name="see-also"></a>関連項目
- [Spy++ の使用](../debugger/using-spy-increment.md)
- [Spy++ ビュー](../debugger/spy-increment-views.md)
- [Spy++ リファレンス](../debugger/spy-increment-reference.md)