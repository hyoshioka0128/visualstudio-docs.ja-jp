---
title: 'チュートリアル: 初めての WPF デスクトップ アプリケーション 2 | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 3c460fa9-2ea1-413f-ae54-54a1f2a499d1
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e800fe651d32435351b2338b4da2f9c55158b3a0
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72664005"
---
# <a name="walkthrough-my-first-wpf-desktop-application"></a>チュートリアル: 初めての WPF デスクトップ アプリケーション
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

名前 = "概要" > </a> このチュートリアルでは、Windows Presentation Foundation (WPF) 開発の概要について説明します。 ここでは、ほとんどの WPF デスクトップ アプリケーションに共通する要素 (XAML マークアップ、分離コード、アプリケーション定義、コントロール、レイアウト、データ バインディング、スタイル) を含む基本的なアプリケーションを作成します。

## <a name="Create_The_Application_Code_Files"></a> アプリケーション プロジェクトの作成
 このセクションでは、プロジェクトとメイン ウィンドウまたはフォームを含むアプリケーション インフラストラクチャを作成します。

#### <a name="to-create-the-project"></a>プロジェクトを作成するには

1. メニュー バーで **[ファイル]** 、 **[新規作成]** 、 **[プロジェクト]** の順にクリックします。

2. **[新しいプロジェクト]** ダイアログで、 **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[Windows]** ノードを選択して **[Windows]** ノードを展開してから **[従来の (クラシック) デスクトップ]** ノードを選択します。

3. テンプレートの一覧で、 **[WPF アプリケーション]** テンプレートを選択します。

4. **[名前]** ボックスに「 `ExpenseIt`」と入力して、 **[OK]** を選択します。

     プロジェクトが作成され、プロジェクト ファイルが **ソリューション エクスプローラー**に追加され、 **MainWindow.xaml** という名前の既定のアプリケーション ウィンドウのデザイナーが表示されます。

#### <a name="to-modify-the-main-window"></a>メイン ウィンドウを変更するには

1. デザイナーで **[MainWindow.xaml]** タブがアクティブでなければ、このタブを選択します。

2. C# を使用する場合は、 `<Window x:Class="ExpenseIt.MainWindow"` という行を見つけ、その行を `<NavigationWindow x:Class="ExpenseIt.MainWindow"`に置き換えます。

     Visual Basic を使用する場合は、 `<Window x:Class=" MainWindow"` という行を見つけ、その行を `<NavigationWindow x:Class="MainWindow"`に置き換えます。

     `<Window` タグを `<NavigationWindow`に変更すると、Intellisense によって終了タグも `</NavigationWindow>` に自動的に変更されます。

    > [!NOTE]
    > タグを変更した後、 **[エラー一覧]** ウィンドウが開いていると、エラーがいくつか表示される場合があります。 心配しないでください。この後の手順で加える変更でそれらのエラーは解消されます。

3. `<Grid>` と `</Grid>` のタグを選択して削除します。

     **NavigationWindow** に、 **グリッド**などの他の UI 要素を含めることはできません。

4. **[プロパティ]** ウィンドウで、 **Common** カテゴリ ノードを展開し **[Title]** プロパティを選択してから、「 `ExpenseIt` 」と入力して **Enter** キーを押します。

     [XAML] ウィンドウの **[タイトル]** 要素も新しい値に変わったことに注目してください。 XAML のプロパティは、[XAML] ウィンドウまたは **[プロパティ]** ウィンドウのいずれかで変更でき、それらの変更は同期されます。

5. [XAML] ウィンドウで **[Height]** 要素の値を `375`に設定し、 **[Width]** プロパティの値を `500`で行うことができます。

     これらの要素は、 **[プロパティ]** ウィンドウの **[レイアウト]** カテゴリにある **[Height]** プロパティと **[Width]** プロパティに対応します。

     **MainWindow.xaml** ファイルは C# では次のようになります。

    ```xaml
    <NavigationWindow x:Class="ExpenseIt.MainWindow"
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
            xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
            xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
            xmlns:local="clr-namespace:ExpenseIt"
            mc:Ignorable="d"
            Title="ExpenseIt" Height="375" Width="500">

    </NavigationWindow>
    ```

     また、Visual Basic では次のようになります。

    ```xaml
    <NavigationWindow x:Class="MainWindow"
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
            xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
            xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
            xmlns:local="clr-namespace:ExpenseIt"
            mc:Ignorable="d"
            Title="ExpenseIt" Height="375" Width="500">

    </NavigationWindow>
    ```

#### <a name="to-modify-the-code-behind-file-c"></a>分離コード ファイルを変更するには (C#)

1. **ソリューション エクスプローラー**で **[MainWindow.xaml]** ノードを展開し、 **MainWindow.xaml.cs** ファイルを開きます。

2. `public partial class MainWindow : Window` という行を見つけ、その行を `public partial class MainWindow : NavigationWindow`に置き換えます。

     これにより、 `MainWindow` クラスが `NavigationWindow`から派生するように変更されます。 Visual Basic では、これは XAML でウィンドウを変更すると自動的に実行されます。そのため、コードを変更する必要はありません。

## <a name="add_files_to_the_application"></a> ファイルのアプリケーションへの追加
 このセクションでは、アプリケーションに 2 つのページと 1 つのイメージを追加します。

