---
title: XAML コード エディター
description: Visual Studio の XAML コード エディターの概要を説明します
ms.date: 06/16/2020
ms.topic: overview
f1_keywords:
- VS.XamlEditor
monikerRange: vs-2019
ms.custom: contperf-fy21q4
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.openlocfilehash: 672bfa6b28e364351f262cb2a2c6e2258ecd9746
ms.sourcegitcommit: 3e1ff87fba290f9e60fb4049d011bb8661255d58
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2021
ms.locfileid: "107879396"
---
# <a name="xaml-code-editor"></a>XAML コード エディター

[Visual Studio IDE](../get-started/visual-studio-ide.md) の XAML コード エディターには、Windows プラットフォーム用と [Xamarin.Forms](/xamarin/xamarin-forms/user-interface/text/editor/) 用の WPF と UWP アプリを作成するために必要なツールがすべて含まれています。 この記事では、XAML ベースのアプリを開発するときにコード エディターが果たす役割と、Visual Studio 2019 での XAML コード エディターに固有の機能の両方について説明します。

まず、開いている WPF プロジェクトで IDE (統合開発環境) を見てみましょう。 次の図では、XAML コード エディターで使用するいくつかの主要な IDE ツールを示します。

:::image type="content" source="media/xaml-code-editor-overview-sml.png" alt-text="XAML の WPF プロジェクトが開かれている Visual Studio 2019 IDE" lightbox="media/xaml-code-editor-overview-lrg.png":::

主要な IDE ツールは、画像の左下から時計回りに次のようになります。

