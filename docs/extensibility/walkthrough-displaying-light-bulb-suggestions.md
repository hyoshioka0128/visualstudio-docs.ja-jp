---
title: 'チュートリアル: 電球の提案を表示する |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 99e5566d-450e-4660-9bca-454e1c056a02
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 153eda065b9a6e845a39c35aaae34bbe1745f7a8
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904994"
---
# <a name="walkthrough-display-light-bulb-suggestions"></a>チュートリアル: 電球の提案を表示する
電球は、Visual Studio エディターのアイコンです。これは、組み込みのコードアナライザーまたはコードリファクタリングで特定された問題の修正など、一連のアクションを表示するために展開されます。

 Visual C# と Visual Basic エディターでは、.NET Compiler Platform ("Roslyn") を使用して、電球を自動的に表示するアクションを使用して独自のコードアナライザーを記述し、パッケージ化することもできます。 詳細については次を参照してください:

- [方法: C# 診断とコード修正プログラムを記述する](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix)

- [方法: Visual Basic 診断とコード修正プログラムを記述する](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-Visual-Basic-Analyzer-and-Code-Fix)

  C++ などの他の言語では、その機能のスタブ実装を作成するための提案など、いくつかのクイックアクションの電球も用意されています。

  電球は次のようになります。 Visual Basic または Visual C# プロジェクトでは、無効な場合、変数名の下に赤い波線が表示されます。 無効な識別子にマウスを置くと、カーソルの近くに電球が表示されます。

  ![電球](../extensibility/media/lightbulb.png "LightBulb")

  電球の下矢印をクリックすると、選択したアクションのプレビューと共に、一連の推奨アクションが表示されます。 この場合、アクションを実行すると、コードに加えられた変更が表示されます。

  ![電球のプレビュー](../extensibility/media/lightbulbpreview.png "ライトのバルクプレビュー")

  電球を使用すると、独自の推奨アクションを提供できます。 たとえば、左中かっこを新しい行に移動したり、前の行の末尾に移動したりするアクションを指定できます。 次のチュートリアルでは、現在の単語に表示される電球を作成する方法を説明します。また、[**大文字に変換**] と [**小文字に**変換] の2つの推奨アクションがあります。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-managed-extensibility-framework-mef-project"></a>Managed Extensibility Framework (MEF) プロジェクトを作成する

1. C# VSIX プロジェクトを作成します。 ([**新しいプロジェクト**] ダイアログで、[Visual C#]、[**拡張機能**]、[ **VSIX プロジェクト**] の順に選択します)。ソリューションにという名前を指定 `LightBulbTest` します。

2. **エディター分類子**項目テンプレートをプロジェクトに追加します。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)する」を参照してください。

3. 既存のクラス ファイルを削除します。

4. 次の参照をプロジェクトに追加し、[**ローカルにコピー** ] をに設定し `False` ます。

     *Microsoft.VisualStudio.Language.Intellisense*

5. 新しいクラスファイルを追加し、それに**電球**という名前を指定します。

6. ディレクティブを使用して以下を追加します。

    ```csharp
    using System;
    using System.Linq;
    using System.Collections.Generic;
    using System.Threading.Tasks;
    using Microsoft.VisualStudio.Language.Intellisense;
    using Microsoft.VisualStudio.Text;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Text.Operations;
    using Microsoft.VisualStudio.Utilities;
    using System.ComponentModel.Composition;
    using System.Threading;

    ```

## <a name="implement-the-light-bulb-source-provider"></a>電球ソースプロバイダーを実装する

1. *LightBulbTest.cs*クラスファイルで、ライトを削除します。 を実装する**TestSuggestedActionsSourceProvider**という名前のクラスを追加 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider> します。 テストの提案された**アクション**の名前と "text" を使用してエクスポートし <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> ます。

    ```csharp
    [Export(typeof(ISuggestedActionsSourceProvider))]
    [Name("Test Suggested Actions")]
    [ContentType("text")]
    internal class TestSuggestedActionsSourceProvider : ISuggestedActionsSourceProvider
    ```

