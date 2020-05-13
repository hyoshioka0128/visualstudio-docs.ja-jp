---
title: 'チュートリアル: Azure モバイル サービスに接続された WPF デスクトップ アプリケーションの作成 | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 8d42620f-553b-4b04-a38b-f6b306d73a50
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 624fffb9c86a7ad874f27797dfd5251c8585870f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72664021"
---
# <a name="walkthrough-create-a-wpf-desktop-application-connected-to-an-azure-mobile-service"></a>チュートリアル: Azure モバイル サービスに接続された WPF デスクトップ アプリケーションの作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows Presentation Foundation (WPF) を使用すれば、Azure モバイル サービスを利用してデータの格納および提供を行う、最新式のデスクトップ アプリケーションをすばやく作成することができます。

## <a name="Requirements"></a> 必要条件
 このチュートリアルを完了させるための要件は次のとおりです。

- Visual Studio 2015 - WPF 開発をサポートする任意のバージョン。

- アクティブな Microsoft Azure アカウント。

  - 無料試用版アカウントのサインアップを、 [ここ](https://azure.microsoft.com/pricing/free-trial/)で行うことができます。

  - [MSDN サブスクライバー特典](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)をアクティブにできます。 MSDN サブスクリプションでは、有料の Azure サービスに対して使用できるクレジットが毎月ユーザーに提供されます。

## <a name="create-a-project-and-add-references"></a>プロジェクトを作成してソース ファイルを追加する
 最初の手順では、WPF プロジェクトを作成し、Azure Mobile Services に接続できる NuGet パッケージを追加します。

#### <a name="to-create-the-project"></a>プロジェクトを作成するには

1. メニュー バーで **[ファイル]** 、 **[新規作成]** 、 **[プロジェクト]** の順にクリックします。

2. **[新しいプロジェクト]** ダイアログで、 **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[Windows]** ノードを選択して **[Windows]** ノードを展開してから **[従来の (クラシック) デスクトップ]** ノードを選択します。

3. テンプレートの一覧で、 **[WPF アプリケーション]** テンプレートを選択します。

4. **[名前]** ボックスに「 `WPFQuickStart`」と入力して、 **[OK]** を選択します。

     プロジェクトが作成され、プロジェクト ファイルが **ソリューション エクスプローラー**に追加され、 **MainWindow.xaml** という名前の既定のアプリケーション ウィンドウのデザイナーが表示されます。

#### <a name="to-add-a-reference-to-the-windows-azure-mobile-services-sdk"></a>Microsoft Azure Mobile Services SDK に参照を追加するには

1. **ソリューション エクスプローラー**で **[参照]** ノードのショートカット メニューを開き、 **[NuGet パッケージの管理]** を選択します。

2. **NuGet パッケージ マネージャー**で、 **[検索]** フィールドを選択して「`mobileservices`」と入力します。

3. 左ウィンドウで、 **WindowsAzure.MobileServices**を選択し、右ウィンドウで **[インストール]** ボタンをクリックします。

    > [!NOTE]
    > **[プレビュー]** ダイアログが表示されたら、提示された変更を確認した後、 **[OK]** ボタンをクリックします。

4. **[ライセンスへの同意]** ダイアログで、各ライセンス条項を確認してから、 **[同意]** ボタンをクリックしてそれらに同意します。

     必要な参照が **ソリューション エクスプローラー**に追加されます。

    > [!NOTE]
    > ライセンス条項に同意しない場合は、 **[同意しない]** ボタンをクリックします。 同意しない場合、このチュートリアルの残りの部分を完了させることはできません。

## <a name="create-the-user-interface"></a>ユーザー インターフェイスを作成する
 次の手順では、アプリケーションのユーザー インターフェイスを作成します。 まず、標準の横並びの 2 つのウィンドウのレイアウトを表示する再利用可能なユーザー コントロールを作成します。 ユーザー コントロールをアプリケーションのメイン ウィンドウに追加し、データを入力および表示するためのコントロールを追加してから、モバイル サービスのバックエンドとの相互作用を定義するコードを記述します。

#### <a name="to-add-a-user-control"></a>ユーザー コントロールを追加するには

1. **ソリューション エクスプローラー**で、 **[WPFQuickStart]** ノードのショートカット メニューを開き、 **[追加]** 、 **[新しいフォルダー]** の順に選択します。

2. フォルダーに「 `Common`で行うことができます。

3. **[Common]** フォルダーのショートカット メニューを開き、 **[追加]** 、 **[ユーザー コントロール]** の順に選択します。

4. **[新しい項目の追加]** ダイアログで、[名前] フィールドを選択して「 `QuickStartTask`」と入力して、 **[追加]** を選択します。

     ユーザー コントロールがプロジェクトに追加され、 **[QuickStartTask.xaml]** ファイルがデザイナーで開きます。

5. デザイナーの下ウィンドウで、 `<Grid>` タグと `</Grid>` タグを選択してから、それらを次の XAML コードに置き換えます。

    ```xaml
    <Grid VerticalAlignment="Top">
            <StackPanel Orientation="Horizontal">
                <Border BorderThickness="0,0,1,0" BorderBrush="DarkGray" Margin="0,10" MinWidth="70">
                    <TextBlock Text="{Binding Number}" FontSize="45" Foreground="DarkGray" Margin="20,0"/>
                </Border>
                <StackPanel>
                    <TextBlock Text="{Binding Title}" Margin="10,10,0,0" FontSize="16" FontWeight="Bold" />
                    <TextBlock Text="{Binding Description}" Margin="10,0,0,0" TextWrapping="Wrap" MaxWidth="500" />
                </StackPanel>
            </StackPanel>
        </Grid>
    ```

     この XAML コードによって、番号、タイトル、および説明の各フィールドのプレース ホルダーの付いた再利用可能なレイアウトが作成されます。 これらのプレースホルダーは、実行時に次の図に示すテキストに置き換えることができます。

     ![QuickStartTask ユーザーコントロール](../designers/media/wpfquickstart1.PNG "WPFQuickStart1")

6. **ソリューション エクスプローラー**で、 **[QuickStartTask.xaml]** ノードを展開して **[QuickStartTask.xaml.cs]** ファイルまたは **[QuickStartTask.xaml.vb]** ファイルを開きます。

7. コード エディターで、 `namespace WPFQuickStart.Common` (C#) 名前空間または `Public Class QuickStartTask` (VB) メソッドを次のコードに書き換えます。

    ```csharp
    namespace WPFQuickStart.Common
    {
        /// <summary>
        /// Interaction logic for QuickStartTask.xaml
        /// </summary>
        public partial class QuickStartTask : UserControl
        {
            public QuickStartTask()
            {
                this.InitializeComponent();
                this.DataContext = this;
            }

            public int Number
            {
                get { return (int)GetValue(NumberProperty); }
                set { SetValue(NumberProperty, value); }
            }

            // Using a DependencyProperty as the backing store for Number.  This enables animation, styling, binding, etc...
            public static readonly DependencyProperty NumberProperty =
                DependencyProperty.Register("Number", typeof(int), typeof(QuickStartTask), new PropertyMetadata(0));

            public string Title
            {
                get { return (string)GetValue(TitleProperty); }
                set { SetValue(TitleProperty, value); }
            }

            // Using a DependencyProperty as the backing store for Title.  This enables animation, styling, binding, etc...
            public static readonly DependencyProperty TitleProperty =
                DependencyProperty.Register("Title", typeof(string), typeof(QuickStartTask), new PropertyMetadata(default(string)));

            public string Description
            {
                get { return (string)GetValue(DescriptionProperty); }
                set { SetValue(DescriptionProperty, value); }
            }

            // Using a DependencyProperty as the backing store for Description.  This enables animation, styling, binding, etc...
            public static readonly DependencyProperty DescriptionProperty =
                DependencyProperty.Register("Description", typeof(string), typeof(QuickStartTask), new PropertyMetadata(default(string)));
        }
    }
    ```

    ```vb
    Partial Public Class QuickStartTask
            Inherits UserControl

            Public Sub New()
                Me.InitializeComponent()
                Me.DataContext = Me
            End Sub

            Public Property Number() As Integer
                Get
                    Return CInt(Fix(GetValue(NumberProperty)))
                End Get
                Set(ByVal value As Integer)
                    SetValue(NumberProperty, value)
                End Set
            End Property

            ' Using a DependencyProperty as the backing store for Number.  This enables animation, styling, binding, etc...
            Public Shared ReadOnly NumberProperty As DependencyProperty = DependencyProperty.Register("Number", GetType(Integer), GetType(QuickStartTask), New PropertyMetadata(0))

            Public Property Title() As String
                Get
                    Return CStr(GetValue(TitleProperty))
                End Get
                Set(ByVal value As String)
                    SetValue(TitleProperty, value)
                End Set
            End Property

            ' Using a DependencyProperty as the backing store for Title.  This enables animation, styling, binding, etc...
            Public Shared ReadOnly TitleProperty As DependencyProperty = DependencyProperty.Register("Title", GetType(String), GetType(QuickStartTask), New PropertyMetadata(Nothing))

            Public Property Description() As String
                Get
                    Return CStr(GetValue(DescriptionProperty))
                End Get
                Set(ByVal value As String)
                    SetValue(DescriptionProperty, value)
                End Set
            End Property

            ' Using a DependencyProperty as the backing store for Description.  This enables animation, styling, binding, etc...
            Public Shared ReadOnly DescriptionProperty As DependencyProperty = DependencyProperty.Register("Description", GetType(String), GetType(QuickStartTask), New PropertyMetadata(Nothing))
        End Class
    ```

     このコードでは依存関係プロパティを使用して、実行時に、番号、タイトル、および説明の各フィールドの値を設定します。

8. メニュー バーで、 **[ビルド]** 、 **[WPFQuickStart のビルド]** の順に選択してユーザー コントロールをビルドします。

#### <a name="to-create-and-modify-the-main-window"></a>メイン ウィンドウを作成および変更するには

1. **ソリューション エクスプローラー**で、 **[MainWindow.xaml]** ファイルを開きます。

2. **重要**。 この手順は、C# の場合のみです。 Visual Basic を使用する場合は、次の手順に進んでください。 デザイナーの下ウィンドウで、 `xmlns:local=”clr-namespace:WPFQuickStart”` という行を見つけてから、それを次の XAML コードに置き換えます。

    ```xaml
    xmlns:local=”clr-namespace:WPFQuickStart.Common”
    ```

3. **[プロパティ]** ウィンドウで、 **Common** カテゴリ ノードを展開し **[Title]** プロパティを選択してから、「 `WPF Todo List` 」と入力して **Enter** キーを押します。

     [XAML] ウィンドウの **[タイトル]** 要素も新しい値に変わったことに注目してください。 XAML のプロパティは、[XAML] ウィンドウまたは **[プロパティ]** ウィンドウのいずれかで変更でき、それらの変更は同期されます。

4. [XAML] ウィンドウで **[Height]** 要素の値を `768`に設定し、 **[Width]** プロパティの値を `1280`で行うことができます。

     これらの要素は、 **[プロパティ]** ウィンドウの **[レイアウト]** カテゴリにある **[Height]** プロパティと **[Width]** プロパティに対応します。

5. `<Grid>` タグと `</Grid>` タグを選択してから、それらを次の XAML コードに置き換えます。

    ```xaml
    <Grid>

            <Grid Margin="50,50,10,10">
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="*" />
                    <ColumnDefinition Width="*" />
                </Grid.ColumnDefinitions>
                <Grid.RowDefinitions>
                    <RowDefinition Height="Auto" />
                    <RowDefinition Height="*" />
                </Grid.RowDefinitions>

                <Grid Grid.Row="0" Grid.ColumnSpan="2" Margin="0,0,0,20">
                    <StackPanel>
                        <TextBlock Foreground="#0094ff" FontFamily="Segoe UI Light" Margin="0,0,0,6">MICROSOFT AZURE MOBILE SERVICES</TextBlock>
                        <TextBlock Foreground="Gray" FontFamily="Segoe UI Light" FontSize="45" ><Run Text="My Todo List"/></TextBlock>
                    </StackPanel>
                </Grid>

                <Grid Grid.Row="1">
                    <StackPanel>

                        <local:QuickStartTask Number="1" Title="Insert a TodoItem" Description="Enter some text below and click Save to insert a new todo item into the list." />

                        <StackPanel Orientation="Horizontal" Margin="72,0,0,0">
                            <TextBox x:Name="TodoInput" Margin="5" MinWidth="300"/>
                            <Button x:Name="ButtonSave" Click="ButtonSave_Click" Content="Save"/>
                        </StackPanel>

                    </StackPanel>
                </Grid>

                <Grid Grid.Row="1" Grid.Column="1">
                    <Grid.RowDefinitions>
                        <RowDefinition Height="Auto" />
                        <RowDefinition />
                    </Grid.RowDefinitions>
                    <StackPanel>
                        <local:QuickStartTask Number="2" Title="Query and Update Data" Description="Click the Refresh button to load the unfinished TodoItems from the Azure Mobile Service. Select the checkbox to mark a ToDo item as complete and update the list." />
                        <Button Margin="72,0,0,0" Name="ButtonRefresh" Click="ButtonRefresh_Click">Refresh</Button>
                    </StackPanel>

                    <ListView Name="ListItems" Margin="62,10,0,0" Grid.Row="1">
                        <ListView.ItemTemplate>
                            <DataTemplate>
                                <StackPanel Orientation="Horizontal">
                                    <CheckBox Name="CheckBoxComplete" IsChecked="{Binding Complete, Mode=TwoWay}" Checked="CheckBoxComplete_Checked" Content="{Binding Text}" Margin="10,5" VerticalAlignment="Center"/>
                                </StackPanel>
                            </DataTemplate>
                        </ListView.ItemTemplate>
                    </ListView>

                </Grid>

            </Grid>
        </Grid>
    ```

     これらの変更が [デザイン] ウィンドウに反映されることに注意してください。 さらに、 **[ツールボックス]** ウィンドウでコントロールを追加し、 **[プロパティ]** ウィンドウでプロパティを設定すれば、ユーザー インターフェイスも定義できます。 デザイナーで実行できることは XAML コードでも実行でき、XAML コードで実行できることはデザイナーでも実行できます。

     この時点で、デザインは次の図のようになっているはずです。

     ![デザイナーの Mainwindow.xaml](../designers/media/wpfquickstart2.PNG "WPFQuickStart2")

    > [!NOTE]
    > **[エラー一覧]** を開いている場合、次のいくつかの手順の実行中にエラーが表示される可能性があります。 心配には及びません。これらのエラーは、残りの手順を完了すれば表示されなくなります。

6. **ソリューション エクスプローラー**で、 **[MainWindow.xaml]** ノードを展開し、 **[MainWindow.xaml.cs]** ファイルまたは **[MainWindow.xaml.vb]** ファイルを開きます。

7. コード エディターで、ファイルの先頭に次の `using` ディレクティブまたは `Imports` ディレクティブを追加します。

    ```csharp
    using Microsoft.WindowsAzure.MobileServices;
    using Newtonsoft.Json;
    ```

    ```vb
    Imports Microsoft.WindowsAzure.MobileServices
    Imports Newtonsoft.Json
    ```

8. **[WPFQuickStart]** 名前空間 (C#) または **[Class MainWindow]** クラス (VB) 内のすべてのコードを次のコードに置き換えます。

    ```csharp
    namespace WPFQuickStart
    {
        /// <summary>
        /// Interaction logic for MainWindow.xaml
        /// </summary>
        public class TodoItem
        {
            public string Id { get; set; }

            [JsonProperty(PropertyName = "text")]
            public string Text { get; set; }

            [JsonProperty(PropertyName = "complete")]
            public bool Complete { get; set; }
        }

        public partial class MainWindow : Window
        {
            private MobileServiceCollection<TodoItem, TodoItem> items;
            private IMobileServiceTable<TodoItem> todoTable = App.MobileService.GetTable<TodoItem>();

            public MainWindow()
            {
                InitializeComponent();
            }

            private async void InsertTodoItem(TodoItem todoItem)
            {
                // This code inserts a new TodoItem into the database. When the operation completes
                // and Mobile Services has assigned an Id, the item is added to the CollectionView
                await todoTable.InsertAsync(todoItem);
                items.Add(todoItem);
            }

            private async void RefreshTodoItems()
            {
                try
                {
                    // This code refreshes the entries in the list view by querying the TodoItem table.
                    // The query excludes completed TodoItems
                    items = await todoTable
                        .Where(todoItem => todoItem.Complete == false)
                        .ToCollectionAsync();
                    ListItems.ItemsSource = items;
                }
                catch (MobileServiceInvalidOperationException e)
                {
                    MessageBox.Show(e.Message, "Error loading items");
                }
            }

            private async void UpdateCheckedTodoItem(TodoItem item)
            {
                // This code takes a freshly completed TodoItem and updates the database. When the MobileService
                // responds, the item is removed from the list
                await todoTable.UpdateAsync(item);
                items.Remove(item);
            }

            private void ButtonRefresh_Click(object sender, RoutedEventArgs e)
            {
                RefreshTodoItems();
            }

            private void ButtonSave_Click(object sender, RoutedEventArgs e)
            {
                var todoItem = new TodoItem { Text = TodoInput.Text };
                InsertTodoItem(todoItem);
                TodoInput.Text = "";
            }

            private void CheckBoxComplete_Checked(object sender, RoutedEventArgs e)
            {
                CheckBox cb = (CheckBox)sender;
                TodoItem item = cb.DataContext as TodoItem;
                UpdateCheckedTodoItem(item);
            }

            protected override void OnActivated(EventArgs e)
            {
                RefreshTodoItems();
            }
        }

    }
    ```

    ```vb
    Public Class TodoItem
        Public Property Id() As String

        <JsonProperty(PropertyName:="text")>
        Public Property Text() As String

        <JsonProperty(PropertyName:="complete")>
        Public Property Complete() As Boolean
    End Class

    Partial Public Class MainWindow
        Inherits Window

        Private items As MobileServiceCollection(Of TodoItem, TodoItem)
        Private todoTable As IMobileServiceTable(Of TodoItem) = Application.MobileService.GetTable(Of TodoItem)()

        Public Sub New()
            InitializeComponent()
        End Sub

        Private Async Sub InsertTodoItem(ByVal todoItem As TodoItem)
            ' This code inserts a new TodoItem into the database. When the operation completes
            ' and Mobile Services has assigned an Id, the item is added to the CollectionView
            Await todoTable.InsertAsync(todoItem)
            items.Add(todoItem)
        End Sub

        Private Async Sub RefreshTodoItems()
            Dim exception As MobileServiceInvalidOperationException = Nothing
            Try
                ' This code refreshes the entries in the list view by querying the TodoItem table.
                ' The query excludes completed TodoItems
                items = Await todoTable.Where(Function(todoItem) todoItem.Complete = False).ToCollectionAsync()
            Catch e As MobileServiceInvalidOperationException
                exception = e
            End Try

            If exception IsNot Nothing Then
                MessageBox.Show(exception.Message, "Error loading items")
            Else
                ListItems.ItemsSource = items
            End If
        End Sub

        Private Async Sub UpdateCheckedTodoItem(ByVal item As TodoItem)
            ' This code takes a freshly completed TodoItem and updates the database. When the MobileService
            ' responds, the item is removed from the list
            Await todoTable.UpdateAsync(item)
            items.Remove(item)
        End Sub

        Private Sub ButtonRefresh_Click(ByVal sender As Object, ByVal e As RoutedEventArgs)
            RefreshTodoItems()
        End Sub

        Private Sub ButtonSave_Click(ByVal sender As Object, ByVal e As RoutedEventArgs)
            Dim todoItem = New TodoItem With {.Text = TodoInput.Text}
            InsertTodoItem(todoItem)
            TodoInput.Text = ""
        End Sub

        Private Sub CheckBoxComplete_Checked(ByVal sender As Object, ByVal e As RoutedEventArgs)
            Dim cb As CheckBox = DirectCast(sender, CheckBox)
            Dim item As TodoItem = TryCast(cb.DataContext, TodoItem)
            UpdateCheckedTodoItem(item)
        End Sub

        Protected Overrides Sub OnActivated(ByVal e As EventArgs)
            RefreshTodoItems()
        End Sub
    End Class
    ```

     このコードでは、非同期メソッドを使用して、ユーザー インターフェイスと、モバイル サービス内のデータベースと間の相互作用を定義しています。

## <a name="create-the-azure-mobile-service"></a>Azure モバイル サービスを作成する
 最後の手順では、Microsoft Azure でモバイル サービスを作成し、データを格納するためのテーブルを追加した後、アプリケーションからサービス インスタンスを参照します。

#### <a name="to-create-a-mobile-service"></a>モバイル サービスを作成するには

1. Web ブラウザーを開いて Microsoft Azure ポータルにログインし、 **[Mobile Services]** タブをクリックします。

2. **[新規]** ボタンをクリックし、ポップアップ ダイアログで **[コンピューティング]** 、 **[モバイル サービス]、[作成]** の順に選択します。

3. **[新しいモバイル サービス]** ダイアログで、 **[URL]** テキストボックスを選択して「`wpfquickstart01`」と入力します。

    > [!NOTE]
    > URL の数字部分の変更が必要になる場合があります。 Microsoft Azure では、モバイル サービスごとに一意の URL が必要になります。

     これにより、サービスの URL が `https://wpfquickstart01.azure-mobile.net/` に設定されます。

4. **[データベース]** 一覧で、データベース オプションを選択します。 このアプリケーションは、おそらく頻繁には使用されないアプリケーションであるため、 **[無料の 20 MB の SQL データベースを作成する]** オプション、またはサブスクリプションに関連付けられている無料のデータベースを選択できます。

5. **[リージョン]** 一覧で、モバイル サービスをデプロイするデータ センターを選択してから、 **[次へ]** (右矢印) ボタンをクリックします。

    > [!NOTE]
    > このサービスの場合、既定の **[バックエンド]** 設定である **JavaScript**を使用します。

6. 新しいデータベースを作成する場合は、 **[データベースの設定の指定]** ページの **[サーバー]** 一覧で **[新しい SQL データベース サーバー]** を選択し、 **SQL ログイン名** と **パスワード**を入力して、 **[完了]** (チェックマーク) ボタンをクリックします。

7. 既存のデータベースを選択した場合は、 **[データベースの設定]** ページで、 **ログイン パスワード** を入力して、 **[完了]** (チェックマーク) ボタンをクリックします。

     モバイル サービスを作成する処理が開始されます。 この処理が完了すると、状態が **[準備完了]** に変わり、次の手順に進むことができます。

8. ポータルで、新しく作成したモバイル サービスを選択して **[キーの管理]** ボタンをクリックします。

9. **[アクセス キーの管理]** ダイアログで、 **アプリケーション キー**をコピーします。

     このキーは次の手順で使用します。

#### <a name="to-create-a-table"></a>テーブルを作成するには

1. Microsoft Azure ポータルで、モバイル サービスの名前の横にある右矢印をクリックし、メニュー バーで **[データ]** を選択してから、 **[テーブルの追加]** リンクを選択します。

2. **[新しいテーブルの作成]** ダイアログの **[テーブル名]** テキスト ボックスに「 `TodoItem`」と入力して、 **[完了]** (チェックマーク) ボタンをクリックします。

     テーブルの作成が完了するのを待機してから、最後の手順に進みます。

#### <a name="to-add-a-declaration-for-the-mobile-service"></a>モバイル サービスの宣言を追加するには

1. Visual Studio に戻ります。 **ソリューション エクスプローラー**で、 **[App.xaml]** (C#) ノードまたは **[Application.xaml]** (Visual Basic) ノードを展開して **[App.xaml.cs]** ファイルまたは **[App.xaml.vb]** ファイルを開きます。

2. コード エディターで、ファイルの先頭に次の `using` ディレクティブまたは **Imports** ディレクティブを追加します。

    ```csharp
    using Microsoft.WindowsAzure.MobileServices;
    ```

    ```vb
    Imports Microsoft.WindowsAzure.MobileServices
    ```

3. 次の宣言をクラスに追加し、作成したサービスの URL の名前で *YOUR-SERVICE_HERE* を置き換え、前の手順でコピーしたアプリケーション キーで *YOUR-KEY-HERE* を置き換えます。

    ```csharp
    public static MobileServiceClient MobileService = new MobileServiceClient(
                 "https://YOUR-SERVICE-HERE.azure-mobile.net/",
                 "YOUR-KEY-HERE"
             );
    ```

    ```vb
    Public Shared MobileService As New MobileServiceClient("https://YOUR-SERVICE-HERE.azure-mobile.net/", "YOUR-KEY-HERE")
    ```

     このコードによって、アプリケーションが、Microsoft Azure 上で実行されているモバイル サービスにアクセスすることが可能になります。

## <a name="test-the-application"></a>アプリケーションをテストする
 これで、Azure モバイル サービスにアクセスする WPF デスクトップ アプリケーションの作成が完了しました。 あとは、アプリケーションを実行してその動作を確認するだけです。

#### <a name="to-run-the-application"></a>アプリケーションを実行するには

1. メニュー バーで、 **[デバッグ]** 、 **[デバッグの開始]** の順に選択します (または F5 キーを押します)。

2. **[Insert a TodoItem]** テキスト ボックスに「 `Do something`」と入力して、 **[Save]** を選択します。

3. Enter `Do something else`」と入力して、 **[Save]** ボタンを再度クリックします。

     次の図に示すように、2 つのエントリが **[Query and Update Data]** (データのクエリおよび更新) リストに追加されることに注意してください。

     ![Todo 項目がリストに追加されます。](../designers/media/wpfquickstart3.PNG "WPFQuickStart3")

4. 一覧の **[Do something else]** エントリのチェックボックスをオンにします。

     これにより、 **UpdateCheckedTodoItem** メソッドが呼び出され、リストとデータベースの両方から項目が削除されます。

## <a name="next-steps"></a>次のステップ
 Azure バックエンドを利用した、かなりシンプルな例の WPF デスクトップ アプリケーションの作成が完了しました。 もちろん、実際のアプリケーションははるかに複雑になる可能性がありますが、同じ基本的な概念が当てはまります。 「 [.NET Framework での WPF](https://msdn.microsoft.com/library/ms754130\(v=vs.100\).aspx)」を参照してください。

 ユーザー インターフェイスは、色、図形、グラフィックス、さらにアニメーションなどを追加することによって、視覚的により訴えかけるものにできます。 [Visual Studio および Blend for Visual Studio での XAML デザインに関する記事](../designers/designing-xaml-in-visual-studio.md)を参照してください。

 Azure Mobile Services を使用して、既存の SQL データベースや他のデータ ソースに接続することができます。 「 [Mobile Services のドキュメント](https://azure.microsoft.com/services/app-service/mobile/)」を参照してください。

## <a name="see-also"></a>参照
 [チュートリアル: 初めての WPF デスクトップアプリケーション](../designers/walkthrough-my-first-wpf-desktop-application2.md)[で Windows Presentation Foundation を使用した最新のデスクトップアプリケーションの作成](../designers/create-modern-desktop-applications-with-windows-presentation-foundation.md)