- **[XAML コード エディター](#xaml-code-editor-ui)** ウィンドウ (この記事のテーマ) で、コードの作成と編集を行います。
- **[XAML デザイナー](creating-a-ui-by-using-xaml-designer-in-visual-studio.md)** ウィンドウで、UI のデザインを行います。
- ドッキング可能な **[ツールボックス](../ide/reference/toolbox.md)** ウィンドウで、UI にコントロールを追加します。
- **[デバッグ](../debugger/debugger-feature-tour.md)** ボタンによって、コードを実行してデバッグすることができます。 <br>([XAML ホット リロード](xaml-hot-reload.md)を使用してデバッグしている間は、コードをリアルタイムで編集することもできます)。
- **[ソリューション エクスプローラー](../ide/solutions-and-projects-in-visual-studio.md)** ウィンドウで、ファイル、プロジェクト、ソリューションを管理します。
- **[プロパティ](../ide/reference/properties-window.md)** ウィンドウで、UI の外観と UI コントロールの動作を変更します。

引き続き、XAML コード エディターについて詳しく学習しましょう。

## <a name="xaml-code-editor-ui"></a>XAML コード エディターの UI

XAML アプリのコード エディター ウィンドウには、標準 IDE にも表示されるいくつかの共通 UI (ユーザー インターフェイス) 要素と、XAML アプリの開発を簡単にするためのいくつかの固有機能が含まれます。

ここでは、XAML コード エディター ウィンドウ自体について説明します。

![Visual Studio での XAML コード エディター ウィンドウ](media/xaml-code-editor-window.png "Visual Studio 2019 での XAML コード エディター ウィンドウのスクリーンショット")

次に、コード エディターの各 UI 要素の機能を見てみましょう。

### <a name="first-row"></a>最初の行

XAML コード ウィンドウの上部にある最初の行の左側には、 **[デザイン]** タブ、 **[ペインの交換]** ボタン、 **[XAML]** タブ、 **[Pop Out XAML]\(XAML のポップアウト\)** ボタンがあります。

![Visual Studio の XAML コード エディター ウィンドウの先頭の 2 行のうち最初の行、最初の行の左側が強調表示されている](media/xaml-code-editor-top-row-left.png "Visual Studio 2019 の XAML コード エディター ウィンドウの先頭の 2 行のうち最初の行のスクリーンショット、左側の UI 要素が強調表示されている")

それぞれの機能は次のとおりです。

- **[デザイン]** タブを選択すると、XAML コード エディターから XAML デザイナーにフォーカスが変更されます。
- **[ペインの交換]** ボタンをクリックすると、IDE で XAML デザイナーと XAML コード エディターの位置が逆になります。
- **[XAML]** タブを選択すると、XAML コード エディターにフォーカスが戻ります。
- **[Pop Out XAML]\(XAML のポップアウト\)** ボタンをクリックすると、IDE の外部に別の XAML コード エディター ウィンドウが作成されます。

右側には、 **[左右分割]** ボタン、 **[上下分割]** ボタン、 **[ペインを折りたたむ]** ボタンがあります。

![Visual Studio の XAML コード エディター ウィンドウの先頭の 2 行のうち最初の行、最初の行の右側が強調表示されている](media/xaml-code-editor-top-row-right.png "Visual Studio 2019 の XAML コード エディター ウィンドウの先頭の 2 行のうち最初の行のスクリーンショット、右側の UI 要素が強調表示されている")

それぞれの機能は次のとおりです。

- **[左右分割]** ボタンを使用すると、IDE での XAML デザイナーと XAML コード エディターの位置が、横配置から縦配置に変わります。
- **[上下分割]** ボタンを使用すると、IDE での XAML デザイナーと XAML コード エディターの位置が、縦配置から横配置に変わります。
- **[ペインを折りたたむ]** ボタンを使用すると、コード エディターまたはデザイナーが表示されている下部ペインの内容を折りたたむことができます。 (下部ペインを元に戻すには、もう一度同じボタンを選択します。ボタンの名前は **[ペインの展開]** になっています)。

<!-- [!TIP]
> You can run two parallel instances of the XAML code editor concurrently by using both the **Pop Out XAML** button and the **Expand Pane** button.
>
> You might find it useful to have one larger window open that reveals more of your code in context and a smaller pane open that has its focus directly on the code that you're working on. -->

### <a name="second-row"></a>2 番目の行

XAML コード ウィンドウ上部の 2 番目の行には、2 つの [ウィンドウ] ドロップダウン リストがあります。 ただし、これらの UI 要素のツールヒントを表示すると、[Element: Window]\(要素: ウィンドウ\) および [Member: Window]\(メンバー: ウィンドウ\) と示されます。

![Visual Studio の XAML コード エディター ウィンドウの先頭の 2 行のうち 2 番目の行、2 つの [ウィンドウ] ドロップダウン リストが表示されている](media/xaml-code-editor-top-row-windows.png "Visual Studio 2019 の XAML コード エディター ウィンドウの先頭の 2 行のうち 2 番目の行のスクリーンショット、両方の [ウィンドウ] ドロップダウン リストが表示されている")

[ウィンドウ] ドロップダウン リストの機能は次のように異なります。

- **[Element: Window]\(要素: ウィンドウ\)** (左側) を使用すると、兄弟要素または親要素を表示してそれらに移動できます。

  具体的には、コードのタグ構造を示すアウトライン形式のビューが表示されます。 一覧から選択すると、コード エディターのフォーカスが、選択した要素を含むコード行にスナップされます。

    ![Visual Studio の [Element: Window]\(要素: ウィンドウ\) ドロップダウン リスト](media/xaml-element-window-dropdown.png "要素: ウィンドウ ドロップダウン リストのスクリーンショット (Visual Studio 2019)")

- **[Member: Window]\(メンバー: ウィンドウ\)** (右側) を使用すると、属性または子要素を表示してそれらに移動できます。

    具体的には、コード内のプロパティの一覧が表示されます。 一覧から選択すると、コード エディターのフォーカスが、選択したプロパティを含むコード行にスナップされます。

    ![Visual Studio の [Member: Window]\(メンバー: ウィンドウ\) ドロップダウン リスト](media/xaml-member-window-dropdown.png "メンバー: ウィンドウ ドロップダウン リストのスクリーンショット (Visual Studio 2019)")

### <a name="middle-pane-code-editor"></a>中央のペイン、コード エディター

中央のペインは、XAML コード エディターの "コード" 部分です。 ここには、[IDE コード エディター](../get-started/tutorial-editor.md)のほとんどの機能が含まれています。 XAML コードの開発に役立つ、いくつかのユニバーサル IDE 機能について説明します。 また、IDE の XAML 固有の機能についても説明します。

![Visual Studio の XAML コード エディターの中央ペインのみ](media/xaml-code-editor-middle.png "Visual Studio 2019 の XAML コード エディターの中央ペインのみのスクリーンショット")

#### <a name="quick-actions"></a>クイック アクション

[クイック アクション](../ide/quick-actions.md)を使用すると、コードのリファクタリング、生成、その他の変更を、1 つの操作で行うことができます。

たとえば、クイック アクションを使用して実行できる便利なタスクの 1 つは、**MainWindow.xaml.cs** タブでの C# コードからの **[不要な using の削除]** です。

以下にその方法を示します。

1. using ステートメントをマウスでポイントし、電球アイコンをクリックして、ドロップダウン リストから **[不要な using の削除]** を選択します。

    ![IDE エディターのクイック アクション メニューの [不要な using の削除] オプション](media/xaml-code-editor-remove-usings.png "IDE エディターのクイック アクション メニューの [不要な using の削除] オプションのスクリーンショット")

1. **[ドキュメント]** 、 **[プロジェクト]** 、 **[ソリューション]** ですべての出現箇所を修正するかどうかを選択します。
1. **[プレビュー]** ダイアログを確認した後、 **[適用]** を選択します。

この機能には、メニュー バーからアクセスすることもできます。 それには、 **[編集]**  >  **[IntelliSense]**  >  **[using の削除と並べ替え]** を選択します。

using の設定の詳細については、「[using を並べ替える](../ide/reference/sort-usings.md)」ページを参照してください。 IntelliSense の詳細については、「[Visual Studio での IntelliSense](../ide/using-intellisense.md)」ページを参照してください。 また、開発者がクイック アクションを使用する一般的な方法の詳細については、「[共通のクイック アクション](../ide/common-quick-actions.md)」ページを参照してください。

#### <a name="change-tracking"></a>変更の追跡

左余白の色を使用すると、ファイルに対する変更を追跡することができます。 ここでは、色が実行する操作にどのように関連しているかを示します。

- ファイルを開いてから行った変更で保存していないものは、左余白 (選択余白と呼ばれます) に **黄色** のバーで示されます。

    ![コード エディターでの黄色いバーでの編集](media/code-editor-edit-yellow.png "選択余白の黄色のバーでマークされた変更を含むコード エディターのスクリーンショット。")

- 変更を保存した後 (ファイルを閉じる前) は、バーが **緑色** に変わります。

    ![コード エディターでの緑色のバーでの編集](media/code-editor-edit-green.png "選択余白の緑色のバーでマークされた変更を含むコード エディターのスクリーンショット。")

この機能のオンとオフを切り替えるには、 **[テキスト エディター]** ( **[ツール]**  >  **[オプション]**  >  **[テキスト エディター]** ) の設定の **[変更履歴を記録する]** オプションを変更します。

変更の追跡 (コード文字列の下に波線を表示する) の詳細については、[Visual Studio コード エディターの機能](../ide/writing-code-in-the-code-and-text-editor.md)に関するページの「 **[エディターの機能](../ide/writing-code-in-the-code-and-text-editor.md#editor-features)** 」セクションを参照してください。

#### <a name="right-click-context-menu"></a>右クリックのショートカット メニュー

XAML コード エディターでコードを編集しているときに、右クリックのコンテキスト メニューを使用してアクセスできる機能がいくつかあります。 これらの機能のほとんどは Visual Studio IDE で普遍的に利用できますが、一部はコード エディターのデザイン ウィンドウ使用時に固有のものです。

![Visual Studio 2019 の XAML コード エディターの右クリック コンテキスト メニューのスクリーンショット。](media/xaml-code-editor-right-click-menu.png)

各機能とその有用性は次のとおりです。

- **[コードの表示]** - プログラミング言語コード ウィンドウが開きます。このウィンドウは通常、デザインウィンドウと XAML コード エディターが含まれる既定のビューの隣のタブです。
- **[ビュー デザイナー]** - デザイン ウィンドウと XAML コード エディターが含まれる既定のビューが開きます。 (既に既定のビューになっている場合は、何も行われません)。
- **[クイック アクションとリファクタリング]** - 1 つの操作で、コードのリファクター、生成、またはその他の変更が行われます。 コードをマウスでポイントすると、クイック アクションまたはリファクタリングを使用できるときは、電球アイコンが表示されます。 <br>参照:「[クイック アクション](../ide/quick-actions.md)」および「[コードのリファクタリング](../ide/refactoring-in-visual-studio.md)」。
- **[名前の変更...]** - 名前空間の名前のみを変更します。 名前を変更する名前空間がない場合は、"名前を変更できるのは名前空間プレフィックスのみです" というエラー メッセージが表示されます。
- **[名前空間の削除と並べ替え]** - 使用されていない名前空間を削除した後、残っている名前空間を並べ替えます。
- **[定義をここに表示]** - エディターで現在の場所を離れずに、型の定義をプレビューします。 <br>参照:「[定義をここに表示](../ide/go-to-and-peek-definition.md#peek-definition)」および「[[定義をここに表示] を使用してコードを表示および編集する](../ide/how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md)」。
- **[定義へ移動]** - 型またはメンバーのソースに移動し、新しいタブで結果を開きます。 <br>参照:「[[定義へ移動]](../ide/go-to-and-peek-definition.md#go-to-definition)」。
- **[ブロックの挿入...]** - 選択したコード ブロックの周囲に追加される surround-with コード スニペットを使用します。 <br>参照:「[拡張スニペットとブロックの挿入用スニペット](../ide/code-snippets.md#expansion-snippets-and-surround-with-snippets)」。
- **[スニペットの挿入]** - カーソル位置にコード スニペットを挿入します。
- **[切り取り]** - 名前のとおりです
- **[コピー]** - 名前のとおりです
- **[貼り付け]** - 名前のとおりです
- **[アウトライン]** - コードのセクションの展開と折りたたみを行います。 <br>参照:「[アウトライン](../ide/outlining.md)」。
- **[ソース管理]** - オープンソース リポジトリに対するコードのコントリビューションの履歴を表示します。

### <a name="middle-pane-scroll-bar"></a>中央のペイン、スクロール バー

スクロール バーには、コードをスクロールすること以外の機能があります。 別のコード エディター ペインを開くためにも使用できます。 また、スクロール バーを使用すると、注釈を追加したり、別の表示モードを使用したりして、コードをより効率的に作成することができます。

#### <a name="split-the-code-window"></a>コード ウィンドウを分割する

コード エディターのスクロール バーの右上には、 **[分割]** ボタンがあります。 それを選択すると、別のコード エディター ペインを開くことができます。 それらは互いに独立して動作し、異なる場所のコードを作業できるため便利です。

![Visual Studio 2019 の XAML コード エディターの中央ウィンドウのスクリーンショット。ウィンドウの右上で [分割] ボタンが強調されています。](media/code-editor-split-window-button.png)

エディター ウィンドウを分割する方法の詳細については、「[エディター ウィンドウを管理する](../ide/how-to-manage-editor-windows.md)」ページを参照してください。

#### <a name="use-annotations-or-map-mode"></a>注釈またはマップ モードを使用する

スクロール バーの外観と、それに含まれるその他の機能を変更することもできます。 たとえば、スクロール バーに "*注釈*" を含めることが好まれます。それにより、コードの変更、ブレークポイント、ブックマーク、エラー、カーソルの位置などの視覚的な手掛かりを提供することができます。

"*マップ モード*" も便利で、コード行がスクロール バーに縮小表示されます。 ファイルのコードが多い場合、既定のスクロール バーより、マップ モードを使用した方が、コード行をより効率的に追跡できる場合があります。

スクロール バーの既定の設定を変更する方法の詳細については、「[スクロール バーのカスタマイズ](../ide/how-to-track-your-code-by-customizing-the-scrollbar.md)」のページを参照してください。

## <a name="xaml-specific-features"></a>XAML 固有の機能

以下の機能のほとんどは Visual Studio IDE のどこでも使用できますが、XAML のコーディングを容易にする機能がいくつか追加されています。

### <a name="xaml-code-snippets"></a>XAML コード スニペット

コード スニペットは、コード ファイルに挿入できる、再利用可能なコードの小さなブロックです。これを行うには、右クリックしてコンテキスト メニューの **[スニペットの挿入]** コマンドを使用するか、キーボード ショートカットの組み合わせ (**Ctrl** + **K** と **Ctrl** + **X**) を使用します。 [IntelliSense](../ide/using-intellisense.md) が拡張されて、XAML スニペットの表示がサポートされるようになりました。これは、組み込みのスニペットと、手動で追加したカスタム スニペットの両方で機能します。 すぐに使用できる XAML スニペットとしては、`#region`、`Column definition`、`Row definition`、`Setter`、`Tag` などがあります。

![IntelliSense に XAML コード スニペット オプションが表示されている XAML コード エディター](media/xaml-code-snippets.png "IntelliSense に XAML コード スニペット オプションが表示されている XAML コード エディターのスクリーンショット")

詳細については、「[コード スニペット](../ide/code-snippets.md)」と「[C# コード スニペット](../ide/visual-csharp-code-snippets.md)」のページを参照してください。

### <a name="xaml-region-support"></a>XAML の #region のサポート

Visual Studio 2015 以降では、WPF および UWP での XAML の開発に #region のサポートを利用できるようになり、最近 [Xamarin.Forms](/xamarin/xamarin-forms/user-interface/text/editor/) でも利用できるようになりました。 Visual Studio 2019 では、引き続き #region のサポートが段階的に改善されています。 たとえば、[バージョン 16.4](/visualstudio/releases/2019/release-notes-v16.4/) 以降では、「`<!`」と入力し始めると #region オプションが表示されます。

![IntelliSense に #region オプションが表示されている XAML コード エディター](media/code-editor-xaml-region.png "IntelliSense に #region オプションが表示されている XAML コード エディターのスクリーンショット")

領域は、展開したり折りたたんだりしたいコードのセクションをグループ化するときに使用できます。

```xaml
    <!--#region NameOfRegion-->
    Your code is here
    <!--#endregion-->
```

領域の詳細については、「[#region (C# リファレンス)](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-region/)」のページを参照してください。 また、コードのセクションの展開と折りたたみの詳細については、「[アウトライン](../ide/outlining.md)」のページを参照してください。

### <a name="xaml-comments"></a>XAML コメント

開発者は、多くの場合、コメントを使用してコードを文書化することを好みます。 **MainWindow.xaml** タブの XAML コードに、次の方法でコメントを追加できます。

- コメントの前に「`<!--`」と入力し、コメントの後に「`-->`」を追加します。
- 「`<!`」と入力し、オプションの一覧から `!--` を選択します。

  ![XAML コード エディターの右クリックによるコメント追加ダイアログ](media/xaml-code-editor-comments.png "XAML コード エディターでコメントを追加するための右クリック コンテキスト メニューのスクリーンショット")

- コメントで囲むコードを選択し、IDE のツール バーで **[コメント]** ボタンをクリックします。 操作を元に戻すには、 **[コメント解除]** ボタンを選択します。

  ![IDE ツール バーの [コメント] ボタンと [コメント解除] ボタン](media/comment-undo-comment-buttons.png "IDE ツール バーの [コメント] ボタンと [コメント解除] ボタンのスクリーンショット")

- コメントで囲むコードを選択し、**Ctrl** + **K** キー、**Ctrl** + **C** キーの順に押します。 選択したコードのコメントを解除するには、**Ctrl** + **K** キー、**Ctrl** + **U** キーの順に押します。

**MainWindow.xaml.cs** タブ内の C# コードでコメントを使用する方法の詳細については、「[ドキュメント コメント](/dotnet/csharp/language-reference/language-specification/documentation-comments/)」のページを参照してください。

### <a name="xaml-lightbulbs"></a>XAML の電球

XAML コードに表示される電球アイコンは[クイック アクション](../ide/quick-actions.md)の一部であり、コードのリファクタリング、生成、またはその他の変更に使用できます。

ここでは、XAML のコーディング エクスペリエンスに対する利点の例をいくつか紹介します。

- **不要な名前空間を削除する**。 XAML コード エディターでは、不要な名前空間が淡色表示のテキストで表示されます。 不要な using をマウスでポイントすると、電球が表示されます。 ドロップダウン リストから **[不要な名前空間の削除]** オプションを選択すると、削除できるもののプレビューが表示されます。

  ![XAML コード エディターのクイック アクションの電球からの [不要な名前空間の削除] オプション](media/xaml-code-editor-dimmed-namespaces-preview.png "XAML コード エディターでクイック アクションの電球を使用して表示される [不要な名前空間の削除] オプションのスクリーンショット")

- **名前空間の名前を変更する**。 この機能は、名前空間を強調表示した後で右クリックのコンテキスト メニューから使用でき、設定の複数のインスタンスを一度に簡単に変更できます。 また、この機能には、メニュー バーの **[編集]**  >  **[リファクター]**  >  **[名前の変更]** を使用して、または **Ctrl** + **R** キーを押してから、再度 **Ctrl** + **R** キーを押すことによって、アクセスすることもできます。

  ![XAML コード エディターの右クリックのコンテキスト メニューからの [名前空間名の変更] オプション](media/code-editor-rename-namespace.png "XAML コード エディターの右クリック コンテキスト メニューを使用して表示される [名前空間名の変更] オプションのスクリーンショット")

  詳細については、「[コード シンボルの名前の変更のリファクタリング](../ide/reference/rename.md)」のページを参照してください。

### <a name="conditional-xaml-for-uwp"></a>UWP の条件付き XAML

条件付き XAML は、XAML マークアップで [ApiInformation.IsApiContractPresent](/uwp/api/windows.foundation.metadata.apiinformation.isapicontractpresent/) メソッドを使う方法を提供するものです。 これにより、分離コードを使わなくても、API の有無に基づいてマークアップでプロパティの設定やオブジェクトのインスタンス化を行うことができます。

詳細については、「[条件付き XAML](/windows/uwp/debug-test-perf/conditional-xaml/)」のページ、および「[デスクトップ アプリで UWP XAML コントロールをホストする (XAML Islands)](/windows/apps/desktop/modernize/xaml-islands/)」のページを参照してください。

### <a name="xaml-structure-visualizer"></a>XAML 構造ビジュアライザー

コード エディターの構造ビジュアライザーでは、構造のガイド線、つまりコード内の対応する開始タグ要素と終了タグ要素を示す縦の破線が表示されます。 これらの縦線を使用すると、論理ブロックの開始位置と終了位置がわかりやすくなります。

詳細については、「[コード間の移動](../ide/navigating-code.md)」のページを参照してください。

### <a name="intellicode-for-xaml"></a>XAML 用の IntelliCode

XAML タグをコードに追加するとき、通常は左山かっこ `<` で始めます。 その山かっこを入力すると、IntelliCode メニューが開き、より一般的ないくつかの XAML タグが表示されます。 目的のものを選択して、コードに簡単に追加することができます。

IntelliCode による選択項目は、一覧の一番上に星付きで表示されるため、見分けることができます。

![XAML テキスト エディターでの IntelliCode の一覧](media/xaml-intellicode-selection.png "XAML テキスト エディターでの IntelliCode の一覧のスクリーンショット")

詳細については、「[IntelliCode の概要](/visualstudio/intellicode/overview/)」のページを参照してください。

### <a name="settings"></a>設定

Visual Studio IDE での "*すべての*" 設定の詳細については、「[コード エディターの機能](../ide/writing-code-in-the-code-and-text-editor.md)」のページを参照してください。

## <a name="xaml-optional-settings"></a>XAML のオプションの設定

[[オプション]](../ide/reference/options-dialog-box-visual-studio.md) ダイアログ ボックスを使用すると、XAML コード エディターの既定の設定を変更できます。 設定を表示するには、 **[ツール]**  >  **[オプション]**  >  **[テキスト エディター]**  >  **[XAML]** を選択します。

![XAML テキスト エディターでの [オプション] の一覧](media/xaml-tools-options.png "XAML テキスト エディターでの [オプション] の一覧のスクリーンショット")

> [!NOTE]
> また、キーボード ショートカットを使用して [オプション] ダイアログ ボックスにアクセスすることもできます。 次の手順に従います。**Ctrl** + **Q** キーを押して IDE を検索し、「**オプション**」と入力して **Enter** キーを押します。 次に、**Ctrl** + **E** キーを押して [オプション] ダイアログ ボックスを検索し、「**テキスト エディター**」と入力して **Enter** キーを押し、「**XAML**」と入力して **Enter** キーを押します。
>
> キーボード ショートカットの詳細については、「[Visual Studio のショートカットに関するヒント](../ide/productivity-shortcuts.md#code-editor)」のページを参照してください。

### <a name="universal-text-editor-options"></a>テキスト エディターの共通のオプション

XAML の [[オプション]](../ide/reference/options-text-editor-xaml-formatting.md) ダイアログ ボックスで、次の最初の 3 項目は、Visual Studio IDE でサポートされているすべてのプログラミング言語に共通です。 これらのオプションの詳細とその使用方法については、次の表のリンク先の情報を参照してください。

|名前  |詳細情報  |
|---------|---------|
|全般  | [[オプション] ダイアログ ボックス:[テキスト エディター] > [すべての言語]](../ide/reference/options-text-editor-all-languages.md) |
|スクロール バー | [[オプション]、[テキスト エディター]、[すべての言語]、[スクロール バー]](../ide/reference/options-text-editor-all-languages-scroll-bars.md) |
|タブ  |  [[オプション]、[テキスト エディター]、[すべての言語]、[タブ]](../ide/reference/options-text-editor-all-languages-tabs.md) |

### <a name="xaml-specific-text-editor-options"></a>テキスト エディターの XAML 固有のオプション

次の表では、XAML ベースのアプリを開発するときに編集エクスペリエンスを拡張できる [[オプション]](../ide/reference/options-text-editor-xaml-formatting.md) ダイアログ ボックスの設定の一覧を示します。 これらのオプションの詳細とその使用方法については、リンク先の情報を参照してください。

|名前  |詳細情報  |
|---------|---------|
|書式設定 | [[オプション]、[テキスト エディター]、[XAML]、[書式設定]](../ide/reference/options-text-editor-xaml-formatting.md) |
|その他 |  [[オプション]、[テキスト エディター]、[XAML]、[その他]](../ide/reference/options-text-editor-xaml-miscellaneous.md) |

> [!TIP]
> **[その他]** セクションの **[イベント ハンドラー メソッド名を大文字にする]** の設定は、XAML 開発者にとって特に便利です。 この設定は新しいので、既定では "*オフ*" になっていますが、コードで適切な大文字と小文字の区別がサポートされるため、"*オン*" に設定することをお勧めします。

## <a name="next-steps"></a>次のステップ

デバッグ モードでアプリを実行しながらリアルタイムでコードを編集する方法の詳細については、[XAML ホット リロード](xaml-hot-reload.md)に関するページを参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio のコード エディターの機能](../ide/writing-code-in-the-code-and-text-editor.md)
- [UWP アプリの XAML](/windows/uwp/xaml-platform/xaml-overview/)
- [Xamarin.Forms アプリの XAML](/xamarin/xamarin-forms/xaml/)
- [Xamarin のモバイル アプリ開発 (Mac)](/visualstudio/mac/xamarin/)
- [Visual Studio 2019 for Mac - IDE ツアー (Mac)](/visualstudio/mac/ide-tour/)
