---
title: Visual Studio 2015 でのデバッグを使用したはじめに |Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: c3a14d28-d811-4ff3-bd09-21dce14025ca
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ca3f3806f9097082d71dd80e74ccf48cd78c951b
ms.sourcegitcommit: a77158415da04e9bb8b33c332f6cca8f14c08f8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2020
ms.locfileid: "86386889"
---
# <a name="getting-started-with-debugging-in-visual-studio-2015"></a>Visual Studio 2015 のデバッグの概要
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 2015 は、プロジェクトのビルドとデバッグ ツールの強力な統合セットを提供します。 このトピックでは、デバッグ UI 機能の最も基本的なセットの使用を開始する方法が説明されます。

 注: より高度な機能およびプラットフォーム固有のトピックまたは機能固有のトピックへのリンクがこのページの下部にあります。

## <a name="my-code-doesnt-work-help-me-visual-studio-2015"></a>コードが機能しません。 Visual Studio 2015 の助けが必要です。
 エディターを見つけ、コードをいくらか作成しました。 これから、そのコードのデバッグを開始します。 ほとんどの IDE と同じように、Visual Studio 2015 には、2 つのデバッグ フェーズがあります。1 つは、コードをビルドして、プロジェクト エラーとコンパイラ エラーをキャッチして解決するフェーズです。もう 1 つは、環境でそのコードを実行し、実行時エラーと動的エラーをキャッチして解決するフェーズです。

### <a name="configuring-a-build"></a>ビルドの構成
 ビルドの構成には、**デバッグ**と**リリース** の 2 つの基本的な種類があります。 最初の構成では、より低速で大きな実行可能ファイルが生成されます。対話型の実行時デバッグ機能はより豊富ですが、これが出荷されることはありません。 2 つ目のビルドはより高速で、より最適化された実行可能ファイルです。(少なくともコンパイラの観点から) このビルドが出荷に適しています。

 既定のビルド構成は、**デバッグ**です。

 ![Visual Studio の [デバッグ ビルド] ボタン](../ide/media/vs-ide-gs-debug-build-type1.PNG "Vs_ide_gs_debug_build_type1")

 対象となる特定のビルド プラットフォームを指定することもできます。たとえば、**x86** (32 ビット Intel CPUs)、**x64** (64 ビット Intel CPU)、**ARM** (特定の種類のアプリでのみサポートされる ARM CPU) などです。 マネージド プロジェクトとネイティブ プロジェクトの既定値は **x86** です。 これを変更するには、ビルド プラットフォームのドロップダウンをクリックし、異なるプラットフォームか **[構成マネージャー]** を選択します。

 ![Visual Studio の構成ファイル マネージャー ウィンドウ](../ide/media/vs-ide-gs-debug-build-cf-mgr.PNG "Vs_ide_gs_debug_build_cf_mgr")

 **構成マネージャー**を使用して、対象のビルド構成を指定できます。 これを起動し、**[構成]** ドロップダウンか **[CPU]** ドロップダウンをクリックし、**[新規作成]** を選択して、 新しいビルドまたはプラットフォームを作成します。

 ![Visual Studio の構成マネージャー ウィンドウ](../ide/media/vs-ide-gs-debug-build-cf-mgr-2.PNG "Vs_ide_gs_debug_build_cf_mgr_2")

 開始時には、ビルド構成、プラットフォームとして**デバッグ**、**x86** だけを使用してください。 コーディングとデバッグが完了したら、構成を**リリース**に変更し、特定のプラットフォームを対象にします。 (以前のバージョンの Visual Studio では、**AnyCPU** が .Net コード プロジェクトの既定のプラットフォームとして提供されていました。)

 注: プロジェクトをビルドする際、実行可能ファイルを格納するために作成されるプロジェクト ディレクトリ パスを判断するために構成の値とプラットフォームの値も使用されます。 通常、これは** \<path-to-project> \\ プロジェクト名 \> \\<構成 \> \\<プラットフォーム \><** ます。 たとえば、構成が `Debug` で、プラットフォームが `x86` のプロジェクトの場合、`Projects\MyProjectNameHere\MyProjectNameHere\bin\Debug\x86` の下で見つかります。 これは、ビルドされたこれらの実行可能ファイルを管理する独自のツールやスクリプトがある場合に役立ちます。