2. ソースプロバイダークラス内で、をインポート <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> し、プロパティとして追加します。

    ```csharp
    [Import(typeof(ITextStructureNavigatorSelectorService))]
    internal ITextStructureNavigatorSelectorService NavigatorService { get; set; }
    ```

3. オブジェクトを <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider.CreateSuggestedActionsSource%2A> 返すメソッドを実装し <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource> ます。 ソースについては、次のセクションで説明します。

    ```csharp
    public ISuggestedActionsSource CreateSuggestedActionsSource(ITextView textView, ITextBuffer textBuffer)
    {
        if (textBuffer == null || textView == null)
        {
            return null;
        }
        return new TestSuggestedActionsSource(this, textView, textBuffer);
    }
    ```

## <a name="implement-the-isuggestedactionsource"></a>ISuggestedActionSource を実装する
 推奨されるアクションソースは、提案されたアクションのセットを収集し、適切なコンテキストで追加します。 この場合、コンテキストは現在の単語であり、推奨されるアクションは**UpperCaseSuggestedAction**と**LowerCaseSuggestedAction**です。これについては、次のセクションで説明します。

1. を実装するクラス**TestSuggestedActionsSource**を追加 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource> します。

    ```csharp
    internal class TestSuggestedActionsSource : ISuggestedActionsSource
    ```

2. 推奨されるアクションソースプロバイダー、テキストバッファー、およびテキストビューに対して、プライベートな読み取り専用フィールドを追加します。

    ```csharp
    private readonly TestSuggestedActionsSourceProvider m_factory;
    private readonly ITextBuffer m_textBuffer;
    private readonly ITextView m_textView;
    ```

3. プライベートフィールドを設定するコンストラクターを追加します。

    ```csharp
    public TestSuggestedActionsSource(TestSuggestedActionsSourceProvider testSuggestedActionsSourceProvider, ITextView textView, ITextBuffer textBuffer)
    {
        m_factory = testSuggestedActionsSourceProvider;
        m_textBuffer = textBuffer;
        m_textView = textView;
    }
    ```

4. 現在カーソルの下にある単語を返すプライベートメソッドを追加します。 次のメソッドは、カーソルの現在の位置を調べ、単語の範囲をテキスト構造ナビゲーターに要求します。 カーソルが単語上にある場合は、 <xref:Microsoft.VisualStudio.Text.Operations.TextExtent> out パラメーターにが返されます。それ以外の場合、 `out` パラメーターはで、 `null` メソッドはを返し `false` ます。

    ```csharp
    private bool TryGetWordUnderCaret(out TextExtent wordExtent)
    {
        ITextCaret caret = m_textView.Caret;
        SnapshotPoint point;

        if (caret.Position.BufferPosition > 0)
        {
            point = caret.Position.BufferPosition - 1;
        }
        else
        {
            wordExtent = default(TextExtent);
            return false;
        }

        ITextStructureNavigator navigator = m_factory.NavigatorService.GetTextStructureNavigator(m_textBuffer);

        wordExtent = navigator.GetExtentOfWord(point);
        return true;
    }
    ```

5. <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource.HasSuggestedActionsAsync%2A> メソッドを実装します。 エディターはこのメソッドを呼び出して、電球を表示するかどうかを確認します。 この呼び出しは頻繁に行われます。たとえば、カーソルがある行から別の行に移動した場合、またはマウスがエラーの波線の上に置かれたときなどです。 このメソッドが動作している間は、他の UI 操作を実行できるようにするために非同期です。 ほとんどの場合、このメソッドは現在の行の解析と分析を実行する必要があるため、処理に時間がかかることがあります。

     この実装では、を非同期に取得 <xref:Microsoft.VisualStudio.Text.Operations.TextExtent> し、空白以外のテキストがあるかどうかなど、エクステントが有意であるかどうかを判断します。

    ```csharp
    public Task<bool> HasSuggestedActionsAsync(ISuggestedActionCategorySet requestedActionCategories, SnapshotSpan range, CancellationToken cancellationToken)
    {
        return Task.Factory.StartNew(() =>
        {
            TextExtent extent;
            if (TryGetWordUnderCaret(out extent))
            {
                // don't display the action if the extent has whitespace
                return extent.IsSignificant;
              }
            return false;
        });
    }
    ```

