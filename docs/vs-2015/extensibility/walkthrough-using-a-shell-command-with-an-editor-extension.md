---
title: 'チュートリアル: エディター拡張機能でシェルコマンドを使用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - add a menu command
ms.assetid: 08526848-a442-4cd4-afa1-b2eac2005adb
caps.latest.revision: 47
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0312d98dd6959cb5d67d593c4bf0af39fa1889eb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65693358"
---
# <a name="walkthrough-using-a-shell-command-with-an-editor-extension"></a>チュートリアル: エディター拡張機能でシェル コマンドを使用する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPackage から、メニューコマンドなどの機能をエディターに追加できます。 このチュートリアルでは、メニューコマンドを呼び出して、エディターのテキストビューに表示要素を追加する方法について説明します。  
  
 このチュートリアルでは、Managed Extensibility Framework (MEF) コンポーネントパーツと共に VSPackage を使用する方法について説明します。 VSPackage を使用してメニューコマンドを Visual Studio シェルに登録する必要があります。また、コマンドを使用して、MEF コンポーネントの部分にアクセスすることもできます。  
  
## <a name="prerequisites"></a>前提条件  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
## <a name="creating-an-extension-with-a-menu-command"></a>メニュー コマンドを使用した拡張機能の作成  
 [**ツール**] メニューに [**装飾要素の追加**] という名前のメニューコマンドを配置する VSPackage を作成します。  
  
1. という名前の C# VSIX プロジェクトを作成 `MenuCommandTest` し、カスタムコマンド項目テンプレート名 **addadornment**を追加します。 詳細については、「 [メニューコマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。  
  
2. MenuCommandTest という名前のソリューションが開かれています。 MenuCommandTestPackage ファイルには、メニューコマンドを作成し、[ **ツール** ] メニューに配置するコードが含まれています。 この時点で、コマンドによってメッセージボックスが表示されます。 後の手順で、これを変更してコメントの表示要素を表示する方法を示します。  
  
3. VSIX マニフェスト エディターで source.extension.vsixmanifest ファイルを開きます。 このタブには、 `Assets` MenuCommandTest という名前の VisualStudio の行が含まれている必要があります。  
  
4. Source.extension.vsixmanifest ファイルを保存して閉じます。  
  
## <a name="adding-a-mef-extension-to-the-command-extension"></a>コマンド拡張機能への MEF 拡張機能の追加  
  