### <a name="building-your-code"></a>コードのビルド
 ビルドを構成すると、実際にプロジェクトのビルドを開始できます。 最も簡単な方法は F7 を押す方法ですが、メイン メニューから **[ビルド]、[ソリューションのビルド]** の順に選択してビルドを開始することもできます。

 ![Visual Studio ビルド プロジェクト メニューの選択](../ide/media/vs-ide-gs-debug-build-menu-item.png "Vs_ide_gs_debug_build_menu_item")

 ビルド プロセスは、Visual Studio UI の下部にある **[出力]** 状況ウィンドウで監視できます。 エラー、警告、ビルド操作がここに表示されます。 エラーがあると (または構成されたレベルより上の警告があると)、ビルドは失敗します。 エラーと警告をクリックすると、それが発生した行に移動できます。 **F7** をもう一度押すか (エラーがあるファイルのみを再コンパイルする場合)、**Ctrl + Alt + F7** を押してプロジェクトを再ビルドします (クリーンかつ完全な再ビルドの場合)。

 エディターの下の結果ウィンドウに 2 つのビルド用のタブ付きウィンドウが表示されます。1 つは [**出力]** ウィンドウで、このウィンドウには生のコンパイラの出力が表示されます (エラー メッセージを含む)。もう 1 つは **[エラー一覧]** ウィンドウで、このウィンドウにはすべてのエラーと警告の、ソートおよびフィルターが可能な一覧が表示されます。

 成功すると、**[出力]** ウィンドウに次のような結果が表示されます。

 ![Visual Studio の成功したビルドの出力](../ide/media/vs-ide-gs-debug-success-build.PNG "vs_ide_gs_debug_success_build")

### <a name="reviewing-the-error-list"></a>エラー一覧のレビュー
 前にコンパイルが成功したコードに変更を加えた場合、エラーが出ることが少なくありません。 コーディングに不慣れな場合には、その可能性が高くなります。 エラーは、単純な構文エラーや変数名の間違いのように分かりやすい場合もあれば、手引きとして暗号のようなコードしかないような分かりにくい場合もあります。 問題を明確に表示するには、[ビルド**出力**] ウィンドウの下部に移動し、[**エラー一覧**] タブをクリックします。これにより、プロジェクトのエラーと警告が整理されたビューに移動し、いくつかの追加オプションも表示されます。

 ![Visual Studio 2015 の出力とエラー一覧](../ide/media/vs-ide-gs-debug-bad-build-error-list.PNG "Vs_ide_gs_debug_bad_build_error_list")

 **[エラー一覧]** ウィンドウのエラー行をクリックし、エラーが発生した行にジャンプします。 または、右上の**クイック起動**バーをクリックして行番号をオンにし、その横に「行番号」と入力して、enter キーを押します。 これは、**[オプション]** ウィンドウ エントリを表示する最も簡単な方法です。そのウィンドウで行番号をオンにすることができます。 **[クイック起動]** バーの使用について学ぶと、UI をクリックする回数を減らすことができます。)

 ![Visual Studio の行番号を含むエディター](../ide/media/vs-ide-gs-debug-line-numbers.png "Vs_ide_gs_debug_line_numbers")

 ![Visual Studio の行番号オプション](../ide/media/vs-ide-gs-debug-options-line-numbers.png "Vs_ide_gs_debug_options_line_numbers")

 Ctrl + G を押すと、エラーが発生した行番号にすぐにジャンプします。

 エラーは、赤い「波線」の下線によって示されます。 その上に移動すると、追加の詳細が表示されます。 修正を加え (これによって新たなエラーが入り込む可能性はあります)、別の場所に移動します。 (これを「回帰」と呼びます。)

 ![Visual Studio のエラー ホバー](../ide/media/vs-ide-gs-debug-error-hover1.png "Vs_ide_gs_debug_error_hover1")

 エラー一覧を確認し、コード内のすべてのエラーを解決します。

 ![Visual Studio の [デバッグ エラー] ウィンドウ](../ide/media/vs-ide-gs-debug-error-list.PNG "Vs_ide_gs_debug_error_list")

