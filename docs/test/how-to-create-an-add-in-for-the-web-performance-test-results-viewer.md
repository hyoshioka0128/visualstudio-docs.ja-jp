---
title: Web パフォーマンス テスト結果ビューアー用のアドインを作成する
description: Visual Studio のアドインを作成して Web パフォーマンス テスト結果ビューアーの UI を拡張する方法と、UI の拡張に必要なクラスを実装する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 10/20/2016
ms.topic: how-to
helpviewer_keywords:
- Web performance tests, Visual Studio Add-in
- Visual Studio Add-in, Web performance tests
ms.assetid: 1118c604-4b1b-4b21-a04e-45995b676fa8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b8fa3b83fb9a92be0118f4222e92364767affcda
ms.sourcegitcommit: 02f14db142dce68d084dcb0a19ca41a16f5bccff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "95441079"
---
# <a name="how-to-create-an-add-in-for-the-web-performance-test-results-viewer"></a>方法: Web パフォーマンス テスト結果ビューアー用のアドインを作成する

次の名前空間を使用して、**Web パフォーマンス テスト結果ビューアー** の UI を拡張できます。

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting>

- <xref:Microsoft.VisualStudio.TestTools.WebTesting>

また、 *%ProgramFiles(x86)%\Microsoft Visual Studio\\\<version>\Enterprise\Common7\IDE\PrivateAssemblies* フォルダーにある LoadTestPackage DLL に参照を追加する必要があります。

**Web パフォーマンス テスト結果ビューアー** の UI を拡張するには、Visual Studio アドインおよびユーザー コントロールを作成する必要があります。 次の手順では、アドインとユーザー コントロールの作成方法、および **Web パフォーマンス テスト結果ビューアー** の UI を拡張するのに必要なクラスを実装する方法について説明します。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="create-or-open-a-solution-that-contains-an-aspnet-web-application-and-a-web-performance-and-load-test-project"></a>ASP.NET Web アプリケーションおよび Web パフォーマンスとロード テストのプロジェクトが含まれるソリューションを作成するか開く

### <a name="to-prepare-for-extending-the-web-performance-test-results-viewer"></a>Web パフォーマンス テスト結果ビューアーの拡張の準備をするには

テストの対象として、ASP.NET Web アプリケーションおよび Web パフォーマンスとロード テストのプロジェクト (ASP.NET Web アプリケーション用の 1 つ以上の Web パフォーマンス テストを備えたプロジェクト) が含まれている非稼動ソリューションを作成するか開きます。

> [!NOTE]
> ASP.NET Web アプリケーションの作成と、Web パフォーマンス テストを備えた Web パフォーマンスとロード テストのプロジェクトの作成を行うには、[Web サービス テストの作成方法](../test/how-to-create-a-web-service-test.md)に関するページと[コード化された Web パフォーマンス テストの生成と実行](../test/generate-and-run-a-coded-web-performance-test.md)に関するページを参照してください。

## <a name="create-a-visual-studio-add-in"></a>Visual Studio アドインの作成

アドインは、Visual Studio 統合開発環境 (IDE: Integrated Development Environment) 内部で実行されるコンパイル済み DLL です。 DLL がコンパイルされていることにより、知的財産権が保護され、パフォーマンスが向上します。 アドインは手動でも作成できますが、**アドイン ウィザード** を使用した方が簡単に作成できます。 このウィザードでは、作成後すぐに実行できる、基本的な機能を備えたアドインが作成されます。 **アドイン ウィザード** で基本プログラムが生成された後に、コードを追加してカスタマイズできます。

**アドイン ウィザード** では、アドインの表示名および説明を指定できます。 両方とも、**アドイン マネージャー** に表示されます。 オプションで、アドインを開くコマンドを **[ツール]** メニューに追加するコードをウィザードで生成することもできます。 また、アドインにカスタムの **[バージョン情報]** ダイアログ ボックスを表示することもできます。 ウィザードが完了すると、アドインを実装するクラスを 1 つだけ含む新しいプロジェクトが作成されます。 そのクラスには Connect という名前が付けられます。

