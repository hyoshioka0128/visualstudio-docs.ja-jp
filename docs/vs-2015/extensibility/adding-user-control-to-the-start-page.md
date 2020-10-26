---
title: スタートページにユーザーコントロールを追加する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- start page dll
- custom start page
- start page assembly
ms.assetid: 5b7997db-af6f-4fa9-a128-bceb42bddaf1
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1171197ba55c2fe3fa59ccc9ca918fa0c8f9e727
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65699127"
---
# <a name="adding-user-control-to-the-start-page"></a>スタート ページへのユーザー コントロールの追加
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、カスタムスタートページに DLL 参照を追加する方法について説明します。 この例では、ユーザーコントロールをソリューションに追加し、ユーザーコントロールをビルドしてから、ビルドされたアセンブリをスタートページ .xaml ファイルから参照します。 新しいタブでは、基本的な Web ブラウザーとして機能するユーザーコントロールをホストします。  
  
 同じプロセスを使用して、.xaml ファイルから呼び出すことのできるアセンブリを追加できます。  
  
## <a name="adding-a-wpf-user-control-to-the-solution"></a>ソリューションへの WPF ユーザーコントロールの追加  
 最初に、スタートページソリューションに Windows Presentation Foundation (WPF) ユーザーコントロールを追加します。  
  
1. 「 [カスタムスタートページの作成](../extensibility/creating-a-custom-start-page.md)」で作成したを使用してスタートページを作成します。  
  
2. **ソリューション エクスプローラー**で該当ソリューションを右クリックして **[追加]** をクリックし、 **[新しいプロジェクト]** をクリックします。  
  
3. [ **新しいプロジェクト** ] ダイアログボックスの左ペインで、[ **Visual Basic** ] または [ **Visual C#** ] ノードのいずれかを展開し、[ **Windows**] をクリックします。 中央のペインで、[ **WPF ユーザーコントロールライブラリ**] を選択します。  
  
4. コントロールに名前を指定し、 `WebUserControl` [ **OK]** をクリックします。  
  
## <a name="implementing-the-user-control"></a>ユーザーコントロールの実装  
 WPF ユーザーコントロールを実装するには、XAML でユーザーインターフェイス (UI) をビルドし、C# または他の .NET 言語で分離コードイベントを記述します。  
  
#### <a name="to-write-the-xaml-for-the-user-control"></a>ユーザーコントロールの XAML を記述するには  
  
1. ユーザーコントロールの XAML ファイルを開きます。 要素で \<Grid> 、次の行定義をコントロールに追加します。  
  
    ```vb  
    <Grid.RowDefinitions>  
        <RowDefinition Height="Auto"/>  
        <RowDefinition Height="*" />  
    </Grid.RowDefinitions>  
  
    ```  
  
2. Main 要素に `Grid` 次の新しい要素を追加します。この要素には `Grid` 、Web アドレスを入力するためのテキストボックスと、新しいアドレスを設定するためのボタンが含まれています。  
  
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
  
3. 次のフレームを、 `Grid` `Grid` ボタンとテキストボックスを含む要素の直後にある最上位の要素に追加します。  
  
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
  
#### <a name="to-write-the-code-behind-events-for-the-user-control"></a>ユーザーコントロールの分離コードイベントを作成するには  
  
1. XAML デザイナーで、コントロールに追加した [ **アドレスの設定** ] ボタンをダブルクリックします。  
  
     コードエディターで UserControl1.cs ファイルが開きます。  
  
2. SetButton_Click イベントハンドラーに次のように入力します。  
  
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
  
     このコードは、テキストボックスに入力された Web アドレスを Web ブラウザーのターゲットとして設定します。 アドレスが有効でない場合、コードはエラーをスローします。  
  
3. また、WebFrame_Navigated イベントも処理する必要があります。  
  
    ```csharp  
    private void WebFrame_Navigated(object sender, EventArgs e)  
    { }  
    ```  
  
4. ソリューションをビルドします。  
  
## <a name="adding-the-user-control-to-the-start-page"></a>スタートページへのユーザーコントロールの追加  
 スタートページプロジェクトでこのコントロールを使用できるようにするには、スタートページのプロジェクトファイルで、新しいコントロールライブラリへの参照を追加します。 その後、スタートページの XAML マークアップにコントロールを追加できます。  
  
1. **ソリューションエクスプローラー**のスタートページプロジェクトで、[**参照**] を右クリックし、[**参照の追加**] をクリックします。  
  
2. [ **プロジェクト** ] タブで [ **Webusercontrol** ] を選択し、[ **OK**] をクリックします。  
  
3. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。  
  
    ソリューションをビルドすると、ソリューション内の他のファイルの IntelliSense でユーザーコントロールを使用できるようになります。  
  
   スタートページの XAML マークアップにコントロールを追加するには、アセンブリへの名前空間参照を追加してから、コントロールをページに配置します。  
  
#### <a name="to-add-the-control-to-the-markup"></a>マークアップにコントロールを追加するには  
  
1. **ソリューションエクスプローラー**で、スタートページの .xaml ファイルを開きます。  
  
2. **XAML**ペインで、最上位レベルの要素に次の名前空間宣言を追加し <xref:System.Windows.Controls.Grid> ます。  
  
   ```xml  
   xmlns:vsc="clr-namespace:WebUserControl;assembly=WebUserControl"  
   ```  
  
3. **XAML**ペインで、セクションまでスクロールし \<Grid> ます。  
  
    セクションには、 <xref:System.Windows.Controls.TabControl> 要素内の要素が含まれてい <xref:System.Windows.Controls.Grid> ます。  
  
4. \<TabControl>ユーザーコントロールへの参照を含むを含む要素を追加 \<TabItem> します。  
  
   ```xml  
  
   <TabItem Header="Web" Height="Auto">  
       <vsc:UserControl1 />  
   </TabItem>  
  
   ```  
  
   これで、コントロールをテストできるようになりました。  
  
## <a name="testing-a-manually-created-custom-start-page"></a>手動で作成したカスタムスタートページのテスト  
  
1. XAML ファイルと、サポートするテキストファイルまたはマークアップファイルを **%USERPROFILE%\My Documents\Visual Studio 2015 \ StartPages \\ **フォルダーにコピーします。  
  
2. スタートページで、Visual Studio によってインストールされていないアセンブリ内のコントロールまたは型が参照されている場合は、アセンブリをコピーし、 _Visual studio のインストールフォルダー_**\Common7\IDE\PrivateAssemblies \\ **に貼り付けます。  
  
3. Visual Studio のコマンドプロンプトで、「 **devenv/rootsuffix Exp** 」と入力して、visual studio の実験用インスタンスを開きます。  
  
4. 実験用インスタンスで、[ツール]、[ **オプション]** 、[環境]、[スタートアップ] ページの順に選択し、[ **スタートページのカスタマイズ** ] ドロップダウンから XAML ファイルを選択します。  
  
5. **[表示]** メニューの **[スタート ページ]** をクリックします。  
  
     カスタムスタートページが表示されます。 ファイルを変更する場合は、実験用インスタンスを閉じて変更を加え、変更されたファイルをコピーして貼り付けてから、実験用インスタンスを再度開いて変更内容を表示する必要があります。  
  
## <a name="see-also"></a>参照  
 [WPF コンテナーコントロール](https://msdn.microsoft.com/a0177167-d7db-4205-9607-8ae316952566)   
 [チュートリアル: カスタム XAML をスタート ページに追加する](../extensibility/walkthrough-adding-custom-xaml-to-the-start-page.md)