### <a name="reviewing-errors-in-detail"></a>エラーの詳細のレビュー
 コンパイラの観点からすると、多くのエラーはあまり意味がない可能性があります。 その場合、追加情報が必要です。 **[エラー一覧]** ウィンドウから、対応する入力行を右クリックし、コンテキスト メニューから **[エラーのヘルプを表示**] 選択することで、Bing の自動検索を実行して、エラー (または警告) に関する詳細を入手することができます。

 ![Visual Studio のエラー一覧の Bing 検索](../ide/media/vs-ide-gs-debug-error-list-error-help.png "Vs_ide_gs_debug_error_list_error_help")

 これにより、エラー コードとテキストの Bing 検索の結果をホストするタブが Visual Studio 2015 内で起動します。 インターネット上の異なるさまざまなソースからの結果を入手できますが、すべてが役立つ情報であるとは限りません。

 **[エラー一覧]** の **[コード]** 列のハイパーリンク付きのエラー コード値をクリックすることもできます。 これにより、エラー コードだけを探す Bing 検索が起動します。

### <a name="performing-static-code-analysis"></a>静的コード分析の実行
 「静的コード分析」とは、「コード管理における実行時エラーまたは問題の発生原因となり得る一般的な問題を探して自動的にコードをチェックすること」のしゃれた言い方です。 ビルドの妨げとなる明らかなエラーをクリーンアップした後に静的コード分析を実行することを習慣づけてください。それによって生成される可能性がある警告に対処するための時間を取ってください。 将来の頭痛の種を取り除き、コード スタイルの手法をいくらか学ぶことになります。

 Alt+F11 を押して (または、上部のメニューから **[分析]、[ソリューションでコード分析を実行]** の順に選択して) 静的コード分析を開始します。 多くのコードがある場合は時間がかかる可能性があります。

 ![Visual Studio 2015 コード分析のメニュー項目](../ide/media/vs-ide-gs-debug-run-code-analysis.png "Vs_ide_gs_debug_run_code_analysis")

 新しい警告または更新された警告があれば、IDE 下部の **[エラー一覧]** タブに表示されます。 警告をクリックして、その警告にジャンプします。

 ![Visual Studio 2015 の警告を含むエラー一覧](../ide/media/vs-ide-gs-debug-code-analysis-warning-error-list.PNG "vs_ide_gs_debug_code_analysis_warning_error_list")

 警告は、赤色の波線ではなく、明るい黄緑色の波線で示されます。 その警告の上に移動すると詳細が表示されます。右クリックすると、コンテキスト メニューが表示され、修正やリファクタリング オプションを支援します。

 ![Visual Studio Code 分析の警告ホバー](../ide/media/vs-ide-gs-debug-code-analysis-warning-hover.png "vs_ide_gs_debug_code_analysis_warning_hover")

### <a name="using-light-bulbs-to-fix-or-refactor-code"></a>電球を使用したコードの修正またはリファクタリング
 電球は、Visual Studio 2015 の新しい機能です。電球を使用すると、コード インラインをリファクタリングできます。 これは、一般的な警告を迅速かつ効率的に修正する簡単な方法です。 電球にアクセスするには、警告の波線を右クリックします (あるいは、波線の上にいる間に Ctrl + を押します)。 その後、**[クイック操作]** を選択します。

 ![Visual Studio 2015 電球のクイック オプション](../ide/media/vs-ide-gs-debug-light-bulb1.png "Vs_ide_gs_debug_light_bulb1")

 そのコード行に適用できる修正またはリファクタの一覧が表示されます。

 ![Visual Studio 2015 電球のプレビュー](../ide/media/vs-ide-gs-debug-light-bulb-preview-changes.PNG "Vs_ide_gs_debug_light_bulb_preview_changes")

 電球は、コード アナライザーが、コードの修正、リファクタリング、改善の機会があると判断したときはいつでも使用できます。 任意のコード行をクリックし、右クリックしてコンテキスト メニューを開き、**[クイック オプション]** を選択します (あるいは、効率的な方法としては、Ctrl + を押します)。 領域リファクタリングまたは改善のオプションが使用可能な場合、そのオプションが表示されます。使用可能でない場合、「`No quick options available here`」というメッセージが IDE の左下隅のベゼルに表示されます。

 ![Visual Studio 2015 電球 'オプションなし' テキスト](../ide/media/vs-ide-gs-debug-light-bulb-no-options.PNG "Vs_ide_gs_debug_light_bulb_no_options")

 慣れてくれば、矢印キーと Ctrl + で簡単に操作できます。 を使用して、クイック オプションのリファクタリング機会をチェックし、コードをクリーンアップできます。

 電球の詳細については、「[電球を使用したクイック操作の実行](../ide/perform-quick-actions-with-light-bulbs.md)」を参照してください。

