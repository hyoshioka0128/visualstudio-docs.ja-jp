---
title: デバッグ中に XAML のプロパティを調べる |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 390edde4-7b8d-4c89-8d69-55106b7e6b11
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 52d978472f057359cb2b1e0375f2d7ba524d1925
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62423856"
---
# <a name="inspect-xaml-properties-while-debugging"></a>デバッグ中に XAML のプロパティを調べます。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**Live Visual Tree** および **Live Property Explorer** により、実行中の XAML コードのリアルタイム ビューを取得できます。 これらのツールは、実行中の XAML アプリケーションの UI 要素のツリー ビューを提供し、選択した UI 要素のランタイム プロパティを表示します。  
  
 これらのツールは、以下の構成で使用できます。  
  
|アプリの種類|オペレーティング システムとツール|  
|-----------------|--------------------------------|  
|Windows Presentation Foundation (4.0 以上) のアプリケーション|Windows 7 以上|  
|Windows ストアおよび Windows Phone 8.1 のアプリ|Windows 10 以降、 [windows 10 SDK](https://dev.windows.com/downloads/windows-10-sdk)|  
|Universal Windows アプリ|Windows 10 以降、 [windows 10 SDK](https://dev.windows.com/downloads/windows-10-sdk)|  
  
## <a name="looking-at-elements-in-the-live-visual-tree"></a>Live Visual Tree 内の要素の表示  
 リスト ビューとボタンのある非常に単純な WPF アプリケーションから開始します。 ボタンをクリックするたびに、項目が 1 つずつ一覧に追加されます。 偶数の項目は灰色で表示され、奇数の項目は黄色で表示されます。  
  
 新しい C# WPF アプリケーションを作成します ([ファイル] / [新規作成] / [プロジェクト]、その後 [C#] を選択して [WPF アプリケーション] を探します)。 名前を **TestXAML** とします。  
  
 MainWindow.xaml を次のように変更します。  
  
```xaml  
<Window x:Class="WpfApplication1.MainWindow"  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"  
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
    xmlns:local="clr-namespace:WpfApplication1"  
    mc:Ignorable="d"  
     Title="MainWindow" Height="350" Width="525">  
    <Grid>  
        <Button x:Name="button" Background="LightBlue" Content="Add Item" HorizontalAlignment="Left" Margin="216,206,0,0" VerticalAlignment="Top" Width="75" Click="button_Click"/>  
        <ListBox x:Name="listBox" HorizontalAlignment="Left" Height="100" VerticalAlignment="Top" Width="100" Margin="205,80,0,0"/>  
    </Grid>  
</Window>  
```  
  
 以下のコマンド ハンドラーを MainWindow.xaml.cs ファイルに追加します。  
  
```csharp  
private void button_Click(object sender, RoutedEventArgs e)  
{  
    ListBoxItem item = new ListBoxItem();  
    item.Content = "Item" + ++count;  
    if (count % 2 == 0)  
    {  
        item.Background = Brushes.LightGray;  
    }  
    else  
    {  
        item.Background = Brushes.LightYellow;  
    }  
    listBox.Items.Add(item);  
}  
```  
  
 プロジェクトをビルドし、デバッグを開始します。 (ビルド構成はリリースではなくデバッグでなければなりません。 ビルド構成の詳細については、「 [ビルド構成](../ide/understanding-build-configurations.md)について」を参照してください。)  
  
 ウィンドウが表示されたら、**[項目の追加]** ボタンを数回クリックします。 次のような結果が表示されます。  
  
 ![アプリのメイン ウィンドウ](../debugger/media/livevisualtree-app.png "LiveVIsualTree-アプリ")  
  
 次に、 **ライブビジュアルツリー** ウィンドウを開きます ([**デバッグ]/[Windows]/[ライブ] ビジュアルツリー**を開くか、IDE の左側で検索します)。 このウィンドウをドッキング位置からドラッグして離し、**[Live Properties]** ウィンドウと横並びになるようにします。 **[Live Visual Tree]** ウィンドウで、**[ContentPresenter]** ノードを展開します。 これにはボタンとリスト ボックスのノードが含まれます。 リスト ボックスを展開し (その後 **ScrollContentPresenter** と **ItemsPresenter** を展開して)、リスト ボックスの項目を検索します。 ウィンドウは、次のようになります。  
  
 ![ライブ ビジュアル ツリーの ListBoxItems](../debugger/media/livevisualtree-listboxitems.png "LiveVisualTree-ListBoxItems")  
  
 アプリケーション ウィンドウに戻り、さらにいくつかの項目を追加します。 **[Live Visual Tree]** に、リスト ボックス項目がさらに表示されます。  
  
 次に、いずれかのリスト ボックス項目のプロパティを検討します。 **[Live Visual Tree]** 内の最初のリスト ボックス項目を選択して、ツールバーの **[プロパティの表示]** アイコンをクリックします。 **Live Property Explorer** が表示されます。 **コンテンツ**フィールドが "Item1" であり、**背景**フィールドが **#FFFFFFE0** (明るい黄色) であることに注意してください。 **[Live Visual Tree]** に戻り、2 番目のリスト ボックス項目を選択します。 **ライブプロパティエクスプローラー**では、**コンテンツ**フィールドが "Item2" であり、[**背景**] フィールドが **#FFD3D3D3** (淡い灰色) であることが示されます。  
  
 XAML の実際の構造にはユーザーに直接関係のない多数の要素が含まれていて、コードをよく理解していない場合は、ツリーを参照して検索対象を見つけることが困難となる可能性があります。 そのため、 **ライブビジュアルツリー** にはいくつかの方法があり、アプリケーションの UI を使用して、確認する要素を見つけることができます。  
  
 **実行中のアプリケーションで選択を有効にする**。 **[Live Visual Tree]** ツール バーの左端のボタンを選択すると、このモードを有効にすることができます。 このモードがオンのときは、アプリケーションの UI 要素を選択できます。**Live Visual Tree** (および **Live Property Viewer**) は自動的に更新されて、その要素に対応するツリー内のノードとそのプロパティが表示されます。  
  
 **実行中のアプリケーションでレイアウトの装飾を表示する**。 選択を有効にするためのボタンのすぐ右にあるボタンを選択すると、このモードを有効にすることができます。 **レイアウトの装飾の表示**がオンのときは、アプリケーション ウィンドウには選択されたオブジェクトの境界に沿って水平と垂直の線が表示され、何に揃えて配置されているかが確認できます。さらに、余白を示すための四角形も表示されます。 たとえば、**[選択範囲を有効にする]** と **[Display layout]\(レイアウト表示\)** の両方をオンにして、アプリケーションの **[項目の追加]** テキスト ブロックを選択します。 **Live Visual Tree** にテキスト ブロック ノードが表示され、**Live Property Viewer** にテキスト ブロック プロパティが表示されます。さらに、テキスト ブロックの境界に垂直な線と水平な線が示されます。  
  
 ![DisplayLayout の  LivePropertyViewer](../debugger/media/livevisualtreelivepropertyviewer-displaylayout.png "LiveVisualTreeLivePropertyViewer-DisplayLayout")  
  
 **選択のプレビュー**。 このモードを有効にするには、Visual Tree ツールバーで左端から 3 番目のボタンを選択します。 このモードは、アプリケーションのソース コードにアクセスできる場合に、要素が宣言されている XAML を示します。 **[選択範囲を有効にする]** と **[Preview Selection]\(選択のプレビュー\)** を選択してから、テスト アプリケーションのボタンを選択します。 MainWindow.xaml ファイルが Visual Studio で開き、ボタンが定義されている行にカーソルが置かれます。  
  
## <a name="using-xaml-tools-with-running-applications"></a>実行中のアプリケーションで XAML のツールを使用する  
 ソース コードがない場合でも、これらの XAML ツールを使用できます。 実行中の XAML アプリケーションにアタッチすると、そのアプリケーションの UI 要素の **Live Visual Tree** も使用できます。 以前に使用したものと同じ WPF テスト アプリケーションを使用する例を次に示します。  
  
1. リリース構成で、**TestXaml** アプリケーションを始動します。 **デバッグ**構成で実行しているプロセスにはアタッチできません。  
  
2. Visual Studio の2番目のインスタンスを開き、[デバッグ]、[ **プロセスにアタッチ**] の順にクリックします。 選択可能なプロセスの一覧から **TestXaml.exe** を見つけて、**[アタッチ]** をクリックします。  
  
3. アプリケーションが実行を開始します。  
  
4. Visual Studio の2番目のインスタンスで、 **ライブビジュアルツリー** を開きます ([**デバッグ]/[Windows]/[live visual tree**])。 **TestXaml** UI 要素が表示され、アプリケーションを直接デバッグしたときと同様に、それらを操作することができます。
