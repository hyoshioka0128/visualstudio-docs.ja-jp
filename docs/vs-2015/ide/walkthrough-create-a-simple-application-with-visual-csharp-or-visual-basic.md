---
title: 'チュートリアル : Visual C# または Visual Basic による簡単なアプリケーションの作成 | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: f84339c7-d617-4f56-bfcd-af2215c347ba
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d5e41dbf3422374add68e351da1e4b703772a3a4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "74296859"
---
# <a name="walkthrough-create-a-simple-application-with-visual-c-or-visual-basic"></a>チュートリアル : Visual C# または Visual Basic による簡単なアプリケーションの作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルを完了すると、Visual Studio を使用してアプリケーションを開発する際に使用できるさまざまなツール、ダイアログ ボックス、およびデザイナーの使用方法を習得できます。 簡単な "Hello, World" スタイルのアプリケーションの作成、UI の設計、コードの追加、およびエラーのデバッグを行いながら、統合開発環境 (IDE) での作業方法について学習します。

 このトピックには、次のセクションが含まれます。

 [IDE の構成](../ide/walkthrough-create-a-simple-application-with-visual-csharp-or-visual-basic.md#BKMK_ConfigureIDE)

 [単純なアプリケーションを作成する](../ide/walkthrough-create-a-simple-application-with-visual-csharp-or-visual-basic.md#BKMK_CreateApp)

 [アプリケーションのデバッグとテスト](../ide/walkthrough-create-a-simple-application-with-visual-csharp-or-visual-basic.md#BKMK_DebugTest)

> [!NOTE]
> このチュートリアルでは、Visual Studio Professional の WPF アプリケーション テンプレートに基づいて、チュートリアル用のプロジェクトを作成します。 このテンプレートは Visual Studio Express for Windows Desktop には用意されていますが、Visual Studio Express for Windows と Visual Studio Express for Web には用意されていません。 Visual Studio Express for Windows の使用方法の概要については、デベロッパー センターの「 [Windows ストア アプリの開発](https://msdn.microsoft.com/windows/apps/br229519)」を参照してください。 Visual Studio Express for Web の使用方法の概要については、「 [Get Started with ASP.NET](https://dotnet.microsoft.com/learn/aspnet/hello-world-tutorial/intro)」 (ASP.NET の概要) を参照してください。 さらに、使用する Visual Studio のエディションと設定によって、ユーザー インターフェイスの一部の要素の名前や場所は異なります。 [Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)を参照してください。

## <a name="configure-the-ide"></a><a name="BKMK_ConfigureIDE"></a> IDE を構成する
 Visual Studio を初めて起動すると、Visual Studio から、Microsoft サービス アカウント (MSA) でサインイン ( [Visual Studio にサインイン](https://devblogs.microsoft.com/visualstudio/welcome-sign-in-to-visual-studio/)) するように求められます。 サインインは必須ではなく、後で実行することもできます。

 Visual Studio が起動すると、次に IDE に定義済みの一連のカスタマイズを適用する設定の組み合わせを選択する必要があります。 各設定の組み合わせは、アプリケーションを簡単に開発できるように設計されています。

 このチュートリアルは、 **[全般的な開発設定]** を適用したと想定しています。この場合、最小限のカスタマイズが IDE に適用されます。 すでに C# か Visual Basic を選択済みの場合は (両方とも適切な選択です)、設定を変更する必要はありません。  設定を変更する場合は、 **設定のインポートとエクスポート ウィザード**を使用できます。 [Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)を参照してください。

 Visual Studio を開くと、ツール ウィンドウ、メニューとツール バー、およびメイン ウィンドウ領域を確認できます。 ツール ウィンドウは、アプリケーション ウィンドウの左側および右側にドッキングされており、上部には **クイック起動**、メニュー バー、および標準ツール バーがあります。 アプリケーション ウィンドウの中央には、 **スタート ページ**が表示されます。 ソリューションかプロジェクトが読み込まれると、 **[スタート ページ]** がある領域にエディターとデザイナーが表示されます。 アプリケーションを開発する場合は、ほとんどの時間をこの中央の領域での作業に費やします。

 図 2: Visual Studio IDE

 ![全般設定が適用された IDE](../ide/media/exploreide-idewithgeneralsettings.png "Exploreide-newprojectcsharp-Ide の全般設定")

 **[オプション]** ダイアログ ボックスを使用すると、Visual Studio をさらにカスタマイズできます。たとえば、エディターのテキストのフォント フェイスとサイズや IDE の配色テーマを変更できます。 適用した設定の組み合わせによっては、そのダイアログ ボックスに自動的に表示されない項目があります。 **[すべての設定を表示]** チェック ボックスをオンにすると、使用可能なすべてのオプションを表示できます。

 図 3: [オプション] ダイアログ ボックス

 ![[すべての設定を表示] オプションをオンにした [オプション] ダイアログ ボックス](../ide/media/exploreide-optionsdialogbox.png "Exploreide-newprojectcsharp-オプションダイアログ")

 この例では、IDE の配色テーマを淡色から濃色に変更します。  望むなら、プロジェクトの作成に進むこともできます。

#### <a name="to-change-the-color-theme-of-the-ide"></a>IDE の配色テーマを変更するには

1. 上部の **[オプション]** メニューを選択してから **[オプション]** 項目を選択し、 **[オプション] …** ダイアログ ボックスを開きます。

    ![[ツール] メニューの [オプション] コマンド](../ide/media/exploreide-toolsoptionsmenu.png "Exploreide-newprojectcsharp-ToolsOptionsmenu")

2. **[配色テーマ]** を **[濃色]** に変更して、 **[OK]** をクリックします。

    ![暗い配色テーマが選択されています](../ide/media/exploreide-darkthemeoptionsdlgbox.png "Exploreide-newprojectcsharp-Darkthemeoptionsdlgbox")

   Visual Studio の配色が次のイメージと一致する必要があります。

   ![ダーク テーマを適用した IDE](../ide/media/exploreide-darkthemeide.png "Exploreide-newprojectcsharp-DarkThemeIDE")

   このチュートリアルの残りの画像で使用する配色テーマは淡色テーマです。 IDE のカスタマイズの詳細については、「 [Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

## <a name="create-a-simple-application"></a><a name="BKMK_CreateApp"></a> 単純なアプリケーションを作成する

### <a name="create-the-project"></a>プロジェクトの作成
 Visual Studio でアプリケーションを作成するには、最初にプロジェクトおよびソリューションを作成します。 この例では、Windows Presentation Foundation (WPF) プロジェクトを作成します。

##### <a name="to-create-the-wpf-project"></a>WPF プロジェクトを作成するには

1. 新しいプロジェクトを作成します。 メニューバーで、[ **ファイル**]、[ **新規作成**]、[ **プロジェクト...**] の順に選択します。

    ![メニューバーで、[ファイル]、[新規作成]、[プロジェクト] の順に選択します。](../ide/media/exploreide-filenewproject.png "Exploreide-newprojectcsharp-FileNewProject")

    また、[ **クイック起動** ] ボックスに「 **新しいプロジェクト** 」と入力しても、同じことができます。

    ![クイック起動ボックスで新しいプロジェクトを指定](../ide/media/exploreide-quicklaunchnewprojectsmall.png "Exploreide-newprojectcsharp-QuickLaunchNewProjectsmall")

2. たとえば、左側のペインで **[インストール済み]**、 **[テンプレート]**、 **[Visual C#]**、 **[Windows]** の順に選択してから、中央のペインで [WPF アプリケーション] を選択して、Visual Basic か Visual C# の WPF アプリケーション テンプレートを選択します。  下部の [新しいプロジェクト] ダイアログで、プロジェクトに HelloWPFApp という名前を付けます。

    ![Visual Basic WPF プロジェクトの作成、HelloWPFApp](../ide/media/exploreide-newprojectvb.png "Exploreide-newprojectcsharp-NewProjectVB")

    OR

    ![Visual C&#35; WPF プロジェクト、アプリケーションの作成](../ide/media/exploreide-newprojectcsharp.png "Exploreide-newprojectcsharp-NewProjectcsharp")

   Visual Studio は HelloWPFApp というプロジェクトとソリューションを作成し、 **ソリューション エクスプローラー** は各種ファイルを表示します。 WPF デザイナーは、MainWindow.xaml のデザイン ビューと XAML ビューを分割ビューに表示します。 分割線をスライドして、それぞれのビューの表示範囲を増減できます。  ビジュアル ビューか XAML ビューの一方のみを表示することも選択できます。 (詳細については、「 [Windows フォーム開発者向けの WPF デザイナー](https://msdn.microsoft.com/47ad0909-e89b-4996-b4ac-874d929f94ca)」を参照してください)。 次の項目が **ソリューション エクスプローラー**に表示されます。

   図 5: プロジェクト項目

   ![HelloWPFApp ファイルを読み込んだソリューション エクスプローラー](../ide/media/exploreide-hellowpfappfiles.png "Exploreide-newprojectcsharp--------ファイル")

   プロジェクトは、作成後にカスタマイズできます。 **[プロパティ]** ウィンドウ ( **[表示]** メニュー上) を使って、プロジェクト項目、コントロール、およびアプリケーション内のその他の項目に関するオプションを表示して変更できます。 プロジェクトのプロパティおよびプロパティ ページを使用すると、プロジェクトおよびソリューションのオプションを表示および変更できます。

##### <a name="to-change-the-name-of-mainwindowxaml"></a>MainWindow.xaml の名前を変更するには

1. 次の手順では、MainWindow にもっと具体的な名前を付けます。 **ソリューション エクスプローラー**で、MainWindow.xaml を選択します。 **[プロパティ]** ウィンドウが表示されているはずですが、表示されない場合は、 **[表示]** メニューをクリックし、 **[プロパティ ウィンドウ]** 項目をクリックします。 **[File Name]** プロパティを `Greetings.xaml`に変更します。

    ![ファイル名が強調表示されたプロパティ ウィンドウ](../ide/media/exploreide-filenameinpropertieswindow.png "Exploreide-newprojectcsharp-FilenameinPropertiesWindow")

    ファイルの名前が Greetings.xaml になったことが**ソリューション エクスプローラー** に示され、MainWindow.xaml ノードを展開する (ノードにフォーカスを設定し、右矢印キーを押す) と、MainWindow.xaml.vb または MainWindow.xaml.cs の名前が Greetings.xaml.vb または Greetings.xaml.cs になったことが示されます。 このコード ファイルは、.xaml ファイル ノードの下に入れ子になっており、相互に非常に密接に関連していることが示されます。

   > [!WARNING]
   > この変更により、エラーが発生します。後の手順で、このエラーをデバッグして修正する方法を学習します。

2. **ソリューション エクスプローラー**で、Greetings.xaml をデザイナー ビューで開き (ノードにフォーカスがあるときに Enter キーを押す) 、マウスを使ってウィンドウのタイトル バーを選択します。

3. **[プロパティ]** ウィンドウで、 **[Title]** プロパティの値を `Greetings`に変更します。

   MainWindow.xaml のタイトル バーに Greetings と表示されます。

### <a name="design-the-user-interface-ui"></a>ユーザー インターフェイス (UI) のデザイン
 このアプリケーションに 3 種類のコントロール (TextBlock コントロール、2 つの RadioButton コントロール、および Button コントロール) を追加します。

##### <a name="to-add-a-textblock-control"></a>TextBlock コントロールを追加するには

1. **[表示]** メニュー、 **[ツールボックス]** 項目の順に選択し、 **[ツールボックス]** ウィンドウを開きます。

2. **[ツールボックス]** で、TextBlock コントロールを探します。

    ![TextBlock コントロールを強調表示したツールボックス](../ide/media/exploreide-textblocktoolbox.png "Exploreide-newprojectcsharp-TextBlockToolbox")

3. TextBlock 項目を選択してデザイン サーフェイス上のウィンドウにドラッグし、TextBlock コントロールをデザイン サーフェイスに追加します。  ウィンドウの上部付近の中央にコントロールを配置します。

   ウィンドウは次の図のようになります。

   図 7: TextBlock コントロールが配置されている Greetings ウィンドウ

   ![グリーティング フォームの TextBlock コントロール](../ide/media/exploreide-greetingswithtextblockonly.png "Exploreide-newprojectcsharp-GreetingswithTextblockonly")

   XAML マークアップは、次のようになります。

```
<TextBlock HorizontalAlignment="Center" TextWrapping="Wrap" VerticalAlignment="Center" RenderTransformOrigin="4.08,2.312" Margin="237,57,221,238"><Run Text="TextBlock"/><InlineUIContainer><TextBlock TextWrapping="Wrap" Text="TextBlock"/>
```

##### <a name="to-customize-the-text-in-the-text-block"></a>テキスト ブロックのテキストをカスタマイズするには

1. XAML ビューで、TextBlock のマークアップを探し、Text 属性を `Text=”Select a message option and then choose the Display button.”` に変更します。

2. デザイン ビューで TextBlock が拡張されない場合は、テキストがすべて表示されるように (端のグラブ ハンドルを使って) TextBlock コントロールを拡大します。

3. Ctrl-s を押すか **[ファイル]** メニュー項目を使って、変更を保存します。

   次に、2つの [RadioButton](https://msdn.microsoft.com/library/6c9ba847-eab7-4bba-9c74-6b56ef72067b) コントロールをフォームに追加します。

##### <a name="to-add-radio-buttons"></a>オプション ボタンを追加するには

1. **[ツールボックス]** で、RadioButton コントロールを探します。

    ![RadioButton コントロールをオンにした [ツールボックス] ウィンドウ](../ide/media/exploreide-radiobuttontoolbox.png "Exploreide-newprojectcsharp-RadioButtonToolbox")

2. 2 回 RadioButton 項目を選択してデザイン サーフェイス上のウィンドウにドラッグし、2 個の RadioButton コントロールをデザイン サーフェイスに追加して、TextBlock コントロールの下に横に並んで表示されるように (選択して矢印キーを使って) ボタンを移動します。

    ウィンドウは、次のようになります。

    図 8: Greetings ウィンドウの RadioButton

    ![テキストブロックと 2 つのオプション ボタンのあるグリーティング フォーム](../ide/media/exploreide-greetingswithradiobuttons.png "Exploreide-newprojectcsharp-Greetingswithradiobuttons")

3. 左側の RadioButton コントロールの **[プロパティ]** ウィンドウで、 **[Name]** プロパティ ( **[プロパティ]** ウィンドウの一番上のプロパティ) を `RadioButton1`に変更します。  フォーム上で Radiobutton を選択し、背景のグリッドを選択していないことを確認します。 [プロパティ] ウィンドウの [Name] フィールドの下の [Type] フィールドに Radiobutton が表示されるはずです。

4. 右側の RadioButton コントロールの **[プロパティ]** ウィンドウで、 **[Name]** プロパティを `RadioButton2`に変更し、Ctrl-s を押すか **[ファイル]** メニュー項目を使って変更を保存します。  変更して保存する前に、RadioButton を選択したことを確認してください。

   これで、各 RadioButton コントロールの表示テキストを追加できます。 次の手順では、RadioButton コントロールの **[Content]** プロパティを更新します。

##### <a name="to-add-display-text-for-each-radio-button"></a>各オプション ボタンの表示テキストを追加するには

1. デザイン サーフェイスで、RadioButton1 を選択しながら右マウス ボタンを押して RadioButton1 のショートカット メニューを開き、 **[テキストの編集]** を選択し、「 `Hello`」と入力します。

2. RadioButton2 を選択しながら右マウス ボタンを押して RadioButton2 のショートカット メニューを開き、 **[テキストの編集]** を選択し、「 `Goodbye`」と入力します。

   最後に追加する UI 要素は、 [ボタン](https://msdn.microsoft.com/library/a9d8f5a5-c98c-463e-808a-5a4e63173098) コントロールです。

##### <a name="to-add-the-button-control"></a>Button コントロールを追加するには

1. **[ツールボックス]** で、 **Button** コントロールを探し、Button を選択してデザイン ビュー内のフォームにドラッグし、デザイン サーフェイスの RadioButton コントロールの下に追加します。

2. IXAML ビューで、Button コントロールの **[Content]** の値を `Content=”Button”` から `Content=”Display”`に変更し、変更を保存します (Ctrl-s または **[ファイル]** メニューを使用)。

    マークアップは、次の例のようになります。`<Button Content="Display" HorizontalAlignment="Left" VerticalAlignment="Top" Width="75" Margin="215,204,0,0"/>`

   ウィンドウは次の図のようになります。

   図 9: Greetings の最後の UI

   ![コントロール ラベルのあるグリーティング フォーム](../ide/media/exploreide-greetingswithconrollabels.png "Exploreide-newprojectcsharp-Greetingswithconrollabels")

### <a name="add-code-to-the-display-button"></a>Display ボタンのコードの追加
 このアプリケーションを実行すると、ユーザーがオプション ボタンを選択した後で **[Display]** ボタンを選択したときに、メッセージ ボックスが表示されます。 1 つのメッセージ ボックスには "Hello" と表示され、もう 1 つメッセージ ボックスには "Goodbye" と表示されます。 この動作を作成するために、Greetings.xaml.vb または Greetings.xaml.cs の Button_Click イベントにコードを追加します。

##### <a name="add-code-to-display-message-boxes"></a>メッセージ ボックスを表示するコードの追加

1. デザイン サーフェイスで、 **[Display]** ボタンをダブルクリックします。

     Greetings.xaml.vb または Greetings.xaml.cs が開き、Button_Click イベントにカーソルが表示されます。 また、次のようにクリック イベント ハンドラーを追加することもできます (貼り付けたコード内の名前の下に赤い波線がある場合、デザイン サーフェイス上で RadioButton コントロールを選択して名前を変更していない可能性があります)。

     Visual Basic では、イベント ハンドラーは次のようになります。

    ```vb
    Private Sub Button_Click_1(sender As Object, e As RoutedEventArgs)

    End Sub
    ```

     Visual C# では、イベント ハンドラーは次のようになります。

    ```csharp
    private void Button_Click_1(object sender, RoutedEventArgs e)
    {

    }
    ```

2. Visual Basic の場合は、次のコードを入力します。

    ```vb
    If RadioButton1.IsChecked = True Then
        MessageBox.Show("Hello.")
    Else RadioButton2.IsChecked = True
        MessageBox.Show("Goodbye.")
    End If

    ```

     Visual C# の場合は、次のコードを入力します。

    ```
    if (RadioButton1.IsChecked == true)
    {
        MessageBox.Show("Hello.");
    }
    else
    {
        RadioButton2.IsChecked = true;
        MessageBox.Show("Goodbye.");
    }
    ```

3. アプリケーションを保存します。

## <a name="debug-and-test-the-application"></a><a name="BKMK_DebugTest"></a> アプリケーションのデバッグとテスト
 次に、アプリケーションをデバッグしてエラーを探し、両方のメッセージ ボックスが正しく表示されることをテストします。 以下の指示にデバッガーをビルドして起動する方法が示されていますが、詳細については、後で「[WPF アプリケーション (WPF) のビルド](https://msdn.microsoft.com/library/a58696fd-bdad-4b55-9759-136dfdf8b91c)」および「[Debugging WPF](../debugger/debugging-wpf.md)」(WPF のデバッグ) を参照することもできます。

### <a name="find-and-fix-errors"></a>エラーの検出と修正
 この手順では、前にメイン ウィンドウの XAML ファイルの名前を変更することで引き起こしたエラーを見つけます。

##### <a name="to-start-debugging-and-find-the-error"></a>デバッグを開始し、エラーを見つけるには

1. **[デバッグ]**、 **[デバッグの開始]** の順に選択して、デバッガーを起動します。

    ![[デバッグ] メニューの [デバッグの開始] コマンド](../ide/media/exploreide-startdebugging.png "Exploreide-newprojectcsharp-StartDebugging")

    ダイアログ ボックスが表示され、IOException が発生し、リソース 'mainwindow.xaml' を見つけることができないことが示されます。

2. **[OK]** を選択し、デバッガーを停止します。

    ![[デバッグ] メニューの [デバッグの停止] コマンド](../ide/media/exploreide-stopdebugging.png "Exploreide-newprojectcsharp-StopDebugging")

   このチュートリアルの最初で Mainwindow.xaml の名前を Greetings.xaml に変更しましたが、このコードではアプリケーションのスタートアップ URI として Mainwindow.xaml が指定されたままになっているため、プロジェクトを起動できません。

##### <a name="to-specify-greetingsxaml-as-the-startup-uri"></a>スタートアップ URI として Greetings.xaml を指定するには

1. **ソリューション エクスプローラー**で、App.xaml ファイル (C# プロジェクトの場合) または Application.xaml ファイル (Visual Basic プロジェクトの場合) を XAML ビューで開きます (デザイン ビューで開くことはできません)。そのためには、ファイルを選択して Enter キーを押すか、ダブルクリックします。

2. `StartupUri="MainWindow.xaml"` を `StartupUri="Greetings.xaml"`に変更し、Ctrl-s を使って変更を保存します。

   デバッガーを再度起動します。 (F5 を押します)。 アプリケーションの Greetings ウィンドウが表示されます。

### <a name="to-debug-with-breakpoints"></a>ブレークポイントを使用してデバッグするには
 ブレークポイントをいくつか追加して、デバッグ中にコードをテストできます。 ブレークポイントを追加するには、メイン メニューで **[デバッグ]** 、 **[ブレークポイントの設定/解除]** の順に選択するか、中断するコード行の横のエディターの左端の余白をクリックします。

##### <a name="to-add-breakpoints"></a>ブレークポイントを追加するには

1. Greetings.xaml.vb または Greetings.xaml.cs を開き、`MessageBox.Show("Hello.")` という行を選択します。

2. **[デバッグ]**、 **[ブレークポイントの設定/解除]** の順に選択して、メニューからブレークポイントを追加します。

     ![[デバッグ] メニューの [ブレークポイントの設定/解除] コマンド](../ide/media/exploreide-togglebreakpoint.png "Exploreide-newprojectcsharp-ToggleBreakpoint")

     コード行の横の、エディター ウィンドウの左端の余白部分に、赤い円が表示されます。

3. `MessageBox.Show("Goodbye.")`という行を選択します。

4. F9 キーを押して、ブレークポイントを追加し、F5 キーを押して、デバッグを開始します。

5. **[Greetings]** ウィンドウで、 **[Hello]** オプション ボタンを選択してから、 **[Display]** ボタンを選択します。

     `MessageBox.Show("Hello.")` という行が黄色で強調表示されます。 IDE の下部では、[自動変数]、[ローカル]、 [ウォッチ] の各ウィンドウが左側にまとめてドッキングされ、[呼び出し履歴]、[ブレークポイント]、[コマンド]、[イミディエイト]、 [出力] の各ウィンドウが右側にまとめてドッキングされます。

6. メニュー バーで **[デバッグ]**、 **[ステップ アウト]** の順に選択します。

     アプリケーションの実行が再開され、メッセージ ボックスに "Hello" と表示されます。

7. メッセージ ボックスの **[OK]** を選択して閉じます。

8. **[Greetings]** ウィンドウで、 **[Goodbye]** オプション ボタンを選択し、 **[Display]** ボタンを選択します。

     `MessageBox.Show("Goodbye.")` という行が黄色で強調表示されます。

9. F5 キーを押してデバッグを続行します。 メッセージ ボックスが表示されたら、メッセージ ボックスの **[OK]** を選択して、閉じます。

10. Shift キーと F5 キーを押して (最初に Shift を押し、押したままの状態で F5 を押す) 、デバッグを停止します。

11. メニュー バーで、 **[デバッグ]**、 **[すべてのブレークポイントを無効にする]** の順に選択します。

### <a name="build-a-release-version-of-the-application"></a>アプリケーションのリリース バージョンのビルド
 すべてが機能することを確認したら、アプリケーションのリリース ビルドを準備できます。

##### <a name="to-clean-the-solution-files-and-build-a-release-version"></a>ソリューション ファイルをクリーンアップし、リリース バージョンをビルドするには

1. メイン メニューで、 **[ビルド]**、 **[ソリューションのクリーン]** の順に選択して、前のビルドで作成された中間ファイルと出力ファイルを削除します。  この作業は必須ではありませんが、デバッグ ビルドの出力がクリーンアップされます。

    ![[ビルド] メニューの [ソリューションのクリーン] コマンド](../ide/media/exploreide-cleansolution.png "Exploreide-newprojectcsharp-CleanSolution")

2. ツールバーのドロップダウンコントロール (現在は "デバッグ" と表示されています) を使用して、"、" のビルド構成を [ **デバッグ** ] から [ **リリース** ] に変更します。

    ![[リリース] を選択した標準ツール バー](../ide/media/exploreide-releaseversion.png "Exploreide-newprojectcsharp-ReleaseVersion")

3. **[ビルド]** を選択し、 **[ソリューションのビルド]** を選択するか F6 キーを押して、ソリューションをビルドします。

    ![[ビルド] メニューの [ソリューションのビルド] コマンド](../ide/media/exploreide-buildsolution.png "Exploreide-newprojectcsharp-BuildSolution")

   このチュートリアルは完了しました。 ビルドした .exe は、ソリューションとプロジェクトのディレクトリ (…\HelloWPFApp\HelloWPFApp\bin\Release\\) の下にあります。 その他の例については、「[Visual Studio Samples](../ide/visual-studio-samples.md)」を参照してください。

## <a name="see-also"></a>参照
 Visual [studio 2015 の新機能](../what-s-new-in-visual-studio-2015.md)visual studio の[生産性に関するヒント](../ide/productivity-tips-for-visual-studio.md)[を使用した開発の開始](../ide/get-started-developing-with-visual-studio.md)
