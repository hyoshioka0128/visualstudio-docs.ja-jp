---
title: デバッガーのヒントとテクニック
description: Visual Studio デバッガーでサポートされている、あまり知られていない機能のいくつかについて説明します
ms.custom: seodec18
ms.date: 06/15/2018
ms.topic: conceptual
helpviewer_keywords:
- stepping
- debugging [Visual Studio], execution control
- execution, controlling in debugger
ms.assetid: 5262d8b1-2648-429e-85d5-90fcaadfb362
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d5b934c0e9532bd3bc1f53d9b00d1cc8273f4120
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99872990"
---
# <a name="learn-productivity-tips-and-tricks-for-the-debugger-in-visual-studio"></a>Visual Studio でのデバッガーの生産性に関するヒントとテクニックについて学習する

このトピックでは、Visual Studio デバッガーの生産性に関するヒントとテクニックについて説明します。 デバッガーの基本的な機能については、「[デバッガーでのはじめに](../debugger/debugger-feature-tour.md)」を参照してください。 このトピックでは、機能ツアーに含まれていないいくつかの領域について説明します。

## <a name="pin-data-tips"></a>データ ヒントをピン留めする

デバッグ中にデータ ヒントを頻繁にポイントする場合は、変数のデータ ヒントをピン留めして、すぐにアクセスできるようにすることができます。 変数は、再起動後もピン留めされたままです。 データ ヒントをピン留めするには、データ ヒントをポイントしてピン アイコンをクリックします。 複数の変数をピン留めすることができます。

![データ ヒントのピン留め](../debugger/media/dbg-tips-data-tips-pinned.png "PinningDataTip")

## <a name="edit-your-code-and-continue-debugging-c-vb-c"></a>コードを編集してデバッグを続行する (C#、VB、C++)

Visual Studio でサポートされているほとんどの言語で、デバッグ セッション中にコードを編集し、デバッグを続行できます。 この機能を使用するには、デバッガーの一時停止中にカーソルを使用してコードをクリックし、編集を行い、**F5**、**F10**、または **F11** キーを押してデバッグを続行します。

![エディット コンティニュのデバッグ](../debugger/media/dbg-tips-edit-and-continue.gif "EditAndContinue")

機能の使用および機能制限の詳細については、[エディット コンティニュ](../debugger/edit-and-continue.md)に関するページを参照してください。

## <a name="edit-xaml-code-and-continue-debugging"></a>XAML コードを編集してデバッグを続行する

デバッグ セッション中に XAML コードを変更するには、[XAML ホット リロードで実行中の XAML コードを記述およびデバッグする](../xaml-tools/xaml-hot-reload.md)方法に関するページを参照してください。

## <a name="debug-issues-that-are-hard-to-reproduce"></a>再現するのが困難な問題をデバッグする

