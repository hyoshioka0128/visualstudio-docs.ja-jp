---
title: プロパティ、タスク一覧、出力、オプションウィンドウを拡張する
ms.date: 11/04/2016
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: c968544c6bf52a901052fc7aedbbee66dcc10e62
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90038479"
---
# <a name="extend-the-properties-task-list-output-and-options-windows"></a>[プロパティ]、[タスク一覧]、[出力]、[オプション] の各ウィンドウを拡張する
Visual Studio では、任意のツールウィンドウにアクセスできます。 このチュートリアルでは、ツールウィンドウに関する情報を新しいオプションページに統合する方法と、[**プロパティ**] ページに新しい設定を統合する方法について説明します。また、[**タスク一覧**と**出力** **]** ウィンドウに書き込む方法についても説明します。

## <a name="prerequisites"></a>前提条件
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-an-extension-with-a-tool-window"></a>ツールウィンドウで拡張機能を作成する

1. VSIX テンプレートを使用して **TodoList** という名前のプロジェクトを作成し、 **TodoWindow**という名前のカスタムツールウィンドウ項目テンプレートを追加します。

    > [!NOTE]
    > ツールウィンドウを使用した拡張機能の作成の詳細については、「 [ツールウィンドウを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」を参照してください。

## <a name="set-up-the-tool-window"></a>ツールウィンドウを設定する
 新しい ToDo 項目を入力するためのテキストボックス、リストに新しい項目を追加するボタン、およびリストの項目を表示するリストボックスを追加します。

1. *TodoWindow*で、UserControl から Button、TextBox、および StackPanel コントロールを削除します。

    > [!NOTE]
    > これにより、後の手順で再利用する **button1_Click** イベントハンドラーは削除されません。

2. **ツールボックス**の [**すべての WPF コントロール**] セクションで、**キャンバス**コントロールをグリッドにドラッグします。

3. **テキストボックス**、**ボタン**、および**リストボックス**をキャンバスにドラッグします。 次の図のように、テキストボックスとボタンが同じレベルになるように要素を配置します。リストボックスは、ウィンドウの残りの部分を次のように入力します。

     ![完成したツール ウィンドウ](../extensibility/media/t5-toolwindow.png "T5-ToolWindow")

4. XAML ペインで、ボタンを見つけ、そのコンテンツプロパティを [ **追加**] に設定します。 属性を追加して、ボタンのイベントハンドラーをボタンコントロールに再接続し `Click="button1_Click"` ます。 Canvas ブロックは次のようになります。

    ```xml
    <Canvas HorizontalAlignment="Left" Width="306">
        <TextBox x:Name="textBox" HorizontalAlignment="Left" Height="23" Margin="10,10,0,0" TextWrapping="Wrap" Text="TextBox" VerticalAlignment="Top" Width="208"/>
            <Button x:Name="button" Content="Add" HorizontalAlignment="Left" Margin="236,13,0,0" VerticalAlignment="Top" Width="48" Click="button1_Click"/>
            <ListBox x:Name="listBox" HorizontalAlignment="Left" Height="222" Margin="10,56,0,0" VerticalAlignment="Top" Width="274"/>
    </Canvas>
    ```

### <a name="customize-the-constructor"></a>コンストラクターをカスタマイズする

1. *TodoWindowControl.xaml.cs*ファイルで、次の using ディレクティブを追加します。

    ```csharp
    using System;
    ```

2. TodoWindow へのパブリック参照を追加し、TodoWindowControl コンストラクターが TodoWindow パラメーターを受け取るようにします。 コードは、次のようになります。

    ```csharp
    public TodoWindow parent;

    public TodoWindowControl(TodoWindow window)
    {
        InitializeComponent();
        parent = window;
    }
    ```

3. *TodoWindow.cs*で、TodoWindowControl コンストラクターを変更して TodoWindow パラメーターを含めます。 コードは、次のようになります。

    ```csharp
    public TodoWindow() : base(null)
    {
        this.Caption = "TodoWindow";
        this.BitmapResourceID = 301;
        this.BitmapIndex = 1;

         this.Content = new TodoWindowControl(this);
    }
    ```

## <a name="create-an-options-page"></a>オプションページを作成する
 [ **オプション** ] ダイアログボックスのページを使用して、ユーザーがツールウィンドウの設定を変更できるようにすることができます。 オプションページを作成するには、オプションを記述するクラスと *TodoListPackage.cs* ファイルまたは *TodoListPackage* ファイル内のエントリの両方が必要です。

1. `ToolsOptions.cs`という名前のクラスを追加します。 クラスがから継承されるように `ToolsOptions` <xref:Microsoft.VisualStudio.Shell.DialogPage> します。

   ```csharp
   class ToolsOptions : DialogPage
   {
   }
   ```

2. 次の using ディレクティブを追加します。

   ```csharp
   using Microsoft.VisualStudio.Shell;
   ```

3. このチュートリアルの [オプション] ページには、DaysAhead という名前のオプションが1つだけ用意されています。 **Daysahead**という名前のプライベートフィールドと、 **daysahead**という名前のプロパティをクラスに追加し `ToolsOptions` ます。

   ```csharp
   private double daysAhead;

   public double DaysAhead
   {
       get { return daysAhead; }
       set { daysAhead = value; }
   }
   ```

   ここで、このオプションページをプロジェクトに認識させる必要があります。

### <a name="make-the-options-page-available-to-users"></a>[オプション] ページをユーザーが使用できるようにする

1. *TodoWindowPackage.cs*で、クラスにを追加し <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> `TodoWindowPackage` ます。

    ```csharp
    [ProvideOptionPage(typeof(ToolsOptions), "ToDo", "General", 101, 106, true)]
    ```

2. 指定されたクラスコンストラクターの最初のパラメーターは、前に作成したクラスの型です `ToolsOptions` 。 2番目のパラメーター "ToDo" は、[ **オプション** ] ダイアログボックスのカテゴリの名前です。 3番目のパラメーター "General" は、オプションページを使用できるようにする [ **オプション** ] ダイアログボックスのサブカテゴリの名前です。 次の2つのパラメーターは、文字列のリソース Id です。1つ目はカテゴリの名前で、2つ目はサブカテゴリの名前です。 最後のパラメーターは、オートメーションを使用してこのページにアクセスできるかどうかを決定します。

     ユーザーが [オプション] ページを開くと、次の図のようになります。

     ![[オプション] ページ)](../extensibility/media/t5optionspage.gif "T5OptionsPage")

     Category **ToDo** およびサブカテゴリ **全般**に注意してください。