#### <a name="to-add-a-home-screen"></a>ホーム画面を追加するには

1. **ソリューション エクスプローラー**で **[ExpenseIt]** ノードのショートカット メニューを開き、 **[追加]** 、 **[ページ]** を選択します。

2. **[新しい項目の追加]** ダイアログで **[名前]** テキスト ボックスを選択して「 `ExpenseItHome`」と入力し、 **[追加]** ボタンを選択します。

     このページが、アプリケーションの起動時に表示される最初のウィンドウになります。

3. デザイナーで **[ExpenseItHome.xaml]** タブがアクティブでなければ、このタブを選択します。

4. `<Title>` 要素を選択し、タイトルを " **ExpenseIt – ホーム**" に変更します。

     **ExpenseItHome.xaml** ファイルは C# では次のようになります。

    ```xaml
    <Page x:Class="ExpenseIt.ExpenseItHome"
          xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
          xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
          xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
          xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
          xmlns:local="clr-namespace:ExpenseIt"
          mc:Ignorable="d"
          d:DesignHeight="300" d:DesignWidth="300"
          Title="ExpenseIt - Home">

        <Grid>

        </Grid>
    </Page>
    ```

     また、Visual Basic では次のようになります。

    ```xaml
    <Page x:Class="ExpenseItHome"
          xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
          xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
          xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
          xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
          xmlns:local="clr-namespace:ExpenseIt"
          mc:Ignorable="d"
          d:DesignHeight="300" d:DesignWidth="300"
          Title="ExpenseIt - Home">
        <Grid>

        </Grid>
    </Page>
    ```

5. デザイナーで **MainWindow.xaml** タブを選択します。

6. 行 `Title="ExpenseIt" Height="375" Width="500">` 要素を見つけ、 `Source="ExpenseItHome.xaml"` プロパティを追加します。

     これにより、 **ExpenseItHome.xaml** が、アプリケーションの起動時に最初に開くページになります。 **MainWindow.xaml** ファイルは C# では次のようになります。

    ```xaml
    <NavigationWindow x:Class="ExpenseIt.MainWindow"
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
            xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
            xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
            xmlns:local="clr-namespace:ExpenseIt"
            mc:Ignorable="d"
            Title="ExpenseIt" Height="375" Width="500" Source="ExpenseItHome.xaml">

    </NavigationWindow>
    ```

     また、Visual Basic では次のようになります。

    ```xaml
    <NavigationWindow x:Class="MainWindow"
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
            xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
            xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
            xmlns:local="clr-namespace:ExpenseIt"
            mc:Ignorable="d"
            Title="ExpenseIt" Height="375" Width="500" Source="ExpenseItHome.xaml">

    </NavigationWindow>
    ```

     これまでに設定したプロパティと同様に、 `Source` [プロパティ] **ウィンドウの** [その他] **カテゴリの** プロパティを設定できます。

#### <a name="to-add-a-details-window"></a>詳細ウィンドウを追加するには

1. **ソリューション エクスプローラー**で **[ExpenseIt]** ノードのショートカット メニューを開き、 **[追加]** 、 **[ページ]** を選択します。

2. **[新しい項目の追加]** ダイアログで **[名前]** テキスト ボックスを選択して「 `ExpenseReportPage`」と入力し、 **[追加]** ボタンを選択します。

     このウィンドウには、個々の経費明細書が表示されます。

3. デザイナーで **[ExpenseReportPage.xaml]** タブがアクティブでなければ、このタブを選択します。

4. `<Title>` 要素を選択し、タイトルを " **ExpenseIt – 経費の表示**" に変更します。

     ExpenseReportPage.xaml ファイルは C# では次のようになります。

    ```xaml
    <Page x:Class="ExpenseIt.ExpenseReportPage"
          xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
          xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
          xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
          xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
          xmlns:local="clr-namespace:ExpenseIt"
          mc:Ignorable="d"
          d:DesignHeight="300" d:DesignWidth="300"
          Title="ExpenseIt - View Expense">

        <Grid>

        </Grid>
    </Page>
    ```

     また、Visual Basic では次のようになります。

    ```xaml
    <Page x:Class="ExpenseReportPage"
          xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
          xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
          xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
          xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
          xmlns:local="clr-namespace:ExpenseIt"
          mc:Ignorable="d"
          d:DesignHeight="300" d:DesignWidth="300"
          Title="ExpenseIt - View Expense">
        <Grid>

        </Grid>
    </Page>
    ```

5. メニュー バーで、 **[デバッグ]** 、 **[デバッグ開始]** の順に選択して (または F5 キーを押して) アプリケーションを実行します。

     次の図は、ナビゲーション ウィンドウ ボタンが配置されたアプリケーションを示しています。

     ![ページのサンプルのスクリーンショット](../designers/media/gettingstartedfigure1.png "GettingStartedFigure1")

6. アプリケーションを閉じてデザイン モードに戻ります。

## <a name="Add_Layout"></a> ユーザー インターフェイスの作成
 レイアウトを使用すると、順序付けされた方法で要素を配置できます。また、フォームのサイズが変更された場合の要素のサイズと位置が管理されます。 このセクションでは、3 つの行を持つ単一列のグリッドを作成します。 2 つのページにコントロールを追加し、いくつかのコードを追加して、最後にコントロールの再利用可能なスタイルを定義します。

