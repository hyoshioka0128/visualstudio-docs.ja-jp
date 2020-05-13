---
title: スタート ページへのユーザー コントロールの追加 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- start page dll
- custom start page
- start page assembly
ms.assetid: 5b7997db-af6f-4fa9-a128-bceb42bddaf1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: b426cfbbfca2e301797644a1fc73f188054d0cfa
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740131"
---
# <a name="add-user-control-to-the-start-page"></a>スタート ページにユーザー コントロールを追加する

このチュートリアルでは、カスタム スタート ページに DLL 参照を追加する方法を示します。 この例では、ソリューションにユーザー コントロールを追加し、ユーザー コントロールをビルドし、次にスタート ページ*の .xaml*ファイルからビルドしたアセンブリを参照します。 新しいタブは、基本的な Web ブラウザーとして機能するユーザー コントロールをホストします。

同じプロセスを使用して *、.xaml*ファイルから呼び出すことができる任意のアセンブリを追加できます。

## <a name="add-a-wpf-user-control-to-the-solution"></a>ソリューションに WPF ユーザー コントロールを追加する

最初に、Windows プレゼンテーション ファンデーション (WPF) ユーザー コントロールをスタート ページ ソリューションに追加します。

1. 「カスタム スタート ページの作成」で作成[したスタート ページを作成します](../extensibility/creating-a-custom-start-page.md)。

2. **ソリューション エクスプローラ**でソリューションを右クリックし、[**追加**]**をクリックします**。