6. <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource.GetSuggestedActions%2A>異なるオブジェクトを含むオブジェクトの配列を返すメソッドを実装し <xref:Microsoft.VisualStudio.Language.Intellisense.SuggestedActionSet> <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction> ます。 このメソッドは、電球が拡張されたときに呼び出されます。

    > [!WARNING]
    > およびの実装に一貫性があることを確認する必要があります。つまり、 `HasSuggestedActionsAsync()` `GetSuggestedActions()` がを返した場合は、 `HasSuggestedActionsAsync()` `true` `GetSuggestedActions()` 表示する何らかのアクションが必要になります。 多くの場合、は直前に呼び出されますが、常にそうである `HasSuggestedActionsAsync()` とは `GetSuggestedActions()` 限りません。 たとえば、ユーザーが (**CTRL +** .) キーを押して電球操作を呼び出す `GetSuggestedActions()` と、が呼び出されます。

    ```csharp
    public IEnumerable<SuggestedActionSet> GetSuggestedActions(ISuggestedActionCategorySet requestedActionCategories, SnapshotSpan range, CancellationToken cancellationToken)
    {
        TextExtent extent;
        if (TryGetWordUnderCaret(out extent) && extent.IsSignificant)
        {
            ITrackingSpan trackingSpan = range.Snapshot.CreateTrackingSpan(extent.Span, SpanTrackingMode.EdgeInclusive);
            var upperAction = new UpperCaseSuggestedAction(trackingSpan);
            var lowerAction = new LowerCaseSuggestedAction(trackingSpan);
            return new SuggestedActionSet[] { new SuggestedActionSet(new ISuggestedAction[] { upperAction, lowerAction }) };
        }
        return Enumerable.Empty<SuggestedActionSet>();
    }
    ```

7. イベントを定義 `SuggestedActionsChanged` します。

    ```csharp
    public event EventHandler<EventArgs> SuggestedActionsChanged;
    ```

8. 実装を完了するには、メソッドおよびメソッドの実装を追加し `Dispose()` `TryGetTelemetryId()` ます。 テレメトリを使用しない場合は、を返し、 `false` GUID をに設定し `Empty` ます。

    ```csharp
    public void Dispose()
    {
    }

    public bool TryGetTelemetryId(out Guid telemetryId)
    {
        // This is a sample provider and doesn't participate in LightBulb telemetry
        telemetryId = Guid.Empty;
        return false;
    }
    ```

## <a name="implement-light-bulb-actions"></a>電球アクションを実装する

1. プロジェクトで*Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime.dll*への参照を追加し、[**ローカルにコピー** ] をに設定し `False` ます。

2. 2 つのクラスを、1 つは `UpperCaseSuggestedAction` という名前で、もう 1 つは `LowerCaseSuggestedAction`という名前で作成します。 どちらのクラスも、<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction> を実装します。

    ```csharp
    internal class UpperCaseSuggestedAction : ISuggestedAction
    internal class LowerCaseSuggestedAction : ISuggestedAction
    ```

     両クラスは似ていますが、一方は <xref:System.String.ToUpper%2A> を呼び出し、他方は <xref:System.String.ToLower%2A> を呼び出します。 次の手順では大文字操作クラスのみを対象にしていますが、両方のクラスを実装する必要があります。 小文字操作を実装するためのパターンとして、大文字操作を実装するための手順を使用します。

3. これらのクラスに対して次の using ディレクティブを追加します。

    ```csharp
    using Microsoft.VisualStudio.Imaging.Interop;
    using System.Windows;
    using System.Windows.Controls;
    using System.Windows.Documents;
    using System.Windows.Media;

    ```

4. 一連のプライベート フィールドを宣言します。

    ```csharp
    private ITrackingSpan m_span;
    private string m_upper;
    private string m_display;
    private ITextSnapshot m_snapshot;
    ```

