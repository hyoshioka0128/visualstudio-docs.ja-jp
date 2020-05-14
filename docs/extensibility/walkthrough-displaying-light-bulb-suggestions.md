---
title: 'チュートリアル: 電球候補を表示する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 99e5566d-450e-4660-9bca-454e1c056a02
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 09773e2be81ce51971709db590a07ca9960104fa
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697471"
---
# <a name="walkthrough-display-light-bulb-suggestions"></a>チュートリアル: 電球候補を表示する
電球は Visual Studio エディターのアイコンであり、一連のアクションを表示するために展開します。

 Visual C# および Visual Basic のエディターでは、.NET コンパイラ プラットフォーム ("Roslyn") を使用して、電球を自動的に表示するアクションを含む独自のコード アナライザーを作成およびパッケージ化することもできます。 詳細については次を参照してください:

- [方法: C# 診断とコード修正プログラムを作成する](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix)

- [方法: Visual Basic 診断とコード修正プログラムを記述する](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-Visual-Basic-Analyzer-and-Code-Fix)

  C++ などの他の言語も、その関数のスタブ実装を作成するための提案など、いくつかのクイック アクション用の電球を提供します。

  電球の外観は次のとおりです。 Visual Basic プロジェクトまたは Visual C# プロジェクトでは、無効な場合は、変数名の下に赤い波線が表示されます。 無効な識別子にマウスを置くと、カーソルの近くに電球が表示されます。

  ![電球](../extensibility/media/lightbulb.png "電球")

  電球の横の下向き矢印をクリックすると、選択したアクションのプレビューと共に、一連の推奨アクションが表示されます。 この場合、アクションを実行した場合にコードに加えられた変更が表示されます。

  ![電球のプレビュー](../extensibility/media/lightbulbpreview.png "電球プレビュー")

  電球を使用して、独自の推奨アクションを提供できます。 たとえば、中かっこを新しい行に移動したり、前の行の末尾に移動したりするアクションを指定できます。 次のチュートリアルでは、現在の単語に表示される電球を作成する方法と、2 つの推奨**アクションを示****します。**

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-managed-extensibility-framework-mef-project"></a>マネージ機能拡張フレームワーク (MEF) プロジェクトを作成する

1. C# VSIX プロジェクトを作成します。 ([**新しいプロジェクト**] ダイアログで、[**ビジュアル C# / 拡張性**] を選択し、次に**VSIX プロジェクト**を選択します)。ソリューションに名前`LightBulbTest`を付ける:

2. **エディター分類子**項目テンプレートをプロジェクトに追加します。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

3. 既存のクラス ファイルを削除します。

4. プロジェクトに次の参照を追加し、[**ローカルコピー** ]`False`を に設定します。

     *Microsoft.VisualStudio.Language.Intellisense*

5. 新しいクラス ファイルを追加し、その名前を**LightBulbTest**にします。

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

## <a name="implement-the-light-bulb-source-provider"></a>電球ソースプロバイダの実装

1. *LightBulbTest.cs*クラス ファイルで、LightBulbTest クラスを削除します。 を実装するクラス**を追加します**<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider>。 **テスト推奨アクション**の名前と「テキスト」の名前<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>を付けてエクスポートします。

    ```csharp
    [Export(typeof(ISuggestedActionsSourceProvider))]
    [Name("Test Suggested Actions")]
    [ContentType("text")]
    internal class TestSuggestedActionsSourceProvider : ISuggestedActionsSourceProvider
    ```

2. ソース プロバイダー クラス内で<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>をインポートし、プロパティとして追加します。

    ```csharp
    [Import(typeof(ITextStructureNavigatorSelectorService))]
    internal ITextStructureNavigatorSelectorService NavigatorService { get; set; }
    ```

3. オブジェクトを<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider.CreateSuggestedActionsSource%2A>返すメソッドを<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource>実装します。 ソースについては、次のセクションで説明します。

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

## <a name="implement-the-isuggestedactionsource"></a>を実装します。
 推奨されるアクションソースは、提案されたアクションのセットを収集し、適切なコンテキストに追加する責任があります。 この場合、コンテキストは現在の単語であり、推奨されるアクションは、次のセクションで説明する**大文字小文字提案アクション**と**小文字提案アクション**です。

1. を実装**するクラスを追加します**。 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource>

    ```csharp
    internal class TestSuggestedActionsSource : ISuggestedActionsSource
    ```

2. 提案されたアクション ソース プロバイダー、テキスト バッファー、およびテキスト ビューのプライベートな読み取り専用フィールドを追加します。

    ```csharp
    private readonly TestSuggestedActionsSourceProvider m_factory;
    private readonly ITextBuffer m_textBuffer;
    private readonly ITextView m_textView;
    ```

3. プライベート フィールドを設定するコンストラクターを追加します。

    ```csharp
    public TestSuggestedActionsSource(TestSuggestedActionsSourceProvider testSuggestedActionsSourceProvider, ITextView textView, ITextBuffer textBuffer)
    {
        m_factory = testSuggestedActionsSourceProvider;
        m_textBuffer = textBuffer;
        m_textView = textView;
    }
    ```

4. 現在カーソルの下にある単語を返すプライベート メソッドを追加します。 次のメソッドは、カーソルの現在の位置を調べ、テキスト構造ナビゲーターに単語の範囲を尋ねます。 カーソルがワード上にある場合<xref:Microsoft.VisualStudio.Text.Operations.TextExtent>は、out パラメーターに 戻されます。それ以外の`out`場合は`null`、パラメーターが返`false`され、メソッドは を返します。

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

5. <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource.HasSuggestedActionsAsync%2A> メソッドを実装します。 エディターは、電球を表示するかどうかを調べるために、このメソッドを呼び出します。 この呼び出しは、カーソルがある行から別の行に移動したときや、マウスがエラー波線の上に置かれたときなどに頻繁に行われます。 このメソッドが動作している間に他の UI 操作を実行できるようにするために非同期です。 ほとんどの場合、このメソッドは現在の行の解析と分析を実行する必要があるため、処理に時間がかかる場合があります。

     この実装では、スペース以外の<xref:Microsoft.VisualStudio.Text.Operations.TextExtent>テキストが含まれているかどうか、そのエクステントが重要かどうかを非同期的に取得し、そのエクステントが重要かどうかを判断します。

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

6. メソッドを<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource.GetSuggestedActions%2A>実装し、異なる<xref:Microsoft.VisualStudio.Language.Intellisense.SuggestedActionSet><xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction>オブジェクトを含むオブジェクトの配列を返します。 電球を展開すると、このメソッドが呼び出されます。

    > [!WARNING]
    > の実装との実装`HasSuggestedActionsAsync()``GetSuggestedActions()`が一貫していることを確認する必要があります。つまり、戻り`HasSuggestedActionsAsync()`値`true`が返`GetSuggestedActions()`された場合は、表示するアクションがいくつかある必要があります。 多くの場合、`HasSuggestedActionsAsync()`直前に`GetSuggestedActions()`呼び出されますが、必ずしもそうであるとは限りません。 たとえば、ユーザーが電球アクションを呼び出した場合 **(Ctrl +** .)を`GetSuggestedActions()`押すだけで呼び出されます。

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

7. イベントを`SuggestedActionsChanged`定義します。

    ```csharp
    public event EventHandler<EventArgs> SuggestedActionsChanged;
    ```

8. 実装を完了するには、`Dispose()`メソッドと`TryGetTelemetryId()`メソッドの実装を追加します。 テレメトリを実行したくないので、GUID を戻`false`してに`Empty`設定するだけです。

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

## <a name="implement-light-bulb-actions"></a>電球アクションの実装

1. プロジェクトで、への参照を追加します *。* **Copy Local** `False`

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

6. アクションプレビュー<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.GetPreviewAsync%2A>を表示するようにメソッドを実装します。

    ```csharp
    public Task<object> GetPreviewAsync(CancellationToken cancellationToken)
    {
        var textBlock = new TextBlock();
        textBlock.Padding = new Thickness(5);
        textBlock.Inlines.Add(new Run() { Text = m_upper });
        return Task.FromResult<object>(textBlock);
    }
    ```

7. 空<xref:Microsoft.VisualStudio.Language.Intellisense.SuggestedActionSet>の<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.GetActionSetsAsync%2A>列挙体を返すメソッドを実装します。

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
    > 電球アクション**Invoke**メソッドは UI を表示しません。 アクションで新しい UI (プレビューや選択ダイアログなど) が表示される場合は **、Invoke**メソッド内から直接 UI を表示するのではなく、 **Invoke**から戻った後に UI を表示するようにスケジュールします。

10. 実装を完了するには、 メソッド`Dispose()`と`TryGetTelemetryId()`メソッドを追加します。

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

11. 表示テキストを "大文字と小文字に変換`LowerCaseSuggestedAction`{0}" に変更する場合と 、 を呼び出す場合<xref:System.String.ToUpper%2A>も<xref:System.String.ToLower%2A>、同じ操作を行うことを忘れないでください。

## <a name="build-and-test-the-code"></a>コードのビルドとテスト
 このコードをテストするには、LightBulbTest ソリューションをビルドし、実験インスタンスで実行します。

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 番目のインスタンスが起動します。

3. テキスト ファイルを作成し、いくつかのテキストを入力します。 テキストの左側に電球が表示されます。

     ![電球のテスト](../extensibility/media/testlightbulb.png "テストリトバルブ")

4. 電球をポイントします。 下向き矢印が表示されます。

5. 電球をクリックすると、選択したアクションのプレビューと共に、2 つの推奨アクションが表示されます。

     ![電球のテスト、展開](../extensibility/media/testlightbulbexpanded.gif "テストリトブルブル展開")

6. 最初のアクションをクリックすると、現在の単語のすべてのテキストが大文字に変換されます。 2 番目のアクションをクリックすると、すべてのテキストが小文字に変換されます。
