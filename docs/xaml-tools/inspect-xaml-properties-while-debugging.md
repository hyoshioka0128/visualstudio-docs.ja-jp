---
title: デバッグ中に XAML のプロパティを調べる |Microsoft Docs
ms.date: 11/12/2019
ms.topic: how-to
ms.assetid: 390edde4-7b8d-4c89-8d69-55106b7e6b11
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: 1c8ac187f5602d1c422fe5699d36deee70341b0f
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85331071"
---
# <a name="inspect-xaml-properties-while-debugging"></a>デバッグ中に XAML のプロパティを調べます。

**Live Visual Tree** および **Live Property Explorer** により、実行中の XAML コードのリアルタイム ビューを取得できます。 これらのツールは、実行中の XAML アプリケーションの UI 要素のツリー ビューを提供し、選択した UI 要素のランタイム プロパティを表示します。

これらのツールは、以下の構成で使用できます。

|アプリの種類|オペレーティング システムとツール|
|-----------------|--------------------------------|
|Windows Presentation Foundation (4.0 以上) のアプリケーション|Windows 7 以上|
|ユニバーサル Windows アプリ|Windows 10 以降、 [windows 10 SDK](https://dev.windows.com/downloads/windows-10-sdk)|

## <a name="look-at-elements-in-the-live-visual-tree"></a>ライブビジュアルツリー内の要素を確認する

リスト ビューとボタンのある非常にシンプルな WPF アプリケーションから開始します。 ボタンをクリックするたびに、項目が 1 つずつ一覧に追加されます。 偶数の項目は灰色で表示され、奇数の項目は黄色で表示されます。

### <a name="create-the-project"></a>プロジェクトを作成する

1. 新しい C# WPF アプリケーションを作成し ([**ファイル]**  >  [**新しい**  >  **プロジェクト**] の順に選択し、「C# wpf」と入力して、[ **wpf アプリ (.net Core)** ] または [ **wpf アプリ (.NET Framework)**)] を選択します。 名前を **TestXAML** とします。

1. MainWindow.xaml を次のように変更します。

   ```xaml
   <Window x:Class="TestXAML.MainWindow"
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
      xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
      xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
      xmlns:local="clr-namespace:TestXAML"
      mc:Ignorable="d"
      Title="MainWindow" Height="350" Width="525">
      <Grid>
         <Button x:Name="button" Background="LightBlue" Content="Add Item" HorizontalAlignment="Left" Margin="216,206,0,0" VerticalAlignment="Top" Width="75" Click="button_Click"/>
         <ListBox x:Name="listBox" HorizontalAlignment="Left" Height="100" VerticalAlignment="Top" Width="100" Margin="205,80,0,0"/>
      </Grid>
   </Window>
   ```

1. 以下のコマンド ハンドラーを MainWindow.xaml.cs ファイルに追加します。

   ```csharp
   int count;

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

1. プロジェクトをビルドし、デバッグを開始します。 (ビルド構成はリリースではなくデバッグでなければなりません。 ビルド構成の詳細については、「[ビルド構成](../ide/understanding-build-configurations.md)について」を参照してください。)

   ウィンドウが表示されると、実行中のアプリケーション内にアプリ内ツールバーが表示されます。

   ::: moniker range=">= vs-2019"
   ![アプリのメイン ウィンドウ](../debugger/media/vs-2019/livevisualtree-app.png "LiveVIsualTree-アプリ")
   ::: moniker-end
   ::: moniker range="vs-2017"
   ![アプリのメイン ウィンドウ](../debugger/media/livevisualtree-app.png "LiveVIsualTree-アプリ")
   ::: moniker-end

1. ここで、[**項目の追加**] ボタンを数回クリックして、一覧に新しい項目を追加します。

### <a name="inspect-xaml-properties"></a>XAML プロパティの検査

1. 次に、アプリ内ツールバーの左側のボタンをクリックして (または、[**デバッグ > Windows > ライブビジュアルツリー**)、**ライブビジュアルツリー**ウィンドウを開きます。 開いたままドッキング位置からドラッグして、このウィンドウと**ライブプロパティ**ウィンドウを並べて表示できるようにします。

1. **[Live Visual Tree]** ウィンドウで、**[ContentPresenter]** ノードを展開します。 これにはボタンとリスト ボックスのノードが含まれます。 リスト ボックスを展開し (その後 **ScrollContentPresenter** と **ItemsPresenter** を展開して)、リスト ボックスの項目を検索します。

   ::: moniker range=">= vs-2019"
   **ContentPresenter**ノードが表示されない場合は、ツールバーの [**マイ XAML のみを表示**] アイコンを切り替えます。 Visual Studio 2019 バージョン16.4 以降では、XAML 要素のビューは既定で [マイ XAML] 機能のみを使用して簡略化されています。 [オプション] で[この設定を無効](../debugger/general-debugging-options-dialog-box.md)にして、常にすべての XAML 要素を表示することもできます。
   ::: moniker-end

   ウィンドウは、次のようになります。

   ::: moniker range=">= vs-2019"
   ![ライブ ビジュアル ツリーの ListBoxItems](../debugger/media/vs-2019/livevisualtree-listboxitems.png "LiveVisualTree-ListBoxItems")
   ::: moniker-end
   ::: moniker range="vs-2017"
   ![ライブ ビジュアル ツリーの ListBoxItems](../debugger/media/livevisualtree-listboxitems.png "LiveVisualTree-ListBoxItems")
   ::: moniker-end

1. アプリケーション ウィンドウに戻り、さらにいくつかの項目を追加します。 **[Live Visual Tree]** に、リスト ボックス項目がさらに表示されます。

1. ここで、リストボックス項目の1つのプロパティを見てみましょう。

   **[Live Visual Tree]** 内の最初のリスト ボックス項目を選択して、ツールバーの **[プロパティの表示]** アイコンをクリックします。 **Live Property Explorer** が表示されます。 **コンテンツ**フィールドが "Item1" であり、[**背景**  >  **色**] フィールドが **#FFFFFFE0**であることに注意してください。

1. **[Live Visual Tree]** に戻り、2 番目のリスト ボックス項目を選択します。 **ライブプロパティエクスプローラー**では、**コンテンツ**フィールドが "Item2" で、**背景**  >  **色**フィールドが (テーマによって) **#FFD3D3D3**ことが示されます。

   > [!NOTE]
   > **ライブプロパティエクスプローラー**でプロパティを囲む黄色い枠は、プロパティ値がのようなバインディングによって設定されることを意味し `Color = {BindingExpression}` ます。 緑の境界線は、などのリソースを使用して値が設定されることを意味し `Color = {StaticResource MyBrush}` ます。

   XAML の実際の構造にはご自分に直接関係のない多数の要素が含まれていて、コードをよく理解していない場合は、ツリーを参照して検索対象を見つけることが困難となる可能性があります。 そのため、**Live Visual Tree** には、ご自分でアプリケーションの UI を使用して検討対象の要素を見つけるために役立ついくつかの手段が備わっています。

   ::: moniker range=">= vs-2019"
   **実行中のアプリケーションの要素を選択**します。 **[Live Visual Tree]** ツール バーの左端のボタンを選択すると、このモードを有効にすることができます。 このモードがオンのときは、アプリケーションの UI 要素を選択できます。**Live Visual Tree** (および **Live Property Viewer**) は自動的に更新されて、その要素に対応するツリー内のノードとそのプロパティが表示されます。 Visual Studio 2019 バージョン16.4 以降では、[要素の選択の動作を構成](../debugger/general-debugging-options-dialog-box.md)できます。

   **実行中のアプリケーションでレイアウトの装飾を表示する**。 選択を有効にするためのボタンのすぐ右にあるボタンを選択すると、このモードを有効にすることができます。 **レイアウトの装飾の表示**がオンのときは、アプリケーション ウィンドウには選択されたオブジェクトの境界に沿って水平と垂直の線が表示され、何に揃えて配置されているかが確認できます。さらに、余白を示すための四角形も表示されます。 たとえば、 **[要素の選択]** と [**レイアウトの表示**] の両方をオンにして、アプリケーションで [項目の**追加**] テキストブロックを選択します。 **Live Visual Tree** にテキスト ブロック ノードが表示され、**Live Property Viewer** にテキスト ブロック プロパティが表示されます。さらに、テキスト ブロックの境界に垂直な線と水平な線が示されます。

   ![DisplayLayout の  LivePropertyViewer](../debugger/media/vs-2019/livevisualtreelivepropertyviewer-displaylayout.png "LiveVisualTreeLivePropertyViewer-DisplayLayout")

   **選択のプレビュー**。 このモードを有効にするには、Visual Tree ツールバーで左端から 3 番目のボタンを選択します。 このモードは、アプリケーションのソース コードにアクセスできる場合に、要素が宣言されている XAML を示します。 [**要素の選択**] と [**選択範囲のプレビュー**] を選択し、テストアプリケーションでボタンを選択します。 MainWindow.xaml ファイルが Visual Studio で開き、ボタンが定義されている行にカーソルが置かれます。
   ::: moniker-end

   ::: moniker range="vs-2017"
   **実行中のアプリケーションで選択を有効にする**。 **[Live Visual Tree]** ツール バーの左端のボタンを選択すると、このモードを有効にすることができます。 このモードがオンのときは、アプリケーションの UI 要素を選択できます。**Live Visual Tree** (および **Live Property Viewer**) は自動的に更新されて、その要素に対応するツリー内のノードとそのプロパティが表示されます。

   **実行中のアプリケーションでレイアウトの装飾を表示する**。 選択を有効にするためのボタンのすぐ右にあるボタンを選択すると、このモードを有効にすることができます。 **レイアウトの装飾の表示**がオンのときは、アプリケーション ウィンドウには選択されたオブジェクトの境界に沿って水平と垂直の線が表示され、何に揃えて配置されているかが確認できます。さらに、余白を示すための四角形も表示されます。 たとえば、**[選択範囲を有効にする]** と **[Display layout]\(レイアウト表示\)** の両方をオンにして、アプリケーションの **[項目の追加]** テキスト ブロックを選択します。 **Live Visual Tree** にテキスト ブロック ノードが表示され、**Live Property Viewer** にテキスト ブロック プロパティが表示されます。さらに、テキスト ブロックの境界に垂直な線と水平な線が示されます。

   ![DisplayLayout の  LivePropertyViewer](../debugger/media/livevisualtreelivepropertyviewer-displaylayout.png "LiveVisualTreeLivePropertyViewer-DisplayLayout")

   **選択のプレビュー**。 このモードを有効にするには、Visual Tree ツールバーで左端から 3 番目のボタンを選択します。 このモードは、アプリケーションのソース コードにアクセスできる場合に、要素が宣言されている XAML を示します。 **[選択範囲を有効にする]** と **[Preview Selection]\(選択のプレビュー\)** を選択してから、テスト アプリケーションのボタンを選択します。 MainWindow.xaml ファイルが Visual Studio で開き、ボタンが定義されている行にカーソルが置かれます。
   ::: moniker-end

## <a name="use-xaml-tools-with-running-applications"></a>実行中のアプリケーションで XAML ツールを使用する

ソース コードがない場合でも、これらの XAML ツールを使用できます。 実行中の XAML アプリケーションにアタッチすると、そのアプリケーションの UI 要素の **Live Visual Tree** も使用できます。 以前に使用したものと同じ WPF テスト アプリケーションを使用する例を次に示します。

1. リリース構成で、**TestXaml** アプリケーションを始動します。 **デバッグ**構成で実行しているプロセスにはアタッチできません。

2. Visual Studio の 2 番目のインスタンスを開き、**[デバッグ] > [プロセスにアタッチ]** をクリックします。 選択可能なプロセスの一覧から **TestXaml.exe** を見つけて、**[アタッチ]** をクリックします。

3. アプリケーションが実行を開始します。

4. Visual Studio の 2 番目のインスタンスで、**Live Visual Tree** を開きます (**[デバッグ] > [Windows] > [Live Visual Tree]**)。 **TestXaml** UI 要素が表示され、アプリケーションを直接デバッグしたときと同様に、それらを操作することができます。

## <a name="see-also"></a>関連項目

[XAML ホットリロードを使用して実行中の XAML コードを記述およびデバッグする](xaml-hot-reload.md)