この記事の最後にある **アドイン マネージャー** を使用します。

### <a name="to-create-an-add-in-by-using-the-add-in-wizard"></a>アドイン ウィザードを使用してアドインを作成するには

1. **ソリューション エクスプローラー** で、ソリューションを右クリックし、 **[追加]** を選択して **[新しいプロジェクト]** を選択します。

2. 新しい **Visual Studio アドイン** プロジェクトを作成します。

    Visual Studio **アドイン ウィザード** が起動します。

3. **[次へ]** をクリックします。

4. **[プログラミング言語の選択]** ページで、アドインを記述するのに使用するプログラミング言語を選択します。

   > [!NOTE]
   > このトピックでは、サンプル コードの実行に Visual C# を使用します。

5. **[アプリケーション ホストの選択]** ページで、**Visual Studio** のチェック ボックスをオンにし、**Visual Studio マクロ** のチェック ボックスをオフにします。

6. **[次へ]** をクリックします。

7. **[名前および説明の入力]** ページで、アドインの名前および説明を入力します。

     アドインが作成されると、**アドイン マネージャー** の **[使用できるアドイン]** の一覧にアドインの名前と説明が表示されます。 アドインの機能や動作などをユーザーが理解できる説明をアドインに追加します。

8. **[次へ]** をクリックします。

9. **[アドイン オプションを選択します。]** ページの **[ホスト アプリケーションの読み込み時にアドインを開始する]** を選択します。

10. 残りのチェック ボックスをオフにします。

11. **[[バージョン情報] に関する情報を選択します。]** ページで、アドインについての情報を **[バージョン情報]** ダイアログ ボックスに表示するかどうかを指定できます。 情報を表示する場合は、 **[[バージョン情報] ボックスの情報を指定する]** チェック ボックスをオンにします。

     Visual Studio の **[バージョン情報]** ダイアログ ボックスに追加できる情報には、バージョン番号、サポートの詳細、ライセンスのデータなどがあります。

12. **[次へ]** をクリックします。

13. 選択したオプションが **[概要]** ページに表示され、選択した内容をレビューできます。 問題がなければ、 **[完了]** を選んで、アドインを作成します。 変更を加える場合は、 **[戻る]** ボタンを選びます。

     新しいソリューションおよびプロジェクトが作成され、**コード エディター** に新しいアドインの *Connect.cs* ファイルが表示されます。

     以下の手順でこの WebPerfTestResultsViewerAddin プロジェクトによって参照されるユーザー コントロールを作成した後に、コードを *Connect.cs* ファイルに追加します。

    作成したアドインを **アドイン マネージャー** でアクティブ化できるようにするには、アドインを Visual Studio に登録する必要があります。 これを行うには、 *.addin* ファイル名拡張子を持つ XML ファイルを使用します。

    この *.addin* ファイルには、Visual Studio の **アドイン マネージャー** にアドインを表示するために必要な情報が記述されています。 Visual Studio は起動時に、使用できる *.addin* ファイルを検出するために *.addin* ファイルの場所を検索します。 使用できる .addin ファイルが検出された場合、この XML ファイルをクリックすると、内容が読み取られて、アドインを起動するのに必要な情報が **アドイン マネージャー** に渡されます。

    *.addin* ファイルは、**アドイン ウィザード** を使用してアドインを作成すると、自動的に作成されます。

### <a name="add-in-file-locations"></a>アドイン ファイルの場所

**アドイン ウィザード** によって、次のような *.addin* ファイルのコピーが 2 つ自動的に作成されます。

|**.Addin ファイルの場所**|**説明**|
|-|----------------------------|-|
|ルート プロジェクト フォルダー|アドイン プロジェクトの配置に使用します。 編集しやすくするためにプロジェクトに含まれており、XCopy 形式の配置用のローカル パスが設定されます。|
|アドイン フォルダー|デバッグ環境でアドインを実行する場合に使用します。 常に、現在のビルド構成の出力パスを示します。|

