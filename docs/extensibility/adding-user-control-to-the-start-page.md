---
title: スタートページにユーザーコントロールを追加する |Microsoft Docs
description: Visual Studio のスタートページに Windows Presentation Foundation (WPF) ユーザーコントロールを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
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
ms.openlocfilehash: fa812b477f88b03b8f0d4bdcba6c69f009ec2894
ms.sourcegitcommit: d6207a3a590c9ea84e3b25981d39933ad5f19ea3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/24/2020
ms.locfileid: "95597549"
---
# <a name="add-user-control-to-the-start-page"></a>スタートページにユーザーコントロールを追加する

このチュートリアルでは、カスタムスタートページに DLL 参照を追加する方法について説明します。 この例では、ユーザーコントロールをソリューションに追加し、ユーザーコントロールをビルドしてから、ビルドされたアセンブリをスタートページ *.xaml* ファイルから参照します。 新しいタブでは、基本的な Web ブラウザーとして機能するユーザーコントロールをホストします。

同じプロセスを使用して、 *.xaml* ファイルから呼び出すことのできるアセンブリを追加できます。

## <a name="add-a-wpf-user-control-to-the-solution"></a>ソリューションに WPF ユーザーコントロールを追加する

最初に、スタートページソリューションに Windows Presentation Foundation (WPF) ユーザーコントロールを追加します。

1. 「 [カスタムスタートページを作成する](../extensibility/creating-a-custom-start-page.md)」で作成したを使用してスタートページを作成します。

2. **ソリューション エクスプローラー** で該当ソリューションを右クリックして **[追加]** をクリックし、 **[新しいプロジェクト]** をクリックします。

3. [ **新しいプロジェクト** ] ダイアログボックスの左ペインで、[ **Visual Basic** ] または [ **Visual C#** ] ノードのいずれかを展開し、[ **Windows**] をクリックします。 中央のペインで、[ **WPF ユーザーコントロールライブラリ**] を選択します。

4. コントロールに名前を指定し、 `WebUserControl` [ **OK]** をクリックします。

## <a name="implement-the-user-control"></a>ユーザーコントロールを実装する

WPF ユーザーコントロールを実装するには、XAML でユーザーインターフェイス (UI) をビルドし、C# または他の .NET 言語で分離コードイベントを記述します。

### <a name="to-write-the-xaml-for-the-user-control"></a>ユーザーコントロールの XAML を記述するには

1. ユーザーコントロールの XAML ファイルを開きます。 要素で `<Grid>` 、次の行定義をコントロールに追加します。

    ```vb
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*" />
    </Grid.RowDefinitions>

    ```

2. Main 要素に `<Grid>` 次の新しい要素を追加します。この要素には `<Grid>` 、Web アドレスを入力するためのテキストボックスと、新しいアドレスを設定するためのボタンが含まれています。

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

3. 次のフレームを、 `<Grid>` `<Grid>` ボタンとテキストボックスを含む要素の直後にある最上位の要素に追加します。

    ```vb
    <Frame Grid.Row="1" x:Name="WebFrame" Source="http://www.bing.com" Navigated="WebFrame_Navigated" />
    ```

4. 次の例は、ユーザーコントロールの完成した XAML を示しています。

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

### <a name="to-write-the-code-behind-events-for-the-user-control"></a>ユーザーコントロールの分離コードイベントを作成するには

1. XAML デザイナーで、コントロールに追加した [ **アドレスの設定** ] ボタンをダブルクリックします。

    コードエディターで *UserControl1.cs* ファイルが開きます。

2. SetButton_Click イベントハンドラーに次のように入力します。

    ```csharp
    private void SetButton_Click(object sender, RoutedEventArgs e)
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

    このコードは、テキストボックスに入力された Web アドレスを Web ブラウザーのターゲットとして設定します。 アドレスが有効でない場合、コードはエラーをスローします。

3. また、WebFrame_Navigated イベントも処理する必要があります。

    ```csharp
    private void WebFrame_Navigated(object sender, EventArgs e)
    { }
    ```

4. ソリューションをビルドします。

## <a name="add-the-user-control-to-the-start-page"></a>スタートページにユーザーコントロールを追加する

スタートページプロジェクトでこのコントロールを使用できるようにするには、スタートページのプロジェクトファイルで、新しいコントロールライブラリへの参照を追加します。 その後、スタートページの XAML マークアップにコントロールを追加できます。

1. **ソリューションエクスプローラー** のスタートページプロジェクトで、[**参照**] を右クリックし、[**参照の追加**] をクリックします。

2. [ **プロジェクト** ] タブで [ **Webusercontrol** ] を選択し、[ **OK**] をクリックします。

3. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

    ソリューションをビルドすると、ソリューション内の他のファイルの IntelliSense でユーザーコントロールを使用できるようになります。

    スタートページの XAML マークアップにコントロールを追加するには、アセンブリへの名前空間参照を追加してから、コントロールをページに配置します。

### <a name="to-add-the-control-to-the-markup"></a>マークアップにコントロールを追加するには

1. **ソリューションエクスプローラー** で、スタートページの *.xaml* ファイルを開きます。

2. **XAML** ペインで、最上位レベルの要素に次の名前空間宣言を追加し <xref:System.Windows.Controls.Grid> ます。

   ```xml
   xmlns:vsc="clr-namespace:WebUserControl;assembly=WebUserControl"
   ```

3. **XAML** ペインで、セクションまでスクロールし \<Grid> ます。

    セクションには、 <xref:System.Windows.Controls.TabControl> 要素内の要素が含まれてい <xref:System.Windows.Controls.Grid> ます。

4. \<TabControl>ユーザーコントロールへの参照を含むを含む要素を追加 \<TabItem> します。

    ```xml

    <TabItem Header="Web" Height="Auto">
        <vsc:UserControl1 />
    </TabItem>

    ```

    これで、コントロールをテストできるようになりました。

## <a name="test-a-manually-created-custom-start-page"></a>手動で作成したカスタムスタートページをテストする

1. XAML ファイルと、サポートするテキストファイルまたはマークアップファイルを *%USERPROFILE%\My Documents\Visual Studio 2015 \ StartPages \\* フォルダーにコピーします。

2. スタートページで、Visual Studio によってインストールされていないアセンブリ内のコントロールまたは型が参照されている場合は、アセンブリをコピーし、 _Visual studio のインストールフォルダー_**\Common7\IDE\PrivateAssemblies \\** に貼り付けます。

3. Visual Studio のコマンドプロンプトで、「 **devenv/rootsuffix Exp** 」と入力して、visual studio の実験用インスタンスを開きます。

4. 実験用インスタンスで、[**ツール**  >  **] [オプション]**[環境] [  >  **Environment**  >  **スタートアップ**] ページにアクセスし、[**スタートページのカスタマイズ**] ドロップダウンから XAML ファイルを選択します。

5. **[表示]** メニューの **[スタート ページ]** をクリックします。

    カスタムスタートページが表示されます。 ファイルを変更する場合は、実験用インスタンスを閉じて変更を加え、変更されたファイルをコピーして貼り付けてから、実験用インスタンスを再度開いて変更内容を表示する必要があります。

## <a name="see-also"></a>関連項目

- [WPF コンテナーコントロール](/previous-versions/bb675291(v=vs.110))
- [チュートリアル: スタートページへのカスタム XAML の追加](../extensibility/walkthrough-adding-custom-xaml-to-the-start-page.md)