#### <a name="to-create-the-layout"></a>レイアウトを作成するには

1. **ExpenseItHome.xaml** を開き、 `<Grid>` 要素を選択します。

2. **[プロパティ]** ウィンドウで **[高さ]** カテゴリ ノードを展開し、 **[余白]** の値を `10`、 `10`、 `0`、 and `10`、 which corresponds to left、 right、 top and bottom margins.

     要素 `Margin="10,0,10,10"` は XAML 内の `<Grid>` 要素に追加されます。 繰り返しになりますが、 **[プロパティ]** ウィンドウの代わりに XAML コード内にこれらの値を直接入力しても同じ結果になります。

3. 次の XAML コードを `Grid` 要素に追加して、行と列の定義を作成します。

    ```xaml
    <Grid.ColumnDefinitions>
        <ColumnDefinition />
    </Grid.ColumnDefinitions>
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition />
        <RowDefinition Height="Auto"/>
    </Grid.RowDefinitions>
    ```

#### <a name="to-add-controls"></a>コントロールを追加するには

1. **ExpenseItHome.xaml**を開きます。

2. 次の XAML コードを `</Grid>` タグのすぐ上に追加して、 `Border`、 `ListBox` 、および `Button` コントロールを作成します。

    ```xaml
    <!-- People list -->
      <Border Grid.Column="0" Grid.Row="0" Height="35" Padding="5" Background="#4E87D4">
          <Label VerticalAlignment="Center" Foreground="White">Names</Label>
      </Border>
      <ListBox Name="peopleListBox" Grid.Column="0" Grid.Row="1">
          <ListBoxItem>Mike</ListBoxItem>
          <ListBoxItem>Lisa</ListBoxItem>
          <ListBoxItem>John</ListBoxItem>
          <ListBoxItem>Mary</ListBoxItem>
      </ListBox>

      <!-- View report button -->
      <Button Grid.Column="0" Grid.Row="2" Margin="0,10,0,0" Width="125"
    Height="25" HorizontalAlignment="Right">View</Button>

    ```

     これらのコントロールがデザイン ウィンドウに表示されたことを確認してください。 コントロールを **[ツールボックス]** ウィンドウからデザイン ウィンドウにドラッグし、 **[プロパティ]** ウィンドウでプロパティを設定することよって、コントロールを作成することもできます。

3. アプリケーションをビルドして実行します。 次の図は、この手順によって XAML で作成されるコントロールの実行時の外観を示しています。

     ![ページのサンプルのスクリーンショット](../designers/media/gettingstartedfigure2.png "GettingStartedFigure2")

4. アプリケーションを閉じてデザイン モードに戻ります。

#### <a name="to-add-a-background-image"></a>背景イメージを追加するには

1. 次のイメージを選択し、 `watermark.png`の順にクリックします。

     ![チュートリアルのウォーターマークイメージ](../designers/media/wpf-watermark.png "WPF_watermark")

    > [!NOTE]
    > または、独自のイメージを作成し、 `watermark.png`の順にクリックします。

2. **ソリューション エクスプローラー**で **[ExpenseIt]** ノードのショートカット メニューを開き、 **[追加]** 、 **[既存の項目]** を選択します。

3. **[既存項目の追加]** ダイアログで、追加したばかりの **watermark.png** イメージを探して選択し、 **[追加]** ボタンを選択します。

    > [!NOTE]
    > **[ファイルの種類]** リストを展開し、 **[イメージ ファイル]** を選択する必要がある場合があります。

4. **ExpenseItHome.xaml** ファイルを開き、次の XAML コードを `</Grid>` タグのすぐ上に追加し、背景イメージを作成します。

    ```xaml
    <Grid.Background>
        <ImageBrush ImageSource="watermark.png"/>
    </Grid.Background>

    ```

#### <a name="to-add-a-title"></a>タイトルを追加するには

1. **ExpenseItHome.xaml**を開きます。

2. 行 `<Grid.ColumnDefinitions>` を見つけ、そのすぐ下に次を追加します。

    ```xaml
    <ColumnDefinition Width="230" />

    ```

     これにより、他の列の左側に、追加の列が 230 ピクセルの固定幅で作成されます。

3. 行 `<Grid.RowDefinitions>` を見つけ、そのすぐ下に次を追加します。

    ```xaml
    <RowDefinition />

    ```

     これにより、グリッドの上部に行が追加されます。

4. `Grid.Column` の値を 1 に設定して、2 番目の列にコントロールを移動します。 それぞれの `Grid.Row` の値を 1 つずつ増やして、各コントロールを 1 行下に移動します。

    1. 行 `<Border Grid.Column="0" Grid.Row="0" Height="35" Padding="5" Background="#4E87D4">`を見つけます。 `Grid.Column="0"` を `Grid.Column="1"` に変更して、 `Grid.Row="0"` を `Grid.Row="1"`に変更します。

    2. 行 `<ListBox Name="peopleListBox" Grid.Column="0" Grid.Row="1"`を見つけます。 `Grid.Column="0"` を `Grid.Column="1"` に変更して、 `Grid.Row="1"` を `Grid.Row="2"`に変更します。

    3. 行 `<Button Grid.Column="0" Grid.Row="2" Margin="0,10,0,0" Width="125"`を見つけます。 `Grid.Column="0"` を `Grid.Column="1"` に変更して、 `Grid.Row="2"` を `Grid.Row="3"`に変更します。

