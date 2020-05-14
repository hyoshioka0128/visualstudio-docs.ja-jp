---
title: ツール ウィンドウに検索を追加する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- tool windows, adding search
ms.assetid: f78c4892-8060-49c4-8ecd-4360f1b4d133
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f9112a3368ba604c4291f9018e763022e953c4fc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740136"
---
# <a name="add-search-to-a-tool-window"></a>ツール ウィンドウに検索を追加する
拡張機能でツール ウィンドウを作成または更新する場合、Visual Studio の他の場所に表示されるのと同じ検索機能を追加できます。 この機能には、次の機能が含まれます。

- 常にツールバーのカスタム領域に配置される検索ボックス。

- 検索ボックス自体にオーバーレイされている進行状況インジケーター。

- 各文字を入力するとすぐに結果を表示する機能 (クイック検索) または**Enter**キーを選択した後にのみ (オンデマンド検索)。

- 最近検索した用語を示すリスト。

- 検索対象の特定のフィールドまたは側面で検索をフィルター処理する機能。

このチュートリアルでは、次のタスクを実行する方法について説明します。

1. VSPackage プロジェクトを作成します。

2. 読み取り専用のテキスト ボックスを持つユーザー コントロールを含むツール ウィンドウを作成します。

3. ツール ウィンドウに検索ボックスを追加します。

4. 検索の実装を追加します。

5. プログレスバーのクイック検索と表示を有効にします。

6. **[大文字と小文字を区別する]** オプションを追加します。

7. **[偶数行のみ検索**] フィルターを追加します。

## <a name="to-create-a-vsix-project"></a>VSIX プロジェクトを作成するには

1. **TestSearch**という名前の`TestToolWindowSearch`ツール ウィンドウで名前を付けた VSIX プロジェクトを作成します。 この操作を行う際のヘルプが必要な場合は、[ツール ウィンドウを使用した拡張機能の作成を](../extensibility/creating-an-extension-with-a-tool-window.md)参照してください。

## <a name="to-create-a-tool-window"></a>ツール ウィンドウを作成するには

1. プロジェクトで`TestToolWindowSearch`、*テストサーチコントロール.xaml*ファイルを開きます。

2. 既存`<StackPanel>`のブロックを次のブロック<xref:System.Windows.Controls.TextBox><xref:System.Windows.Controls.UserControl>に置き換えます。

    ```xaml
    <StackPanel Orientation="Vertical">
        <TextBox Name="resultsTextBox" Height="800.0"
            Width="800.0"
            IsReadOnly="True">
        </TextBox>
    </StackPanel>
    ```

3. *TestSearchControl.xaml.cs*ファイルに、次の using ディレクティブを追加します。

    ```csharp
    using System.Text;
    ```

