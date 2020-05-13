---
title: 'チュートリアル: テキストを強調表示する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - highlight text
ms.assetid: 64b772ad-4392-42e9-a237-5137f0384bf0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c35b1a032993a6c183191aafff77d8adeba4a3ef
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697404"
---
# <a name="walkthrough-highlight-text"></a>チュートリアル: テキストを強調表示する
マネージ機能拡張フレームワーク (MEF) コンポーネントパーツを作成することで、エディターにさまざまな視覚効果を追加できます。 このチュートリアルでは、テキスト ファイル内の現在の単語の出現箇所をすべて強調表示する方法を示します。 テキスト ファイル内で単語が複数回出現し、キャレットを 1 回に配置すると、すべての出現箇所が強調表示されます。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-mef-project"></a>MEF プロジェクトを作成する

1. C# VSIX プロジェクトを作成します。 ([**新しいプロジェクト**] ダイアログで、[**ビジュアル C# / 拡張性**] を選択し、次に**VSIX プロジェクト**を選択します)。ソリューションに名前`HighlightWordTest`を付ける:

2. エディター分類子項目テンプレートをプロジェクトに追加します。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

3. 既存のクラス ファイルを削除します。

## <a name="define-a-textmarkertag"></a>テキストマーカータグの定義
 テキストをハイライト表示する最初の手順は、サブ<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>クラス化とその外観の定義です。

### <a name="to-define-a-textmarkertag-and-a-markerformatdefinition"></a>テキスト マーカー タグとマーカーフォーマット定義を定義するには

1. クラス ファイルを追加し、名前を**強調表示ワード タグ**。

2. 次の参照を追加します。

    1. ユーティリティ

    2. データ

    3. ロジック

    4. UI

    5. Wpf

    6. System.ComponentModel.Composition

    7. プレゼンテーション.コア

    8. プレゼンテーション.フレームワーク