5. `<Border` 要素の直前に、次の XAML コードを追加してタイトルを表示します。

    ```xaml
    <Label Grid.Column="1" VerticalAlignment="Center" FontFamily="Trebuchet MS"
            FontWeight="Bold" FontSize="18" Foreground="#0066cc">
        View Expense Report
    </Label>

    ```

     **ExpenseItHome.xaml** ファイルの内容は、C# では次のようになります。

    ```xaml
    <Page x:Class="ExpenseIt.ExpenseItHome"
          xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
          xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
          xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
          xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
          xmlns:local="clr-namespace:ExpenseIt"
          mc:Ignorable="d"
          d:DesignHeight="300" d:DesignWidth="300"
          Title="ExpenseIt - Home">
        <Grid Margin="10,0,10,10">
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="230" />
                <ColumnDefinition />
            </Grid.ColumnDefinitions>
            <Grid.RowDefinitions>
                <RowDefinition />
                <RowDefinition Height="Auto"/>
                <RowDefinition />
                <RowDefinition Height="Auto"/>
            </Grid.RowDefinitions>
            <Border Grid.Column="1" Grid.Row="1" Height="35" Padding="5" Background="#4E87D4">
                <Label VerticalAlignment="Center" Foreground="White">Names</Label>
            </Border>
            <!-- People list -->
            <Label Grid.Column="1" VerticalAlignment="Center" FontFamily="Trebuchet MS"
            FontWeight="Bold" FontSize="18" Foreground="#0066cc">
                View Expense Report
            </Label>
            <ListBox Name="peopleListBox" Grid.Column="1" Grid.Row="2">
                <ListBoxItem>Mike</ListBoxItem>
                <ListBoxItem>Lisa</ListBoxItem>
                <ListBoxItem>John</ListBoxItem>
                <ListBoxItem>Mary</ListBoxItem>
            </ListBox>

            <!-- View report button -->
            <Button Grid.Column="1" Grid.Row="3" Margin="0,10,0,0" Width="125"
    Height="25" HorizontalAlignment="Right">View</Button>
            <Grid.Background>
                <ImageBrush ImageSource="watermark.png"/>
            </Grid.Background>
        </Grid>
    </Page>
    ```

     また、Visual Basic では次のようになります。

    ```xaml
    <Page x:Class="ExpenseItHome"
          xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
          xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
          xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
          xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
          xmlns:local="clr-namespace:ExpenseIt"
          mc:Ignorable="d"
          d:DesignHeight="300" d:DesignWidth="300"
          Title="ExpenseIt - Home" >
        <Grid Margin="10,0,10,10">
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="230" />
                <ColumnDefinition />
            </Grid.ColumnDefinitions>
            <Grid.RowDefinitions>
                <RowDefinition />
                <RowDefinition Height="Auto"/>
                <RowDefinition />
                <RowDefinition Height="Auto"/>
            </Grid.RowDefinitions>
            <Border Grid.Column="1" Grid.Row="1" Height="35" Padding="5" Background="#4E87D4">
                <Label VerticalAlignment="Center" Foreground="White">Names</Label>
            </Border>
            <!-- People list -->
            <Label Grid.Column="1" VerticalAlignment="Center" FontFamily="Trebuchet MS"
            FontWeight="Bold" FontSize="18" Foreground="#0066cc">
                View Expense Report
            </Label>
            <ListBox Name="peopleListBox" Grid.Column="1" Grid.Row="2">
                <ListBoxItem>Mike</ListBoxItem>
                <ListBoxItem>Lisa</ListBoxItem>
                <ListBoxItem>John</ListBoxItem>
                <ListBoxItem>Mary</ListBoxItem>
            </ListBox>

            <!-- View report button -->
            <Button Grid.Column="1" Grid.Row="3" Margin="0,10,0,0" Width="125"
    Height="25" HorizontalAlignment="Right">View</Button>
            <Grid.Background>
                <ImageBrush ImageSource="watermark.png"/>
            </Grid.Background>
        </Grid>
    </Page>
    ```

6. この時点でアプリケーションをビルドして実行すると、次の図のようになります。

     ![ページのサンプルのスクリーンショット](../designers/media/gettingstartedfigure3.png "GettingStartedFigure3")

#### <a name="to-add-code-to-the-button"></a>コードをボタンに追加するには

1. **ExpenseItHome.xaml**を開きます。

2. `<Button` 要素を選択し、次の XAML コード **を、** HorizontalAlignment="Right" `Click="Button_Click"`要素の直後に追加します。

     これにより、ボタンの `Click` イベントのイベント ハンドラーが追加されます。 **<Button** 要素のコードは、次のようになります。

    ```
    <!-- View report button -->
      <Button Grid.Column="1" Grid.Row="3" Margin="0,10,0,0" Width="125"
    Height="25" HorizontalAlignment="Right" Click="Button_Click">View</Button>
    ```

3. **ExpenseItHome.xaml.cs** または **ExpenseItHome.xaml.vb** ファイルを開きます。