アプリで特定の状態を再現することが難しい場合や時間がかかる場合は、条件付きブレークポイントを使用すると効果があるかどうかを検討します。 [条件付きブレークポイント](../debugger/using-breakpoints.md#BKMK_Specify_a_breakpoint_condition_using_a_code_expression)を使用し、ブレークポイントをフィルター処理することで、アプリが目的の状態 (変数に不適切なデータが格納された状態など) になるまで、アプリ コードが中断されないようにすることができます。 式、フィルター、ヒット カウントなどを使用して、条件を設定できます。

#### <a name="to-create-a-conditional-breakpoint"></a>条件付きブレークポイントを作成するには

1. ブレークポイント アイコン (赤いボール) を右クリックして、 **[条件]** を選択します。

2. **[ブレークポイントの設定]** ウィンドウで、式を入力します。

    ![条件付きブレークポイント](../debugger/media/dbg-multithreaded-conditional-breakpoint.png "ConditionalBreakpoint")

3. 別の種類の条件に関心がある場合は、 **[ブレークポイントの設定]** ダイアログ ボックスで **[条件式]** の代わりに **[フィルター]** を選択して、フィルターのヒントに従います。

## <a name="configure-the-data-to-show-in-the-debugger"></a>デバッガーに表示されっるようにデータを構成する

C#、Visual Basic、C++ (C++/CLI コードのみ) の場合、[DebuggerDisplay](../debugger/using-the-debuggerdisplay-attribute.md) 属性を使用して、表示する情報をデバッガーに指定できます。 C++ コードの場合は、[Natvis の視覚化](create-custom-views-of-native-objects.md)を使用して同じことを行うことができます。

## <a name="change-the-execution-flow"></a>実行フローを変更する

デバッガーがコード行で一時停止したら、マウスを使用して、左側の黄色い矢印ポインターをグラブします。 黄色い矢印ポインターをコード実行パスの別の場所に移動します。 その後、F5 キーまたはステップ コマンドを使用して、アプリの実行を続行します。

![実行ポインターを移動する](../debugger/media/dbg-tour-move-the-execution-pointer.gif "実行ポインターを移動する")

実行フローを変更することにより、さまざまなコード実行パスをテストしたり、デバッガーを再起動することなくコードを再実行したりできます。

> [!WARNING]
> 多くの場合、この機能には注意する必要があり、ツールヒントに警告が表示されます。 他の警告が表示される場合もあります。 ポインターを移動しても、アプリを以前のアプリケーション状態に戻すことはできません。

## <a name="track-an-out-of-scope-object-c-visual-basic"></a>スコープ外のオブジェクトを追跡する (C#、Visual Basic)

**[ウォッチ]** ウィンドウのようなデバッガー ウィンドウを使用して、変数を簡単に表示できます。 ただし、 **[ウォッチ]** ウィンドウで変数がスコープ外になると、淡色表示になることがわかります。アプリのシナリオによっては、変数がスコープ外になった場合でも変数の値が変更されることがあり、それを細かく監視したいことがあります (たとえば、変数がガベージ コレクトされる可能性があります)。 **[ウォッチ]** ウィンドウで変数のオブジェクト ID を作成することで、変数を追跡できます。

#### <a name="to-create-an-object-id"></a>オブジェクト ID を作成するには

1. 追跡する変数の近くにブレークポイントを設定します。

2. デバッガーを開始し (**F5** キー)、ブレークポイントで停止します。

3. **[ローカル]** ウィンドウ( **[デバッグ] > [ウィンドウ] > [ローカル]** ) で変数を探し、変数を右クリックして、 **[オブジェクト ID の作成]** を選択します。

    ![オブジェクト ID を作成する](../debugger/media/dbg-tips-watch-create-object-id.png "CreateObjectID")

4. **$** ウィンドウに、 **[ローカル]** ウィンドウを閉じます。 この変数はオブジェクト ID です。

5. オブジェクト ID 変数を右クリックし、 **[ウォッチの追加]** を選択します。

詳細については、[オブジェクト ID の作成](../debugger/watch-and-quickwatch-windows.md#bkmk_objectIds)に関するページを参照してください。

## <a name="view-return-values-for-functions"></a>関数の戻り値を表示する

関数の戻り値を表示するには、コードのステップ実行中に、 **[自動変数]** ウィンドウに表示されている関数を調べます。 関数の戻り値を調べるには、対象の関数が既に実行されていることを確認します (関数呼び出しで現在停止している場合は **F10** キーを 1 回押します)。 ウィンドウが閉じている場合は、 **[デバッグ] > [ウィンドウ] > [自動変数]** を使用して、 **[自動変数]** ウィンドウを開きます。

![[自動変数] ウィンドウ](../debugger/media/dbg-tips-autos-window.png "AutosWindow")

また、 **[イミディエイト]** ウィンドウで関数を入力して、戻り値を表示することもできます。 ( **[デバッグ] > [ウィンドウ] > [イミディエイト]** を使用して開きます)。

![イミディエイト ウィンドウ](../debugger/media/dbg-tips-immediate-window.png "ImmediateWindow")

また、 **[ウォッチ]** ウィンドウと **[イミディエイト]** ウィンドウでは、`$ReturnValue` などの [擬似変数](../debugger/pseudovariables.md)を使用することもできます。

## <a name="inspect-strings-in-a-visualizer"></a><a name="string_visualizer"></a>ビジュアライザーで文字列を調べる

文字列を使用する場合、書式設定された文字列全体を表示すると便利なことがあります。 プレーンテキスト、XML、HTML、または JSON の文字列を表示するには、文字列値が含まれる変数をポイントして、虫眼鏡アイコン ![ビジュアライザー アイコン](../debugger/media/dbg-tips-visualizer-icon.png "ビジュアライザー アイコン") をクリックします。

![文字列ビジュアライザーを開く](../debugger/media/dbg-tips-string-visualizers.png "OpenStringVisualizer")

文字列ビジュアライザーは、文字列の種類に応じて、文字列の形式が正しくないかどうかを調べるのに役立ちます。 たとえば、空白の **[値]** フィールドは、ビジュアライザーの種類によって文字列が認識されないことを示します。 詳細については、「[[String ビジュアライザー] ダイアログ ボックス](../debugger/string-visualizer-dialog-box.md)」を参照してください。

![JSON 文字列ビジュアライザー](../debugger/media/dbg-tips-string-visualizer-json.png "JSONStringVisualizer")

デバッガー ウィンドウに表示される DataSet オブジェクトや DataTable オブジェクトなどの他のいくつかの型については、組み込みビジュアライザーを開くこともできます。

## <a name="break-into-code-on-handled-exceptions"></a>ハンドルされる例外でコードを中断する

デバッガーでは、ハンドルされない例外でコードを中断します。 しかし、ハンドルされる例外 (`try/catch` ブロック内で発生する例外など) もバグの原因になる可能性があり、発生した場合は調査する必要があります。 **[例外設定]** ダイアログ ボックスでオプションを構成することにより、ハンドルされる例外でもコードを中断するようにデバッガーを構成できます。 **[デバッグ] > [ウィンドウ] > [例外設定]** を選択して、このダイアログ ボックスを開きます。

**[例外設定]** ダイアログ ボックスを使用すると、特定の例外でコードを中断するようにデバッガーに指示できます。 次の図では、`System.NullReferenceException` が発生するたびにデバッガーはコードを中断します。 詳細については、[例外の管理](../debugger/managing-exceptions-with-the-debugger.md)に関するページを参照してください。

![[例外設定] ダイアログ ボックス](../debugger/media/dbg-tips-exception-settings.png "ExceptionSettingsDialogBox")

## <a name="debug-deadlocks-and-race-conditions"></a>デッドロックと競合の状態をデバッグする

マルチスレッド アプリに共通する問題の種類をデバッグする必要がある場合、デバッグ中にスレッドの場所を確認すると役に立つことがよくあります。 これは、 **[ソースのスレッドを表示]** ボタンを使用して簡単に行うことができます。

#### <a name="to-show-threads-in-your-source-code"></a>ソース コードのスレッドを表示するには

1. デバッグ中に、 **[デバッグ]** ツール バーの **[ソースのスレッドを表示]** ボタン ![ソースのスレッドを表示](../debugger/media/dbg-multithreaded-show-threads.png "ThreadMarker") をクリックします。

2. ウィンドウ左端の余白に注目します。 この行には、2 本の布糸に似た "*スレッド マーカー*" アイコン ![スレッド マーカー](../debugger/media/dbg-thread-marker.png "ThreadMarker") が表示されます。 スレッド マーカーは、スレッドが停止している位置を示します。

    スレッド マーカーは、ブレークポイントによって部分的に隠されている場合があることに注意してください。

3. スレッド マーカーの上にポインターを置きます。 DataTip が表示されます。 データヒントは、停止したスレッドごとに名前とスレッド ID 番号を表示します。

    [[並列スタック] ウィンドウ](../debugger/get-started-debugging-multithreaded-apps.md)でスレッドの場所を表示することもできます。

::: moniker range="vs-2017"
## <a name="examine-payloads-for-web-services-and-network-resources-uwp"></a>Web サービスとネットワーク リソース (UWP) のペイロードを調べる

UWP アプリでは、実行されたネットワーク操作を、`Windows.Web.Http` API を使用して分析できます。 このツールは、Web サービスとネットワーク リソースのデバッグに役立つことがあります。 このツールを使用するには、 **[デバッグ] > [パフォーマンス プロファイラー]** を選択します。 **[ネットワーク]** を選択し、 **[開始]** を選択します。 アプリで、`Windows.Web.Http` を使用するシナリオを実行し、 **[コレクションの停止]** を選択してレポートを生成します。

![ネットワーク使用率プロファイリング ツール](../profiling/media/prof-tour-network-usage.png "NetworkUsageProfTool")

概要ビューで操作を選択すると、詳細が表示されます。

![ネットワーク使用率ツールの詳細情報](../profiling/media/prof-tour-network-usage-details.png "DetailedViewNetworkUsage")

詳細については、「[ネットワーク使用率](../profiling/network-usage.md)」を参照してください。
::: moniker-end

## <a name="get-more-familiar-with-how-the-debugger-attaches-to-your-app-c-c-visual-basic-f"></a><a name="modules_window"></a> アプリにデバッガーをアタッチする方法について理解を深める (C#、C++、Visual Basic、F#)

実行中のアプリにアタッチするために、デバッガーでは、デバッグ対象のアプリとまったく同じビルド用に生成されたシンボル (.pdb) ファイルが読み込まれます。 場合によっては、シンボル ファイルに関する知識が少しあると役に立つことがあります。 Visual Studio でシンボル ファイルがどのように読み込まれているかは、 **[モジュール]** ウィンドウを使用して調べることができます。

デバッグ中に **[デバッグ] > [ウィンドウ] > [モジュール]** を選択して、 **[モジュール]** ウィンドウを開きます。 **[モジュール]** ウィンドウでは、デバッガーによってユーザー コード ("[*マイ コード*](../debugger/just-my-code.md)") として扱われているモジュールや、モジュールのシンボル読み込み状態を確認できます。 ほとんどのシナリオでは、ユーザー コードのシンボル ファイルはデバッガーによって自動的に検出されますが、.NET コード、システム コード、またはサードパーティのライブラリ コードにステップ イン (デバッグ) する場合は、正しいシンボル ファイルを取得するために追加の手順が必要になります。

![[モジュール] ウィンドウでシンボル情報を表示する](../debugger/media/dbg-tips-modules-window.png "ViewSymbolInformation")

**[モジュール]** ウィンドウで右クリックして **[シンボルの読み込み]** を選択することで、シンボル情報を直接読み込むことができます。

場合によっては、(フットプリントを削減するため) アプリに一致するシンボル ファイルが付属していなくても、アプリ開発者は、後でリリースされるバージョンをデバッグできるように、ビルドと一致するシンボル ファイルのコピーを保持していることがあります。

デバッガーでコードがユーザー コードとして分類される方法については、[マイ コードのみ](../debugger/just-my-code.md)に関するページを参照してください。 シンボル ファイルの詳細については、「[Visual Studio デバッガーでのシンボル (.pdb) ファイルとソース ファイルの指定](specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)」を参照してください。

## <a name="learn-more"></a>詳細情報

その他のヒントとテクニックおよびさらに詳しい情報については、次のブログ投稿を参照してください。

- [Visual Studio でのデバッグのためのあまり知られていない 7 つのハック](https://devblogs.microsoft.com/visualstudio/7-lesser-known-hacks-for-debugging-in-visual-studio/)
- [Visual Studio の 7 つの秘宝](https://devblogs.microsoft.com/visualstudio/7-hidden-gems-in-visual-studio-2017/)

## <a name="see-also"></a>関連項目

[キーボード ショートカット](../ide/productivity-shortcuts.md)