## <a name="create-a-windows-form-control-library-project"></a>Windows フォーム コントロール ライブラリ プロジェクトの作成

前の手順で作成された Visual Studio アドインが Windows フォーム コントロール ライブラリ プロジェクトを参照して、<xref:System.Windows.Forms.UserControl> クラスのインスタンスを作成します。

### <a name="to-create-a-control-to-be-used-in-the-web-test-results-viewer"></a>コントロールを作成して Web テスト結果ビューアーで使用するには

1. **ソリューション エクスプローラー** で、ソリューションを右クリックし、 **[追加]** を選択して **[新しいプロジェクト]** を選択します。

2. 新しい **Windows フォーム コントロール ライブラリ** プロジェクトを作成します。

3. **ツールボックス** から userControl1 のサーフェイスに <xref:System.Windows.Forms.DataGridView> をドラッグします。

4. <xref:System.Windows.Forms.DataGridView> の右上隅のアクション タグ グリフ (![スマート タグ グリフ](../test/media/vs_winformsmttagglyph.gif)) をクリックし、次の手順を実行します。

    1. **[親コンテナーにドッキングする]** を選択します。

    2. **[追加を有効にする]** 、 **[編集を有効にする]** 、 **[削除を有効にする]** 、および **[列の並べ替えを有効にする]** の各チェック ボックスをオフにします。

    3. **[列の追加]** を選択します。

         **[列の追加]** ダイアログ ボックスが表示されます。

    4. **[種類]** ドロップダウン リストの **[DataGridViewTextBoxColumn]** を選択します。

    5. **[ヘッダー テキスト]** の「Column1」というテキストを削除します。

    6. **[追加]** をクリックします。

    7. **[閉じる]** を選択します。

5. **[プロパティ]** ウィンドウで、<xref:System.Windows.Forms.DataGridView> の **(Name)** プロパティを **resultControlDataGridView** に変更します。

6. デザイン サーフェイスを右クリックし、 **[コードの表示]** を選択します。

     **コード エディター** に *UserControl1.cs* ファイルが表示されます。

7. インスタンス化された <xref:System.Windows.Forms.UserControl> クラスの名前を UserContro1 から resultControl に変更します。

    ```csharp
    namespace WebPerfTestResultsViewerControl
    {
        public partial class resultControl : UserControl
        {
            public resultControl()
            {
                InitializeComponent();
            }
    ```

     次の手順では、resultControl クラスを参照する WebPerfTestResultsViewerAddin プロジェクトの *Connect.cs* ファイルにコードを追加します。

     後で、*Connect.cs* ファイルにいくつかのコードを追加します。

## <a name="add-code-to-the-webperftestresultsvieweraddin"></a>WebPerfTestResultsViewerAddin へのコードの追加

1. **ソリューション エクスプローラー** で、WebPerfTestResultsViewerAddin プロジェクトの **[参照設定]** ノードを右クリックし、 **[参照の追加]** を選択します。

2. **[参照の追加]** ダイアログ ボックスの **[.NET]** タブを選びます。

3. 下にスクロールして、 **[Microsoft.VisualStudio.QualityTools.WebTestFramework]** を選択し、 **[System.Windows.Forms]** を選択します。

4. **[OK]** をクリックします。

5. 再度 **[参照設定]** ノードを右クリックして、 **[参照の追加]** を選択します。

6. **[参照の追加]** ダイアログ ボックスの **[参照]** タブを選びます。

7. **[検索対象]** のドロップダウンを選んで、 *%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\PrivateAssemblies* に移動し、*Microsoft.VisualStudio.QualityTools.LoadTestPackage.dll* ファイルを選択します。

8. **[OK]** をクリックします。

9. WebPerfTestResultsViewerAddin プロジェクト ノードを右クリックして、 **[参照の追加]** を選択します。

10. **[参照の追加]** ダイアログ ボックスの **[プロジェクト]** タブを選びます。

11. **[プロジェクト名]** で、 **[WebPerfTestResultsViewerControl]** プロジェクトを選択し、 **[OK]** を選びます。