3. 次の名前空間をインポートします。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.ComponentModel.Composition;
    using System.Linq;
    using System.Threading;
    using Microsoft.VisualStudio.Text;
    using Microsoft.VisualStudio.Text.Classification;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Text.Operations;
    using Microsoft.VisualStudio.Text.Tagging;
    using Microsoft.VisualStudio.Utilities;
    using System.Windows.Media;
    ```

4. から<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>継承し、名前を付けるクラスを`HighlightWordTag`作成します。

    ```csharp
    internal class HighlightWordTag : TextMarkerTag
    {

    }
    ```

5. から<xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition>継承する 2 番目のクラスを作成し`HighlightWordFormatDefinition`、 という名前を付けます。 このフォーマット定義をタグに使用するには、次の属性を指定してエクスポートする必要があります。

    - <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: タグはこの形式を参照するためにこれを使用します

    - <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>: これにより、UI に表示される形式が表示されます。

    ```csharp

    [Export(typeof(EditorFormatDefinition))]
    [Name("MarkerFormatDefinition/HighlightWordFormatDefinition")]
    [UserVisible(true)]
    internal class HighlightWordFormatDefinition : MarkerFormatDefinition
    {

    }
    ```

6. のコンストラクターで、表示名と外観を定義します。 Background プロパティは塗りつぶしの色を定義し、Foreground プロパティは境界線の色を定義します。

    ```csharp
    public HighlightWordFormatDefinition()
    {
                this.BackgroundColor = Colors.LightBlue;
        this.ForegroundColor = Colors.DarkBlue;
        this.DisplayName = "Highlight Word";
        this.ZOrder = 5;
    }
    ```

7. HighlightWordTag のコンストラクターで、作成した書式定義の名前を渡します。

    ```
    public HighlightWordTag() : base("MarkerFormatDefinition/HighlightWordFormatDefinition") { }
    ```

## <a name="implement-an-itagger"></a>ITagger を実装する
 次の手順では、インターフェイスを<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>実装します。 このインターフェイスは、テキストの強調表示やその他の視覚効果を提供するタグを、指定されたテキスト バッファーに割り当てます。

### <a name="to-implement-a-tagger"></a>タガーを実装するには

1. 型<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>`HighlightWordTag`を実装するクラスを作成し、 という`HighlightWordTagger`名前を付けます。

    ```csharp
    internal class HighlightWordTagger : ITagger<HighlightWordTag>
    {

    }
    ```

2. 次のプライベート フィールドとプロパティをクラスに追加します。

    - 現在<xref:Microsoft.VisualStudio.Text.Editor.ITextView>のテキスト ビューに対応する 、 。

    - テキスト<xref:Microsoft.VisualStudio.Text.ITextBuffer>ビューの基になるテキスト バッファーに対応する 。

    - テキスト<xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService>を検索するために使用します。

    - テキスト<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator>範囲内を移動するためのメソッドを持つ 。

    - A <xref:Microsoft.VisualStudio.Text.NormalizedSnapshotSpanCollection>:強調表示する単語のセットを含みます。

    - 現在<xref:Microsoft.VisualStudio.Text.SnapshotSpan>の単語に対応します。

    - A<xref:Microsoft.VisualStudio.Text.SnapshotPoint>キャレットの現在位置に対応します。

    - ロック オブジェクト。

    ```csharp
    ITextView View { get; set; }
    ITextBuffer SourceBuffer { get; set; }
    ITextSearchService TextSearchService { get; set; }
    ITextStructureNavigator TextStructureNavigator { get; set; }
    NormalizedSnapshotSpanCollection WordSpans { get; set; }
    SnapshotSpan? CurrentWord { get; set; }
    SnapshotPoint RequestedPoint { get; set; }
    object updateLock = new object();

    ```

3. 前に示したプロパティを初期化し、追加およびイベント<xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged><xref:Microsoft.VisualStudio.Text.Editor.ITextCaret.PositionChanged>ハンドラーを実行するコンストラクターを追加します。

    ```csharp
    public HighlightWordTagger(ITextView view, ITextBuffer sourceBuffer, ITextSearchService textSearchService,
    ITextStructureNavigator textStructureNavigator)
    {
        this.View = view;
        this.SourceBuffer = sourceBuffer;
        this.TextSearchService = textSearchService;
        this.TextStructureNavigator = textStructureNavigator;
        this.WordSpans = new NormalizedSnapshotSpanCollection();
        this.CurrentWord = null;
        this.View.Caret.PositionChanged += CaretPositionChanged;
        this.View.LayoutChanged += ViewLayoutChanged;
    }

    ```

4. イベント ハンドラーは、両方`UpdateAtCaretPosition`ともメソッドを呼び出します。

    ```csharp
    void ViewLayoutChanged(object sender, TextViewLayoutChangedEventArgs e)
    {
        // If a new snapshot wasn't generated, then skip this layout 
        if (e.NewSnapshot != e.OldSnapshot)
        {
            UpdateAtCaretPosition(View.Caret.Position);
        }
    }

    void CaretPositionChanged(object sender, CaretPositionChangedEventArgs e)
    {
        UpdateAtCaretPosition(e.NewPosition);
    }
    ```

5. また、update メソッド`TagsChanged`によって呼び出されるイベントを追加する必要があります。

     [!code-csharp[VSSDKHighlightWordTest#10](../extensibility/codesnippet/CSharp/walkthrough-highlighting-text_1.cs)]
     [!code-vb[VSSDKHighlightWordTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-highlighting-text_1.vb)]

6. この`UpdateAtCaretPosition()`メソッドは、カーソルが置かれている単語と同じテキスト バッファー内のすべての単語を検索し、その単語の出現<xref:Microsoft.VisualStudio.Text.SnapshotSpan>に対応するオブジェクトのリストを作成します。 次に、`SynchronousUpdate`を呼び出`TagsChanged`し、イベントを発生させます。

    ```csharp
    void UpdateAtCaretPosition(CaretPosition caretPosition)
    {
        SnapshotPoint? point = caretPosition.Point.GetPoint(SourceBuffer, caretPosition.Affinity);

        if (!point.HasValue)
            return;

        // If the new caret position is still within the current word (and on the same snapshot), we don't need to check it 
        if (CurrentWord.HasValue
            && CurrentWord.Value.Snapshot == View.TextSnapshot
            && point.Value >= CurrentWord.Value.Start
            && point.Value <= CurrentWord.Value.End)
        {
            return;
        }

        RequestedPoint = point.Value;
        UpdateWordAdornments();
    }

    void UpdateWordAdornments()
    {
        SnapshotPoint currentRequest = RequestedPoint;
        List<SnapshotSpan> wordSpans = new List<SnapshotSpan>();
        //Find all words in the buffer like the one the caret is on
        TextExtent word = TextStructureNavigator.GetExtentOfWord(currentRequest);
        bool foundWord = true;
        //If we've selected something not worth highlighting, we might have missed a "word" by a little bit
        if (!WordExtentIsValid(currentRequest, word))
        {
            //Before we retry, make sure it is worthwhile 
            if (word.Span.Start != currentRequest
                 || currentRequest == currentRequest.GetContainingLine().Start
                 || char.IsWhiteSpace((currentRequest - 1).GetChar()))
            {
                foundWord = false;
            }
            else
            {
                // Try again, one character previous.  
                //If the caret is at the end of a word, pick up the word.
                word = TextStructureNavigator.GetExtentOfWord(currentRequest - 1);

                //If the word still isn't valid, we're done 
                if (!WordExtentIsValid(currentRequest, word))
                    foundWord = false;
            }
        }

        if (!foundWord)
        {
            //If we couldn't find a word, clear out the existing markers
            SynchronousUpdate(currentRequest, new NormalizedSnapshotSpanCollection(), null);
            return;
        }

        SnapshotSpan currentWord = word.Span;
        //If this is the current word, and the caret moved within a word, we're done. 
        if (CurrentWord.HasValue && currentWord == CurrentWord)
            return;

        //Find the new spans
        FindData findData = new FindData(currentWord.GetText(), currentWord.Snapshot);
        findData.FindOptions = FindOptions.WholeWord | FindOptions.MatchCase;

        wordSpans.AddRange(TextSearchService.FindAll(findData));

        //If another change hasn't happened, do a real update 
        if (currentRequest == RequestedPoint)
            SynchronousUpdate(currentRequest, new NormalizedSnapshotSpanCollection(wordSpans), currentWord);
    }
    static bool WordExtentIsValid(SnapshotPoint currentRequest, TextExtent word)
    {
        return word.IsSignificant
            && currentRequest.Snapshot.GetText(word.Span).Any(c => char.IsLetter(c));
    }

    ```

7. プロパティ`SynchronousUpdate`の同期更新を`WordSpans``CurrentWord`実行し、イベントを`TagsChanged`発生させます。

    ```csharp
    void SynchronousUpdate(SnapshotPoint currentRequest, NormalizedSnapshotSpanCollection newSpans, SnapshotSpan? newCurrentWord)
    {
        lock (updateLock)
        {
            if (currentRequest != RequestedPoint)
                return;

            WordSpans = newSpans;
            CurrentWord = newCurrentWord;

            var tempEvent = TagsChanged;
            if (tempEvent != null)
                tempEvent(this, new SnapshotSpanEventArgs(new SnapshotSpan(SourceBuffer.CurrentSnapshot, 0, SourceBuffer.CurrentSnapshot.Length)));
        }
    }
    ```

8. メソッドを実装する<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A>必要があります。 このメソッドは、オブジェクトの<xref:Microsoft.VisualStudio.Text.SnapshotSpan>コレクションを受け取り、タグ範囲の列挙を返します。

     C# では、このメソッドを、タグの遅延評価 (つまり、個々の項目がアクセスされた場合にのみセットの評価) を可能にする、yield イテレータとして実装します。 Visual Basic で、リストにタグを追加し、リストを返します。

     ここでは、このメソッドは<xref:Microsoft.VisualStudio.Text.Tagging.TagSpan%601>、青の背景を提供する<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>"青" を持つオブジェクトを返します。

    ```csharp
    public IEnumerable<ITagSpan<HighlightWordTag>> GetTags(NormalizedSnapshotSpanCollection spans)
    {
        if (CurrentWord == null)
            yield break;

        // Hold on to a "snapshot" of the word spans and current word, so that we maintain the same
        // collection throughout
        SnapshotSpan currentWord = CurrentWord.Value;
        NormalizedSnapshotSpanCollection wordSpans = WordSpans;

        if (spans.Count == 0 || wordSpans.Count == 0)
            yield break;

        // If the requested snapshot isn't the same as the one our words are on, translate our spans to the expected snapshot 
        if (spans[0].Snapshot != wordSpans[0].Snapshot)
        {
            wordSpans = new NormalizedSnapshotSpanCollection(
                wordSpans.Select(span => span.TranslateTo(spans[0].Snapshot, SpanTrackingMode.EdgeExclusive)));

            currentWord = currentWord.TranslateTo(spans[0].Snapshot, SpanTrackingMode.EdgeExclusive);
        }

        // First, yield back the word the cursor is under (if it overlaps) 
        // Note that we'll yield back the same word again in the wordspans collection; 
        // the duplication here is expected. 
        if (spans.OverlapsWith(new NormalizedSnapshotSpanCollection(currentWord)))
            yield return new TagSpan<HighlightWordTag>(currentWord, new HighlightWordTag());

        // Second, yield all the other words in the file 
        foreach (SnapshotSpan span in NormalizedSnapshotSpanCollection.Overlap(spans, wordSpans))
        {
            yield return new TagSpan<HighlightWordTag>(span, new HighlightWordTag());
        }
    }
    ```

## <a name="create-a-tagger-provider"></a>タガー プロバイダの作成
 タガーを作成するには、 を実装する<xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider>必要があります。 このクラスは MEF コンポーネントの部分であるため、この拡張機能が認識されるように正しい属性を設定する必要があります。

> [!NOTE]
> MEF の詳細については、「[マネージ機能拡張フレームワーク (MEF) 」](/dotnet/framework/mef/index)を参照してください。

### <a name="to-create-a-tagger-provider"></a>タガー プロバイダーを作成するには

1. を実装するという`HighlightWordTaggerProvider`名前のクラス<xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider>を作成し、それを<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>"text" および<xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>of<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>の でエクスポートします。

    ```csharp
    [Export(typeof(IViewTaggerProvider))]
    [ContentType("text")]
    [TagType(typeof(TextMarkerTag))]
    internal class HighlightWordTaggerProvider : IViewTaggerProvider
    { }
    ```

2. タガーをインスタンス化するには、<xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService>と<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>の 2 つのエディター サービスをインポートする必要があります。

    ```csharp
    [Import]
    internal ITextSearchService TextSearchService { get; set; }

    [Import]
    internal ITextStructureNavigatorSelectorService TextStructureNavigatorSelector { get; set; }

    ```

3. のインスタンス<xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A>を返すメソッドを実装`HighlightWordTagger`します。

    ```csharp
    public ITagger<T> CreateTagger<T>(ITextView textView, ITextBuffer buffer) where T : ITag
    {
        //provide highlighting only on the top buffer 
        if (textView.TextBuffer != buffer)
            return null;

        ITextStructureNavigator textStructureNavigator =
            TextStructureNavigatorSelector.GetTextStructureNavigator(buffer);

        return new HighlightWordTagger(textView, buffer, TextSearchService, textStructureNavigator) as ITagger<T>;
    }
    ```

## <a name="build-and-test-the-code"></a>コードのビルドとテスト
 このコードをテストするには、HighlightWordTest ソリューションをビルドし、実験用インスタンスで実行します。

### <a name="to-build-and-test-the-highlightwordtest-solution"></a>ソリューションをビルドしてテストするには

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 番目のインスタンスが起動します。

3. テキスト ファイルを作成し、単語が繰り返されるテキストを入力します。たとえば"hello hello hello"。

4. 「hello」の出現の1つにカーソルを置きます。 すべての出現箇所は青で強調表示する必要があります。

## <a name="see-also"></a>関連項目
- [チュートリアル: コンテンツ タイプをファイル名拡張子にリンクする](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