### <a name="debugging-your-running-code"></a>実行されているコードのデバッグ
 これでコードが正常にビルドされ、クリーンアップが実行されたので、次に、F5 を押すか **[デバッグ]、[デバッグの開始]** の順に選択してコードを実行します。 これにより、デバッグ環境でアプリが開始され、その動作を詳しく監視できるようになります。 Visual Studio 2015 IDE は、アプリの実行中に変更されます。**[出力]** ウィンドウは、2 つの新しいウィンドウに置き換えられます (既定のウィンドウ構成)。その 1 つは **[自動変数]/[ローカル]/[モジュール]/[ウォッチ]** タブのあるウィンドウで、もう 1 つは **[呼び出し履歴]/[ブレークポイント]/[例外設定]/[出力]** タブのあるウィンドウです。 これらのウィンドウには複数のタブがあり、そのタブでアプリの変数、スレッド、呼び出し履歴、その他さまざまな動作を実行と同時に調べ、評価することができます。

 ![VS2015 の自動変数ウィンドウと呼び出し履歴ウィンドウ](../ide/media/vs-ide-gs-debug-autos-and-call-stack.PNG "Vs_ide_gs_debug_autos_and_call_stack")

 さまざまなアプリで操作を試し、変更を確認してください。 異常が表示された場合は、Ctrl + Alt + Break を押してアプリを一時停止してください (あるいは、**[一時停止]** ボタンをクリックしてください)。

 ![Visual Studio の [すべて中断] ボタン](../ide/media/vs-ide-gs-debug-break-all-button.png "vs_ide_gs_debug_break_all_button")

 F5 を押し、アプリの実行を続行します (または **[続行]** ボタンをクリックします)。

 ![Visual Studio の [デバッグの続行] ボタン](../ide/media/vs-ide-gs-debug-continue-button.png "Vs_ide_gs_debug_continue_button")

 Shift+F5 を押すか、**[停止]** ボタンをクリックすると、アプリを一時停止できます。 あるいは、単にアプリのメイン ウィンドウを閉じます (またはコマンド ライン ダイアログ)。

 コードが完璧に、予想通りに実行されれば、成功です。 ビルド構成を **[リリース]** に変更し、配置のために再ビルドします。 (専門家は、最後に単体テストのビットにジャンプしたい場合があります)。ただし、応答が停止したりクラッシュしたりした場合、または予期しない結果が発生した場合は、それらの問題の原因を特定し、バグを修正する必要があります。

### <a name="setting-simple-breakpoints"></a>単純なブレークポイントの設定
 ブレークポイントは、信頼できるデバッグの最も基本的で重要な機能です。 ブレークポイントは、Visual Studio が実行コードを中断する場所を示します。これにより、変数の値またはメモリの動作を確認したり、コードの分岐が実行されるかどうかを確認したりすることができます。 ブレークポイントを設定して削除した後、プロジェクトを再ビルドする必要はありません。

 中断させたい場所の行の外側の余白をクリックし、コードの行を選択し、F9 を押して、ブレークポイントを設定します。 コードを実行すると、このコードの行の指示が実行される前に停止します。

 ![Visual Studio のブレークポイント](../ide/media/vs-ide-gs-debug-breakpoint1.png "Vs_ide_gs_debug_breakpoint1")

 コードが中断すると、コードのマークの付いた行はまだ実行されません。 この時点で、ブレークポイントによってマークが付けられているコードの行の指示を実行し、変更された値を確認することもできます。 これを、コードの「ステップ イン」と呼びます。 マークされているコードがメソッド呼び出しの場合、F11 キーを押してステップ インすることができます。 F10 キーを押して、コードの行を "ステップ オーバー" することもできます。 ブレークポイント ステップ アクションについては、「[デバッガーでのコード間の移動](../debugger/navigating-through-code-with-the-debugger.md)」を参照してください。

 ブレークポイントの一般的な使用は、次のとおりです。

1. クラッシュまたは応答しないプログラムのソースを絞り込むには、エラーの原因と考えられるメソッド呼び出しのコード全体を中心に散布図を作成します。 コードをステップ実行しながら、問題の原因になっているコードの行が見つかるまで、そこに近づくよう、コードのブレークポイントを削除してリセットしていきます。

2. 新しいコードを導入する際、その先頭にブレークポイントを設定し、コードをステップ実行し、予想どおり動作するかを確かめます。

3. 複雑な動作を実装している場合は、プログラムが中断したときに変数の値やデータを調べることができるよう、アルゴリズムのコードに対してブレークポイントを設定します。

