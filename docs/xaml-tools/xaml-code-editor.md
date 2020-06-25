---
title: XAML コードエディター
ms.date: 06/16/2020
ms.topic: conceptual
monikerRange: vs-2019
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: d789ac099e6d0bba7a44f0d6efd7a19beec54c19
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85289830"
---
# <a name="xaml-code-editor"></a>XAML コードエディター

[Visual STUDIO IDE](../get-started/visual-studio-ide.md)の XAML コードエディターには、Windows プラットフォーム用の WPF アプリと UWP アプリを作成するために必要なすべてのツールと、 [Xamarin. フォーム](/xamarin/xamarin-forms/user-interface/text/editor/)が含まれています。 この記事では、XAML ベースのアプリを開発するときにコードエディターで果たす役割と、Visual Studio 2019 の XAML コードエディターに固有の機能の両方について説明します。

まず、開いている WPF プロジェクトで IDE (統合開発環境) を見てみましょう。 次の図は、XAML コードエディターと共に使用する主要な IDE ツールのいくつかを示しています。

:::image type="content" source="media/xaml-code-editor-overview-sml.png" alt-text="XAML で WPF プロジェクトが開かれている Visual Studio 2019 IDE" lightbox="media/xaml-code-editor-overview-lrg.png":::

イメージの左下から時計回りに、主要な IDE ツールは次のようになります。