12. *Connect.cs* ファイルが表示されない場合、**ソリューション エクスプローラー** で、WebPerfTestResultsViewerAddin プロジェクトの **Connect.cs** ファイルを右クリックして、 **[コードの表示]** を選択します。

13. *Connect.cs* ファイルで、次の Using ステートメントを追加します。

    ```csharp
    using System.IO;
    using System.Windows.Forms;
    using System.Collections.Generic;
    using Microsoft.VisualStudio.TestTools.LoadTesting;
    using Microsoft.VisualStudio.TestTools.WebTesting;
    using WebPerfTestResultsViewerControl;
    ```

14. *Connect.cs* ファイルの最下部までスクロール ダウンします。 **Web パフォーマンス テスト結果ビューアー** の複数のインスタンスが開いている場合は、<xref:System.Windows.Forms.UserControl> の GUID のリストを追加する必要があります。 後で、このリストを使用するコードを追加します。

     文字列の 2 番目のリストは、後でコード化する OnDiscconection メソッドで使用されます。

    ```csharp
    private DTE2 _applicationObject;
    private AddIn _addInInstance;

    private Dictionary<Guid, List<UserControl>> m_controls = new Dictionary<Guid, List<UserControl>>();        private List<string> temporaryFilePaths = new List<string>();
    ```

15. *Connect.cs* ファイルは、<xref:Extensibility.IDTExtensibility2> クラスから Connect という名前のクラスをインスタンス化します。また、このファイルには、Visual Studio アドインを実装するいくつかのメソッドが含まれています。 メソッドのうちの 1 つは OnConnection メソッドで、アドインが読み込まれている通知を受け取ります。 OnConnection メソッドでは、LoadTestPackageExt クラスを使用して、**Web パフォーマンス テスト結果ビューアー** 用の機能拡張パッケージを作成します。 次のコードを OnConnection メソッドに追加します。

    ```csharp
    public void OnConnection(object application, ext_ConnectMode connectMode, object addInInst, ref Array custom)
                {
                _applicationObject = (DTE2)application;
                _addInInstance = (AddIn)addInInst;

                // Create a load test packge extensibility class.            LoadTestPackageExt loadTestPackageExt = _applicationObject.GetObject("Microsoft.VisualStudio.TestTools.LoadTesting.LoadTestPackageExt") as LoadTestPackageExt;            // Process open windows.            foreach (WebTestResultViewer webTestResultViewer in loadTestPackageExt.WebTestResultViewerExt.ResultWindows)            {                WindowCreated(webTestResultViewer);            }            // Create event handlers.            loadTestPackageExt.WebTestResultViewerExt.WindowCreated += new EventHandler<WebTestResultViewerExt.WindowCreatedEventArgs>(WebTestResultViewerExt_WindowCreated);            loadTestPackageExt.WebTestResultViewerExt.WindowClosed += new EventHandler<WebTestResultViewerExt.WindowClosedEventArgs>(WebTesResultViewer_WindowClosed);            loadTestPackageExt.WebTestResultViewerExt.SelectionChanged += new EventHandler<WebTestResultViewerExt.SelectionChangedEventArgs>(WebTestResultViewer_SelectedChanged);
            }
    ```

16. 次のコードを接続クラスに追加して、OnConnection メソッドに追加した loadTestPackageExt.WebTestResultViewerExt.WindowCreated イベント ハンドラー用、および WebTestResultViewerExt_WindowCreated メソッドで呼び出される WindowCreated メソッド用の WebTestResultViewerExt_WindowCreated メソッドを作成します。

    ```csharp
            void WebTestResultViewerExt_WindowCreated(object sender, WebTestResultViewerExt.WindowCreatedEventArgs e)
            {
                // New control added to new result viewer window.
                WindowCreated(e.WebTestResultViewer);
            }

    private void WindowCreated(WebTestResultViewer viewer)        {            // Instantiate an instance of the resultControl referenced in the WebPerfTestResultsViewerControl project.
                resultControl resultControl = new resultControl();            // Add to the dictionary of open playback windows.            System.Diagnostics.Debug.Assert(!m_controls.ContainsKey(viewer.TestResultId));            List<UserControl> userControls = new List<UserControl>();            userControls.Add(resultControl);            // Add Guid to the m_control List to manage Result viewers and controls.            m_controls.Add(viewer.TestResultId, userControls);            // Add tabs to the playback control.            resultControl.Dock = DockStyle.Fill;            viewer.AddResultPage(new Guid(), "Sample", resultControl);        }
    ```

