---
title: 'チュートリアル: エディター拡張機能でシェル コマンドを使用する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - add a menu command
ms.assetid: 08526848-a442-4cd4-afa1-b2eac2005adb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 52b151b09c1bb7306b4270f9408d0f04a7600aa2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697163"
---
# <a name="walkthrough-use-a-shell-command-with-an-editor-extension"></a>チュートリアル: エディター拡張機能でシェル コマンドを使用する
VSPackage から、メニュー コマンドなどの機能をエディターに追加できます。 このチュートリアルでは、メニュー コマンドを呼び出してエディターのテキスト ビューに表示要素を追加する方法を示します。

 このチュートリアルでは、マネージ機能拡張フレームワーク (MEF) コンポーネント パーツと共に VSPackage を使用する方法について説明します。 メニュー コマンドを Visual Studio シェルに登録するには、VSPackage を使用する必要があります。 また、このコマンドを使用して MEF コンポーネント部品にアクセスできます。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-an-extension-with-a-menu-command"></a>メニュー コマンドを使用して拡張機能を作成する
 **[ツール**] メニューに [**表示要素の追加]** という名前のメニュー コマンドを配置する VSPackage を作成します。

1. という名前`MenuCommandTest`の C# VSIX プロジェクトを作成し、カスタム コマンド項目テンプレート名**AddAdornment**を追加します。 詳細については、「[メニュー コマンドを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

2. という名前のソリューションが開きます。 MenuCommandTestPackage ファイルには、メニュー コマンドを作成し、[**ツール]** メニューに配置するコードがあります。 この時点で、コマンドはメッセージ ボックスを表示させるだけです。 後の手順では、コメントの表示要素を表示するためにこれを変更する方法を示します。

3. VSIX マニフェスト エディターで *、ソース.extension.vsixmanifest*ファイルを開きます。 タブ`Assets`には、メニューコマンドテストという名前の行が必要です。

4. *ファイル*を保存して閉じます。

## <a name="add-a-mef-extension-to-the-command-extension"></a>コマンド拡張機能に MEF 拡張機能を追加する

