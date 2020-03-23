---
title: デバッガでのヒントとコツ
description: Visual Studio デバッガーでサポートされるあまり知られていない機能の一部について説明します。
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bf8d6df020694bb10fe4f3f051551056549d5673
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301177"
---
# <a name="learn-productivity-tips-and-tricks-for-the-debugger-in-visual-studio"></a>Visual Studio でのデバッガーの生産性に関するヒントとコツについて学習する

Visual Studio デバッガーの生産性に関するいくつかのヒントとコツについては、このトピックを参照してください。 デバッガーの基本的な機能については、「[最初にデバッガーを見る](../debugger/debugger-feature-tour.md)」を参照してください。 このトピックでは、機能ツアーに含まれていない領域について説明します。

## <a name="pin-data-tips"></a>ピン データのヒント

デバッグ中に頻繁にデータヒントにカーソルを合わせる場合は、変数のデータヒントをピン留めして、すばやくアクセスできます。 変数は再起動後も固定されたままになります。 データヒントをピン留めするには、ピンアイコンをクリックしてピンをポイントします。 複数の変数をピン留めできます。

![データヒントのピン留め](../debugger/media/dbg-tips-data-tips-pinned.png "ピン留めデータヒント")

## <a name="edit-your-code-and-continue-debugging-c-vb-c"></a>コードを編集してデバッグを続行する (C#、VB、C++)

Visual Studio でサポートされているほとんどの言語で、デバッグ セッション中にコードを編集し、デバッグを続行できます。 この機能を使用するには、デバッガーの一時停止中にカーソルを使用してコードをクリックし、編集を行い、**F5**、**F10**、または **F11** キーを押してデバッグを続行します。

![エディット コンティニュのデバッグ](../debugger/media/dbg-tips-edit-and-continue.gif "EditAndContinue")

機能の使用および機能制限の詳細については、[エディット コンティニュ](../debugger/edit-and-continue.md)に関するページを参照してください。

## <a name="edit-xaml-code-and-continue-debugging"></a>XAML コードを編集してデバッグを続行する

デバッグ セッション中に XAML コードを変更するには、[XAML ホット リロードで実行中の XAML コードを記述およびデバッグする](../xaml-tools/xaml-hot-reload.md)方法に関するページを参照してください。

## <a name="debug-issues-that-are-hard-to-reproduce"></a>再現が困難なデバッグの問題