17. 次のコードを接続クラスに追加して、OnConnection メソッドに追加した loadTestPackageExt.WebTestResultViewerExt.SelectionChanged イベント ハンドラー用の WebTestResultViewer_SelectedChanged メソッドを作成します。

    ```csharp
    void WebTestResultViewer_SelectedChanged(object sender, WebTestResultViewerExt.SelectionChangedEventArgs e)
    {
        foreach (UserControl userControl in m_controls[e.TestResultId])            {                // Update the userControl in each result viewer.                resultControl resultControl = userControl as resultControl;                if (resultControl != null)                    // Call the resultControl's Update method (This will be added in the next procedure).                    resultControl.Update(e.WebTestRequestResult);            }
    }
    ```

18. 次のコードを接続クラスに追加して、OnConnection メソッドに追加した loadTestPackageExt.WebTestResultViewerExt.WindowClosed のイベント ハンドラー用の WebTesResultViewer_WindowClosed メソッドを作成します。

    ```csharp
    void WebTesResultViewer_WindowClosed(object sender, WebTestResultViewerExt.WindowClosedEventArgs e)
    {
        if (m_controls.ContainsKey(e.WebTestResultViewer.TestResultId))
        {
            m_controls.Remove(e.WebTestResultViewer.TestResultId);
        }
    }
    ```

     Visual Studio アドイン向けのコードが完成したので、Update メソッドを WebPerfTestResultsViewerControl プロジェクトの resultControl に追加する必要があります。

## <a name="add-code-to-the-webperftestresultsviewercontrol"></a>WebPerfTestResultsViewerControl にコードを追加する

1. **ソリューション エクスプローラー** で、WebPerfTestResultsViewerControl プロジェクト ノードを右クリックし、 **[プロパティ]** を選択します。

2. **[アプリケーション]** タブを選択して **[ターゲット フレームワーク]** ドロップダウン リストを選びます。次に、 **.NET Framework 4** 以降を選択します。 **[プロパティ]** ウィンドウを閉じます。

   これは、**Web パフォーマンス テスト結果ビューアー** の拡張に必要な DLL 参照をサポートするために必要です。

3. **ソリューション エクスプローラー** で、WebPerfTestResultsViewerControl プロジェクトの **[参照設定]** ノードを右クリックし、 **[参照の追加]** を選択します。

4. **[参照の追加]** ダイアログ ボックスの **[.NET]** タブをクリックします。

5. 下にスクロールして、 **[Microsoft.VisualStudio.QualityTools.WebTestFramework]** を選択します。

6. **[OK]** をクリックします。

7. *UserControl1.cs* ファイルに、次の Using ステートメントを追加します。

    ```csharp
    using Microsoft.VisualStudio.TestTools.WebTesting;
    using Microsoft.VisualStudio.TestTools.WebTesting.Rules;
    ```