4. `ExpenseItHome` クラスに次のコードを追加します。

    ```csharp
    private void Button_Click(object sender, RoutedEventArgs e)
    {
        // View Expense Report
        ExpenseReportPage expenseReportPage = new ExpenseReportPage();
        this.NavigationService.Navigate(expenseReportPage);

    }
    ```

    ```vb
    Private Sub Button_Click(ByVal sender As Object, ByVal e As RoutedEventArgs)
        ' View Expense Report
        Dim expenseReportPage As New ExpenseReportPage()
    Me.NavigationService.Navigate(expenseReportPage)
    End Sub
    ```

     このイベント ハンドラーは、ボタンがクリックされたときに経費明細書ページを開きます。

#### <a name="to-create-the-ui-for-the-report-page"></a>レポート ページの UI を作成するには

1. **ExpenseReportPage.xaml**を開きます。

     このページには、ホーム ページで選択されたユーザーの経費明細書が表示されます。

2. `<Grid>` と `</Grid>` のタグの間に次の XAML を追加します。

    ```xaml
    <Grid.Background>
        <ImageBrush ImageSource="watermark.png" />
    </Grid.Background>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="230" />
        <ColumnDefinition />
    </Grid.ColumnDefinitions>
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto" />
        <RowDefinition />
    </Grid.RowDefinitions>

    <Label Grid.Column="1" VerticalAlignment="Center" FontFamily="Trebuchet MS"
    FontWeight="Bold" FontSize="18" Foreground="#0066cc">
        Expense Report For:
    </Label>
    <Grid Margin="10" Grid.Column="1" Grid.Row="1">

        <Grid.ColumnDefinitions>
            <ColumnDefinition />
            <ColumnDefinition />
        </Grid.ColumnDefinitions>
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto" />
            <RowDefinition Height="Auto" />
            <RowDefinition />
        </Grid.RowDefinitions>

        <!-- Name -->
        <StackPanel Grid.Column="0" Grid.ColumnSpan="2" Grid.Row="0" Orientation="Horizontal">
            <Label Margin="0,0,0,5" FontWeight="Bold">Name:</Label>
            <Label Margin="0,0,0,5" FontWeight="Bold"></Label>
        </StackPanel>

        <!-- Department -->
        <StackPanel Grid.Column="0" Grid.ColumnSpan="2" Grid.Row="1" Orientation="Horizontal">
            <Label Margin="0,0,0,5" FontWeight="Bold">Department:</Label>
            <Label Margin="0,0,0,5" FontWeight="Bold"></Label>
        </StackPanel>

        <Grid Grid.Column="0" Grid.ColumnSpan="2" Grid.Row="2" VerticalAlignment="Top"
              HorizontalAlignment="Left">
            <!-- Expense type and Amount table -->
            <DataGrid  AutoGenerateColumns="False" RowHeaderWidth="0" >
                <DataGrid.ColumnHeaderStyle>
                    <Style TargetType="{x:Type DataGridColumnHeader}">
                        <Setter Property="Height" Value="35" />
                        <Setter Property="Padding" Value="5" />
                        <Setter Property="Background" Value="#4E87D4" />
                        <Setter Property="Foreground" Value="White" />
                    </Style>
                </DataGrid.ColumnHeaderStyle>
                <DataGrid.Columns>
                    <DataGridTextColumn Header="ExpenseType" />
                    <DataGridTextColumn Header="Amount"  />
                </DataGrid.Columns>
            </DataGrid>
        </Grid>
    </Grid>
    ```

     この UI はホーム ページで作成した UI と似ていますが、 **DataGrid** コントロールにレポート データが表示されます。

3. アプリケーションをビルドして実行します。

4. **[表示]** ボタンを選択します。

     経費明細書ページが表示されます。

     次の図は、経費明細書ページを示しています。 [戻る] ナビゲーション ボタンが有効になっていることを確認してください。

     ![ページのサンプルのスクリーンショット](../designers/media/gettingstartedfigure4.png "GettingStartedFigure4")

#### <a name="to-style-controls"></a>コントロールのスタイルを設定するには

