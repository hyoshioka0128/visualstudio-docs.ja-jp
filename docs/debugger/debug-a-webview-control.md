---
title: WebView コントロールのデバッグ (UWP) |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
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
ms.openlocfilehash: f0cab4a77c601414e766851aaf048fb3c32f6458
ms.sourcegitcommit: da7f093db52df5dcd67e0a030e616b307f0dc2a8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2020
ms.locfileid: "91211116"
---
# <a name="debug-a-webview-control-in-a-uwp-app"></a>UWP アプリでの WebView コントロールのデバッグ

 Windows Runtime アプリで `WebView` コントロールを検査しデバッグするには、アプリの開始時にスクリプト デバッガーをアタッチするよう Visual Studio を設定できます。 デバッガーを使用して `WebView` コントロールと 2 つの方法で対話できます。

- `WebView` インスタンスで [DOM Explorer](../debugger/quickstart-debug-html-and-css.md) を開き、DOM 要素を検査し、CSS スタイルの問題を調査し、スタイルに対する動的な変更をテストします。

- [JavaScript コンソール](../debugger/javascript-console-commands.md?view=vs-2017&preserve-view=true) ウィンドウで `WebView` インスタンスに表示される Web ページまたは `iFrame` をターゲットとして選択し、コンソール コマンドを使用して Web ページと対話します。 コンソールは、現在のスクリプト実行コンテキストへのアクセスを提供します。

### <a name="attach-the-debugger-c-visual-basic-c"></a>デバッガーのアタッチ (C#、Visual Basic、C++)

1. Visual Studio で、Windows Runtime アプリに `WebView` コントロールを追加します。

2. ソリューション エクスプローラーで、プロジェクトのショートカット メニューから **[プロパティ]** を選択して、プロジェクトのプロパティを開きます。

3. **[デバッグ]** を選択します。 **[アプリケーション プロセス]** ボックスの一覧の **[スクリプト]** をクリックします。

     ![スクリプト デバッガーのアタッチ](../debugger/media/js_dom_webview_script_debugger.png "JS_DOM_WebView_Script_Debugger")

4. (オプション) Visual Studio の非 Express バージョンの場合、 **[ツール]、[オプション]、[デバッグ]、[Just-In-Time]** の順にクリックして、スクリプトの JIT デバッグを無効にします。

    > [!NOTE]
    > JIT デバッグを無効にすると、一部の Web ページで生じる未処理の例外のダイアログ ボックスを非表示にできます。 Visual Studio Express では、JIT デバッグは常に無効となっています。

5. F5 キーを押してデバッグを開始します。

### <a name="use-the-dom-explorer-to-inspect-and-debug-a-webview-control"></a>DOM Explorer を使って WebView コントロールを検査およびデバッグします。

1. (C#、Visual Basic、C++) スクリプト デバッガーをアプリにアタッチします。 手順については最初のセクションを参照してください。

2. まだ行っていない場合はアプリに `WebView` コントロールを追加して、F5 を押すとデバッグが開始します。

3. `Webview` コントロールが含まれるページに移動します。

4. **[デバッグ]** 、 **[ウィンドウ]** 、 **[DOM Explorer]** の順に選択して、`WebView` コントロールの DOM Explorer ウィンドウを開き、検索する `WebView` の URL を選択します。

     ![DOM Explorer を開く](../debugger/media/js_dom_webview.png "JS_DOM_WebView")

     `WebView` に関連付けられた DOM Explorer が Visual Studio の新しいタブとして表示されます。

5. 「[DOM Explorer を使用した CSS スタイルのデバッグ](quickstart-debug-html-and-css.md)」で説明されているように、ライブ DOM 要素と CSS スタイルを表示および変更します。

### <a name="use-the-javascript-console-window-to-inspect-and-debug-a-webview-control"></a>JavaScript コンソール ウィンドウを使って WebView コントロールを検査およびデバッグします。

1. (C#、Visual Basic、C++) スクリプト デバッガーをアプリにアタッチします。 手順については最初のセクションを参照してください。

2. まだ行っていない場合はアプリに `WebView` コントロールを追加して、F5 を押すとデバッグが開始します。

3. **[デバッグ]** 、 **[ウィンドウ]** 、 **[JavaScript コンソール]** の順に選択して、`WebView` コントロールの JavaScript コンソール ウインドウを開きます。

     JavaScript コンソール ウィンドウが開きます。

4. `Webview` コントロールが含まれるページに移動します。

5. コンソール ウィンドウで、 **[ターゲット]** 一覧の `WebView` コントロールの横に表示されている Web ページまたは `iFrame` を選択します。

     ![JavaScript コンソール ウィンドウでのターゲット選択](../debugger/media/js_console_target.png "JS_Console_Target")

    > [!NOTE]
    > コンソールを使って、1 度に 1 つの `WebView`、`iFrame`、共有コントラクト、または Web ワーカーとやり取りできます。 各要素では、Web プラットフォーム ホストの個別のインスタンスが必要となります (WWAHost.exe)。 一度に 1 つのホストとやり取りできます。

6. アプリの変数を表示および変更するか、コンソール コマンドを使用します。これは、[JavaScript のデバッグのためのクイックスタート](../debugger/quickstart-debug-javascript-using-the-console.md)および [JavaScript コンソール コマンド](../debugger/javascript-console-commands.md?view=vs-2017&preserve-view=true)に関するページで説明されています。

## <a name="see-also"></a>関連項目

- [クイック スタート:HTML および CSS のデバッグ](../debugger/quickstart-debug-html-and-css.md)