4. メソッドを`button1_Click()`削除します。

     **クラスに**次のコードを追加します。

     このコードは<xref:System.Windows.Controls.TextBox>**、"SearchResultsTextBox"** という名前のパブリック プロパティと **、"SearchContent"** という名前のパブリック文字列プロパティを追加します。 コンストラクタでは、テキスト ボックスに設定され、検索コンテンツは改行で区切られた文字列のセットに初期化されます。 テキスト ボックスの内容も文字列のセットに初期化されます。

     [!code-csharp[ToolWindowSearch#1](../extensibility/codesnippet/CSharp/adding-search-to-a-tool-window_1.cs)]
     [!code-vb[ToolWindowSearch#1](../extensibility/codesnippet/VisualBasic/adding-search-to-a-tool-window_1.vb)]

5. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。

6. メニュー バーで、[**他の Windows** > **テスト検索**の**表示** > ] をクリックします。

     ツール ウィンドウが表示されますが、検索コントロールはまだ表示されません。

## <a name="to-add-a-search-box-to-the-tool-window"></a>ツール ウィンドウに検索ボックスを追加するには

1. *TestSearch.cs*ファイルで、次のコードをクラスに`TestSearch`追加します。 このコードは、get<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.SearchEnabled%2A>アクセサーが返`true`されるようにプロパティをオーバーライドします。

     検索を有効にするには、プロパティをオーバーライド<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.SearchEnabled%2A>する必要があります。 この<xref:Microsoft.VisualStudio.Shell.ToolWindowPane>クラスは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch>検索を有効にしない既定の実装を実装し、提供します。

    ```csharp
    public override bool SearchEnabled
    {
        get { return true; }
    }
    ```

2. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

3. Visual Studio の実験用インスタンスで、**テストサーチ**を開きます。

     ツール ウィンドウの上部に、検索透かしと虫眼鏡の**Search**アイコンが表示されます。 ただし、検索プロセスが実装されていないため、検索はまだ機能しません。

## <a name="to-add-the-search-implementation"></a>検索の実装を追加するには
 で検索を有効にすると、<xref:Microsoft.VisualStudio.Shell.ToolWindowPane>前の手順のように、ツール ウィンドウは検索ホストを作成します。 このホストは、常にバックグラウンド スレッドで発生する検索プロセスを設定および管理します。 このクラス<xref:Microsoft.VisualStudio.Shell.ToolWindowPane>は検索ホストの作成と検索の設定を管理するため、検索タスクを作成して検索方法を提供するだけで済みます。 検索プロセスはバックグラウンド スレッドで発生し、ツール ウィンドウ コントロールへの呼び出しは UI スレッドで発生します。 したがって[、ThreadHelper.Invoke*](https://msdn.microsoft.com/data/ee197798(v=vs.85))メソッドを使用して、コントロールを処理するときに行う呼び出しを管理する必要があります。

1. *TestSearch.cs*ファイルに、次`using`のディレクティブを追加します。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Runtime.InteropServices;
    using System.Text;
    using System.Windows.Controls;
    using Microsoft.Internal.VisualStudio.PlatformUI;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.PlatformUI;
    using Microsoft.VisualStudio.Shell;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

2. クラスに`TestSearch`、次のアクションを実行する次のコードを追加します。

    - 検索タスクを<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.CreateSearch%2A>作成するメソッドをオーバーライドします。

    - テキスト ボックス<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.ClearSearch%2A>の状態を復元するメソッドをオーバーライドします。 このメソッドは、ユーザーが検索タスクをキャンセルしたとき、およびユーザーがオプションまたはフィルターを設定または設定解除したときに呼び出されます。 両方<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.CreateSearch%2A>とも<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.ClearSearch%2A>、UI スレッドで呼び出されます。 したがって[、ThreadHelper.Invoke*](https://msdn.microsoft.com/data/ee197798(v=vs.85))メソッドを使用してテキスト ボックスにアクセスする必要はありません。

    - の既定の実装を提供する`TestSearchTask`を継承<xref:Microsoft.VisualStudio.Shell.VsSearchTask>する名前のクラスを作成<xref:Microsoft.VisualStudio.Shell.Interop.IVsSearchTask>します。

         では`TestSearchTask`、コンストラクターはツール ウィンドウを参照するプライベート フィールドを設定します。 検索メソッドを提供するには、 メソッドと<xref:Microsoft.VisualStudio.Shell.VsSearchTask.OnStartSearch%2A><xref:Microsoft.VisualStudio.Shell.VsSearchTask.OnStopSearch%2A>メソッドをオーバーライドします。 メソッド<xref:Microsoft.VisualStudio.Shell.VsSearchTask.OnStartSearch%2A>は、検索プロセスを実装する場所です。 このプロセスには、検索の実行、テキスト ボックスでの検索結果の表示、および検索が完了したことを報告するこのメソッドの基本クラス実装の呼び出しが含まれます。

    ```csharp
    public override IVsSearchTask CreateSearch(uint dwCookie, IVsSearchQuery pSearchQuery, IVsSearchCallback pSearchCallback)
    {
        if (pSearchQuery == null || pSearchCallback == null)
            return null;
         return new TestSearchTask(dwCookie, pSearchQuery, pSearchCallback, this);
    }

    public override void ClearSearch()
    {
        TestSearchControl control = (TestSearchControl)this.Content;
        control.SearchResultsTextBox.Text = control.SearchContent;
    }

    internal class TestSearchTask : VsSearchTask
    {
        private TestSearch m_toolWindow;

        public TestSearchTask(uint dwCookie, IVsSearchQuery pSearchQuery, IVsSearchCallback pSearchCallback, TestSearch toolwindow)
            : base(dwCookie, pSearchQuery, pSearchCallback)
        {
            m_toolWindow = toolwindow;
        }

        protected override void OnStartSearch()
        {
            // Use the original content of the text box as the target of the search.
            var separator = new string[] { Environment.NewLine };
            TestSearchControl control = (TestSearchControl)m_toolWindow.Content;
            string[] contentArr = control.SearchContent.Split(separator, StringSplitOptions.None);

            // Get the search option.
            bool matchCase = false;
            // matchCase = m_toolWindow.MatchCaseOption.Value;

                // Set variables that are used in the finally block.
                StringBuilder sb = new StringBuilder("");
                uint resultCount = 0;
                this.ErrorCode = VSConstants.S_OK;

                try
                {
                    string searchString = this.SearchQuery.SearchString;

                    // Determine the results.
                    uint progress = 0;
                    foreach (string line in contentArr)
                    {
                        if (matchCase == true)
                        {
                            if (line.Contains(searchString))
                            {
                                sb.AppendLine(line);
                                resultCount++;
                            }
                        }
                        else
                            {
                                if (line.ToLower().Contains(searchString.ToLower()))
                                {
                                    sb.AppendLine(line);
                                    resultCount++;
                                }
                            }

                            // SearchCallback.ReportProgress(this, progress++, (uint)contentArr.GetLength(0));

                            // Uncomment the following line to demonstrate the progress bar.
                            // System.Threading.Thread.Sleep(100);
                        }
                    }
                    catch (Exception e)
                    {
                        this.ErrorCode = VSConstants.E_FAIL;
                    }
                    finally
                    {
                        ThreadHelper.Generic.Invoke(() =>
                        { ((TextBox)((TestSearchControl)m_toolWindow.Content).SearchResultsTextBox).Text = sb.ToString(); });

                        this.SearchResults = resultCount;
                    }

            // Call the implementation of this method in the base class.
            // This sets the task status to complete and reports task completion.
            base.OnStartSearch();
        }

        protected override void OnStopSearch()
        {
            this.SearchResults = 0;
        }
    }
    ```

3. 次の手順を実行して、検索の実装をテストします。

    1. プロジェクトをリビルドし、デバッグを開始します。

    2. Visual Studio の実験用インスタンスで、ツール ウィンドウを再度開き、検索ウィンドウに検索テキストを入力して **、[ENTER]** をクリックします。

         正しい結果が表示されます。

## <a name="to-customize-the-search-behavior"></a>検索動作をカスタマイズするには
 検索設定を変更することで、検索コントロールの表示方法や検索方法をさまざまな変更を加えることができます。たとえば、ウォーターマーク (検索ボックスに表示される既定のテキスト)、検索コントロールの最小幅と最大幅、進行状況バーを表示するかどうかを変更できます。 また、検索結果が表示され始めるポイント (オンデマンド検索または即時検索) や、最近検索した語句のリストを表示するかどうかも変更できます。 クラスの設定の完全なリストを<xref:Microsoft.VisualStudio.PlatformUI.SearchSettingsDataSource>見つけることができます。

1. * TestSearch.cs* ファイルで、次のコードをクラス`TestSearch`に追加します。 このコードは、オンデマンド検索ではなく、即座に検索を有効にします ( ユーザーが**Enter**キーを押す必要はありません ) 。 このコードは、既定`ProvideSearchSettings`の設定を`TestSearch`変更するために必要なクラスのメソッドをオーバーライドします。

    ```csharp
    public override void ProvideSearchSettings(IVsUIDataSource pSearchSettings)
    {
        Utilities.SetValue(pSearchSettings,
            SearchSettingsDataSource.SearchStartTypeProperty.Name,
            (uint)VSSEARCHSTARTTYPE.SST_INSTANT);}
    ```

2. ソリューションを再構築し、デバッガーを再起動して、新しい設定をテストします。

     検索ボックスに文字を入力するたびに検索結果が表示されます。

3. メソッドで`ProvideSearchSettings`、進行状況バーの表示を有効にする次の行を追加します。

    ```csharp
    public override void ProvideSearchSettings(IVsUIDataSource pSearchSettings)
    {
        Utilities.SetValue(pSearchSettings,
            SearchSettingsDataSource.SearchStartTypeProperty.Name,
             (uint)VSSEARCHSTARTTYPE.SST_INSTANT);
        Utilities.SetValue(pSearchSettings,
            SearchSettingsDataSource.SearchProgressTypeProperty.Name,
             (uint)VSSEARCHPROGRESSTYPE.SPT_DETERMINATE);
    }
    ```

     進行状況バーが表示されるようにするには、進行状況を報告する必要があります。 進行状況を報告するには、クラスのメソッドで次のコード`OnStartSearch`のコメントを`TestSearchTask`外します。

    ```csharp
    SearchCallback.ReportProgress(this, progress++, (uint)contentArr.GetLength(0));
    ```

4. プログレス バーが表示されるほど処理を遅くするには、クラスのメソッド`OnStartSearch`で次の`TestSearchTask`行のコメントを外します。

    ```csharp
    System.Threading.Thread.Sleep(100);
    ```

5. ソリューションを再構築し、デバッグを開始して、新しい設定をテストします。

     プログレス バーは、検索を実行するたびに検索ウィンドウに表示されます (検索テキスト ボックスの下に青い線として)。

## <a name="to-enable-users-to-refine-their-searches"></a>ユーザーが検索を絞り込む
 [大文字と小文字を区別] や [**単語全体**を**検索**] などのオプションを使用して、ユーザーが検索を絞り込むことを許可できます。 オプションは、チェック ボックスとして表示されるブール値、またはボタンとして表示されるコマンドを指定できます。 このチュートリアルでは、ブール型オプションを作成します。

1. *TestSearch.cs*ファイルで、次のコードをクラスに`TestSearch`追加します。 このコードはメソッドを`SearchOptionsEnum`オーバーライドし、検索の実装が特定のオプションがオンかオフかを検出できるようにします。 のコードは`SearchOptionsEnum`、列挙子に大文字と小文字を<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumWindowSearchOptions>一致させるオプションを追加します。 ケースに合わせるオプションも`MatchCaseOption`プロパティとして利用可能になります。

    ```csharp
    private IVsEnumWindowSearchOptions m_optionsEnum;
    public override IVsEnumWindowSearchOptions SearchOptionsEnum
    {
        get
        {
            if (m_optionsEnum == null)
            {
                List<IVsWindowSearchOption> list = new List<IVsWindowSearchOption>();

                list.Add(this.MatchCaseOption);

                m_optionsEnum = new WindowSearchOptionEnumerator(list) as IVsEnumWindowSearchOptions;
            }
            return m_optionsEnum;
        }
    }

    private WindowSearchBooleanOption m_matchCaseOption;
    public WindowSearchBooleanOption MatchCaseOption
    {
        get
        {
            if (m_matchCaseOption == null)
            {
                m_matchCaseOption = new WindowSearchBooleanOption("Match case", "Match case", false);
            }
            return m_matchCaseOption;
        }
    }
    ```

2. クラスでは`TestSearchTask`、メソッドの次の行をコメント解除`OnStartSearch`します。

    ```csharp
    matchCase = m_toolWindow.MatchCaseOption.Value;
    ```

3. オプションをテストします。

    1. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

    2. ツール ウィンドウで、テキスト ボックスの右側にある下矢印を選択します。

         [**大文字と小文字を区別する**] チェック ボックスが表示されます。

    3. [**大文字と小文字を区別する**] チェック ボックスをオンにし、いくつかの検索を実行します。

## <a name="to-add-a-search-filter"></a>検索フィルターを追加するには
 検索対象のセットを絞り込むことができる検索フィルターを追加できます。 たとえば、ファイル エクスプローラーで、最近変更された日付とファイル名拡張子でファイルをフィルター処理できます。 このチュートリアルでは、偶数行のみのフィルターを追加します。 ユーザーがそのフィルターを選択すると、検索ホストは、指定した文字列を検索クエリに追加します。 検索メソッド内でこれらの文字列を識別し、それに応じて検索対象をフィルター処理できます。

1. *TestSearch.cs*ファイルで、次のコードをクラスに`TestSearch`追加します。 このコードは、`SearchFiltersEnum`偶数行のみが<xref:Microsoft.VisualStudio.PlatformUI.WindowSearchSimpleFilter>表示されるように検索結果をフィルター処理するように指定する を追加することによって実装します。

    ```csharp
    public override IVsEnumWindowSearchFilters SearchFiltersEnum
    {
        get
        {
            List<IVsWindowSearchFilter> list = new List<IVsWindowSearchFilter>();
            list.Add(new WindowSearchSimpleFilter("Search even lines only", "Search even lines only", "lines", "even"));
            return new WindowSearchFilterEnumerator(list) as IVsEnumWindowSearchFilters;
        }
    }

    ```

     これで、検索コントロールに検索フィルタ`Search even lines only`が表示されます。 ユーザーがフィルターを選択すると、検索ボックスに`lines:"even"`文字列が表示されます。 他の検索条件は、フィルターと同時に表示できます。 検索文字列は、フィルターの前、フィルターの後、またはその両方の前に表示されます。

2. *TestSearch.cs*ファイルで、クラス内の次の`TestSearchTask`メソッドをクラスに追加します。 `TestSearch` これらのメソッドは、`OnStartSearch`次の手順で変更するメソッドをサポートします。

    ```csharp
    private string RemoveFromString(string origString, string stringToRemove)
    {
        int index = origString.IndexOf(stringToRemove);
        if (index == -1)
            return origString;
        else 
             return (origString.Substring(0, index) + origString.Substring(index + stringToRemove.Length)).Trim();
    }

    private string[] GetEvenItems(string[] contentArr)
    {
        int length = contentArr.Length / 2;
        string[] evenContentArr = new string[length];

        int indexB = 0;
        for (int index = 1; index < contentArr.Length; index += 2)
        {
            evenContentArr[indexB] = contentArr[index];
            indexB++;
        }

        return evenContentArr;
    }
    ```

3. クラスでは`TestSearchTask`、次のコード`OnStartSearch`でメソッドを更新します。 この変更により、フィルタをサポートするコードが更新されます。

    ```csharp
    protected override void OnStartSearch()
    {
        // Use the original content of the text box as the target of the search. 
        var separator = new string[] { Environment.NewLine };
        string[] contentArr = ((TestSearchControl)m_toolWindow.Content).SearchContent.Split(separator, StringSplitOptions.None);

        // Get the search option. 
        bool matchCase = false;
        matchCase = m_toolWindow.MatchCaseOption.Value;

        // Set variables that are used in the finally block.
        StringBuilder sb = new StringBuilder("");
        uint resultCount = 0;
        this.ErrorCode = VSConstants.S_OK;

        try
        {
            string searchString = this.SearchQuery.SearchString;

            // If the search string contains the filter string, filter the content array. 
            string filterString = "lines:\"even\"";

            if (this.SearchQuery.SearchString.Contains(filterString))
            {
                // Retain only the even items in the array.
                contentArr = GetEvenItems(contentArr);

                // Remove 'lines:"even"' from the search string.
                searchString = RemoveFromString(searchString, filterString);
            }

            // Determine the results. 
            uint progress = 0;
            foreach (string line in contentArr)
            {
                if (matchCase == true)
                {
                    if (line.Contains(searchString))
                    {
                        sb.AppendLine(line);
                        resultCount++;
                    }
                }
                else
                {
                    if (line.ToLower().Contains(searchString.ToLower()))
                    {
                        sb.AppendLine(line);
                        resultCount++;
                    }
                }

                SearchCallback.ReportProgress(this, progress++, (uint)contentArr.GetLength(0));

                // Uncomment the following line to demonstrate the progress bar. 
                // System.Threading.Thread.Sleep(100);
            }
        }
        catch (Exception e)
        {
            this.ErrorCode = VSConstants.E_FAIL;
        }
        finally
        {
            ThreadHelper.Generic.Invoke(() =>
            { ((TextBox)((TestSearchControl)m_toolWindow.Content).SearchResultsTextBox).Text = sb.ToString(); });

            this.SearchResults = resultCount;
        }

        // Call the implementation of this method in the base class. 
        // This sets the task status to complete and reports task completion. 
        base.OnStartSearch();
    }
    ```

4. コードをテストします。

5. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスで、ツール ウィンドウを開き、検索コントロールの下矢印を選択します。

     [**大文字と小文字を区別する**] チェック ボックスと **[偶数行のみ検索**] フィルターが表示されます。

6. フィルタを選択します。

     検索ボックスには **"even"という行**が含まれ、次の結果が表示されます。

     2良い

     4 良い

     6 さようなら

7. 検索`lines:"even"`ボックスから削除し、[大文字と**小文字を区別する**] チェック`g`ボックスをオンにして、検索ボックスに入力します。

     次の結果が表示されます。

     1行く

     2良い

     5さようなら

8. 検索ボックスの右側にある [X] を選択します。

     検索がクリアされ、元の内容が表示されます。 ただし、[**大文字と小文字を区別する**] チェック ボックスはオンになっています。