## <a name="make-data-available-to-the-properties-window"></a>プロパティウィンドウでデータを使用できるようにする
 Todo リストの情報を取得するには、という名前のクラスを作成します。このクラスには、 `TodoItem` todo リスト内の個々の項目に関する情報が格納されます。

1. `TodoItem.cs`という名前のクラスを追加します。

     ユーザーがツールウィンドウを使用できる場合、リストボックス内の項目は TodoItems によって表されます。 ユーザーがリストボックスでこれらの項目のいずれかを選択すると、[ **プロパティ** ] ウィンドウに項目に関する情報が表示されます。

     [ **プロパティ** ] ウィンドウでデータを使用できるようにするには、とという2つの特殊な属性を持つパブリックプロパティにデータを変換し `Description` `Category` ます。 `Description` は、[ **プロパティ** ] ウィンドウの下部に表示されるテキストです。 `Category` [ **プロパティ** ] ウィンドウが **カテゴリ別** ビューに表示されている場合に、プロパティを表示する場所を決定します。 次の図では、[**プロパティ**] ウィンドウがカテゴリ**別**ビューにあり、[ **ToDo フィールド**] カテゴリの [**名前**] プロパティが選択されており、[**名前**] プロパティの説明がウィンドウの下部に表示されています。

     ![[プロパティ] ウィンドウ](../extensibility/media/t5properties.png "T5Properties")