3. [**新しいプロジェクト**] ダイアログ ボックスの左ペインで **、[Visual Basic]** ノードまたは **[Visual C#]** ノードを展開し、[**ウィンドウ**] をクリックします。 中央のペインで、[ **WPF ユーザー コントロール ライブラリ**] を選択します。

4. コントロール`WebUserControl`に名前を付け **、[OK]** をクリックします。

## <a name="implement-the-user-control"></a>ユーザー コントロールを実装する

WPF ユーザー コントロールを実装するには、XAML でユーザー インターフェイス (UI) をビルドし、C# または別の .NET 言語で分離コード イベントを記述します。

### <a name="to-write-the-xaml-for-the-user-control"></a>ユーザー コントロールの XAML を記述するには

1. ユーザー コントロールの XAML ファイルを開きます。 要素で`<Grid>`、コントロールに次の行定義を追加します。

    ```vb
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*" />
    </Grid.RowDefinitions>

    ```

2. main`<Grid>`要素に、Web アドレスを`<Grid>`入力するためのテキスト ボックスと新しいアドレスを設定するためのボタンを含む、次の新しい要素を追加します。

    ```xml
    <Grid Grid.Row="0">
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="*" />
            <ColumnDefinition Width="Auto" />
        </Grid.ColumnDefinitions>
        <TextBox x:Name="UserSource" Grid.Column="0" />
        <Button Grid.Column="1" x:Name="SetButton" Content="Set Address" Click="SetButton_Click" />
    </Grid>
    ```

3. ボタンとテキスト ボックスを含む`<Grid>`要素の直後に、`<Grid>`最上位の要素に次のフレームを追加します。

    ```vb
    <Frame Grid.Row="1" x:Name="WebFrame" Source="http://www.bing.com" Navigated="WebFrame_Navigated" />
    ```

4. ユーザー コントロールの完成した XAML の例を次に示します。

    ```xml
    <UserControl x:Class="WebUserControl.UserControl1"
                 xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
                 xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                 xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
                 xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
                 mc:Ignorable="d"
                 d:DesignHeight="300" d:DesignWidth="300">
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*" />
            </Grid.RowDefinitions>
            <Grid Grid.Row="0">
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="*" />
                    <ColumnDefinition Width="Auto" />
                </Grid.ColumnDefinitions>
                <TextBox x:Name="UserSource" Grid.Column="0" />
                <Button Grid.Column="1" x:Name="SetButton" Content="Set Address" Click="SetButton_Click" />
            </Grid>
            <Frame Grid.Row="1" x:Name="WebFrame" Source="http://www.bing.com" Navigated="WebFrame_Navigated" />
        </Grid>
    </UserControl>

    ```

### <a name="to-write-the-code-behind-events-for-the-user-control"></a>ユーザー コントロールの分離コード イベントを記述するには

1. XAML デザイナーで、コントロールに追加した **[アドレスの設定**] ボタンをダブルクリックします。

    *UserControl1.cs*ファイルがコード エディターで開きます。

2. SetButton_Clickイベント ハンドラに次のように入力します。

    ```csharp
    private void SetButton_Click(object sender, RoutedEventArgs e)
    {
        try
        {
            this.WebFrame.Source = new Uri(this.UserSource.Text, UriKind.Absolute);
        }
        catch (Exception error)
        {
            MessageBox.Show(error.Message);
        }
    }
    ```

    このコードは、テキスト ボックスに入力された Web アドレスを Web ブラウザのターゲットとして設定します。 アドレスが無効な場合、コードはエラーをスローします。

3. WebFrame_Navigated イベントも処理する必要があります。

    ```csharp
    private void WebFrame_Navigated(object sender, EventArgs e)
    { }
    ```

4. ソリューションをビルドします。

## <a name="add-the-user-control-to-the-start-page"></a>スタート ページにユーザー コントロールを追加する

このコントロールをスタート ページ プロジェクトで使用できるようにするには、スタート ページ プロジェクト ファイルで、新しいコントロール ライブラリへの参照を追加します。 その後、スタート ページ XAML マークアップにコントロールを追加できます。

1. **ソリューション エクスプローラー**のスタート ページ プロジェクトで、[参照設定] を右クリックし、[**参照**の**追加**] をクリックします。

2. [**プロジェクト**] タブで **[WebUserControl]** を選択し **、[OK]** をクリックします。

3. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

    ソリューションをビルドすると、ソリューション内の他のファイルに対してユーザー コントロールを IntelliSense で使用できるようになります。

    スタート ページ XAML マークアップにコントロールを追加するには、名前空間参照をアセンブリに追加し、ページにコントロールを配置します。

### <a name="to-add-the-control-to-the-markup"></a>コントロールをマークアップに追加するには

1. **ソリューション エクスプローラー**で、スタート ページ*の .xaml*ファイルを開きます。

2. **XAML**ペインで、最上位の<xref:System.Windows.Controls.Grid>要素に次の名前空間宣言を追加します。

   ```xml
   xmlns:vsc="clr-namespace:WebUserControl;assembly=WebUserControl"
   ```

3. **XAML**ウィンドウで、[\<グリッド>] セクションまでスクロールします。

    セクションには要素内<xref:System.Windows.Controls.TabControl>の要素が<xref:System.Windows.Controls.Grid>含まれています。

4. ユーザー\<コントロールへの参照を含む\<TabItem>を含む TabControl>要素を追加します。

    ```xml

    <TabItem Header="Web" Height="Auto">
        <vsc:UserControl1 />
    </TabItem>

    ```

    これで、コントロールをテストできます。

## <a name="test-a-manually-created-custom-start-page"></a>手動で作成したカスタム スタート ページをテストする

1. XAML ファイルとサポートテキスト ファイルまたはマークアップ ファイルを *%USERPROFILE%\マイ ドキュメント\Visual Studio 2015\StartPages\\*フォルダーにコピーします。

2. Visual Studio によってインストールされていないアセンブリ内のコントロールまたは型をスタート ページが参照する場合は、アセンブリをコピーし _、Visual Studio のインストール フォルダー_**\Common7\IDE\PrivateAssembly\\**に貼り付けます。

3. Visual Studio のコマンド プロンプトで **、devenv /ルートサフィックス Exp と**入力して、Visual Studio の実験的なインスタンスを開きます。

4. 実験用インスタンスで、[**ツール** > **オプション** > **環境** > の**スタートアップ**] ページに移動し、[スタート**ページのカスタマイズ**] ドロップダウンから XAML ファイルを選択します。

5. **[表示]** メニューの **[スタート ページ]** をクリックします。

    カスタムスタートページが表示されます。 ファイルを変更する場合は、実験用インスタンスを閉じ、変更を加え、変更されたファイルをコピーして貼り付け、その後、実験用インスタンスを再度開いて変更を表示する必要があります。

## <a name="see-also"></a>関連項目

- [WPF コンテナー コントロール](https://msdn.microsoft.com/library/a0177167-d7db-4205-9607-8ae316952566)
- [チュートリアル: カスタム XAML をスタート ページに追加する](../extensibility/walkthrough-adding-custom-xaml-to-the-start-page.md)