1. **ソリューション エクスプローラ**で、ソリューション ノードを右クリックし、[**追加**] を**クリックします**。 [**新しいプロジェクトの追加**] ダイアログ ボックスで **、[Visual C#]** の [**機能拡張**] をクリックし **、[VSIX プロジェクト**] をクリックします。 プロジェクトに `CommentAdornmentTest` と名前を付けます。

2. このプロジェクトは厳密な名前を持つ VSPackage アセンブリと対話するため、アセンブリに署名する必要があります。 VSPackage アセンブリ用に既に作成されているキー ファイルを再利用できます。

    1. プロジェクトのプロパティを開き、[**署名**] タブを選択します。

    2. [**アセンブリに署名する ] を**選択します。

    3. [**厳密な名前のキー ファイルを選択**してください] で、MenuCommandTest アセンブリ用に生成された*Key.snk*ファイルを選択します。

## <a name="refer-to-the-mef-extension-in-the-vspackage-project"></a>VSPackage プロジェクトで MEF 拡張機能を参照してください。
 VSPackage に MEF コンポーネントを追加するため、マニフェストで両方の種類のアセットを指定する必要があります。

> [!NOTE]
> MEF の詳細については、「[マネージ機能拡張フレームワーク (MEF) 」](/dotnet/framework/mef/index)を参照してください。

### <a name="to-refer-to-the-mef-component-in-the-vspackage-project"></a>VSPackage プロジェクトの MEF コンポーネントを参照するには

1. メニューコマンドテスト プロジェクトで、VSIX マニフェスト エディターで*ソース.extension.vsixmanifest*ファイルを開きます。

2. [**資産**] タブで、[**新規作成**] をクリックします。

3. **[種類**] ボックスの一覧**で**、[コンポーネント] をクリックします。

4. [**ソース**] ボックスの一覧**で、[現在のソリューションのプロジェクト**] を選択します。

5. [**プロジェクト**] ボックスの一覧**で、[コメントアドーメントテスト**] を選択します。

6. *ファイル*を保存して閉じます。

7. プロジェクトがコメント AdornmentTest プロジェクトへの参照を持っていることを確認します。

8. コメント AdornmentTest プロジェクトで、アセンブリを生成するプロジェクトを設定します。 ソリューション**エクスプローラ**でプロジェクトを選択し、[**プロパティ]** ウィンドウの [**ビルド出力を OutputDirectory にコピー** ] プロパティを探し、これを**true**に設定します。

## <a name="define-a-comment-adornment"></a>コメント表示要素の定義
 コメントの表示要素自体は、選択したテキスト<xref:Microsoft.VisualStudio.Text.ITrackingSpan>を追跡する 要素と、作成者とテキストの説明を表す文字列で構成されます。

#### <a name="to-define-a-comment-adornment"></a>コメント表示要素を定義するには

1. プロジェクトで、新しいクラス ファイルを追加し、名前を付けます`CommentAdornment`。

2. 次の参照を追加します。

    1. ユーティリティ

    2. データ

    3. ロジック

    4. UI

    5. Wpf

    6. System.ComponentModel.Composition

    7. PresentationCore

    8. PresentationFramework

    9. WindowsBase

3. 次`using`のディレクティブを追加します。

    ```csharp
    using Microsoft.VisualStudio.Text;
    ```

4. ファイルには、 という名前`CommentAdornment`のクラスが含まれている必要があります。

    ```csharp
    internal class CommentAdornment
    ```

5. の`CommentAdornment`クラス<xref:Microsoft.VisualStudio.Text.ITrackingSpan>に 3 つのフィールドを追加します。

    ```csharp
    public readonly ITrackingSpan Span;
    public readonly string Author;
    public readonly string Text;
    ```

6. フィールドを初期化するコンストラクターを追加します。

    ```csharp
    public CommentAdornment(SnapshotSpan span, string author, string text)
    {
        this.Span = span.Snapshot.CreateTrackingSpan(span, SpanTrackingMode.EdgeExclusive);
        this.Author = author;
        this.Text = text;
    }
    ```

## <a name="create-a-visual-element-for-the-adornment"></a>表示要素のビジュアル要素を作成する
 表示要素のビジュアル要素を定義します。 このチュートリアルでは、Windows プレゼンテーション ファウンデーション (WPF) クラス<xref:System.Windows.Controls.Canvas>から継承するコントロールを定義します。

1. コメント AdornmentTest プロジェクトでクラスを作成し、名前`CommentBlock`を付けます。

2. 次`using`のディレクティブを追加します。

    ```csharp
    using Microsoft.VisualStudio.Text;
    using System;
    using System.Windows;
    using System.Windows.Controls;
    using System.Windows.Media;
    using System.Windows.Shapes;
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Utilities;
    ```

3. クラスを`CommentBlock`から<xref:System.Windows.Controls.Canvas>継承させる。

    ```csharp
    internal class CommentBlock : Canvas
    { }
    ```

4. いくつかのプライベート フィールドを追加して、表示要素の視覚的な側面を定義します。

    ```csharp
    private Geometry textGeometry;
    private Grid commentGrid;
    private static Brush brush;
    private static Pen solidPen;
    private static Pen dashPen;
    ```

5. コメントの表示要素を定義し、関連するテキストを追加するコンストラクターを追加します。

    ```csharp
    public CommentBlock(double textRightEdge, double viewRightEdge,
            Geometry newTextGeometry, string author, string body)
    {
        if (brush == null)
        {
            brush = new SolidColorBrush(Color.FromArgb(0x20, 0x00, 0xff, 0x00));
            brush.Freeze();
            Brush penBrush = new SolidColorBrush(Colors.Green);
            penBrush.Freeze();
            solidPen = new Pen(penBrush, 0.5);
            solidPen.Freeze();
            dashPen = new Pen(penBrush, 0.5);
            dashPen.DashStyle = DashStyles.Dash;
            dashPen.Freeze();
        }

        this.textGeometry = newTextGeometry;

        TextBlock tb1 = new TextBlock();
        tb1.Text = author;
        TextBlock tb2 = new TextBlock();
        tb2.Text = body;

        const int MarginWidth = 8;
        this.commentGrid = new Grid();
        this.commentGrid.RowDefinitions.Add(new RowDefinition());
        this.commentGrid.RowDefinitions.Add(new RowDefinition());
        ColumnDefinition cEdge = new ColumnDefinition();
        cEdge.Width = new GridLength(MarginWidth);
        ColumnDefinition cEdge2 = new ColumnDefinition();
        cEdge2.Width = new GridLength(MarginWidth);
        this.commentGrid.ColumnDefinitions.Add(cEdge);
        this.commentGrid.ColumnDefinitions.Add(new ColumnDefinition());
        this.commentGrid.ColumnDefinitions.Add(cEdge2);

        System.Windows.Shapes.Rectangle rect = new System.Windows.Shapes.Rectangle();
        rect.RadiusX = 6;
        rect.RadiusY = 3;
        rect.Fill = brush;
        rect.Stroke = Brushes.Green;

            Size inf = new Size(double.PositiveInfinity, double.PositiveInfinity);
            tb1.Measure(inf);
            tb2.Measure(inf);
            double middleWidth = Math.Max(tb1.DesiredSize.Width, tb2.DesiredSize.Width);
            this.commentGrid.Width = middleWidth + 2 * MarginWidth;

        Grid.SetColumn(rect, 0);
        Grid.SetRow(rect, 0);
        Grid.SetRowSpan(rect, 2);
        Grid.SetColumnSpan(rect, 3);
        Grid.SetRow(tb1, 0);
        Grid.SetColumn(tb1, 1);
        Grid.SetRow(tb2, 1);
        Grid.SetColumn(tb2, 1);
        this.commentGrid.Children.Add(rect);
        this.commentGrid.Children.Add(tb1);
        this.commentGrid.Children.Add(tb2);

        Canvas.SetLeft(this.commentGrid, Math.Max(viewRightEdge - this.commentGrid.Width - 20.0, textRightEdge + 20.0));
        Canvas.SetTop(this.commentGrid, textGeometry.GetRenderBounds(solidPen).Top);

        this.Children.Add(this.commentGrid);
    }
    ```

6. また、表示<xref:System.Windows.Controls.Panel.OnRender%2A>要素を描画するイベント ハンドラーも実装します。

    ```csharp
    protected override void OnRender(DrawingContext dc)
    {
        base.OnRender(dc);
        if (this.textGeometry != null)
        {
            dc.DrawGeometry(brush, solidPen, this.textGeometry);
            Rect textBounds = this.textGeometry.GetRenderBounds(solidPen);
            Point p1 = new Point(textBounds.Right, textBounds.Bottom);
            Point p2 = new Point(Math.Max(Canvas.GetLeft(this.commentGrid) - 20.0, p1.X), p1.Y);
            Point p3 = new Point(Math.Max(Canvas.GetLeft(this.commentGrid), p1.X), (Canvas.GetTop(this.commentGrid) + p1.Y) * 0.5);
            dc.DrawLine(dashPen, p1, p2);
            dc.DrawLine(dashPen, p2, p3);
        }
    }
    ```

## <a name="add-an-iwpftextviewcreationlistener"></a>リスナーを追加します。
 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener>は、作成イベントの表示を待機するために使用できる MEF コンポーネント部分です。

1. クラス ファイルをコメント AdornmentTest プロジェクトに追加し`Connector`、名前を付けます。

2. 次`using`のディレクティブを追加します。

    ```csharp
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Utilities;
    ```

3. を実装<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener>するクラスを宣言し、それを "text" および a と共<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>に<xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>エクスポート<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document>します。 コンテンツ タイプ属性は、コンポーネントが適用されるコンテンツの種類を指定します。 テキスト型は、すべての非バイナリ ファイルの種類の基本型です。 したがって、作成されるほとんどすべてのテキスト ビューは、このタイプになります。 テキスト ビュー ロール属性は、コンポーネントが適用されるテキスト ビューの種類を指定します。 ドキュメント テキスト ビュー ロールは、通常、行で構成され、ファイルに格納されているテキストを表示します。

     [!code-vb[VSSDKMenuCommandTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-using-a-shell-command-with-an-editor-extension_1.vb)]
     [!code-csharp[VSSDKMenuCommandTest#11](../extensibility/codesnippet/CSharp/walkthrough-using-a-shell-command-with-an-editor-extension_1.cs)]

4. メソッドを<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A>実装して、 の静的`Create()`イベントを呼び`CommentAdornmentManager`出します。

    ```csharp
    public void TextViewCreated(IWpfTextView textView)
    {
        CommentAdornmentManager.Create(textView);
    }
    ```

5. コマンドの実行に使用できるメソッドを追加します。

    ```csharp
    static public void Execute(IWpfTextViewHost host)
    {
        IWpfTextView view = host.TextView;
        //Add a comment on the selected text. 
        if (!view.Selection.IsEmpty)
        {
            //Get the provider for the comment adornments in the property bag of the view.
            CommentAdornmentProvider provider = view.Properties.GetProperty<CommentAdornmentProvider>(typeof(CommentAdornmentProvider));

            //Add some arbitrary author and comment text. 
            string author = System.Security.Principal.WindowsIdentity.GetCurrent().Name;
            string comment = "Four score....";

            //Add the comment adornment using the provider.
            provider.Add(view.Selection.SelectedSpans[0], author, comment);
        }
    }
    ```

## <a name="define-an-adornment-layer"></a>表示要素レイヤーの定義
 新しい表示要素を追加するには、表示要素レイヤーを定義する必要があります。

### <a name="to-define-an-adornment-layer"></a>表示要素レイヤーを定義するには

1. `Connector`クラスで、type<xref:Microsoft.VisualStudio.Text.Editor.AdornmentLayerDefinition>のパブリック フィールドを宣言し、表示要素レイヤー<xref:Microsoft.VisualStudio.Utilities.NameAttribute>の一意の名前を指定する を指定し<xref:Microsoft.VisualStudio.Utilities.OrderAttribute>、この表示要素レイヤーと他のテキスト ビュー レイヤー (テキスト、キャレット、および選択) との Z 順序関係を定義する を使用してエクスポートします。

    ```csharp
    [Export(typeof(AdornmentLayerDefinition))]
    [Name("CommentAdornmentLayer")]
    [Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]
    public AdornmentLayerDefinition commentLayerDefinition;

    ```

## <a name="provide-comment-adornments"></a>コメントの表示要素を提供する
 表示要素を定義する場合は、コメント表示要素プロバイダーとコメント表示要素マネージャーも実装します。 コメント表示要素プロバイダーは、コメントの表示要素の一覧を保持し、基になるテキスト<xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed>バッファーのイベントをリッスンし、基になるテキストが削除されたときにコメントの表示要素を削除します。

1. 新しいクラス ファイルをコメント AdornmentTest プロジェクトに追加`CommentAdornmentProvider`し、名前を付けます。

2. 次`using`のディレクティブを追加します。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Collections.ObjectModel;
    using Microsoft.VisualStudio.Text;
    using Microsoft.VisualStudio.Text.Editor;
    ```

3. `CommentAdornmentProvider`という名前のクラスを追加します。

    ```csharp
    internal class CommentAdornmentProvider
    {
    }
    ```

4. テキスト バッファーのプライベート フィールドと、バッファーに関連するコメントの表示要素の一覧を追加します。

    ```csharp
    private ITextBuffer buffer;
    private IList<CommentAdornment> comments = new List<CommentAdornment>();

    ```

5. のコンストラクタを追加`CommentAdornmentProvider`します。 プロバイダーはメソッドによってインスタンス化されるため、このコンストラクターにはプライベート アクセス`Create()`が必要です。 コンストラクターは、`OnBufferChanged`イベント ハンドラーをイベント<xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed>に追加します。

    ```csharp
    private CommentAdornmentProvider(ITextBuffer buffer)
    {
        this.buffer = buffer;
        //listen to the Changed event so we can react to deletions. 
        this.buffer.Changed += OnBufferChanged;
    }

    ```

6. `Create()` メソッドを追加します。

    ```csharp
    public static CommentAdornmentProvider Create(IWpfTextView view)
    {
        return view.Properties.GetOrCreateSingletonProperty<CommentAdornmentProvider>(delegate { return new CommentAdornmentProvider(view.TextBuffer); });
    }

    ```

7. `Detach()` メソッドを追加します。

    ```csharp
    public void Detach()
    {
        if (this.buffer != null)
        {
            //remove the Changed listener 
            this.buffer.Changed -= OnBufferChanged;
            this.buffer = null;
        }
    }
    ```

8. イベント`OnBufferChanged`ハンドラーを追加します。

     [!code-csharp[VSSDKMenuCommandTest#21](../extensibility/codesnippet/CSharp/walkthrough-using-a-shell-command-with-an-editor-extension_2.cs)]
     [!code-vb[VSSDKMenuCommandTest#21](../extensibility/codesnippet/VisualBasic/walkthrough-using-a-shell-command-with-an-editor-extension_2.vb)]

9. イベントの宣言を`CommentsChanged`追加します。

    ```csharp
    public event EventHandler<CommentsChangedEventArgs> CommentsChanged;
    ```

10. 表示要素`Add()`を追加するメソッドを作成します。

    ```csharp
    public void Add(SnapshotSpan span, string author, string text)
    {
        if (span.Length == 0)
            throw new ArgumentOutOfRangeException("span");
        if (author == null)
            throw new ArgumentNullException("author");
        if (text == null)
            throw new ArgumentNullException("text");

        //Create a comment adornment given the span, author and text.
        CommentAdornment comment = new CommentAdornment(span, author, text);

        //Add it to the list of comments. 
        this.comments.Add(comment);

        //Raise the changed event.
        EventHandler<CommentsChangedEventArgs> commentsChanged = this.CommentsChanged;
        if (commentsChanged != null)
            commentsChanged(this, new CommentsChangedEventArgs(comment, null));
    }

    ```

11. メソッドを`RemoveComments()`追加します。

    ```csharp
    public void RemoveComments(SnapshotSpan span)
    {
        EventHandler<CommentsChangedEventArgs> commentsChanged = this.CommentsChanged;

        //Get a list of all the comments that are being kept
        IList<CommentAdornment> keptComments = new List<CommentAdornment>(this.comments.Count);

        foreach (CommentAdornment comment in this.comments)
        {
            //find out if the given span overlaps with the comment text span. If two spans are adjacent, they do not overlap. To consider adjacent spans, use IntersectsWith. 
            if (comment.Span.GetSpan(span.Snapshot).OverlapsWith(span))
            {
                //Raise the change event to delete this comment. 
                if (commentsChanged != null)
                    commentsChanged(this, new CommentsChangedEventArgs(null, comment));
            }
            else
                keptComments.Add(comment);
        }

        this.comments = keptComments;
    }
    ```

12. 指定された`GetComments()`スナップショット範囲内のすべてのコメントを返すメソッドを追加します。

    ```csharp
    public Collection<CommentAdornment> GetComments(SnapshotSpan span)
    {
        IList<CommentAdornment> overlappingComments = new List<CommentAdornment>();
        foreach (CommentAdornment comment in this.comments)
        {
            if (comment.Span.GetSpan(span.Snapshot).OverlapsWith(span))
                overlappingComments.Add(comment);
        }

        return new Collection<CommentAdornment>(overlappingComments);
    }
    ```

13. という名前`CommentsChangedEventArgs`のクラスを次のように追加します。

    ```csharp
    internal class CommentsChangedEventArgs : EventArgs
    {
        public readonly CommentAdornment CommentAdded;

        public readonly CommentAdornment CommentRemoved;

        public CommentsChangedEventArgs(CommentAdornment added, CommentAdornment removed)
        {
            this.CommentAdded = added;
            this.CommentRemoved = removed;
        }
    }
    ```

## <a name="manage-comment-adornments"></a>コメント表示要素の管理
 コメント表示要素マネージャーは、表示要素を作成し、表示要素レイヤーに追加します。 これは、イベント<xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged>と<xref:Microsoft.VisualStudio.Text.Editor.ITextView.Closed>をリッスンして、表示要素を移動または削除できるようにします。 また、コメントが`CommentsChanged`追加または削除されたときにコメント表示要素プロバイダーによって発生するイベントも待機します。

1. クラス ファイルをコメント AdornmentTest プロジェクトに追加し`CommentAdornmentManager`、名前を付けます。

2. 次`using`のディレクティブを追加します。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Windows.Media;
    using Microsoft.VisualStudio.Text;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Text.Formatting;
    ```

3. `CommentAdornmentManager`という名前のクラスを追加します。

    ```csharp
    internal class CommentAdornmentManager
        {
        }
    ```

4. いくつかのプライベート フィールドを追加します。

    ```csharp
    private readonly IWpfTextView view;
    private readonly IAdornmentLayer layer;
    private readonly CommentAdornmentProvider provider;
    ```

5. および<xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged><xref:Microsoft.VisualStudio.Text.Editor.ITextView.Closed>イベントにマネージャーをサブスクライブするコンストラクターを追加します`CommentsChanged`。 このコンストラクターは、マネージャーが静的`Create()`メソッドによってインスタンス化されるため、プライベートです。

    ```csharp
    private CommentAdornmentManager(IWpfTextView view)
    {
        this.view = view;
        this.view.LayoutChanged += OnLayoutChanged;
        this.view.Closed += OnClosed;

        this.layer = view.GetAdornmentLayer("CommentAdornmentLayer");

        this.provider = CommentAdornmentProvider.Create(view);
        this.provider.CommentsChanged += OnCommentsChanged;
    }
    ```

6. プロバイダーを`Create()`取得するメソッドを追加するか、必要に応じてプロバイダーを作成します。

    ```csharp
    public static CommentAdornmentManager Create(IWpfTextView view)
    {
        return view.Properties.GetOrCreateSingletonProperty<CommentAdornmentManager>(delegate { return new CommentAdornmentManager(view); });
    }
    ```

7. ハンドラーを`CommentsChanged`追加します。

    ```csharp
    private void OnCommentsChanged(object sender, CommentsChangedEventArgs e)
    {
        //Remove the comment (when the adornment was added, the comment adornment was used as the tag). 
        if (e.CommentRemoved != null)
            this.layer.RemoveAdornmentsByTag(e.CommentRemoved);

        //Draw the newly added comment (this will appear immediately: the view does not need to do a layout). 
        if (e.CommentAdded != null)
            this.DrawComment(e.CommentAdded);
    }
    ```

8. ハンドラーを<xref:Microsoft.VisualStudio.Text.Editor.ITextView.Closed>追加します。

    ```csharp
    private void OnClosed(object sender, EventArgs e)
    {
        this.provider.Detach();
        this.view.LayoutChanged -= OnLayoutChanged;
        this.view.Closed -= OnClosed;
    }
    ```

9. ハンドラーを<xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged>追加します。

    ```csharp
    private void OnLayoutChanged(object sender, TextViewLayoutChangedEventArgs e)
    {
        //Get all of the comments that intersect any of the new or reformatted lines of text.
        List<CommentAdornment> newComments = new List<CommentAdornment>();

        //The event args contain a list of modified lines and a NormalizedSpanCollection of the spans of the modified lines.  
        //Use the latter to find the comments that intersect the new or reformatted lines of text. 
        foreach (Span span in e.NewOrReformattedSpans)
        {
            newComments.AddRange(this.provider.GetComments(new SnapshotSpan(this.view.TextSnapshot, span)));
        }

        //It is possible to get duplicates in this list if a comment spanned 3 lines, and the first and last lines were modified but the middle line was not. 
        //Sort the list and skip duplicates.
        newComments.Sort(delegate(CommentAdornment a, CommentAdornment b) { return a.GetHashCode().CompareTo(b.GetHashCode()); });

        CommentAdornment lastComment = null;
        foreach (CommentAdornment comment in newComments)
        {
            if (comment != lastComment)
            {
                lastComment = comment;
                this.DrawComment(comment);
            }
        }
    }
    ```

10. コメントを描画するプライベート メソッドを追加します。

     [!code-csharp[VSSDKMenuCommandTest#35](../extensibility/codesnippet/CSharp/walkthrough-using-a-shell-command-with-an-editor-extension_3.cs)]
     [!code-vb[VSSDKMenuCommandTest#35](../extensibility/codesnippet/VisualBasic/walkthrough-using-a-shell-command-with-an-editor-extension_3.vb)]

## <a name="use-the-menu-command-to-add-the-comment-adornment"></a>メニュー コマンドを使用してコメント表示要素を追加する
 メニュー コマンドを使用して、VSPackage の`MenuItemCallback`メソッドを実装することでコメント表示を作成できます。

1. 次の参照を MenuCommandTest プロジェクトに追加します。

    - 相互運用機能

    - エディター

    - Wpf

2. *AddAdornment.cs*ファイルを開き、次`using`のディレクティブを追加します。

    ```csharp
    using Microsoft.VisualStudio.TextManager.Interop;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Editor;
    using CommentAdornmentTest;
    ```

3. メソッドを`Execute()`削除し、次のコマンド ハンドラーを追加します。

    ```csharp
    private async void AddAdornmentHandler(object sender, EventArgs e)
    {
    }
    ```

4. アクティブなビューを取得するコードを追加します。 アクティブ`IVsTextView`な を`SVsTextManager`取得するには、Visual Studio シェルの を取得する必要があります。

    ```csharp
    private async void AddAdornmentHandler(object sender, EventArgs e)
    {
        IVsTextManager txtMgr = (IVsTextManager) await ServiceProvider.GetServiceAsync(typeof(SVsTextManager));
        IVsTextView vTextView = null;
        int mustHaveFocus = 1;
        txtMgr.GetActiveView(mustHaveFocus, null, out vTextView);
    }
    ```

5. このテキスト ビューがエディター テキスト ビューのインスタンスである場合は、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData>インターフェイスにキャストし、<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost>および関連付けられている<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView>を取得できます。 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost>を使用して、コメント`Connector.Execute()`表示要素プロバイダーを取得し、表示要素を追加するメソッドを呼び出します。 コマンド ハンドラーは、次のコードのようになります。

    ```csharp
    private async void AddAdornmentHandler(object sender, EventArgs e)
    {
        IVsTextManager txtMgr = (IVsTextManager) await ServiceProvider.GetServiceAsync(typeof(SVsTextManager));
        IVsTextView vTextView = null;
        int mustHaveFocus = 1;
        txtMgr.GetActiveView(mustHaveFocus, null, out vTextView);
        IVsUserData userData = vTextView as IVsUserData;
         if (userData == null)
        {
            Console.WriteLine("No text view is currently open");
            return;
        }
        IWpfTextViewHost viewHost;
        object holder;
        Guid guidViewHost = DefGuidList.guidIWpfTextViewHost;
        userData.GetData(ref guidViewHost, out holder);
        viewHost = (IWpfTextViewHost)holder;
        Connector.Execute(viewHost);
    }
    ```

6. AddAdornment コンストラクターの AddAdornment コマンドのハンドラーとして AddAdornmentHandler メソッドを設定します。

    ```csharp
    private AddAdornment(AsyncPackage package, OleMenuCommandService commandService)
    {
        this.package = package ?? throw new ArgumentNullException(nameof(package));
        commandService = commandService ?? throw new ArgumentNullException(nameof(commandService));

        var menuCommandID = new CommandID(CommandSet, CommandId);
        var menuItem = new MenuCommand(this.AddAdornmentHandler, menuCommandID);
        commandService.AddCommand(menuItem);
    }
    ```

## <a name="build-and-test-the-code"></a>コードのビルドとテスト

1. ソリューションをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

2. テキスト ファイルを作成します。 テキストを入力して選択します。

3. [**ツール**] メニューの [**表示要素の追加**] をクリックします。 バルーンは、テキスト ウィンドウの右側に表示され、次のようなテキストを含む必要があります。

     あなたのユーザー名

     フォースコア..

## <a name="see-also"></a>関連項目
- [チュートリアル: コンテンツ タイプをファイル名拡張子にリンクする](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