1. **App.xaml** ファイル (C#) または **Application.xaml** ファイル (Visual Basic) を開きます。

2. `<Application.Resources>` と `</Application.Resources>` のタグの間に次の XAML を追加します。

    ```xaml
    <!-- Header text style -->
    <Style x:Key="headerTextStyle">
        <Setter Property="Label.VerticalAlignment" Value="Center"></Setter>
        <Setter Property="Label.FontFamily" Value="Trebuchet MS"></Setter>
        <Setter Property="Label.FontWeight" Value="Bold"></Setter>
        <Setter Property="Label.FontSize" Value="18"></Setter>
        <Setter Property="Label.Foreground" Value="#0066cc"></Setter>
    </Style>

    <!-- Label style -->
    <Style x:Key="labelStyle" TargetType="{x:Type Label}">
        <Setter Property="VerticalAlignment" Value="Top" />
        <Setter Property="HorizontalAlignment" Value="Left" />
        <Setter Property="FontWeight" Value="Bold" />
        <Setter Property="Margin" Value="0,0,0,5" />
    </Style>

    <!-- DataGrid header style -->
    <Style x:Key="columnHeaderStyle" TargetType="{x:Type DataGridColumnHeader}">
        <Setter Property="Height" Value="35" />
        <Setter Property="Padding" Value="5" />
        <Setter Property="Background" Value="#4E87D4" />
        <Setter Property="Foreground" Value="White" />
    </Style>

    <!-- List header style -->
    <Style x:Key="listHeaderStyle" TargetType="{x:Type Border}">
        <Setter Property="Height" Value="35" />
        <Setter Property="Padding" Value="5" />
        <Setter Property="Background" Value="#4E87D4" />
    </Style>

    <!-- List header text style -->
    <Style x:Key="listHeaderTextStyle" TargetType="{x:Type Label}">
        <Setter Property="Foreground" Value="White" />
        <Setter Property="VerticalAlignment" Value="Center" />
        <Setter Property="HorizontalAlignment" Value="Left" />
    </Style>

    <!-- Button style -->
    <Style x:Key="buttonStyle" TargetType="{x:Type Button}">
        <Setter Property="Width" Value="125" />
        <Setter Property="Height" Value="25" />
        <Setter Property="Margin" Value="0,10,0,0" />
        <Setter Property="HorizontalAlignment" Value="Right" />
    </Style>
    ```

     この XAML は、次のスタイルを追加します。

    - `headerTextStyle`: ページ タイトル `Label`の書式を設定します。

    - `labelStyle`: `Label` コントロールの書式を設定します。

    - `columnHeaderStyle`: `DataGridColumnHeader`の書式を設定します。

    - `listHeaderStyle`: リスト ヘッダーの `Border` コントロールの書式を設定します。

    - `listHeaderTextStyle`: リスト ヘッダー **Label**の書式を設定します。

    - `buttonStyle`: `Button` [ExpenseItHome.xaml] **ページの** の書式を設定します。

3. **ExpenseItHome.xaml** を開き、 `<Grid>` と `</Grid>` の要素の間にあるすべてを次の XAML に置き換えます。

    ```xaml
    <Grid.ColumnDefinitions>
                <ColumnDefinition Width="230" />
                <ColumnDefinition />
            </Grid.ColumnDefinitions>

            <Grid.RowDefinitions>
                <RowDefinition/>
                <RowDefinition Height="Auto"/>
                <RowDefinition />
                <RowDefinition Height="Auto"/>
            </Grid.RowDefinitions>
            <Label Grid.Column="1" Style="{StaticResource headerTextStyle}" >
                View Expense Report
            </Label>
            <!-- People list -->
                  <Border Grid.Column="1" Grid.Row="1" Style="{StaticResource listHeaderStyle}">
                <Label Style="{StaticResource listHeaderTextStyle}">Names</Label>
            </Border>
            <ListBox Name="peopleListBox" Grid.Column="1" Grid.Row="2">
                <ListBoxItem>Mike</ListBoxItem>
                <ListBoxItem>Lisa</ListBoxItem>
                <ListBoxItem>John</ListBoxItem>
                <ListBoxItem>Mary</ListBoxItem>
            </ListBox>

            <!-- View report button -->
            <Button Grid.Column="1" Grid.Row="3" Click="Button_Click" Style="{StaticResource buttonStyle}">View</Button>
            <Grid.Background>
                <ImageBrush ImageSource="watermark.png"  />
            </Grid.Background>
    ```

     各コントロールの外観を定義する `VerticalAlignment` や `FontFamily` などのプロパティは、これらのスタイルを適用することで、削除されて置き換えられます。

4. **ExpenseReportPage.xaml** を開き、 `<Grid>` と最後の `</Grid>` の要素の間にあるすべてを次の XAML に置き換えます。

    ```xaml
    <Grid.Background>
        <ImageBrush ImageSource="watermark.png" />
    </Grid.Background>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="230" />
        <ColumnDefinition />
    </Grid.ColumnDefinitions>
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto" />
        <RowDefinition />
    </Grid.RowDefinitions>
    <Label Grid.Column="1" Style="{StaticResource headerTextStyle}">
        Expense Report For:
    </Label>
    <Grid Margin="10" Grid.Column="1" Grid.Row="1">
        <Grid.ColumnDefinitions>
            <ColumnDefinition />
            <ColumnDefinition />
        </Grid.ColumnDefinitions>
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto" />
            <RowDefinition Height="Auto" />
            <RowDefinition />
        </Grid.RowDefinitions>

        <!-- Name -->
        <StackPanel Grid.Column="0" Grid.ColumnSpan="2" Grid.Row="0" Orientation="Horizontal">
            <Label Style="{StaticResource labelStyle}">Name:</Label>
            <Label Style="{StaticResource labelStyle}"></Label>
        </StackPanel>

        <!-- Department -->
        <StackPanel Grid.Column="0" Grid.ColumnSpan="2" Grid.Row="1"
    Orientation="Horizontal">
            <Label Style="{StaticResource labelStyle}">Department:</Label>
            <Label Style="{StaticResource labelStyle}"></Label>
        </StackPanel>

        <Grid Grid.Column="0" Grid.ColumnSpan="2" Grid.Row="2" VerticalAlignment="Top"
              HorizontalAlignment="Left">
            <!-- Expense type and Amount table -->
            <DataGrid ColumnHeaderStyle="{StaticResource columnHeaderStyle}"
                      AutoGenerateColumns="False" RowHeaderWidth="0" >
                <DataGrid.Columns>
                    <DataGridTextColumn Header="ExpenseType" />
                    <DataGridTextColumn Header="Amount"  />
                </DataGrid.Columns>
            </DataGrid>
        </Grid>
    </Grid>

    ```

     これにより、スタイルが `<Label>` と `<Border>` の要素に追加されます。

## <a name="connecting-to-data"></a>データへの接続
 このセクションでは、データ プロバイダーとデータ テンプレートを作成して、データを表示するコントロールを接続します。

#### <a name="to-bind-data-to-a-control"></a>データをコントロールにバインドするには

1. **ExpenseItHome.xaml** を開き、 `<Grid>` 要素を選択します。

2. 次の XAML コードを追加します。

    ```xaml

    <Grid.Resources>
    <!-- Expense Report Data -->
    <XmlDataProvider x:Key="ExpenseDataSource" XPath="Expenses">
        <x:XData>
            <Expenses xmlns="">
                <Person Name="Mike" Department="Legal">
                    <Expense ExpenseType="Lunch" ExpenseAmount="50" />
                    <Expense ExpenseType="Transportation" ExpenseAmount="50" />
                </Person>
                <Person Name="Lisa" Department="Marketing">
                    <Expense ExpenseType="Document printing"
          ExpenseAmount="50"/>
                    <Expense ExpenseType="Gift" ExpenseAmount="125" />
                </Person>
                <Person Name="John" Department="Engineering">
                    <Expense ExpenseType="Magazine subscription"
         ExpenseAmount="50"/>
                    <Expense ExpenseType="New machine" ExpenseAmount="600" />
                    <Expense ExpenseType="Software" ExpenseAmount="500" />
                </Person>
                <Person Name="Mary" Department="Finance">
                    <Expense ExpenseType="Dinner" ExpenseAmount="100" />
                </Person>
            </Expenses>
        </x:XData>
    </XmlDataProvider>
    </Grid.Resources>
    ```

     このコードにより、各ユーザーのデータを格納する `XmlDataProvider` クラスが作成されます。 通常、これはファイルとして読み込まれますが、説明を簡単にするため、データをインラインで追加します。

3. `<Grid.Resources>` 要素内に、次の XAML コードを追加します。

    ```xaml
    <!-- Name item template -->
    <DataTemplate x:Key="nameItemTemplate">
        <Label Content="{Binding XPath=@Name}"/>
    </DataTemplate>
    ```

     これにより、 `Data Template` ListBox **にデータを表示する方法を定義する**が追加されます。

4. 既存の `<ListBox>` 要素を次の XAML に置き換えます。

    ```xaml
    <ListBox Name="peopleListBox" Grid.Column="1" Grid.Row="2"
             ItemsSource="{Binding Source={StaticResource ExpenseDataSource}, XPath=Person}"
             ItemTemplate="{StaticResource nameItemTemplate}">
    </ListBox>
    ```

     このコードは、 `ItemsSource` の `ListBox` プロパティをデータ ソースにバインドし、データ テンプレートを `ItemTemplate`として適用します。

#### <a name="to-connect-data-to-controls"></a>コントロールにデータを接続するには

1. **ExpenseReportPage.xaml.vb** または **ExpenseReportPage.xaml.cs**を開きます。

2. C# では、次のコンストラクターを **ExpenseReportPage** クラスに追加します。また、Visual Basic では、既存のクラスを次に置き換えます。

    ```csharp
    // Custom constructor to pass expense report data
        public ExpenseReportPage(object data):this()
        {
            // Bind to expense report data.
            this.DataContext = data;
        }
    ```

    ```vb
    Partial Public Class ExpenseReportPage
    Inherits Page
    Public Sub New()
    InitializeComponent()
    End Sub

    ' Custom constructor to pass expense report data
    Public Sub New(ByVal data As Object)
    Me.New()
    ' Bind to expense report data.
    Me.DataContext = data
    End Sub

    End Class
    ```

     このコンストラクターは、データ オブジェクトをパラメーターとして受け取ります。 この場合、データ オブジェクトには、選択したユーザーの名前が格納されます。

3. **ExpenseItHome.xaml.vb** または **ExpenseItHome.xaml.cs**ファイルを開きます。

4. `Click` イベント ハンドラー コードを次に置き換えます。

    ```csharp
    private void Button_Click(object sender, RoutedEventArgs e)
    {
        // View Expense Report
        ExpenseReportPage expenseReportPage = new ExpenseReportPage(this.peopleListBox.SelectedItem);
        this.NavigationService.Navigate(expenseReportPage);

    }
    ```

    ```vb
    Private Sub Button_Click(ByVal sender As Object, ByVal e As RoutedEventArgs)
        ' View Expense Report
        Dim expenseReportPage As New ExpenseReportPage(Me.peopleListBox.SelectedItem)
        Me.NavigationService.Navigate(expenseReportPage)
    End Sub
    ```

     このコードは、新しいコンストラクターを呼び出します。

#### <a name="to-update-the-ui-with-data-templates"></a>データ テンプレートを使用して UI を更新するには

1. **ExpenseReportPage.xaml**を開きます。

2. **[名前]** と **Department**`<StackPanel` 要素の XAML コードを次に置き換えます。

    ```xaml
    <!-- Name -->
    <StackPanel Grid.Column="0" Grid.ColumnSpan="2" Grid.Row="0" Orientation="Horizontal">
        <Label Style="{StaticResource labelStyle}">Name:</Label>
        <Label Style="{StaticResource labelStyle}" Content="{Binding XPath=@Name}"></Label>
    </StackPanel>

    <!-- Department -->
    <StackPanel Grid.Column="0" Grid.ColumnSpan="2" Grid.Row="1" Orientation="Horizontal">
        <Label Style="{StaticResource labelStyle}">Department:</Label>
        <Label Style="{StaticResource labelStyle}" Content="{Binding XPath=@Department}"></Label>
    </StackPanel>

    ```

     これにより、 **Label** コントロールを適切なデータ ソース プロパティにバインドします。

3. `<Grid>` 要素内に、次の XAML コードを追加します。

    ```xaml
    <!--Templates to display expense report data-->
    <Grid.Resources>
        <!-- Reason item template -->
        <DataTemplate x:Key="typeItemTemplate">
            <Label Content="{Binding XPath=@ExpenseType}"/>
        </DataTemplate>
        <!-- Amount item template -->
        <DataTemplate x:Key="amountItemTemplate">
            <Label Content="{Binding XPath=@ExpenseAmount}"/>
        </DataTemplate>
    </Grid.Resources>

    ```

     これにより、経費明細書データを表示する方法が定義されます。

4. `<DataGrid>` 要素を次に置き換えます。

    ```xaml
    <!-- Expense type and Amount table -->
    <DataGrid ItemsSource="{Binding XPath=Expense}" ColumnHeaderStyle="{StaticResource columnHeaderStyle}" AutoGenerateColumns="False" RowHeaderWidth="0" >

        <DataGrid.Columns>
            <DataGridTextColumn Header="ExpenseType" Binding="{Binding XPath=@ExpenseType}"  />
            <DataGridTextColumn Header="Amount" Binding="{Binding XPath=@ExpenseAmount}" />
        </DataGrid.Columns>

    </DataGrid>
    ```

     これにより、 **ItemSource** が追加され、経費品目のバインディングが定義されます。

5. アプリケーションをビルドして実行します。

6. ユーザーを選択し、 **[表示]** ボタンを選択します。

     次の図には、コントロール、レイアウト、スタイル、データ バインディング、データ テンプレートが適用された ExpenseIt アプリケーションの両方のページが示されています。

     ![ページのサンプルスクリーンショット](../designers/media/gettingstartedfigure5.png "GettingStartedFigure5")

## <a name="Best_Practices"></a> ベスト プラクティス
 このサンプルは、WPF の基礎を説明するものであり、アプリケーション開発のベスト プラクティスには従っていません。 WPF と .NET Framework のアプリケーション開発のベスト プラクティスの包括的な情報については、必要に応じて次のトピックを参照してください。

- ユーザー補助 - [ユーザー補助のベスト プラクティス](https://msdn.microsoft.com/library/aa350483\(v=vs.100\).aspx)

- セキュリティ - [Windows Presentation Foundation のセキュリティ](https://msdn.microsoft.com/library/aa970906\(v=vs.100\).aspx)

- ローカリゼーション - [WPF のグローバリゼーションおよびローカリゼーションの概要](https://msdn.microsoft.com/library/ms788718\(v=vs.100\).aspx)

- パフォーマンス - [WPF アプリケーションのパフォーマンスの最適化](https://msdn.microsoft.com/library/aa970683\(v=vs.100\).aspx)

## <a name="Whats_Next"></a> 次の内容
 これで、WPF を使用してデスクトップ アプリケーションを作成するためのいくつかの手法を習得できました。 データ バインドされた WPF アプリケーションの構成要素についての基本を理解することもできました。 このトピックは決して網羅的なものではありませんが、このトピックの手法を基に、自分で学習を進められるようになったはずです。

 WPF のアーキテクチャおよびプログラミング モデルの詳細については、次のトピックを参照してください。

- [WPF アーキテクチャ](https://msdn.microsoft.com/library/ms750441\(v=vs.100\).aspx)

- [XAML の概要](https://msdn.microsoft.com/library/ms752059\(v=vs.100\).aspx)

- [依存関係プロパティの概要](https://msdn.microsoft.com/library/ms752914\(v=vs.100\).aspx)

- [レイアウト システム](https://msdn.microsoft.com/library/ms745058\(v=vs.100\).aspx)

- [スタイルおよびテンプレート](https://msdn.microsoft.com/library/bb613570\(v=vs.100\).aspx)

  アプリケーションの作成の詳細については、次のトピックを参照してください。

- [アプリケーション開発の概要](https://msdn.microsoft.com/library/bb613549\(v=vs.100\).aspx)

- [コントロールの概要](https://msdn.microsoft.com/library/bb613551\(v=vs.100\).aspx)

- [データ バインディングの概要](https://msdn.microsoft.com/library/ms752347\(v=vs.100\).aspx)

- [WPF のグラフィックス、アニメーション、およびメディアの概要](https://msdn.microsoft.com/library/ms742562\(v=vs.100\).aspx)

- [WPF のドキュメント](https://msdn.microsoft.com/library/ms748388\(v=vs.100\).aspx)

## <a name="see-also"></a>参照
 [チュートリアル: Azure モバイルサービスに接続された WPF デスクトップアプリケーションの作成](../designers/walkthrough-create-a-wpf-desktop-application-connected-to-an-azure-mobile-service.md) [Windows Presentation Foundation を使用した最新のデスクトップアプリケーションの作成](../designers/create-modern-desktop-applications-with-windows-presentation-foundation.md)
