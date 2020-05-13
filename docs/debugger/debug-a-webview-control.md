---
title: WebView コントロールのデバッグ (UWP) |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 7d105907-8b39-4d07-8762-5c5ed74c7f21
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- uwp
ms.openlocfilehash: 15c9a2b489aeb091224536bfb87398197f6e4f62
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2019
ms.locfileid: "73188661"
---
# <a name="debug-a-webview-control-in-a-uwp-app"></a>UWP アプリでの WebView コントロールのデバッグ

 Windows Runtime アプリで `WebView` コントロールを検査しデバッグするには、アプリの開始時にスクリプト デバッガーをアタッチするよう Visual Studio を設定できます。 デバッガーを使用して `WebView` コントロールと対話するには、次の2つの方法があります。

- `WebView` インスタンスで [DOM Explorer](../debugger/quickstart-debug-html-and-css.md) を開き、DOM 要素を検査し、CSS スタイルの問題を調査し、スタイルに対する動的な変更をテストします。

- [JavaScript コンソール](../debugger/javascript-console-commands.md?view=vs-2017)ウィンドウで、`WebView` インスタンスに表示されている web ページまたは `iFrame` をターゲットとして選択し、コンソールコマンドを使用して web ページを操作します。 コンソールは、現在のスクリプト実行コンテキストへのアクセスを提供します。

### <a name="attach-the-debugger-c-visual-basic-c"></a>デバッガーのアタッチ (C#、Visual Basic、C++)

1. Visual Studio で、Windows Runtime アプリに `WebView` コントロールを追加します。

2. ソリューション エクスプローラーで、プロジェクトのショートカット メニューから **[プロパティ]** を選択して、プロジェクトのプロパティを開きます。

3. **[デバッグ]** を選択します。 **[アプリケーション プロセス]** ボックスの一覧の **[スクリプト]** をクリックします。

     ![スクリプトデバッガーをアタッチする](../debugger/media/js_dom_webview_script_debugger.png "JS_DOM_WebView_Script_Debugger")

4. (オプション) Visual Studio の非 Express バージョンの場合、 **[ツール]、[オプション]、[デバッグ]、[Just-In-Time]** の順にクリックして、スクリプトの JIT デバッグを無効にします。

    > [!NOTE]
    > JIT デバッグを無効にすると、一部の Web ページで生じる未処理の例外のダイアログ ボックスを非表示にできます。 Visual Studio Express では、JIT デバッグは常に無効となっています。

5. F5 キーを押してデバッグを開始します。

### <a name="use-the-dom-explorer-to-inspect-and-debug-a-webview-control"></a>DOM Explorer を使って WebView コントロールを検査およびデバッグします。

1. (C#、Visual Basic、C++) スクリプト デバッガーをアプリにアタッチします。 手順については最初のセクションを参照してください。

2. まだ行っていない場合はアプリに `WebView` コントロールを追加して、F5 を押すとデバッグが開始します。

3. `Webview` コントロールが含まれるページに移動します。

4. **[デバッグ]** 、 **[Windows]** 、 **[DOM Explorer]** の順に選択して `WebView` コントロールの [DOM Explorer] ウィンドウを開き、検査する `WebView` の URL を選択します。

     ![DOM Explorer を開く](../debugger/media/js_dom_webview.png "JS_DOM_WebView")

     `WebView` に関連付けられた DOM Explorer が Visual Studio の新しいタブとして表示されます。

5. 「 [DOM Explorer を使用した css スタイルのデバッグ](quickstart-debug-html-and-css.md)」の説明に従って、ライブ DOM 要素と css スタイルを表示および変更します。

### <a name="use-the-javascript-console-window-to-inspect-and-debug-a-webview-control"></a>JavaScript コンソール ウィンドウを使って WebView コントロールを検査およびデバッグします。

1. (C#、Visual Basic、C++) スクリプト デバッガーをアプリにアタッチします。 手順については最初のセクションを参照してください。

2. まだ行っていない場合はアプリに `WebView` コントロールを追加して、F5 を押すとデバッグが開始します。

3. **[デバッグ]** 、 **[Windows]** 、 **[javascript コンソール]** の順に選択して、`WebView` コントロールの JavaScript コンソールウィンドウを開きます。

     JavaScript コンソール ウィンドウが開きます。

4. `Webview` コントロールが含まれるページに移動します。

5. コンソールウィンドウで、 **[ターゲット]** ボックスの一覧の `WebView` コントロールに表示される web ページまたは `iFrame` を選択します。

     ![JavaScript コンソールウィンドウでのターゲット選択](../debugger/media/js_console_target.png "JS_Console_Target")

    > [!NOTE]
    > コンソールを使って、1 度に 1 つの `WebView`、`iFrame`、共有コントラクト、または Web ワーカーとやり取りできます。 各要素では、Web プラットフォーム ホストの個別のインスタンスが必要となります (WWAHost.exe)。 一度に 1 つのホストとやり取りできます。

6. アプリケーションで変数を表示および変更するか、コンソールコマンドを使用します。詳細については、「[クイックスタート: javascript](../debugger/quickstart-debug-javascript-using-the-console.md)と[javascript コンソールのコマンド](../debugger/javascript-console-commands.md?view=vs-2017)のデバッグ」を参照してください。

## <a name="see-also"></a>関連項目

- [クイック スタート: HTML および CSS のデバッグ](../debugger/quickstart-debug-html-and-css.md)