1. **ソリューションエクスプローラー**で、ソリューションノードを右クリックし、[**追加**] をクリックして、[**新しいプロジェクト**] をクリックします。 [**新しいプロジェクトの追加**] ダイアログボックスで、[ **Visual C#**] の [**拡張機能**]、[ **VSIX プロジェクト**] の順にクリックします。 プロジェクトに `CommentAdornmentTest` という名前を付けます。  
  
2. このプロジェクトは、厳密に名前が付けられた VSPackage アセンブリと対話するため、アセンブリに署名する必要があります。 VSPackage アセンブリ用に既に作成されているキーファイルを再利用することができます。  
  
    1. プロジェクトのプロパティを開き、[ **署名** ] タブを選択します。  
  
    2. [ **アセンブリの署名**] を選択します。  
  
    3. [ **厳密な名前のキーファイルを選択し**てください] で、MenuCommandTest アセンブリ用に生成されたキー .snk ファイルを選択します。  
  
## <a name="referring-to-the-mef-extension-in-the-vspackage-project"></a>VSPackage プロジェクトでの MEF 拡張機能の参照  
 MEF コンポーネントを VSPackage に追加するため、マニフェストで両方の種類のアセットを指定する必要があります。  
  
> [!NOTE]
> MEF の詳細については、「 [Managed Extensibility Framework (mef)](https://msdn.microsoft.com/library/6c61b4ec-c6df-4651-80f1-4854f8b14dde)」を参照してください。  
  
#### <a name="to-refer-to-the-mef-component-in-the-vspackage-project"></a>VSPackage プロジェクトで MEF コンポーネントを参照するには  
  
1. MenuCommandTest プロジェクトで、VSIX マニフェストエディターの source.extension.vsixmanifest ファイルを開きます。  
  
2. [ **アセット** ] タブで、[ **新規**] をクリックします。  
  
3. [ **種類** ] ボックスの一覧で、[ **VisualStudio**] を選択します。  
  
4. [ **ソース** ] ボックスの一覧で、 **現在のソリューション内のプロジェクト**を選択します。  
  
5. [ **プロジェクト** ] ボックスの一覧で [ **CommentAdornmentTest**] を選択します。  
  
6. Source.extension.vsixmanifest ファイルを保存して閉じます。  
  
7. MenuCommandTest プロジェクトに CommentAdornmentTest プロジェクトへの参照があることを確認します。  
  
8. CommentAdornmentTest プロジェクトで、アセンブリを生成するようにプロジェクトを設定します。 **ソリューションエクスプローラー**でプロジェクトを選択し、[**プロパティ**] ウィンドウで [**ビルド出力を outputdirectory にコピー** ] プロパティを確認し、[ **true**] に設定します。  
  
## <a name="defining-a-comment-adornment"></a>コメントの装飾を定義する  
 コメントの表示記号自体は、 <xref:Microsoft.VisualStudio.Text.ITrackingSpan> 選択されたテキストを追跡すると、作成者とテキストの説明を表す文字列で構成されます。  
  
#### <a name="to-define-a-comment-adornment"></a>コメントの装飾を定義するには  
  
1. CommentAdornmentTest プロジェクトで、新しいクラスファイルを追加し、という名前を指定 `CommentAdornment` します。  
  
2. 次の参照を追加します。  
  
    1. VisualStudio. CoreUtility  
  
    2. VisualStudio のデータ  
  
    3. VisualStudio. Logic  
  
    4. VisualStudio. UI  
  
    5. VisualStudio (Microsoft. UI)  
  
    6. System.ComponentModel.Composition  
  
    7. PresentationCore  
  
    8. PresentationFramework  
  
    9. WindowsBase  
  
3. 次の `using` ステートメントを追加します。  
  
    ```vb  
    using Microsoft.VisualStudio.Text;  
    ```  
  
4. ファイルには、という名前のクラスが含まれている必要があり `CommentAdornment` ます。  
  
    ```  
    internal class CommentAdornment  
    ```  
  
5. 、 `CommentAdornment` <xref:Microsoft.VisualStudio.Text.ITrackingSpan> 作成者、および説明のクラスに、3つのフィールドを追加します。  
  
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
  
## <a name="creating-a-visual-element-for-the-adornment"></a>表示要素のビジュアル要素を作成する  
 また、表示要素のビジュアル要素も定義する必要があります。 このチュートリアルでは、Windows Presentation Foundation (WPF) クラスを継承するコントロールを定義し <xref:System.Windows.Controls.Canvas> ます。  
  
1. CommentAdornmentTest プロジェクトにクラスを作成し、という名前を指定し `CommentBlock` ます。  
  
2. 次の `using` ステートメントを追加します。  
  
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
  
3. クラスがから継承されるように `CommentBlock` <xref:System.Windows.Controls.Canvas> します。  
  
    ```csharp  
    internal class CommentBlock : Canvas  
    { }  
    ```  
  
4. いくつかのプライベートフィールドを追加して、表示要素の視覚的な側面を定義します。  
  
    ```csharp  
    private Geometry textGeometry;  
    private Grid commentGrid;  
    private static Brush brush;  
    private static Pen solidPen;  
    private static Pen dashPen;  
    ```  
  
5. コメントの表示要素を定義するコンストラクターを追加し、関連するテキストを追加します。  
  
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
  
6. また <xref:System.Windows.Controls.Panel.OnRender%2A> 、装飾を描画するイベントハンドラーも実装します。  
  
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
  
## <a name="adding-an-iwpftextviewcreationlistener"></a>IWpfTextViewCreationListener の追加  
 は、 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener> 作成イベントの表示をリッスンするために使用できる MEF コンポーネント部分です。  
  
1. CommentAdornmentTest プロジェクトにクラスファイルを追加し、という名前を指定 `Connector` します。  
  
2. 次の `using` ステートメントを追加します。  
  
    ```csharp  
    using System.ComponentModel.Composition;  
    using Microsoft.VisualStudio.Text.Editor;  
    using Microsoft.VisualStudio.Utilities;  
    ```  
  
3. を実装するクラスを宣言 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener> し、 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "text" およびのを使用してエクスポートし <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document> ます。 Content type 属性は、コンポーネントが適用されるコンテンツの種類を指定します。 テキスト型は、すべての非バイナリファイルの種類の基本型です。 このため、作成されるほとんどすべてのテキストビューがこの型になります。 Text view role 属性は、コンポーネントが適用されるテキストビューの種類を指定します。 ドキュメントテキストビューロールでは、通常、行で構成され、ファイルに格納されているテキストが表示されます。  
  
     [!code-csharp[VSSDKMenuCommandTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdkmenucommandtest/cs/commentadornmenttest/connector.cs#11)]
     [!code-vb[VSSDKMenuCommandTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkmenucommandtest/vb/commentadornmenttest/connector.vb#11)]  
  
4. <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A>の静的イベントを呼び出すように、メソッドを実装し `Create()` `CommentAdornmentManager` ます。  
  
    ```csharp  
    public void TextViewCreated(IWpfTextView textView)  
    {  
        CommentAdornmentManager.Create(textView);  
    }  
    ```  
  
5. コマンドを実行するために使用できるメソッドを追加します。  
  
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
  
## <a name="defining-an-adornment-layer"></a>装飾層の定義  
 新しい表示要素を追加するには、表示要素レイヤーを定義する必要があります。  
  
#### <a name="to-define-an-adornment-layer"></a>装飾層を定義するには  
  
1. クラス内で `Connector` 、型のパブリックフィールドを宣言 <xref:Microsoft.VisualStudio.Text.Editor.AdornmentLayerDefinition> し、表示要素の一意の名前を指定するを使用してエクスポートし <xref:Microsoft.VisualStudio.Utilities.NameAttribute> <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> ます。これは、この装飾層の他のテキストビューレイヤー (テキスト、キャレット、および選択) への Z オーダー関係を定義するによってエクスポートされます。  
  
    ```csharp  
    [Export(typeof(AdornmentLayerDefinition))]  
    [Name("CommentAdornmentLayer")]  
    [Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]  
    public AdornmentLayerDefinition commentLayerDefinition;  
  
    ```  
  
## <a name="providing-comment-adornments"></a>コメントの修飾を指定する  
 表示要素を定義するときは、コメント表示項目の表示プロバイダーとコメントの表示要素を実装することもできます。 コメント表示の表示プロバイダーは、コメントの表示要素の一覧を保持し、 <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> 基になるテキストバッファーでイベントをリッスンし、基になるテキストが削除されたときにコメントの修飾を削除します。  
  
1. CommentAdornmentTest プロジェクトに新しいクラスファイルを追加し、という名前を指定 `CommentAdornmentProvider` します。  
  
2. 次の `using` ステートメントを追加します。  
  
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
  
4. テキストバッファーのプライベートフィールドと、バッファーに関連付けられているコメントの表示要素の一覧を追加します。  
  
    ```csharp  
    private ITextBuffer buffer;  
    private IList<CommentAdornment> comments = new List<CommentAdornment>();  
  
    ```  
  
5. のコンストラクターを追加 `CommentAdornmentProvider` します。 プロバイダーはメソッドによってインスタンス化されるため、このコンストラクターにはプライベートアクセスが必要 `Create()` です。 コンストラクターはイベント `OnBufferChanged` にイベントハンドラーを追加し <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> ます。  
  
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
  
8. `OnBufferChanged`イベントハンドラーを追加します。  
  
    ```csharp  
    private void OnBufferChanged(object sender, TextContentChangedEventArgs e)  
    {  
        //Make a list of all comments that have a span of at least one character after applying the change. There is no need to raise a changed event for the deleted adornments. The adornments are deleted only if a text change would cause the view to reformat the line and discard the adornments.  
        IList<CommentAdornment> keptComments = new List<CommentAdornment>(this.comments.Count);  
  
        foreach (CommentAdornment comment in this.comments)  
        {  
            Span span = comment.Span.GetSpan(e.After);  
            //if a comment does not span at least one character, its text was deleted.   
            if (span.Length != 0)  
            {  
                keptComments.Add(comment);  
            }  
        }  
  
        this.comments = keptComments;  
    }  
  
    ```  
  
     [!code-csharp[VSSDKMenuCommandTest#21](../snippets/csharp/VS_Snippets_VSSDK/vssdkmenucommandtest/cs/commentadornmenttest/commentadornmentprovider.cs#21)]
     [!code-vb[VSSDKMenuCommandTest#21](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkmenucommandtest/vb/commentadornmenttest/commentadornmentprovider.vb#21)]  
  
9. イベントの宣言を追加 `CommentsChanged` します。  
  
    ```csharp  
    public event EventHandler<CommentsChangedEventArgs> CommentsChanged;  
    ```  
  
10. 装飾を `Add()` 追加するメソッドを作成します。  
  
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
  
11. メソッドを追加 `RemoveComments()` します。  
  
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
  
12. `GetComments()`指定されたスナップショットスパン内のすべてのコメントを返すメソッドを追加します。  
  
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
  
13. 次のように、という名前のクラスを追加し `CommentsChangedEventArgs` ます。  
  
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
  
## <a name="managing-comment-adornments"></a>コメントの修飾の管理  
 コメントの装飾マネージャーは、装飾を作成し、それを装飾層に追加します。 このメソッドは、およびイベントをリッスンして、 <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> <xref:Microsoft.VisualStudio.Text.Editor.ITextView.Closed> 装飾を移動または削除できるようにします。 また、 `CommentsChanged` コメントが追加または削除されたときに、コメントの装飾のプロバイダーによって発生するイベントをリッスンします。  
  
1. CommentAdornmentTest プロジェクトにクラスファイルを追加し、という名前を指定 `CommentAdornmentManager` します。  
  
2. 次の `using` ステートメントを追加します。  
  
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
  
4. いくつかのプライベートフィールドを追加します。  
  
    ```csharp  
    private readonly IWpfTextView view;  
    private readonly IAdornmentLayer layer;  
    private readonly CommentAdornmentProvider provider;  
    ```  
  
5. イベントおよびイベントに対して、マネージャーをサブスクライブするコンストラクターを追加 <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> <xref:Microsoft.VisualStudio.Text.Editor.ITextView.Closed> し `CommentsChanged` ます。 このコンストラクターは、静的メソッドによってマネージャーがインスタンス化されるため、プライベートです `Create()` 。  
  
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
  
6. プロバイダーを `Create()` 取得するメソッドを追加するか、必要に応じて作成します。  
  
    ```csharp  
    public static CommentAdornmentManager Create(IWpfTextView view)  
    {  
        return view.Properties.GetOrCreateSingletonProperty<CommentAdornmentManager>(delegate { return new CommentAdornmentManager(view); });  
    }  
    ```  
  
7. ハンドラーを追加 `CommentsChanged` します。  
  
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
  
8. ハンドラーを追加 <xref:Microsoft.VisualStudio.Text.Editor.ITextView.Closed> します。  
  
    ```csharp  
    private void OnClosed(object sender, EventArgs e)  
    {  
        this.provider.Detach();  
        this.view.LayoutChanged -= OnLayoutChanged;  
        this.view.Closed -= OnClosed;  
    }  
    ```  
  
9. ハンドラーを追加 <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> します。  
  
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
  
10. コメントを描画するプライベートメソッドを追加します。  
  
     [!code-csharp[VSSDKMenuCommandTest#35](../snippets/csharp/VS_Snippets_VSSDK/vssdkmenucommandtest/cs/commentadornmenttest/commentadornmentmanager.cs#35)]
     [!code-vb[VSSDKMenuCommandTest#35](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkmenucommandtest/vb/commentadornmenttest/commentadornmentmanager.vb#35)]  
  
## <a name="using-the-menu-command-to-add-the-comment-adornment"></a>メニューコマンドを使用してコメントの装飾を追加する  
 メニューコマンドを使用して、VSPackage のメソッドを実装することにより、コメントの表示要素を作成でき `MenuItemCallback` ます。  
  
1. MenuCommandTest プロジェクトに次の参照を追加します。  
  
    - VisualStudio。相互運用  
  
    - VisualStudio  
  
    - VisualStudio (Microsoft. UI)  
  
2. AddAdornment.cs ファイルを開き、次のステートメントを追加し `using` ます。  
  
    ```csharp  
    using Microsoft.VisualStudio.TextManager.Interop;  
    using Microsoft.VisualStudio.Text.Editor;  
    using Microsoft.VisualStudio.Editor;  
    using CommentAdornmentTest;  
    ```  
  
3. ShowMessageBox () メソッドを削除し、次のコマンドハンドラーを追加します。  
  
    ```csharp  
    private void AddAdornmentHandler(object sender, EventArgs e)  
    {  
    }  
    ```  
  
4. アクティブなビューを取得するコードを追加します。 `SVsTextManager`アクティブなを取得するには、Visual Studio シェルのを取得する必要があり `IVsTextView` ます。  
  
    ```csharp  
    private void AddAdornmentHandler(object sender, EventArgs e)  
    {  
        IVsTextManager txtMgr = (IVsTextManager)ServiceProvider.GetService(typeof(SVsTextManager));  
        IVsTextView vTextView = null;  
        int mustHaveFocus = 1;  
        txtMgr.GetActiveView(mustHaveFocus, null, out vTextView);  
    }  
    ```  
  
5. このテキストビューがエディターのテキストビューのインスタンスである場合は、それをインターフェイスにキャスト <xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData> して、 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> とそれに関連付けられたを取得することができ <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView> ます。 を使用して <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> メソッドを呼び出し `Connector.Execute()` ます。このメソッドは、コメントの装飾のプロバイダーを取得し、装飾を追加します。 コマンドハンドラーは、次のようになります。  
  
    ```csharp  
    private void AddAdornmentHandler(object sender, EventArgs e)  
    {  
        IVsTextManager txtMgr = (IVsTextManager)ServiceProvider.GetService(typeof(SVsTextManager));  
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
  
6. Addadornment コンストラクターの AddAdornment コマンドのハンドラーとして、このメソッドを設定します。  
  
    ```csharp  
    private AddAdornment(Package package)  
    {  
        if (package == null)  
        {  
            throw new ArgumentNullException(nameof(package));  
        }  
  
        this.package = package;  
  
        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;  
        if (commandService != null)  
        {  
            CommandID menuCommandID = new CommandID(MenuGroup, CommandId);  
            EventHandler eventHandler = this.AddAdornmentHandler;  
            MenuCommand menuItem = new MenuCommand(eventHandler, menuCommandID);  
            commandService.AddCommand(menuItem);  
        }  
    }  
    ```  
  
## <a name="building-and-testing-the-code"></a>コードのビルドとテスト  
  
1. ソリューションをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。  
  
2. テキスト ファイルを作成します。 テキストを入力して選択します。  
  
3. [ **ツール** ] メニューの [ **装飾の追加**] をクリックします。 バルーンはテキストウィンドウの右側に表示され、次のテキストのようなテキストが含まれている必要があります。  
  
     ユーザー名  
  
     4スコア...  
  
## <a name="see-also"></a>参照  
 [チュートリアル: コンテンツの種類とファイル名拡張子とをリンクさせる](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