5. フィールドを設定するコンストラクターを追加します。

    ```csharp
    public UpperCaseSuggestedAction(ITrackingSpan span)
    {
        m_span = span;
        m_snapshot = span.TextBuffer.CurrentSnapshot;
        m_upper = span.GetText(m_snapshot).ToUpper();
        m_display = string.Format("Convert '{0}' to upper case", span.GetText(m_snapshot));
    }
    ```

6. アクションの <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.GetPreviewAsync%2A> プレビューを表示するようにメソッドを実装します。

    ```csharp
    public Task<object> GetPreviewAsync(CancellationToken cancellationToken)
    {
        var textBlock = new TextBlock();
        textBlock.Padding = new Thickness(5);
        textBlock.Inlines.Add(new Run() { Text = m_upper });
        return Task.FromResult<object>(textBlock);
    }
    ```

7. 空の <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.GetActionSetsAsync%2A> 列挙型を返すようにメソッドを実装し <xref:Microsoft.VisualStudio.Language.Intellisense.SuggestedActionSet> ます。

    ```csharp
    public Task<IEnumerable<SuggestedActionSet>> GetActionSetsAsync(CancellationToken cancellationToken)
    {
        return Task.FromResult<IEnumerable<SuggestedActionSet>>(null);
    }
    ```

8. 次のようにプロパティを設定します。

    ```csharp
    public bool HasActionSets
    {
        get { return false; }
    }
    public string DisplayText
    {
        get { return m_display; }
    }
    public ImageMoniker IconMoniker
    {
       get { return default(ImageMoniker); }
    }
    public string IconAutomationText
    {
        get
        {
            return null;
        }
    }
    public string InputGestureText
    {
        get
        {
            return null;
        }
    }
    public bool HasPreview
    {
        get { return true; }
    }
    ```

9. 範囲内のテキストを等価な大文字に置き換えることで、メソッド <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.Invoke%2A> を実装します。

    ```csharp
    public void Invoke(CancellationToken cancellationToken)
    {
        m_span.TextBuffer.Replace(m_span.GetSpan(m_snapshot), m_upper);
    }
    ```

    > [!WARNING]
    > 電球のアクション**呼び出し**メソッドは、UI を表示する必要がありません。 アクションによって新しい UI が表示される場合 (たとえば、[プレビュー] または [選択] ダイアログ)、 **invoke メソッド内**から直接 ui を表示するのではなく、 **invoke**から戻ると ui を表示するようにスケジュールします。

10. 実装を完了するには、 `Dispose()` メソッドとメソッドを追加し `TryGetTelemetryId()` ます。

    ```csharp
    public void Dispose()
    {
    }

    public bool TryGetTelemetryId(out Guid telemetryId)
    {
        // This is a sample action and doesn't participate in LightBulb telemetry
        telemetryId = Guid.Empty;
        return false;
    }
    ```

11. `LowerCaseSuggestedAction`表示テキストを "Convert ' {0} ' を小文字に変換する" と "の呼び出し" に変更する場合は、必ず同じことを行ってください <xref:System.String.ToUpper%2A> <xref:System.String.ToLower%2A> 。

## <a name="build-and-test-the-code"></a>コードをビルドしてテストする
 このコードをテストするには、ライトの組み込みのテストソリューションをビルドし、実験用インスタンスで実行します。

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の2番目のインスタンスが開始されます。

3. テキスト ファイルを作成し、いくつかのテキストを入力します。 テキストの左側に電球が表示されます。

     ![電球のテスト](../extensibility/media/testlightbulb.png "TestLIghtBulb")

4. 電球をポイントします。 下矢印が表示できます。

5. 電球をクリックすると、選択したアクションのプレビューと共に、推奨される2つのアクションが表示されます。

     ![電球のテスト、展開](../extensibility/media/testlightbulbexpanded.gif "Testライトの展開")

6. 最初のアクションをクリックすると、現在の単語内のすべてのテキストが大文字に変換されます。 2番目のアクションをクリックすると、すべてのテキストが小文字に変換されます。