- **[XAML コードエディター](#xaml-code-editor-ui)** ウィンドウで &mdash; は、コードを作成して編集するこの記事の内容が表示され &mdash; ます。
- UI をデザインする**[XAML デザイナー](creating-a-ui-by-using-xaml-designer-in-visual-studio.md)** ウィンドウ。
- **[ツールボックス](../ide/reference/toolbox.md)** のドッキング可能ウィンドウ。 UI にコントロールを追加します。
- [**[デバッグ](../debugger/debugger-feature-tour.md)**] ボタン。コードを実行してデバッグします。 <br>( [XAML ホットリロード](xaml-hot-reload.md)でデバッグしているときに、コードをリアルタイムで編集することもできます)。
- [**[ソリューションエクスプローラー](../ide/solutions-and-projects-in-visual-studio.md)** ] ウィンドウ。ファイル、プロジェクト、およびソリューションを管理します。
- [**[プロパティ](../ide/reference/properties-window.md)**] ウィンドウ。 ui の外観と ui コントロールの動作を変更します。

続行するには、XAML コードエディターに関するページを参照してください。

## <a name="xaml-code-editor-ui"></a>XAML コードエディターの UI

XAML アプリのコードエディターウィンドウは、標準 IDE にも表示されるいくつかの UI (ユーザーインターフェイス) 要素を共有しますが、XAML アプリの開発を簡単にするためのいくつかの固有の機能も含まれています。

ここでは、XAML コードエディターウィンドウ自体について説明します。

![Visual Studio の [XAML コードエディター] ウィンドウ](media/xaml-code-editor-window.png "Visual Studio 2019 の [XAML コードエディター] ウィンドウのスクリーンショット")

次に、コードエディターで各 UI 要素の機能を見てみましょう。

### <a name="first-row"></a>最初の行

XAML コードウィンドウの上部にある最初の行の左側には、[**デザイン**] タブ、[**スワップウィンドウ**] ボタン、[ **xaml** ] タブ、および [**ポップアウト xaml** ] ボタンがあります。

![Visual Studio の XAML コードエディターウィンドウの先頭の2行のうち、最初の行の左側が強調表示されているもの。](media/xaml-code-editor-top-row-left.png "左側の UI 要素が強調表示されている、Visual Studio 2019 の XAML コードエディターウィンドウの2つ目の先頭行のスクリーンショット")

そのしくみは次のとおりです。

- [**デザイン**] タブでは、XAML コードエディターのフォーカスを XAML デザイナーに変更します。
- [**ペインの交換**] ボタンをクリックすると、IDE の XAML デザイナーと XAML コードエディターが反転されます。
- Xaml**タブは**、フォーカスを xaml コードエディターに戻します。
- [**ポップアウト xaml** ] ボタンをクリックすると、IDE の外部にある別の xaml コードエディターウィンドウが作成されます。

右側には、**縦方向の分割**ボタン、**横方向の分割**ボタン、および [ペインの**折りたたみ**] ボタンがあります。

![Visual Studio の XAML コードエディターウィンドウの先頭の2行のうち、最初の行の右側が強調表示されているもの。](media/xaml-code-editor-top-row-right.png "右側の UI 要素が強調表示されている Visual Studio 2019 の XAML コードエディターウィンドウの最初の2つの行のスクリーンショット")

そのしくみは次のとおりです。

- **垂直分割**ボタンは、IDE の XAML デザイナーと XAML コードエディターの位置を水平方向の配置から垂直方向の配置に変更します。
- [**水平分割**] ボタンをクリックすると、IDE の XAML デザイナーの場所と XAML コードエディターが垂直方向の配置から水平方向の配置に変わります。
- [**ウィンドウの折りたたみ**] ボタンを使用すると、コードエディターであるかデザイナーであるかにかかわらず、下部のウィンドウの内容を折りたたむことができます。 (下のウィンドウを復元するには、もう一度同じボタンを選択します。これは、[**ウィンドウの展開**] ボタンという名前になっています)。

<!-- [!TIP]
> You can run two parallel instances of the XAML code editor concurrently by using both the **Pop Out XAML** button and the **Expand Pane** button.
>
> You might find it useful to have one larger window open that reveals more of your code in context and a smaller pane open that has its focus directly on the code that you're working on. -->

### <a name="second-row"></a>2番目の行

XAML コードウィンドウの上部にある2番目の行には、2つのウィンドウのドロップダウンリストがあります。 ただし、これらの UI 要素のツールヒントを表示すると、さらに "Element: Window" と "Member: Window" として識別されます。

![Visual Studio の XAML コードエディターウィンドウの2つ目の行のうち、両方のウィンドウのドロップダウンリストが表示されます。](media/xaml-code-editor-top-row-windows.png "両方のウィンドウのドロップダウンリストが表示されている Visual Studio 2019 の XAML コードエディターウィンドウの2つ目の上位行のスクリーンショット")

ウィンドウのドロップダウンリストには、次のようにさまざまな機能があります。

- 左側の [**要素:] ウィンドウ**を使用すると、兄弟または親要素を表示して移動できます。

  具体的には、コードのタグ構造を表示するアウトライン形式のビューが表示されます。 一覧から選択すると、コードエディターのフォーカスが、選択した要素を含むコード行にスナップされます。

    ![要素: Visual Studio のウィンドウのドロップダウンリスト](media/xaml-element-window-dropdown.png "Visual Studio 2019 の [要素: ウィンドウ] ボックスの一覧のスクリーンショット")

- 右側にある [**メンバー:] ウィンドウ**を使用すると、属性または子要素を表示して移動できます。

    具体的には、コード内のプロパティの一覧が表示されます。 一覧から選択すると、コードエディターのフォーカスが、選択したプロパティを含むコード行にスナップされます。

    ![Visual Studio の [メンバー: ウィンドウ] ドロップダウンリスト](media/xaml-member-window-dropdown.png "Visual Studio 2019 の [メンバー: ウィンドウ] ドロップダウンリストのスクリーンショット")

### <a name="middle-pane-code-editor"></a>中央のペイン、コードエディター

中央のペインは、XAML コードエディターの "コード" 部分です。 これには、 [IDE コードエディター](../get-started/tutorial-editor.md)で確認できるほとんどの機能が含まれています。 ここでは、XAML コードの開発に役立つ、いくつかのユニバーサル IDE 機能について説明します。 また、IDE の固有の XAML 機能も強調表示します。

![Visual Studio の [XAML コードエディター] (中央のウィンドウのみ)](media/xaml-code-editor-middle.png "Visual Studio 2019 の [XAML コードエディター] (中央のウィンドウのみ) のスクリーンショット")

#### <a name="quick-actions"></a>クイック アクション

[クイックアクション](../ide/quick-actions.md)を使用して、コードを1回の操作でリファクタリング、生成、または変更することができます。

たとえば、クイックアクションを使用して実行できる便利なタスクの1つは、[ **MainWindow.xaml.cs** ] タブの C# コードから**不要な using を削除**することです。

その方法は次のとおりです。

1. Using ステートメントの上にマウスポインターを移動し、電球アイコンをクリックして、ドロップダウンリストから [**不要な using の削除**] を選択します。

    ![IDE エディターの [クイックアクション] メニューの [不要な Using の削除] オプション](media/xaml-code-editor-remove-usings.png "[クイックアクション] メニューの IDE エディターの [不要な Using の削除] オプションのスクリーンショット")

1. **ドキュメント**、**プロジェクト**、または**ソリューション**内のすべての発生箇所を修正するかどうかを選択します。
1. [**プレビュー** ] ダイアログボックスを表示し、[**適用**] を選択します。

この機能には、メニューバーからアクセスすることもできます。 これを行うには、[**編集**] [IntelliSense] [using の  >  **IntelliSense**  >  **削除と並べ替え**] の順に選択します。

Using の設定の詳細については、「 [using の並べ替え](../ide/reference/sort-usings.md)」ページを参照してください。 IntelliSense の詳細については、 [Visual Studio の intellisense](../ide/using-intellisense.md)に関するページを参照してください。 また、開発者がクイックアクションを使用する一般的な方法の詳細については、「[一般的なクイックアクション](../ide/common-quick-actions.md)」ページを参照してください。

#### <a name="change-tracking"></a>Change tracking

左余白の色を使用すると、ファイルに対する変更を追跡することができます。 次に、色が実行する操作にどのように関連しているかを示します。

- ファイルが開かれた後に加えられた変更は保存されません。左余白 (選択余白と呼ばれます) に**黄色**のバーが表示されます。

    ![黄色いバーを使用したコードエディターの編集](media/code-editor-edit-yellow.png "選択範囲の黄色のバーでマークされた変更を含むコードエディターのスクリーンショット。")

- 変更を保存した後 (ファイルを閉じる前) は、バーが**緑色**に変わります。

    ![緑色のバーでのコードエディターの編集](media/code-editor-edit-green.png "選択範囲の緑色のバーでマークされた変更があるコードエディターのスクリーンショット。")

この機能のオンとオフを切り替えるには、**[テキスト エディター]** (**[ツール]** > **[オプション]** > **[テキスト エディター]**) の設定の **[変更履歴を記録する]** オプションを変更します。

変更の追跡の詳細については、「 &mdash; コード文字列」に表示される波線 ("波線" とも呼ばれます) については、 &mdash; 「 [Visual Studio コードエディターの機能](../ide/writing-code-in-the-code-and-text-editor.md)」の「**[エディターの機能](../ide/writing-code-in-the-code-and-text-editor.md#editor-features)**」セクションを参照してください。

#### <a name="right-click-context-menu"></a>ショートカットメニューを右クリック

XAML コードエディターでコードを編集しているときに、右クリックのコンテキストメニューを使用してアクセスできる機能がいくつかあります。 これらの機能のほとんどは Visual Studio IDE で汎用的に利用できますが、コードエディターとデザインウィンドウの使用に固有のものもあります。

![Visual Studio の XAML コードエディターの右クリックコンテキストメニュー](media/xaml-code-editor-right-click-menu.png "Visual Studio 2019 の XAML コードエディターの右クリックコンテキストメニューのスクリーンショット")

各機能の機能とその有用性は次のとおりです。

- [**コードの表示**]-[プログラミング言語コード] ウィンドウを開きます。このウィンドウは通常、デザインウィンドウと XAML コードエディターを含む既定のビューの横にタブが表示されます。
- **ビューデザイナー** : デザインウィンドウと XAML コードエディターを含む既定のビューを開きます。 (既に既定のビューになっている場合は、何も行われません)。
- **クイックアクションとリファクタリング**-リファクタ、を生成するか、1つのアクションでコードを変更します。 コードにマウスポインターを合わせると、クイックアクションまたはリファクタリングが使用可能になったときに電球アイコンが表示されます。 <br>関連項目:[クイックアクション](../ide/quick-actions.md)と[リファクターコード](../ide/refactoring-in-visual-studio.md)
- **名前の変更...**-名前空間の名前のみを変更します。 名前を変更する名前空間がない場合は、"名前空間プレフィックスのみを変更できる" というエラーメッセージが表示されます。
- **名前空間の削除と並べ替え**-未使用の名前空間を削除し、残っている名前空間を並べ替えます。
- [**定義**をここに表示-エディターで現在の場所を離れずに型の定義をプレビューします。 <br>関連[項目: [定義を](../ide/go-to-and-peek-definition.md#peek-definition)ここに表示] を使用して[コードを表示および編集する](../ide/how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md)
- **[定義へ移動**]-型またはメンバーのソースに移動し、結果を新しいタブで開きます。 <br>関連項目: 「[定義に進む](../ide/go-to-and-peek-definition.md#go-to-definition)」も参照してください。
- **ブロックの挿入...**-選択したコードブロックの周囲に追加される、ブロックの挿入コードスニペットを使用します。 <br>参照:[拡張スニペットとブロックの挿入スニペット](../ide/code-snippets.md#expansion-snippets-and-surround-with-snippets)
- [**スニペットの挿入**-カーソル位置にコードスニペットを挿入します。
- **カット**-自己説明
- **コピー** -自己説明
- **貼り付け**-自己説明
- **アウトライン**: コードのセクションを展開したり折りたたんだりします。 <br>「[アウトライン](../ide/outlining.md)」も参照してください。
- **ソース管理**-オープンソースリポジトリに対するコードの投稿の履歴を表示します。

### <a name="middle-pane-scroll-bar"></a>中央のペイン、スクロールバー

スクロールバーは、コードをスクロールするよりも多くのことができます。 また、別のコードエディターペインを開くためにも使用できます。 また、スクロールバーを使用して、注釈を追加したり、別の表示モードを使用したりすることにより、コードを効率的に作成できます。

#### <a name="split-the-code-window"></a>コードウィンドウを分割する

コードエディターのスクロールバーには、右上に**分割**ボタンがあります。 このオプションを選択すると、別のコードエディターペインを開くことができます。 これは、互いに独立して動作するため便利です。そのため、さまざまな場所でコードを操作するために使用できます。

![Visual Studio の [XAML コードエディター] (中央のウィンドウのみ)](media/code-editor-split-window-button.png "Visual Studio 2019 の [XAML コードエディター] (中央のウィンドウのみ) のスクリーンショット")

エディターウィンドウを分割する方法の詳細については、「[エディター] ウィンドウの[管理](../ide/how-to-manage-editor-windows.md)」ページを参照してください。

#### <a name="use-annotations-or-map-mode"></a>注釈またはマップモードの使用

スクロールバーの外観と、それに含まれるその他の機能を変更することもできます。 たとえば、多くの担当者がスクロールバーに*注釈*を含め、コードの変更、ブレークポイント、ブックマーク、エラー、カーソル位置などの視覚的な手掛かりを提供しています。

また、*マップモード*の使用に感謝します。このモードでは、スクロールバーにコード行が表示されます。 多くのコードをファイルに記述している開発者は、既定のスクロールバーよりも、マップモードでコード行をより効果的に追跡できます。

スクロールバーの既定の設定を変更する方法の詳細については、「[スクロールバーのカスタマイズ](../ide/how-to-track-your-code-by-customizing-the-scrollbar.md)」ページを参照してください。

## <a name="xaml-specific-features"></a>XAML 固有の機能

次の機能のほとんどは Visual Studio IDE で一般公開されていますが、XAML 開発者にとってコーディングが容易になるディメンションがいくつか追加されています。

### <a name="xaml-code-snippets"></a>XAML コードスニペット

コードスニペットは、再利用可能なコードの小さなブロックで、右クリックコンテキストメニューコマンドの**挿入スニペット**を使用するか、キーボードショートカットの組み合わせ (**ctrl** + **K**、 **ctrl** + **X**) を使用してコードファイルに挿入できます。 [IntelliSense](../ide/using-intellisense.md)が拡張され、組み込みのスニペットと手動で追加したカスタムスニペットの両方で機能する XAML スニペットの表示がサポートされるようになりました。 すぐに使える XAML スニペットには、、、 `#region` 、 `Column definition` `Row definition` 、およびがあり `Setter` `Tag` ます。

![IntelliSense で表示される #region オプションを持つ XAML コードエディター](media/xaml-code-snippets.png "IntelliSense で表示される #region オプションを含む XAML コードエディターのスクリーンショット")

詳細については、「[コードスニペット](../ide/code-snippets.md)」と「 [C# コードスニペット](../ide/visual-csharp-code-snippets.md)」のページを参照してください。

### <a name="xaml-region-support"></a>XAML #region サポート

Visual Studio 2015 以降では、WPF と UWP の XAML 開発者、さらには[Xamarin. Forms](/xamarin/xamarin-forms/user-interface/text/editor/)でも #region サポートを利用できるようになりました。 Visual Studio 2019 では、#region サポートを段階的に改善し続けます。 たとえば、[バージョン 16.4](/visualstudio/releases/2019/release-notes-v16.4/)以降では、入力を開始すると #region オプションが表示さ `<!` れます。

![IntelliSense で表示される #region オプションを持つ XAML コードエディター](media/code-editor-xaml-region.png "IntelliSense で表示される #region オプションを含む XAML コードエディターのスクリーンショット")

展開または折りたたみを行うコードのセクションをグループ化する場合は、領域を使用できます。

```xaml
    <!--#region NameOfRegion-->
    Your code is here
    <!--#endregion-->
```

領域の詳細については、「 [#region (C# リファレンス)](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-region/) 」ページを参照してください。 また、コードのセクションの展開と折りたたみの詳細については、「[アウトライン](../ide/outlining.md)」ページを参照してください。

### <a name="xaml-comments"></a>XAML コメント

開発者は、多くの場合、コメントを使用してコードを記述することをお勧めします。 **Mainwindow.xaml**タブにある xaml コードにコメントを追加するには、次の方法を使用します。

- `<!--`コメントの前に「」と入力し `-->` 、コメントの後にを追加します。
- 「」と入力し `<!` `!--` 、オプションの一覧から選択します。

  ![XAML コードエディター右クリックによる [コメントの追加] ダイアログ](media/xaml-code-editor-comments.png "XAML コードエディターでコメントを追加するための右クリックコンテキストメニューのスクリーンショット")

- コメントで囲むコードを選択し、IDE のツールバーの [**コメント**] ボタンをクリックします。 操作を元に戻すには、[**コメント**解除] をクリックします。

  ![IDE ツールバーの [コメント] ボタンと [コメント解除] ボタン](media/comment-undo-comment-buttons.png "IDE ツールバーの [コメント] ボタンと [コメント解除] ボタンのスクリーンショット")

- コメントで囲むコードを選択し、 **ctrl** + **K**キー、 **ctrl**C キーの順に押し + **C**ます。 選択したコードのコメントを解除するには、 **ctrl** + **K**キーを押し**ながら** + **U**キーを押します。

[ **MainWindow.xaml.cs** ] タブの C# コードでコメントを使用する方法の詳細については、[ドキュメントのコメント](/dotnet/csharp/language-reference/language-specification/documentation-comments/)に関するページを参照してください。

### <a name="xaml-lightbulbs"></a>XAML ライト電球

XAML コードに表示される電球アイコンは、コードのリファクタリング、生成、または変更に使用できる[クイックアクション](../ide/quick-actions.md)の一部です。

ここでは、XAML のコーディングエクスペリエンスを活用する方法の例をいくつか紹介します。

- **不要な名前空間を削除**します。 XAML コードエディターでは、不要な名前空間が淡色表示のテキストで表示されます。 を使用しないでカーソルをポイントすると、電球が表示されます。 ドロップダウンリストから [**不要な名前空間を削除**する] オプションを選択すると、のプレビューが表示され、削除することができます。

  ![XAML コードエディターの [クイックアクション] 電球の [不要な名前空間の削除] オプション](media/xaml-code-editor-dimmed-namespaces-preview.png "クイックアクション電球を使用して表示される XAML コードエディターの [不要な名前空間を削除する] オプションのスクリーンショット")

- **名前空間の名前を変更**します。 この機能は、名前空間を強調表示した後、右クリックのコンテキストメニューから使用できます。これにより、一度に1つの設定の複数のインスタンスを簡単に変更できるようになります。 この機能にアクセスするには、メニューバーを使用するか、[リファクター名前の変更] を**編集**するか、ctrl r キーを押してから  >  **Refactor**  >  **Rename** **Ctrl** + **R**もう一度**ctrl +** + **r**キーを押します。

  ![右クリックコンテキストメニューからの XAML コードエディターの名前空間の名前変更オプション](media/code-editor-rename-namespace.png "右クリックコンテキストメニューを使用して表示される XAML コードエディターの名前空間の名前変更オプションのスクリーンショット")

  詳細については、「[コードシンボルの名前変更](../ide/reference/rename.md)」のリファクタリングページを参照してください。

### <a name="conditional-xaml-for-uwp"></a>UWP の条件付き XAML

条件付き XAML は、XAML マークアップで [ApiInformation.IsApiContractPresent](/uwp/api/windows.foundation.metadata.apiinformation.isapicontractpresent/) メソッドを使う方法を提供するものです。 これにより、分離コードを使わなくても、API の有無に基づいてマークアップでプロパティの設定やオブジェクトのインスタンス化を行うことができます。

詳細については、「[条件付き xaml](/windows/uwp/debug-test-perf/conditional-xaml/) 」ページと、「[デスクトップアプリ (XAML アイランド)」ページのホスト UWP XAML コントロールに](/windows/apps/desktop/modernize/xaml-islands/)関するページを参照してください。

### <a name="xaml-structure-visualizer"></a>XAML 構造ビジュアライザー

コードエディターの構造ビジュアライザー機能では、構造のガイド線が表示されます。これは、コード内の開いて閉じられたタグ要素と一致することを示す垂直破線です。 これらの垂直線を使用すると、論理ブロックの開始位置と終了位置を簡単に確認できます。

詳細については、「[コードの移動](../ide/navigating-code.md)」ページを参照してください。

### <a name="intellicode-for-xaml"></a>XAML の IntelliCode

XAML タグをコードに追加する場合、通常は左山かっこで始め `<` ます。 山かっこを入力すると、IntelliCode メニューが表示され、より一般的な XAML タグのいくつかが表示されます。 コードに簡単に追加するものを選択します。

IntelliCode の選択項目は、一覧の一番上に表示され、星付きであるため、認識できます。

![XAML テキストエディターの IntelliCode リスト](media/xaml-intellicode-selection.png "XAML テキストエディターの IntelliCode リストのスクリーンショット")

詳細については、「 [IntelliCode の概要](/visualstudio/intellicode/overview/)」ページを参照してください。

### <a name="settings"></a>設定

Visual Studio IDE の*すべて*の設定の詳細については、「[コードエディター」ページの機能](../ide/writing-code-in-the-code-and-text-editor.md)を参照してください。

## <a name="xaml-optional-settings"></a>XAML オプションの設定

[[オプション](../ide/reference/options-dialog-box-visual-studio.md)] ダイアログボックスを使用すると、XAML コードエディターの既定の設定を変更できます。 設定を表示するには、[**ツール**  >  **] [オプション]**[  >  **テキストエディター**] [  >  **XAML**] の順に選択します。

![XAML テキストエディターのオプションリスト](media/xaml-tools-options.png "XAML テキストエディターのオプション一覧のスクリーンショット")

> [!NOTE]
> また、キーボードショートカットを使用して [オプション] ダイアログボックスにアクセスすることもできます。 その方法は次のとおりです。 **Ctrl** + **Q**キーを押して IDE を検索し、「 **Options**」と入力して、 **enter**キーを押します。 次に、 **Ctrl**E キーを押して [ + **E**オプション] ダイアログボックスを検索し、「**テキストエディター**」と入力し**て enter**キーを押し、「 **XAML**」と入力して **、enter**キーを押します。
>  
> キーボードショートカットの詳細については、 [Visual Studio のショートカットヒント](../ide/productivity-shortcuts.md#code-editor)に関するページを参照してください。

### <a name="universal-text-editor-options"></a>ユニバーサルテキストエディターオプション

XAML の [[オプション](../ide/reference/options-text-editor-xaml-formatting.md)] ダイアログボックスで、次の最初の3つの項目は、VISUAL Studio IDE でサポートされているすべてのプログラミング言語に共通です。 これらのオプションとその使用方法の詳細については、次の表のリンク先の情報を参照してください。

|名前  |詳細情報  |
|---------|---------|
|全般  | [[オプション] ダイアログボックス: すべての言語 > テキストエディター](../ide/reference/options-text-editor-all-languages.md) |
|スクロール バー | [[オプション]、[テキスト エディター]、[すべての言語]、[スクロール バー]](../ide/reference/options-text-editor-all-languages-scroll-bars.md) |
|タブ  |  [[オプション]、[テキスト エディター]、[すべての言語]、[タブ]](../ide/reference/options-text-editor-all-languages-tabs.md) |

### <a name="xaml-specific-text-editor-options"></a>XAML 固有のテキストエディターオプション

次の表に、XAML ベースのアプリを開発するときの編集エクスペリエンスを向上させるための [[オプション](../ide/reference/options-text-editor-xaml-formatting.md)] ダイアログボックスの設定を示します。 これらのオプションとその使用方法の詳細については、リンクされた情報を参照してください。

|名前  |詳細情報  |
|---------|---------|
|書式設定 | [[オプション]、[テキスト エディター]、[XAML]、[書式設定]](../ide/reference/options-text-editor-xaml-formatting.md) |
|その他 |  [[オプション]、[テキスト エディター]、[XAML]、[その他]](../ide/reference/options-text-editor-xaml-miscellaneous.md) |

> [!TIP]
> [**その他**] セクションの [**イベントハンドラーメソッド名の大文字**化] 設定は、XAML 開発者にとって特に便利です。 この設定は新しいため、既定では*オフ*になっていますが、コードでの適切な大文字と小文字の区別をサポートするには、 *[オン*] に設定することをお勧めします。

## <a name="next-steps"></a>次の手順

デバッグモードでのアプリの実行中にリアルタイムでコードを編集する方法の詳細については、 [XAML のホットリロード](xaml-hot-reload.md)に関するページを参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio code エディターの機能](../ide/writing-code-in-the-code-and-text-editor.md)
- [UWP アプリの XAML](/windows/uwp/xaml-platform/xaml-overview/)
- [Xamarin.Forms アプリの XAML](/xamarin/xamarin-forms/xaml/)
- [Xamarin モバイルアプリ開発 (Mac)](/visualstudio/mac/xamarin/)
- [Mac 用 Visual Studio 2019-IDE ツアー (Mac)](/visualstudio/mac/ide-tour/)