アプリで特定の状態を再作成することが困難または時間がかかる場合は、条件付きブレークポイントを使用することが役立つかどうかを検討してください。 [条件付きブレークポイント](../debugger/using-breakpoints.md#BKMK_Specify_a_breakpoint_condition_using_a_code_expression)とフィルター ブレークポイントを使用すると、アプリが目的の状態 (変数が不適切なデータを格納している状態など) に切り込むのを防ぐことができます。 式、フィルター、ヒットカウントなどを使用して条件を設定できます。

#### <a name="to-create-a-conditional-breakpoint"></a>条件付きブレークポイントを作成するには

1. ブレークポイントアイコン (赤いボール) を右クリックし、[**条件 ]** を選択します。

2. [**ブレークポイントの設定]** ウィンドウで、式を入力します。

    ![条件付きブレークポイント](../debugger/media/dbg-multithreaded-conditional-breakpoint.png "条件付きブレークポイント")

3. 別の種類の条件を使用する場合は、[**ブレークポイントの設定]** ダイアログ ボックスで **[条件式**] ではなく [**フィルター** ] を選択し、フィルターヒントに従います。

## <a name="configure-the-data-to-show-in-the-debugger"></a>デバッガーに表示するデータを構成する

C# 、Visual Basic、および C++ (C++/CLI コードのみ) の場合は、[デバッガー表示](../debugger/using-the-debuggerdisplay-attribute.md)属性を使用して表示する情報をデバッガーに指示できます。 C++ コードの場合は[、Natvis の視覚化](create-custom-views-of-native-objects.md)を使用して同じことができます。

## <a name="change-the-execution-flow"></a>実行フローを変更する

デバッガーがコード行で一時停止している状態で、マウスを使用して左側の黄色い矢印ポインタを取得します。 黄色の矢印ポインタをコード実行パス内の別のポイントに移動します。 次に、F5 またはステップ コマンドを使用して、アプリの実行を続行します。

![実行ポインタを移動する](../debugger/media/dbg-tour-move-the-execution-pointer.gif "実行ポインタを移動する")

実行フローを変更することにより、さまざまなコード実行パスをテストしたり、デバッガーを再起動することなくコードを再実行したりできます。

> [!WARNING]
> 多くの場合、この機能には注意する必要があり、ツールヒントに警告が表示されます。 他の警告が表示される場合もあります。 ポインターを移動しても、アプリを以前のアプリケーション状態に戻すことはできません。

## <a name="track-an-out-of-scope-object-c-visual-basic"></a>スコープ外のオブジェクトを追跡する (C#、Visual Basic)

**ウォッチ**ウィンドウのようなデバッガー ウィンドウを使用して変数を表示するのは簡単です。 ただし、**ウォッチ**ウィンドウで変数がスコープ外に出ると、その変数がグレー表示されていることに気付くことがあります。アプリのシナリオによっては、変数がスコープ外の場合でも変数の値が変化する場合があり、変数を注意深く監視する必要があります (たとえば、変数がガベージ コレクションを受ける場合など)。 ウォッチ**ウィンドウで**変数のオブジェクト ID を作成することで、変数を追跡できます。

#### <a name="to-create-an-object-id"></a>オブジェクト ID を作成するには

1. 追跡する変数の近くにブレークポイントを設定します。

2. デバッガを起動して **(F5)** し、ブレークポイントで停止します。

3. [ローカル] ウィンドウ (**[Windows >****の**デバッグ > ローカル] ) で変数を見つけて、変数を右クリックし、[オブジェクト**ID の作成**] を選択します。

    ![オブジェクト ID の作成](../debugger/media/dbg-tips-watch-create-object-id.png "CreateObjectID")

4. **[ローカル**]**$** ウィンドウにプラスの数字が表示されます。 この変数はオブジェクト ID です。

5. オブジェクト ID 変数を右クリックし、[**ウォッチの追加 ]** を選択します。

詳細については、「オブジェクト[ID の作成](../debugger/watch-and-quickwatch-windows.md#bkmk_objectIds)」を参照してください。

## <a name="view-return-values-for-functions"></a>関数の戻り値を表示する

関数の戻り値を表示するには、コードのステップ実行中に **[自動変数**] ウィンドウに表示される関数を確認します。 関数の戻り値を確認するには、対象の関数が既に実行されていることを確認します (関数呼び出しで現在停止している場合は **、F10**を 1 回押します)。 ウィンドウが閉じている場合は **、Windows > Autos >デバッグ**を使用して**自動ウィンドウを**開きます。

![自動ウィンドウ](../debugger/media/dbg-tips-autos-window.png "オートウィンドウ")

さらに、**イミディエイト**ウィンドウに関数を入力して、戻り値を表示することもできます。 (**デバッグ > Windows >即時**を使用して開きます。

![イミディエイト ウィンドウ](../debugger/media/dbg-tips-immediate-window.png "イミディエイトウィンドウ")

[**ウォッチ]** ウィンドウや **[イミディエイト**] ウィンドウ`$ReturnValue`で[擬似変数](../debugger/pseudovariables.md)を使用することもできます。

## <a name="inspect-strings-in-a-visualizer"></a><a name="string_visualizer"></a>ビジュアライザーで文字列を検査する

文字列を操作する場合は、書式設定された文字列全体を表示すると便利です。 プレーンテキスト、XML、HTML、または JSON 文字列を表示するには、虫眼鏡アイコン![VisualizerIcon](../debugger/media/dbg-tips-visualizer-icon.png "ビジュアライザー アイコン")をクリックし、文字列値を含む変数の上にマウスを移動します。

![文字列ビジュアライザーを開く](../debugger/media/dbg-tips-string-visualizers.png "ビジュアライザーを開く")

文字列ビジュアライザーは、文字列の種類に応じて、文字列の形式が正しくないかどうかを確認するのに役立ちます。 たとえば、空白の**値**フィールドは、ビジュアライザーの種類によって文字列が認識されないことを示します。 詳細については、「 [[文字列ビジュアライザー] ダイアログ ボックス](../debugger/string-visualizer-dialog-box.md)」を参照してください。

![JSON 文字列ビジュアライザー](../debugger/media/dbg-tips-string-visualizer-json.png "ビジュアライザー")

デバッガー ウィンドウに表示される DataSet オブジェクトや DataTable オブジェクトなど、その他のいくつかの種類の場合は、組み込みのビジュアライザーを開くことができます。

## <a name="break-into-code-on-handled-exceptions"></a>処理された例外のコードに分割する

デバッガは、未処理の例外に対してコードに分割されます。 ただし、処理された例外 (`try/catch`ブロック内で発生する例外など) もバグの原因となり、発生した場合に調査を行う必要があります。 **例外の設定**] ダイアログ ボックスでオプションを構成することによって、処理された例外のコードに分割するデバッガーを構成することもできます。 [Windows **>例外設定 >]** を選択してこのダイアログ ボックス>開きます。

**[例外の設定]** ダイアログ ボックスでは、デバッガーに特定の例外に関するコードに分割するように指示できます。 次の図では、デバッガーは`System.NullReferenceException`、発生するたびにコードに分割します。 詳しくは、[例外の管理を](../debugger/managing-exceptions-with-the-debugger.md)参照してください。

![[例外の設定] ダイアログ ボックス](../debugger/media/dbg-tips-exception-settings.png "ダイアログ ボックス")

## <a name="debug-deadlocks-and-race-conditions"></a>デッドロックと競合状態のデバッグ

マルチスレッド アプリに共通する問題の種類をデバッグする必要がある場合は、多くの場合、デバッグ中にスレッドの場所を表示するのに役立ちます。 [**ソースにスレッドを表示**] ボタンを使用すると、簡単に操作できます。

#### <a name="to-show-threads-in-your-source-code"></a>ソース コード内のスレッドを表示するには

1. デバッグ中に、[**デバッグ**] ツールバーの [**ソースのスレッド**を![表示](../debugger/media/dbg-multithreaded-show-threads.png "スレッドマーカー")] ボタンをクリックします。

2. ウィンドウ左端の余白に注目します。 この行には、2 つの布の*糸*に似た![スレッド マーカー](../debugger/media/dbg-thread-marker.png "スレッドマーカー")アイコンが表示されます。 スレッド マーカーは、スレッドが停止している位置を示します。

    スレッド マーカーは、ブレークポイントによって部分的に隠される場合があることに注意してください。

3. スレッド マーカーの上にポインターを置きます。 DataTip が表示されます。 データヒントは、停止したスレッドごとに名前とスレッド ID 番号を表示します。

    [[並列スタック] ウィンドウ](../debugger/get-started-debugging-multithreaded-apps.md)でスレッドの場所を表示することもできます。

::: moniker range="vs-2017"
## <a name="examine-payloads-for-web-services-and-network-resources-uwp"></a>Web サービスとネットワーク リソース (UWP) のペイロードを調べる

UWP アプリでは、API を使用して実行される`Windows.Web.Http`ネットワーク操作を分析できます。 このツールを使用すると、Web サービスおよびネットワーク リソースのデバッグに役立ちます。 このツールを使用するには、[**パフォーマンス プロファイラーのデバッグ>]** を選択します。 [**ネットワーク**] をクリックし、[**開始**] をクリックします。 アプリで、`Windows.Web.Http` を使用するシナリオを実行し、**[コレクションの停止]** を選択してレポートを生成します。

![ネットワーク使用率プロファイリング ツール](../profiling/media/prof-tour-network-usage.png "ネットワーク用途プロフツール")

概要ビューで操作を選択すると、詳細が表示されます。

![ネットワーク使用率ツールの詳細情報](../profiling/media/prof-tour-network-usage-details.png "詳細ビューネットワークの使用法")

詳細については、「[ネットワーク使用率](../profiling/network-usage.md)」を参照してください。
::: moniker-end

## <a name="get-more-familiar-with-how-the-debugger-attaches-to-your-app-c-c-visual-basic-f"></a><a name="modules_window"></a>デバッガーがアプリにアタッチする方法について詳しく説明します (C#、C++、Visual Basic、F#)。

実行中のアプリにアタッチするには、デバッガーは、デバッグしようとしているアプリとまったく同じビルドに対して生成されたシンボル (.pdb) ファイルを読み込みます。 シナリオによっては、シンボル ファイルに関する知識が少し役に立ちます。 Visual Studio では、[**モジュール**] ウィンドウを使用してシンボル ファイルを読み込む方法を確認できます。

デバッグ中に **[Windows** **> モジュールのデバッグ] >** 選択して、[モジュール] ウィンドウを開きます。 **[モジュール]** ウィンドウでは、デバッガーがユーザー コードまたは[*My Code*](../debugger/just-my-code.md)として処理しているモジュール、およびモジュールのシンボル読み込み状態を確認できます。 ほとんどの場合、デバッガーはユーザー コードのシンボル ファイルを自動的に検索しますが、.NET コード、システム コード、またはサードパーティのライブラリ コードにステップ イン (またはデバッグ) する場合は、正しいシンボル ファイルを取得するために追加の手順が必要です。

![[モジュール] ウィンドウでシンボル情報を表示する](../debugger/media/dbg-tips-modules-window.png "情報を表示する")

右クリックして [シンボルの読み込み] を選択すると **、[モジュール**] ウィンドウからシンボル情報を直接**読み込むことができます**。

アプリ開発者は、一致するシンボル ファイルを使用せずにアプリを出荷する (フットプリントを減らすために) が、リリースされたバージョンを後でデバッグできるように、ビルド用の一致するシンボル ファイルのコピーを保持することがあります。

デバッガーがコードをユーザー コードとして分類する方法については、「[マイ コードのみを](../debugger/just-my-code.md)参照してください。 シンボル ファイルの詳細については、「 [Visual Studio デバッガーでシンボル (.pdb) とソース ファイルを指定する](specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)」を参照してください。

## <a name="learn-more"></a>詳細情報

その他のヒントやテクニック、および詳細については、次のブログ記事を参照してください。

- [Visual Studio でデバッグするための 7 つのあまり知られていないハック](https://devblogs.microsoft.com/visualstudio/7-lesser-known-hacks-for-debugging-in-visual-studio/)
- [ビジュアルスタジオで7隠された宝石](https://devblogs.microsoft.com/visualstudio/7-hidden-gems-in-visual-studio-2017/)

## <a name="see-also"></a>関連項目

[キーボード ショートカット](../ide/productivity-shortcuts.md)