8. *Connect.cs* ファイルの WebPerfTestResultsViewerAddin WebTestResultViewer_SelectedChanged メソッドから呼び出されて WebTestRequestResult が渡される Update メソッドを追加します。 Update メソッドは、WebTestRequestResult のメソッドに渡されるさまざまなプロパティを使用して DataGridView を設定します。

    ```csharp
    public void Update(WebTestRequestResult WebTestResults)
            {
                // Clear the DataGridView when a request is selected.
                resultControlDataGridView.Rows.Clear();
                // Populate the DataGridControl with properties from the WebTestResults.
                this.resultControlDataGridView.Rows.Add("Request: " + WebTestResults.Request.Url.ToString());
                this.resultControlDataGridView.Rows.Add("Response: " + WebTestResults.Response.ResponseUri.ToString());
                foreach (RuleResult ruleResult in WebTestResults.ExtractionRuleResults)
                {
                    this.resultControlDataGridView.Rows.Add("Extraction rule results: " + ruleResult.Message.ToString());
                }
                foreach (RuleResult ruleResult in WebTestResults.ValidationRuleResults)
                {
                    this.resultControlDataGridView.Rows.Add("Validation rule results: " + ruleResult.Message.ToString());
                }
                foreach (WebTestError webTestError in WebTestResults.Errors)
                {
                    this.resultControlDataGridView.Rows.Add("Error: " + webTestError.ErrorType.ToString() + " " + webTestError.ErrorSubtype.ToString() + " " + webTestError.ExceptionText.ToString());
                }
            }
    ```

## <a name="build-the-solution"></a>ソリューションをビルドする

- **[ビルド]** メニューの **[ソリューションのビルド]** を選択します。

## <a name="register-the-webperftestresultsvieweraddin-add-in"></a>WebPerfTestResultsViewerAddin アドインの登録

1. **[ツール]** メニューの **[アドイン マネージャー]** を選択します。

2. **[アドイン マネージャー]** ダイアログ ボックスが表示されます。

3. **[使用可能なアドイン]** 列の WebPerfTestResultsViewerAddin アドイン向けのチェック ボックスをオンにして、 **[スタートアップ]** および **[コマンド ライン]** 列の下のチェック ボックスをオフにします。

4. **[OK]** をクリックします。

## <a name="run-the-web-performance-test-using-the-web-test-results-viewer"></a>Web テスト結果ビューアーを使用し、Web パフォーマンス テストを実行する

1. Web パフォーマンス テストを実行すると、WebPerfTestResultsViewerAddin アドインの「サンプル」というタイトルの新しいタブが **Web パフォーマンス テスト結果ビューアー** に表示されます。

2. このタブをクリックして、DataGridView に示されているプロパティを確認します。

## <a name="net-security"></a>.NET セキュリティ

悪質なアドインが自動的にアクティブにならないようにしてセキュリティを強化するために、Visual Studio の **[ツール] メニューの [オプション]** ページには、 **[アドイン/マクロ セキュリティ]** という名前の設定が用意されています。

さらに、このオプション ページでは、Visual Studio が *.AddIn* 登録ファイルを検索するためのフォルダーを指定できます。 このようにフォルダーを指定すると、 *.AddIn* 登録ファイルを読み取ることができる場所が制限されるので、セキュリティが強化されます。 これは、悪意のある *.AddIn* ファイルが意図せず使用されるのを防ぐのに役立ちます。

**アドインのセキュリティ設定**

アドイン セキュリティのオプション ページにある設定は、次のとおりです。

- **アドイン コンポーネントに読み込みを許可する。** 既定でオンになっています。 オンにすると、アドインを Visual Studio で読み込むことができます。 オフにすると、アドインを Visual Studio で読み込むことができなくなります。

- **アドイン コンポーネントに URL からの読み込みを許可する。** 既定ではオンになっていません。 オンにすると、アドインは外部 Web サイトから読み込むことができます。 オフにすると、リモート アドインは Visual Studio で読み込むことができなくなります。 何らかの原因でアドインを読み込むことができない場合は、Web から読み込むこともできません。 この設定では、アドイン DLL の読み込みだけが制御されます。 *.Addin* 登録ファイルは、常にローカル システムに存在する必要があります。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.UserControl>
- <xref:Microsoft.VisualStudio.TestTools.LoadTesting>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules>
- <xref:System.Windows.Forms.UserControl>
- <xref:System.Windows.Forms.DataGrid>
- [ロード テスト用のカスタム コードおよびカスタム プラグインの作成](../test/create-custom-code-and-plug-ins-for-load-tests.md)