2. *TodoItem.cs*ファイルに次の using ディレクティブを追加します。

    ```csharp
    using System.ComponentModel;
    using System.Windows.Forms;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

3. `public`アクセス修飾子をクラス宣言に追加します。

    ```csharp
    public class TodoItem
    {
    }
    ```

     とという2つのプロパティを追加し `Name` `DueDate` ます。 以降を実行し `UpdateList()` `CheckForErrors()` ます。

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

4. ユーザーコントロールにプライベート参照を追加します。 ユーザーコントロールとこの ToDo 項目の名前を受け取るコンストラクターを追加します。 の値を検索するために、 `daysAhead` [オプション] ページのプロパティを取得します。

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

5. クラスのインスタンス `TodoItem` はリストボックスに格納され、listbox は関数を呼び出すため、 `ToString` 関数をオーバーロードする必要があり `ToString` ます。 コンストラクターの後、クラスの末尾の前に、 *TodoItem.cs*に次のコードを追加します。

    ```csharp
    public override string ToString()
    {
        return name + " Due: " + dueDate.ToShortDateString();
    }
    ```

6. *TodoWindowControl.xaml.cs*で、 `TodoWindowControl` メソッドとメソッドのクラスにスタブメソッドを追加し `CheckForError` `UpdateList` ます。 これらの文字列は、Processの文字の後、ファイルの末尾の前に配置します。

    ```csharp
    public void CheckForErrors()
    {
    }
    public void UpdateList(TodoItem item)
    {
    }
    ```

     メソッドは、 `CheckForError` 親オブジェクトで同じ名前を持つメソッドを呼び出します。このメソッドは、エラーが発生したかどうかを確認し、適切に処理します。 メソッドは、 `UpdateList` 親コントロールのリストボックスを更新します。メソッドは、 `Name` `DueDate` このクラスのプロパティとプロパティが変更されたときに呼び出されます。 これらは後で実装されます。

## <a name="integrate-into-the-properties-window"></a>プロパティウィンドウに統合する
 次に、[ **プロパティ** ] ウィンドウに関連付けられる ListBox を管理するコードを記述します。

 ボタンクリックハンドラーを変更してテキストボックスを読み取り、TodoItem を作成して、リストボックスに追加する必要があります。

1. 既存の `button1_Click` 関数を新しい TodoItem を作成するコードに置き換え、それをリストボックスに追加します。 このメソッドは `TrackSelection()` を呼び出します。これは後で定義されます。

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

2. デザインビュー ListBox コントロールを選択します。 [ **プロパティ** ] ウィンドウで、[ **イベントハンドラー** ] ボタンをクリックし、 **selectionchanged** イベントを見つけます。 テキストボックスに **listBox_SelectionChanged**を入力します。 これにより、SelectionChanged ハンドラーのスタブが追加され、イベントに割り当てられます。

3. `TrackSelection()` メソッドを実装します。 サービスを取得する必要があるため、 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> TodoWindowControl からアクセスできるようにする必要があり <xref:Microsoft.VisualStudio.Shell.WindowPane.GetService%2A> ます。 次のメソッドを `TodoWindow` クラスに追加します。

    ```
    internal object GetVsService(Type service)
    {
        return GetService(service);
    }
    ```

4. 次の using ディレクティブを *TodoWindowControl.xaml.cs*に追加します。

    ```csharp
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio.Shell.Interop;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Shell;
    ```

5. SelectionChanged ハンドラーに次のように入力します。

    ```
    private void listBox_SelectionChanged(object sender, SelectionChangedEventArgs e)
    {
        TrackSelection();
    }
    ```

6. 次に、TrackSelection 関数に入力します。これにより、[ **プロパティ** ] ウィンドウとの統合が提供されます。 この関数は、ユーザーが項目を ListBox に追加したとき、またはリストボックス内の項目をクリックしたときに呼び出されます。 ListBox の内容を SelectionContainer に追加し、SelectionContainer を [ **プロパティ** ] ウィンドウの <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> イベントハンドラーに渡します。 TrackSelection サービスは、ユーザーインターフェイス (UI) で選択されたオブジェクトを追跡し、それらのプロパティを表示します。

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

     これで、[ **プロパティ** ] ウィンドウで使用できるクラスが作成されたので、[ **プロパティ** ] ウィンドウをツールウィンドウと統合できます。 ユーザーがツールウィンドウのリストボックス内の項目をクリックすると、それに応じて [ **プロパティ** ] ウィンドウが更新されます。 同様に、ユーザーが [ **プロパティ** ] ウィンドウで ToDo 項目を変更した場合は、関連付けられている項目を更新する必要があります。

7. 次に、 *TodoWindowControl.xaml.cs*で updatelist 関数の残りのコードを追加します。 リストボックスから変更された TodoItem を削除し、再追加する必要があります。

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

9. [**ツール**  >  **オプション**] ページを開きます。 左側のウィンドウに ToDo カテゴリが表示されます。 カテゴリはアルファベット順に表示されるので、Ts の下を確認してください。

10. [ **Todo** オプション] ページで、 `DaysAhead` プロパティが **0**に設定されていることを確認します。 **2**に変更します。

11. [ **表示]/[その他のウィンドウ** ] メニューで、 **TodoWindow**を開きます。 テキストボックスに「 **EndDate** 」と入力し、[ **追加**] をクリックします。

12. リストボックスには、今日より2日後の日付が表示されます。

## <a name="add-text-to-the-output-window-and-items-to-the-task-list"></a>[出力] ウィンドウにテキストを追加し、項目をタスク一覧に追加します。
 **タスク一覧**には、task 型の新しいオブジェクトを作成し、そのメソッドを呼び出してそのタスクオブジェクトを**タスク一覧**に追加し `Add` ます。 **出力**ウィンドウに書き込むには、そのメソッドを呼び出し `GetPane` てペインオブジェクトを取得し、次に `OutputString` pane オブジェクトのメソッドを呼び出します。

1. *TodoWindowControl.xaml.cs*のメソッドで、 `button1_Click` [**出力**] ウィンドウの **[全般**] ウィンドウ (既定) を取得するコードを追加し、それに書き込みます。 メソッドは次のようになります。

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

2. タスク一覧に項目を追加するには、TodoWindowControl クラスに入れ子になったクラスを追加するためのが必要です。 入れ子になったクラスは、から派生する必要があり <xref:Microsoft.VisualStudio.Shell.TaskProvider> ます。 クラスの末尾に次のコードを追加し `TodoWindowControl` ます。

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

3. 次に、にプライベート参照を追加 `TodoTaskProvider` し、 `CreateProvider()` メソッドをクラスに追加し `TodoWindowControl` ます。 コードは、次のようになります。

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

4. を追加します。これにより、 `ClearError()` タスク一覧がクリアされ、 `ReportError()` タスク一覧にエントリが追加され `TodoWindowControl` ます。

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

5. ここで `CheckForErrors` 、次のようにメソッドを実装します。

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

## <a name="try-it-out"></a>試してみましょう

1. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

2. **TodoWindow** (**View**  >  **他の Windows**  >  **TodoWindow**を表示) を開きます。

3. テキストボックスに何かを入力し、[ **追加**] をクリックします。

     今日から2日後に期日がリストボックスに追加されます。 エラーは生成されず、**タスク一覧**(**ビュー**  >  **タスク一覧**) にはエントリがありません。

4. 次に、[**ツール**  >  **オプション]**  >  **ToDo**ページの設定を**2**から**0**に変更します。

5. **TodoWindow**に他の項目を入力し、もう一度 [**追加**] をクリックします。 これにより、エラーが発生し、 **タスク一覧**でもエントリがトリガーされます。

     項目を追加すると、最初の日付が [現在] に2日を加えた状態に設定されます。

6. [ **表示** ] メニューの [ **出力** ] をクリックして、[ **出力** ] ウィンドウを開きます。

     項目を追加するたびに、[ **タスク一覧** ] ウィンドウにメッセージが表示されることに注意してください。

7. リストボックス内の項目のいずれかをクリックします。

     [ **プロパティ** ] ウィンドウには、項目の2つのプロパティが表示されます。

8. プロパティのいずれかを変更し、 **enter キー**を押します。

     リストボックスの項目が更新されます。
