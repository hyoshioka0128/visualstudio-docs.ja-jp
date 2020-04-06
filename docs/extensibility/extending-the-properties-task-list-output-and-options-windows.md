---
title: プロパティ、タスクリスト、出力、オプションウィンドウを拡張する
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- properties pane
- task list
- output window
- properties window
- tutorials
- tool windows
ms.assetid: 06990510-5424-44b8-9fd9-6481acec5c76
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: db14068c97ff6868f5fb73c9ddd790020e99e7c8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711630"
---
# <a name="extend-the-properties-task-list-output-and-options-windows"></a>プロパティ、タスク一覧、出力、およびオプションウィンドウを拡張する
Visual Studio では、任意のツール ウィンドウにアクセスできます。 このチュートリアルでは、ツール ウィンドウに関する情報を新しい **[オプション]** ページと **[プロパティ]** ページの新しい設定に統合する方法と、[**タスク一覧**] ウィンドウと **[出力**] ウィンドウに書き込む方法について説明します。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-an-extension-with-a-tool-window"></a>ツール ウィンドウを使用して拡張機能を作成する

1. VSIX テンプレートを使用して**TodoList**という名前のプロジェクトを作成し **、TodoWindow**という名前のカスタム ツール ウィンドウ項目テンプレートを追加します。

    > [!NOTE]
    > ツール ウィンドウを使用した拡張機能の作成の詳細については、「ツール[ウィンドウを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」を参照してください。

## <a name="set-up-the-tool-window"></a>ツール ウィンドウを設定する
 新しい ToDo 項目を入力するためのテキスト ボックス、新しい項目をリストに追加するボタン、リストに項目を表示する ListBox を追加します。

1. *TodoWindow.xaml*で、ボタン、テキスト ボックス、およびスタックパネルのコントロールをユーザー コントロールから削除します。

    > [!NOTE]
    > この場合 **、button1_Click**イベント ハンドラーは削除されません。

2. **ツールボックス**の **[すべての WPF コントロール**] セクションから、**キャンバス**コントロールをグリッドにドラッグします。

3. テキスト**ボックス**、**ボタン**、およびリスト**ボックス**をキャンバスにドラッグします。 要素を配置して、TextBox とボタンが同じレベルに配置され、下の図のように、リスト ボックスがウィンドウの下の残りの部分を塗りつぶします。

     ![完成したツール ウィンドウ](../extensibility/media/t5-toolwindow.png "T5-ツールウィンドウ")

4. XAML ペインで、ボタンを見つけ、そのコンテンツ プロパティを **[追加**] に設定します。 属性を追加して、ボタン イベント ハンドラーを`Click="button1_Click"`Button コントロールに再接続します。 キャンバスブロックは次のようになります。

    ```xml
    <Canvas HorizontalAlignment="Left" Width="306">
        <TextBox x:Name="textBox" HorizontalAlignment="Left" Height="23" Margin="10,10,0,0" TextWrapping="Wrap" Text="TextBox" VerticalAlignment="Top" Width="208"/>
            <Button x:Name="button" Content="Add" HorizontalAlignment="Left" Margin="236,13,0,0" VerticalAlignment="Top" Width="48" Click="button1_Click"/>
            <ListBox x:Name="listBox" HorizontalAlignment="Left" Height="222" Margin="10,56,0,0" VerticalAlignment="Top" Width="274"/>
    </Canvas>
    ```

### <a name="customize-the-constructor"></a>コンストラクタをカスタマイズする

1. *TodoWindowControl.xaml.cs*ファイルに、次の using ディレクティブを追加します。

    ```csharp
    using System;
    ```

2. TodoWindow へのパブリック参照を追加し、TodoWindow コントロールのコンストラクターに TodoWindow パラメーターを指定します。 コードは、次のようになります。

    ```csharp
    public TodoWindow parent;

    public TodoWindowControl(TodoWindow window)
    {
        InitializeComponent();
        parent = window;
    }
    ```

3. *TodoWindow.cs*で、TodoWindow コントロールのコンストラクターを変更して、TodoWindow パラメーターを含めます。 コードは、次のようになります。

    ```csharp
    public TodoWindow() : base(null)
    {
        this.Caption = "TodoWindow";
        this.BitmapResourceID = 301;
        this.BitmapIndex = 1;

         this.Content = new TodoWindowControl(this);
    }
    ```

## <a name="create-an-options-page"></a>[オプション] ページを作成する
 [**オプション]** ダイアログ ボックスでページを指定すると、ユーザーがツール ウィンドウの設定を変更できるようになります。 [オプション] ページを作成するには、オプションを説明するクラスと *、TodoListPackage.cs*または*TodoListPackage.vb*ファイルのエントリの両方が必要です。

1. `ToolsOptions.cs`という名前のクラスを追加します。 クラスを`ToolsOptions`から<xref:Microsoft.VisualStudio.Shell.DialogPage>継承させる。

   ```csharp
   class ToolsOptions : DialogPage
   {
   }
   ```

2. 次の using ディレクティブを追加します。

   ```csharp
   using Microsoft.VisualStudio.Shell;
   ```

3. このチュートリアルの [オプション] ページには、DaysAhead という名前のオプションが 1 つだけ用意されています。 **daysAhead**という名前のプライベート フィールドと**DaysAhead**という`ToolsOptions`名前のプロパティをクラスに追加します。

   ```csharp
   private double daysAhead;

   public double DaysAhead
   {
       get { return daysAhead; }
       set { daysAhead = value; }
   }
   ```

   次に、プロジェクトにこの [オプション] ページを認識させる必要があります。

### <a name="make-the-options-page-available-to-users"></a>[オプション] ページをユーザーが使用できるようにする

1. *TodoWindowPackage.cs*で`TodoWindowPackage`、クラス<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>に を追加します。

    ```csharp
    [ProvideOptionPage(typeof(ToolsOptions), "ToDo", "General", 101, 106, true)]
    ```

2. コンストラクタの最初のパラメータは、前に作成したクラス`ToolsOptions`の型です。 2 番目のパラメータである "ToDo" は、[**オプション]** ダイアログ ボックスのカテゴリの名前です。 3 番目のパラメータである "General" は、[オプション] ページが使用できる **[オプション]** ダイアログ ボックスのサブカテゴリの名前です。 次の 2 つのパラメーターは、文字列のリソース ID です。最初の名前はカテゴリの名前で、2 番目はサブカテゴリの名前です。 最後のパラメーターは、オートメーションを使用してこのページにアクセスできるかどうかを決定します。

     ユーザーが [オプション] ページを開くと、次の図のようになります。

     ![オプション ページ](../extensibility/media/t5optionspage.gif "T5 オプションページ")

     カテゴリ**ToDo**とサブカテゴリの**全般**に注意してください。

## <a name="make-data-available-to-the-properties-window"></a>[プロパティ] ウィンドウでデータを使用できるようにする
 ToDo リストの各項目に関する情報を格納`TodoItem`するクラスを作成することで、ToDo リスト情報を利用できます。

1. `TodoItem.cs`という名前のクラスを追加します。

     ツール ウィンドウがユーザーに表示される場合、リスト ボックスの項目は TodoItems で表されます。 ユーザーがリスト ボックスでこれらの項目のいずれかを選択すると、**プロパティ**ウィンドウに項目に関する情報が表示されます。

     **[プロパティ]** ウィンドウでデータを使用できるようにするには、データを 2 つの特別な属性を持`Description`つ`Category`パブリック プロパティに変換します。 `Description`**は、[プロパティ]** ウィンドウの下部に表示されるテキストです。 `Category`**[プロパティ**] ウィンドウが **[分類済**み] ビューに表示されるときに、プロパティが表示される場所を指定します。 次の図では、[**プロパティ]** ウィンドウが **[分類済み**] ビューで **、[ToDo フィールド]** カテゴリの **[名前]** プロパティが選択され、ウィンドウの下部に**Name**プロパティの説明が表示されます。

     ![[プロパティ] ウィンドウ](../extensibility/media/t5properties.png "T5 プロパティ")

2. *TodoItem.cs*ファイルに次の using ディレクティブを追加します。

    ```csharp
    using System.ComponentModel;
    using System.Windows.Forms;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

3. クラス宣言`public`にアクセス修飾子を追加します。

    ```csharp
    public class TodoItem
    {
    }
    ```

     2 つのプロパティ`Name`と`DueDate`を追加します。 私たちは、`CheckForErrors()`後で`UpdateList()`行います。

    ```csharp
    public class TodoItem
    {
        private TodoWindowControl parent;
        private string name;
        [Description("Name of the ToDo item")]
        [Category("ToDo Fields")]
        public string Name
        {
            get { return name; }
            set
            {
                name = value;
                parent.UpdateList(this);
            }
        }

        private DateTime dueDate;
        [Description("Due date of the ToDo item")]
        [Category("ToDo Fields")]
        public DateTime DueDate
        {
            get { return dueDate; }
            set
            {
                dueDate = value;
                parent.UpdateList(this);
                parent.CheckForErrors();
            }
        }
    }
    ```

4. ユーザー コントロールにプライベート参照を追加します。 ユーザー コントロールとこの ToDo 項目の名前を受け取るコンストラクターを追加します。 の値を見つける`daysAhead`には、オプション ページのプロパティを取得します。

    ```csharp
    private TodoWindowControl parent;

    public TodoItem(TodoWindowControl control, string itemName)
    {
        parent = control;
        name = itemName;
        dueDate = DateTime.Now;

        double daysAhead = 0;
        IVsPackage package = parent.parent.Package as IVsPackage;
        if (package != null)
        {
            object obj;
            package.GetAutomationObject("ToDo.General", out obj);

            ToolsOptions options = obj as ToolsOptions;
            if (options != null)
            {
                daysAhead = options.DaysAhead;
            }
        }

        dueDate = dueDate.AddDays(daysAhead);
    }
    ```

5. `TodoItem`クラスのインスタンスは ListBox に格納され、ListBox 関数が呼び出`ToString`されるため、関数を`ToString`オーバーロードする必要があります。 コンストラクターの後、クラスの終了前*TodoItem.cs*に次のコードを追加します。

    ```csharp
    public override string ToString()
    {
        return name + " Due: " + dueDate.ToShortDateString();
    }
    ```

6. *TodoWindowControl.xaml.cs*で、 メソッド`TodoWindowControl``CheckForError`のクラスにスタブ メソッドを`UpdateList`追加します。 ファイルの末尾の前に、後に配置します。

    ```csharp
    public void CheckForErrors()
    {
    }
    public void UpdateList(TodoItem item)
    {
    }
    ```

     この`CheckForError`メソッドは、親オブジェクト内の同じ名前のメソッドを呼び出し、そのメソッドはエラーが発生したかどうかをチェックし、正しく処理します。 メソッド`UpdateList`は親コントロールの ListBox を更新します。メソッドは、このクラスの`Name``DueDate`プロパティと プロパティが変更されたときに呼び出されます。 これらは後で実装されます。

## <a name="integrate-into-the-properties-window"></a>[プロパティ] ウィンドウに統合する
 次に **、ListBox**を管理するコードを作成します。

 ボタンのクリック ハンドラーを変更して TextBox を読み取り、TodoItem を作成し、リスト ボックスに追加する必要があります。

1. 既存`button1_Click`の関数を新しい TodoItem を作成し、リスト ボックスに追加するコードに置き換えます。 これは、`TrackSelection()`後で定義される を呼び出します。

    ```csharp
    private void button1_Click(object sender, RoutedEventArgs e)
    {
        if (textBox.Text.Length > 0)
        {
            var item = new TodoItem(this, textBox.Text);
            listBox.Items.Add(item);
            TrackSelection();
            CheckForErrors();
        }
    }
    ```

2. デザイン ビューで、リスト ボックス コントロールを選択します。 **[プロパティ**] ウィンドウで [**イベント ハンドラー** ] ボタンをクリックし **、SelectionChanged**イベントを見つけます。 テキスト ボックスに**listBox_SelectionChanged**を入力します。 これにより、SelectionChanged ハンドラのスタブが追加され、イベントに割り当てられます。

3. `TrackSelection()` メソッドを実装します。 サービスを取得<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>する必要があるため、TodoWindowControl によって<xref:Microsoft.VisualStudio.Shell.WindowPane.GetService%2A>アクセス可能にする必要があります。 <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> 次のメソッドを `TodoWindow` クラスに追加します。

    ```
    internal object GetVsService(Type service)
    {
        return GetService(service);
    }
    ```

4. 次の using ディレクティブを*TodoWindowControl.xaml.cs*に追加します。

    ```csharp
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio.Shell.Interop;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Shell;
    ```

5. 次のように、SelectionChanged ハンドラーを入力します。

    ```
    private void listBox_SelectionChanged(object sender, SelectionChangedEventArgs e)
    {
        TrackSelection();
    }
    ```

6. ここで、**プロパティ**ウィンドウとの統合を提供するTrackSelection関数を入力します。 この関数は、ユーザーが ListBox に項目を追加するか、ListBox の項目をクリックしたときに呼び出されます。 このプロパティは、リスト ボックスの内容を選択コンテナに追加し、選択コンテナを**プロパティ**ウィンドウの<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A>イベント ハンドラーに渡します。 TrackSelection サービスは、ユーザー インターフェイス (UI) で選択したオブジェクトを追跡し、そのプロパティを表示します。

    ```csharp
    private SelectionContainer mySelContainer;
    private System.Collections.ArrayList mySelItems;
    private IVsWindowFrame frame = null;

    private void TrackSelection()
    {
        if (frame == null)
        {
            var shell = parent.GetVsService(typeof(SVsUIShell)) as IVsUIShell;
            if (shell != null)
            {
                var guidPropertyBrowser = new
                Guid(ToolWindowGuids.PropertyBrowser);
                shell.FindToolWindow((uint)__VSFINDTOOLWIN.FTW_fForceCreate,
                ref guidPropertyBrowser, out frame);
            }
        }
        if (frame != null)
            {
                frame.Show();
            }
        if (mySelContainer == null)
        {
            mySelContainer = new SelectionContainer();
        }

        mySelItems = new System.Collections.ArrayList();

        var selected = listBox.SelectedItem as TodoItem;
        if (selected != null)
        {
            mySelItems.Add(selected);
        }

        mySelContainer.SelectedObjects = mySelItems;

        ITrackSelection track = parent.GetVsService(typeof(STrackSelection))
                                as ITrackSelection;
        if (track != null)
        {
            track.OnSelectChange(mySelContainer);
        }
    }
    ```

     **[プロパティ]** ウィンドウで使用できるクラスが作成できたので、[**プロパティ]** ウィンドウをツール ウィンドウに統合できます。 ユーザーがツール ウィンドウの ListBox の項目をクリックすると、それに応じて **[プロパティ]** ウィンドウが更新されます。 同様に、ユーザーが**プロパティ**ウィンドウで ToDo 項目を変更すると、関連付けられている項目を更新する必要があります。

7. ここで、UpdateList 関数コードの残りの部分を*TodoWindowControl.xaml.cs*に追加します。 変更した TodoItem を削除し、リスト ボックスから再度追加する必要があります。

    ```csharp
    public void UpdateList(TodoItem item)
    {
        var index = listBox.SelectedIndex;
        listBox.Items.RemoveAt(index);
        listBox.Items.Insert(index, item);
        listBox.SelectedItem = index;
    }
    ```

8. コードをテストします。 プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

9. **[ツール** > **オプション]** ページを開きます。 左側のウィンドウに [ToDo] カテゴリが表示されます。 カテゴリはアルファベット順でリストされているので、Tsの下を見てください。

10. **[Todo**オプション] ページで、プロパティ`DaysAhead`が**0**に設定されているはずです。 **2**に変更します。

11. [**表示/ その他のウィンドウ**] メニュー**で、TodoWindow**を開きます。 テキスト ボックスに **「終了日**」と入力し、[**追加**] をクリックします。

12. リスト ボックスには、今日より 2 日後に日付が表示されます。

## <a name="add-text-to-the-output-window-and-items-to-the-task-list"></a>出力ウィンドウにテキストを追加し、タスクリストに項目を追加する
 **タスク一覧**では、Task 型の新しいオブジェクトを作成し、そのメソッドを呼び出して**タスク一覧**に Task オブジェクトを`Add`追加します。 **出力**ウィンドウに書き込むには、その`GetPane`メソッドを呼び出してペイン オブジェクトを取得し`OutputString`、ペイン オブジェクトのメソッドを呼び出します。

1. TodoWindowControl.xaml.cs*で*、`button1_Click`メソッドで **、出力**ウィンドウの **[全般**] ウィンドウ (既定) を取得するコードを追加し、書き込みを行います。 メソッドは次のようになります。

    ```csharp
    private void button1_Click(object sender, EventArgs e)
    {
        if (textBox.Text.Length > 0)
        {
            var item = new TodoItem(this, textBox.Text);
            listBox.Items.Add(item);

            var outputWindow = parent.GetVsService(
                typeof(SVsOutputWindow)) as IVsOutputWindow;
            IVsOutputWindowPane pane;
            Guid guidGeneralPane = VSConstants.GUID_OutWindowGeneralPane;
            outputWindow.GetPane(ref guidGeneralPane, out pane);
            if (pane != null)
            {
                 pane.OutputString(string.Format(
                    "To Do item created: {0}\r\n",
                 item.ToString()));
        }
            TrackSelection();
            CheckForErrors();
        }
    }
    ```

2. タスク一覧に項目を追加するには、 を追加する必要があります、 TodoWindowControl クラスに入れ子になったクラスです。 入れ子になったクラスは<xref:Microsoft.VisualStudio.Shell.TaskProvider>から派生する必要があります。 クラスの最後に次のコードを追加`TodoWindowControl`します。

    ```csharp
    [Guid("72de1eAD-a00c-4f57-bff7-57edb162d0be")]
    public class TodoWindowTaskProvider : TaskProvider
    {
        public TodoWindowTaskProvider(IServiceProvider sp)
            : base(sp)
        {
        }
    }
    ```

3. 次に、プライベート参照`TodoTaskProvider`とメソッドを`CreateProvider()`クラスに追加`TodoWindowControl`します。 コードは、次のようになります。

    ```csharp
    private TodoWindowTaskProvider taskProvider;
    private void CreateProvider()
    {
        if (taskProvider == null)
        {
            taskProvider = new TodoWindowTaskProvider(parent);
            taskProvider.ProviderName = "To Do";
        }
    }
    ```

4. Add`ClearError()`は、タスク一覧をクリアし`ReportError()`、タスク一覧にエントリを追加するクラスに追加`TodoWindowControl`します。

    ```csharp
    private void ClearError()
    {
        CreateProvider();
        taskProvider.Tasks.Clear();
    }
    private void ReportError(string p)
    {
        CreateProvider();
        var errorTask = new Task();
        errorTask.CanDelete = false;
        errorTask.Category = TaskCategory.Comments;
        errorTask.Text = p;

        taskProvider.Tasks.Add(errorTask);

        taskProvider.Show();

        var taskList = parent.GetVsService(typeof(SVsTaskList))
            as IVsTaskList2;
        if (taskList == null)
        {
            return;
        }

        var guidProvider = typeof(TodoWindowTaskProvider).GUID;
         taskList.SetActiveProvider(ref guidProvider);
    }
    ```

5. 次のようにメソッド`CheckForErrors`を実装します。

    ```csharp
    public void CheckForErrors()
    {
        foreach (TodoItem item in listBox.Items)
        {
            if (item.DueDate < DateTime.Now)
            {
                ReportError("To Do Item is out of date: "
                    + item.ToString());
            }
        }
    }
    ```

## <a name="try-it-out"></a>試してみる

1. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

2. **Todo ウィンドウ**(**他のウィンドウ** > を**表示** > する**TodoWindow**) を開きます。

3. テキスト ボックスに何かを入力し、[**追加**] をクリックします。

     今日の 2 日後の期日がリスト ボックスに追加されます。 エラーは生成されず、**タスク一覧**( タスク 一**覧**の**表示** > ) にはエントリを含めずに済みます。

4. ツール オプションの **[To** **Do]** > **ページの設定** > を**2**から**0**に変更します。

5. **TodoWindow**に他の項目を入力し、もう一度 **[追加**] をクリックします。 これにより、エラーが発生し、**タスク一覧**のエントリも表示されます。

     項目を追加すると、初期日付は現在と 2 日に設定されます。

6. [**表示**] メニューの [**出力**] をクリックして、[**出力**] ウィンドウを開きます。

     アイテムを追加するたびに、メッセージが **[タスク一覧**] ウィンドウに表示されます。

7. リスト ボックス内の項目のいずれかをクリックします。

     **[プロパティ]** ウィンドウには、項目の 2 つのプロパティが表示されます。

8. プロパティの 1 つを変更し **、Enter**キーを押します。

     項目がリスト ボックスで更新されます。