4. C または C++ コードを作成している場合、ブレークポイントを使用してコードを停止します。これにより、メモリに関連した障害をデバッグするときに、アドレス値 (NULL の検索) および参照カウントを調べることができます。

   ブレークポイントの使用の詳細については、「[ブレークポイントの使用](../debugger/using-breakpoints.md)」を参照してください。

### <a name="setting-conditional-breakpoints"></a>条件付きブレークポイントの設定
 ループまたは再帰処理の中にブレークポイントがある場合、または頻繁にステップ実行するブレークポイントが多数ある場合、条件付きブレークポイントを使用して、特定の条件が満たされる場合のみコードが中断するようにしてください。 そうしないと、F11 をひたすら押し続けることになります。

 条件付きブレークポイントを設定し、変数が特定の値に設定されたとき、または特定のしきい値を渡したときにコードを中断するようにするには、余白をクリックしてブレークポイントを設定し、表示されるホバー メニューから「歯車」を選択します。

 ![Visual Studio 2015 のブレークポイントの設定](../ide/media/vs-ide-gs-debug-breakpoint-settings.png "Vs_ide_gs_debug_breakpoint_settings")

 次のようなダイアログが表示され、このダイアログで、中断が発生するための特定の条件を設定できます。

 ![Visual Studio 2015 の条件付きブレークポイント](../ide/media/vs-ide-gs-debug-breakpoint-conditional.PNG "Vs_ide_gs_debug_breakpoint_conditional")

 条件付きブレークポイントの評価に使用する式を宣言する方法については、Channel9 ビデオ「[Breakpoint Configuration Experience in Visual Studio 2015](https://channel9.msdn.com/Events/Visual-Studio/Connect-event-2014/711)」(Visual Studio 2015 でのブレークポイント構成操作) をご覧ください。

### <a name="inspecting-your-code-at-run-time"></a>実行時のコードの検査
 実行中のコードがブレークポイントにヒットして停止したときに、変数と呼び出し履歴を調べ、内容を確認することができます。 範囲内の値は、予期していたとおりのものですか。 呼び出しの順序は正しいですか。

 ![Visual Studio 2015 run&#45;time 値の検査](../ide/media/vs-ide-gs-debug-inspect-value.PNG "vs_ide_gs_debug_inspect_value")

 変数の上に移動し、その変数に現在格納されている値と参照を確認します。 表示される値が、予期していたものと異なる場合、先行するコード行または呼び出しているコード行にバグがある可能性があります。 ブレークポイントを上に移動するか、条件を既存のブレークポイントに追加して、検索の範囲を狭めます。

 さらに、Visual Studio 2015 では [診断ツール] ウィンドウが表示されます。このウィンドウで、時間の経過に伴うアプリの CPU 使用率とメモリ使用量の変化を監視することができます。 これを使用して、予期していなかった高い CPU 使用率またはメモリ割り当てがないか調べます。 これを **[ウォッチ]** ウィンドウおよびブレークポイントとともに使用して、予期していなかった多量の使用の原因となっているもの、または解放されていないリソースを特定します。

 ![Visual Studio 2015 の [診断ツール] ウィンドウ](../ide/media/vs-ide-gs-debug-diagnostic-tools.PNG "Vs_ide_gs_debug_diagnostic_tools")

### <a name="running-unit-tests"></a>単体テストの実行
 単体テストは、アプリやサービスのコード パスを実行するプログラムです。 Visual Studio 2015 は、マネージド コードおよびネイティブ コード用の Microsoft 単体テスト フレームワークをインストールします。 単体テスト フレームワークを使用して、単体テストを作成して実行し、そのテストの結果を報告します。 変更を加えたときは単体テストを再実行し、コードが正しく機能するかテストします。 Visual Studio 2015 Enterprise を使用すると、ビルドの後にテストを自動的に実行できます。

 最初に、「[IntelliTest でのコードの単体テストの生成](../test/generate-unit-tests-for-your-code-with-intellitest.md)」をお読みください。

 Visual Studio 2015 の単体テストの詳細、およびより優れた品質のコードの作成に単体テストがどのように役立つかについては、「[単体テストの基本](../test/unit-test-basics.md)」をお読みください。

## <a name="see-also"></a>参照
 [Visual Studio デバッガーでのデバッグ](../debugger/debugging-in-visual-studio.md)[設定と準備](../debugger/debugger-settings-and-preparation.md)[デバッグ64ビットアプリケーション](../debugger/debug-64-bit-applications.md)[デバッガーの基本](../debugger/debugger-basics.md)
