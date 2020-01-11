---
title: 'チュートリアル: コード化された UI テストの作成、編集、および保守 | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: f7c25ba7-5c9c-455b-9242-701cda56f90c
caps.latest.revision: 43
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d14de396e24874f39a09172a483ebef81a5886f2
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75851229"
---
# <a name="walkthrough-creating-editing-and-maintaining-a-coded-ui-test"></a>チュートリアル: コード化された UI テストの作成、編集、および保守
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、簡単な Windows Presentation Foundation (WPF) アプリケーションを作成して、コード化された UI テストの作成、編集、および保守を行う方法について説明します。 また、さまざまなタイミングの問題やコントロールのリファクタリングによって機能が損なわれたテストを修正するための解決策を示します。

## <a name="prerequisites"></a>[前提条件]
 このチュートリアルに必要な条件は次のとおりです。

- Visual Studio Enterprise

### <a name="create-a-simple-wpf-application"></a>簡単な WPF アプリケーションの作成

1. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** を選択します。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

2. **[インストールされたテンプレート]** ペインで、 **[Visual C#]** を展開し、 **[Windows デスクトップ]** を選択します。

3. 中央のペインの上にあるターゲット フレームワーク ドロップダウン リストが **[.NET Framework 4.5]** に設定されていることを確認します。

4. 中央のペインで、 **[WPF アプリケーション]** テンプレートを選択します。

5. **[名前]** テキスト ボックスに「**SimpleWPFApp**」と入力します。

6. プロジェクトの保存先のフォルダーを選択します。 **[場所]** テキスト ボックスにフォルダーの名前を入力します。

7. **[OK]** をクリックします。

     Visual Studio の WPF デザイナーが開き、プロジェクトの MainWindow が表示されます。

8. ツールボックスが現在開いていない場合は開きます。 **[表示]** メニューを選択し、 **[ツールボックス]** を選択します。

9. **[すべての WPF コントロール]** セクションの **[Button]** 、 **[CheckBox]** 、 **[ProgressBar]** の各コントロールをデザイン サーフェイスの MainWindow にドラッグします。

10. Button コントロールを選択します。 [プロパティ] ウィンドウで、 **[名前]** プロパティの値を \<No Name> から button1 に変更します。 次に、 **[コンテンツ]** プロパティの値を Button から Start に変更します。

11. ProgressBar コントロールを選択します。 [プロパティ] ウィンドウで、 **[名前]** プロパティの値を \<No Name> から progressBar1 に変更します。 次に、 **[最大値]** プロパティの値を **100** から **10000** に変更します。

12. Checkbox コントロールを選択します。 [プロパティ] ウィンドウで、 **[名前]** プロパティの値を \<No Name> から checkBox1 に変更し、 **[IsEnabled]** プロパティをクリアします。

     ![単純な WPF アプリケーション](../test/media/codedui-wpfapp.png "CodedUI_WPFApp")

13. ボタン コントロールをダブルクリックしてクリック イベント ハンドラーを追加します。

     コード エディターに MainWindow.xmal.cs が表示され、新しい button1_Click メソッドにカーソルが置かれます。

14. MainWindow クラスの先頭にデリゲートを追加します。 このデリゲートはプログレス バーに使用されます。 デリゲートを追加するには、次のコードを追加します。

    ```csharp
    public partial class MainWindow : Window
    {
            private delegate void ProgressBarDelegate(System.Windows.DependencyProperty dp, Object value);

        public MainWindow()
        {

            InitializeComponent();
        }

    ```

15. button1_Click メソッドに次のコードを追加します。

    ```csharp
    private void button1_Click(object sender, RoutedEventArgs e)
    {
        double progress = 0;

        ProgressBarDelegate updatePbDelegate =
            new ProgressBarDelegate(progressBar1.SetValue);

        do
        {
            progress ++;

            Dispatcher.Invoke(updatePbDelegate,
                System.Windows.Threading.DispatcherPriority.Background,
                new object[] { ProgressBar.ValueProperty, progress });
            progressBar1.Value = progress;
        }
        while (progressBar1.Value != progressBar1.Maximum);

        checkBox1.IsEnabled = true;
    }

    ```

16. ファイルを保存します。

### <a name="verify-the-wpf-application-runs-correctly"></a>WPF アプリケーションの動作の確認

1. **[デバッグ]** メニューの **[デバッグ開始]** を選択するか、**F5** キーを押します。

2. チェック ボックス コントロールが無効にされることに注意してください。 **[開始]** を選択します。

     数秒でプログレス バーが 100% になります。

3. これで、チェック ボックス コントロールを選択できます。

4. SimpleWPFApp を閉じます。

### <a name="create-and-run-a-coded-ui-test-for-simplewpfapp"></a>SimpleWPFApp のコード化された UI テストの作成と実行

1. 前に作成した SimpleWPFApp アプリケーションを見つけます。 既定では、アプリケーションは C:\Users\\<ユーザー名\>\Documents\Visual Studio \<バージョン>\Projects\SimpleWPFApp\SimpleWPFApp\bin\Debug\SimpleWPFApp.exe にあります。

2. SimpleWPFApp アプリケーションのデスクトップ ショートカットを作成します。 SimpleWPFApp.exe を右クリックし、 **[コピー]** を選択します。 デスクトップで右クリックし、 **[ショートカットの貼り付け]** を選択します。

    > [!TIP]
    > アプリケーションのショートカットを使用するとアプリケーションをすばやく起動できるため、アプリケーションのコード化された UI テストを追加または変更しやすくなります。

3. ソリューション エクスプローラーで、ソリューションを右クリックし、 **[追加]** を選択して **[新しいプロジェクト]** を選択します。

     **[新しいプロジェクトの追加]** ダイアログ ボックスが表示されます。

4. **[インストールされたテンプレート]** ペインで、 **[Visual C#]** を展開し、 **[テスト]** を選択します。

5. 中央のペインで、 **[コード化された UI テスト プロジェクト]** テンプレートを選択します。

6. **[OK]** をクリックします。

     ソリューション エクスプローラーで、**CodedUITestProject1** という名前の新しいコード化された UI テスト プロジェクトがソリューションに追加されます。

     **[コード化された UI テストのコードの生成]** ダイアログ ボックスが表示されます。

7. **[操作の記録、UI マップの編集、またはアサーションの追加]** オプションを選択し、 **[OK]** を選択します。

     [UIMap - コード化された UI テスト ビルダー] が表示され、Visual Studio ウィンドウは最小化されます。

     ダイアログ ボックスのオプションの詳細については、「[コード化された UI テストを作成する](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate)」を参照してください。

8. [UIMap – コード化された UI テスト ビルダー] で **[記録の開始]** を選択します。

     ![記録の開始](../test/media/cuit-builder-record.png "CUIT_Builder_Record")

     受信メールを処理する場合など、必要に応じて記録を一時停止できます。

     ![記録を一時停止する](../test/media/cuit.png "CUIT_")

    > [!WARNING]
    > デスクトップ上で実行されるすべてのアクションが記録されます。 機密データが記録される可能性のあるアクションを実行する場合には、記録を一時停止します。

9. デスクトップ ショートカットを使用して、SimpleWPFApp を起動します。

     前と同じく、チェック ボックス コントロールが無効にされることに注意してください。

10. SimpleWPFApp で **[開始]** を選択します。

     数秒でプログレス バーが 100% になります。

11. 有効になったチェック ボックス コントロールを確認します。

12. SimpleWPFApp アプリケーションを閉じます。

13. [UIMap - コード化された UI テスト ビルダー] で、 **[コードの生成]** を選択します。

14. [メソッド名] に「**SimpleAppTest**」と入力し、 **[追加と生成]** を選択します。 数秒でコード化された UI テストが表示され、ソリューションに追加されます。

15. [UIMap – コード化された UI テスト ビルダー] を閉じます。

     コード エディターに CodedUITest1.cs ファイルが表示されます。

16. プロジェクトを保存します。

### <a name="run-the-coded-ui-test"></a>コード化された UI テストの実行

1. **[テスト]** メニューの **[ウィンドウ]** を選択し、 **[テスト エクスプローラー]** を選択します。

2. **[ビルド]** メニューの **[ソリューションのビルド]** を選択します。

3. CodedUITest1.cs ファイルで、**CodedUITestMethod** メソッドを見つけて右クリックし、 **[テストの実行]** を選択します。または、テスト エクスプローラーでテストを実行します。

     コード化された UI テストを実行すると、SimpleWPFApp が表示されます。 前の手順で実行した各ステップが実行されます。 ただし、テストで チェック ボックス コントロールのチェック ボックスをオンにしようとすると、[テスト結果] ウィンドウにテストが失敗したことが示されます。 チェック ボックス コントロールはプログレス バーが 100% になるまで無効化されています。テストではこの点が認識されておらず、まだ有効になっていないチェック ボックスをオンにしようとしたことが失敗の原因です。 コード化された UI テストで使用できるさまざまな `UITestControl.WaitForControlXXX()` メソッドを使用することで、この問題や同様の問題を解決できます。 次の手順では、`WaitForControlEnabled()` メソッドを使用して、このテストの失敗の原因となった問題を解決する方法を示します。 詳細については、「[再生中に特定のイベントを待機するようにコード化された UI テストを設定](../test/making-coded-ui-tests-wait-for-specific-events-during-playback.md)」を参照してください。

### <a name="edit-and-rerun-the-coded-ui-test"></a>コード化された UI テストの編集と再実行

1. テスト エクスプローラー ウィンドウで、失敗したテストを選択し、 **[StackTrace]** セクションで **[UIMap.SimpleAppTest()]** の最初のリンクを選択します。

2. UIMap.Designer.cs ファイルが開き、コードのエラー ポイントが強調表示されます。

    ```csharp

    // Select 'CheckBox' check box
    uICheckBoxCheckBox.Checked = this.SimpleAppTestParams.UICheckBoxCheckBoxChecked;
    ```

3. この問題を解決するには、`WaitForControlEnabled()` メソッドを使用して、コード化された UI テストで CheckBox コントロールが有効になるのを待ってからこの行に進むようにします。

    > [!WARNING]
    > UIMap.Designer.cs ファイルは変更しないでください。 UIMapDesigner.cs ファイルでコードを変更しても、[UIMap - コード化された UI テスト ビルダー] を使用してコードを生成するたびに変更が上書きされます。 記録されたメソッドを変更する必要がある場合は、メソッドを UIMap.cs ファイルにコピーし、メソッド名を変更する必要があります。 UIMap.cs ファイルを使用すると、UIMapDesigner.cs ファイルのメソッドやプロパティをオーバーライドできます。 Coded UITest.cs ファイルの元のメソッドへの参照を削除し、変更したメソッド名に置き換える必要があります。

4. ソリューション エクスプローラーで、コード化された UI テスト プロジェクトの **UIMap.uitest** を見つけます。

5. **UIMap.uitest** のショートカット メニューを開き、 **[開く]** を選択します。

     コード化された UI テスト エディターに、コード化された UI テストが表示されます。 これで、コード化された UI テストを表示および編集できます。

6. **[UI 操作]** ペインで、UIMap.cs または UIMap.vb ファイルに移動するテスト メソッド (SimpleAppTest) を選択します。移動すると、カスタム コード機能は容易になり、テスト コードが再コンパイルされても上書きされません。

7. コード化された UI テスト エディターのツール バーにある **[コードの移動]** ボタンを選択します。

8. Microsoft Visual Studio のダイアログ ボックスが表示されます。 警告で、メソッドが UIMap.uitest ファイルから UIMap.cs ファイルへ移動すること、およびコード化された UI テスト エディターを使用してメソッドを編集できなくなることが表示されます。 **[はい]** をクリックします。

     テスト メソッドが UIMap.uitest ファイルから削除され、[UI Actions] (UI 操作) ペインに表示されなくなります。 移動したテスト ファイルを編集するには、ソリューション エクスプローラーから UIMap.cs ファイルを開きます。

9. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ツール バーの **[保存]** を選択します。

     テスト メソッドの更新内容が UIMap.Designer ファイルに保存されます。

    > [!CAUTION]
    > メソッドを移動すると、コード化された UI テスト エディターを使用してそのメソッドを編集できなくなります。 カスタム コードを追加し、コード エディターを使って管理する必要があります。

10. メソッド名を `SimpleAppTest()` から `ModifiedSimpleAppTest()` に変更します。

11. 次の using ステートメントをファイルに追加します。

    ```csharp

    using Microsoft.VisualStudio.TestTools.UITesting.WpfControls;

    ```

12. 確認済みの問題のコード行の前に、次の `WaitForControlEnabled()` メソッドを追加します。

    ```csharp

              uICheckBoxCheckBox.WaitForControlEnabled();

    // Select 'CheckBox' check box
    uICheckBoxCheckBox.Checked = this.SimpleAppTestParams.UICheckBoxCheckBoxChecked;

    ```

13. CodedUITest1.cs ファイルで、**CodedUITestMethod** メソッドを見つけてコメントアウトするか、元の SimpleAppTest() メソッドへの参照の名前を変更し、新しい ModifiedSimpleAppTest() に置き換えます。

    ```csharp
    [TestMethod]
            public void CodedUITestMethod1()
            {
                // To generate code for this test, select "Generate Code for Coded UI Test" from the shortcut menu and select one of the menu items.
                // For more information on generated code, see http://go.microsoft.com/fwlink/?LinkId=179463
                //this.UIMap.SimpleAppTest();
                this.UIMap.ModifiedSimpleAppTest();
            }

    ```

14. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

15. **CodedUITestMethod** メソッドを右クリックし、 **[テストの実行]** を選択します。

16. 今回は、コード化された UI テストでテストのすべてのステップが正常に完了し、テスト エクスプローラー ウィンドウに **[成功]** と表示されます。

### <a name="refactor-a-control-in-the-simplewpfapp"></a>SimpleWPFApp のコントロールのリファクタリング

1. MainWindow.xaml ファイルで、デザイナーのボタン コントロールを選択します。

2. [プロパティ] ウィンドウの上部にある **[名前]** プロパティの値を button1 から buttonA に変更します。

3. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

4. テスト エクスプローラーで、**CodedUITestMethod1** を実行します。

     テストは失敗します。コード化された UI テストでは、UIMap で元は button1 としてマップされていたボタン コントロールを見つけることができないためです。 このように、リファクタリングがコード化された UI テストに影響を及ぼす場合があります。

5. [テスト エクスプローラー] ウィンドウの **[StackTrace]** セクションで、 **[UIMpa.ModifiedSimpleAppTest()]** の横にある最初のリンクを選択します。

     UIMap.cs ファイルが開きます。 コードでエラー ポイントが強調表示されます。

    ```csharp

    // Click 'Start' button
    Mouse.Click(uIStartButton, new Point(27, 10));
    ```

     この手順の前半のコード行では `UiStartButton` を使用していることに注意してください。これがリファクタリング前の UIMap 名です。

     この問題を解決するには、コード化された UI テスト ビルダーを使用して、リファクタリングしたコントロールを UIMap に追加します。 次の手順に示すように、このコードを使用するようテストのコードを更新できます。

### <a name="map-refactored-control-and-edit-and-rerun-the-coded-ui-test"></a>リファクタリングしたコントロールのマッピングおよびコード化された UI テストの編集と再実行

1. CodedUITest1.cs ファイルで、**CodedUITestMethod1()** メソッドを右クリックし、 **[コード化された UI テストのコードの生成]** を選択して、 **[コード化された UI テスト ビルダーの使用]** を選択します。

     [UIMap – コード化された UI テスト ビルダー] が表示されます。

2. 前半で作成したデスクトップ ショートカットを使用して、作成済みの SimpleWPFApp アプリケーションを実行します。

3. [UIMap – コード化された UI テスト ビルダー] で、十字ツールを SimpleWPFApp の **[開始]** ボタンまでドラッグします。

     **[開始]** ボタンが青いボックスで囲まれます。コード化された UI テスト ビルダーによって、選択したコントロールのデータが数秒で処理され、コントロールのプロパティが表示されます。 **AutomationUId** の名前が **buttonA** になっていることに注意してください。

4. コントロールのプロパティで、左上隅の矢印を選択して UI コントロール マップを展開します。 **UIStartButton1** が選択されていることを確認します。

5. ツール バーの **[コントロールの UI コントロール マップへの追加]** を選択します。

     ウィンドウの下部のステータスに、 **[選択されたコントロールが UI コントロール マップに追加されました]** と表示され、操作が確認されます。

6. [UIMap - コード化された UI テスト ビルダー] で、 **[コードの生成]** を選択します。

     [コード化された UI テスト ビルダー - コードの生成] が表示され、新しいメソッドは不要であり、UI コントロール マップの変更のみを目的としてコードが生成されることが通知されます。

7. **[生成]** を選択します。

8. SimpleWPFApp.exe を閉じます。

9. [UIMap – コード化された UI テスト ビルダー] を閉じます。

     [UIMap – コード化された UI テスト ビルダー] によって、数秒で UI コントロール マップの変更が処理されます。

10. ソリューション エクスプローラーで、UIMap.Designer.cs ファイルを開きます。

11. UIMap.Designer.cs ファイルで、UIStartButton1 プロパティを見つけます。 `SearchProperties` が `"buttonA"` に設定されていることを確認します。

    ```csharp

    public WpfButton UIStartButton1
            {
                get
                {
                    if ((this.mUIStartButton1 == null))
                    {
                        this.mUIStartButton1 = new WpfButton(this);
                        #region Search Criteria
                        this.mUIStartButton1.SearchProperties[WpfButton.PropertyNames.AutomationId] = "buttonA";
                        this.mUIStartButton1.WindowTitles.Add("MainWindow");
                        #endregion
                    }
                    return this.mUIStartButton1;
                }
            }

    ```

     これで、コード化された UI テストを変更して、新しくマップされたコントロールを使用できます。 前の手順で説明したように、コード化された UI テストのメソッドまたはプロパティをオーバーライドする場合は、UIMap.cs ファイルで実行する必要があります。

12. UIMap.cs ファイルで、コンストラクターを追加し、値として `SearchProperties` を指定した `UIStartButton` プロパティを使用するように、`AutomationID` プロパティの `"buttonA":` プロパティを指定します。

    ```csharp

    public UIMap()
            {
                this.UIMainWindowWindow.UIStartButton.SearchProperties[WpfButton.PropertyNames.AutomationId] = "buttonA";
            }

    ```

13. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

14. テスト エクスプローラーで、[CodedUITestMethod1] を実行します。

     今回は、コード化された UI テストでテストのすべてのステップが正常に完了します。  [テスト結果] ウィンドウに、 **[成功]** というステータスが表示されます。

## <a name="external-resources"></a>外部資料

### <a name="videos"></a>Videos
 ![ビデオ](../data-tools/media/playvideo.gif "PlayVideo")[コード化された UI テストへのリンク-tests-deepdive-episode1-gettingstarted-Tests-deepdive-episode1-gettingstarted-gettingstarted](https://skydrive.live.com/?cid=2db0e1efe1c1d3b8&id=2DB0E1EFE1C1D3B8%21118)ています

 ビデオコード化された UI テスト![へのリンク](../data-tools/media/playvideo.gif "PlayVideo") [-tests-deepdive-episode1-gettingstarted-tests-deepdive-episode2-maintainenceanddebugging-tests-deepdive-episode2-maintainenceanddebugging](https://skydrive.live.com/?cid=2db0e1efe1c1d3b8&id=2DB0E1EFE1C1D3B8%21116)

 ビデオコード化された UI テスト![へのリンク](../data-tools/media/playvideo.gif "PlayVideo") [-Tests-deepdive-episode1-gettingstarted-tests-deepdive-episode3-handcoding コーディング](https://skydrive.live.com/?cid=2db0e1efe1c1d3b8&id=2DB0E1EFE1C1D3B8%21117)

### <a name="hands-on-lab"></a>ハンズ オン ラボ
 [MSDN 仮想ラボ: Visual Studio 2010 でのコード化された UI テストの作成の概要](https://windows.microsoft.com/en-US/windows/products/windows-media-player)

### <a name="faq"></a>よく寄せられる質問
 [Coded UI Tests FAQ - 1 (コード化された UI テストの FAQ - 1)](https://blogs.msdn.com/b/mathew_aniyan/archive/tags/faq/)

 [Coded UI Tests FAQ - 2 (コード化された UI テストの FAQ - 2)](https://social.msdn.microsoft.com/Forums/en-US/vsautotest/thread/3a74dd2c-cef8-4923-abbf-7a91f489e6c4)

### <a name="forum"></a>フォーラム
 [Visual Studio の UI オートメーションのテスト (CodedUI を含む)](https://social.msdn.microsoft.com/Forums/en-US/vsautotest)

## <a name="see-also"></a>参照
 UI オートメーションを使用して[、WPF デザイナーで](https://msdn.microsoft.com/18e61d03-b96a-4058-a166-8ec6b3f6116b)[サポートされている構成およびコード化された Ui テストおよび操作の記録のためのプラットフォーム](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)を使用してはじめに[コードをテストするコード](../test/use-ui-automation-to-test-your-code.md)化された ui テスト[エディター](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)
