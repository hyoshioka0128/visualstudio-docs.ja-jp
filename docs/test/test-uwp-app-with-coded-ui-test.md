---
title: コード化された UI テストを使用して UWP アプリをテストする
ms.date: 05/31/2018
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- uwp
ms.openlocfilehash: fdd3d98bd848bb6fe679809a58f2e316a316f012
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75590359"
---
# <a name="create-a-coded-ui-test-to-test-a-uwp-app"></a>UWP アプリをテストするためのコード化された UI テストの作成

この記事では、ユニバーサル Windows プラットフォーム (UWP) アプリのコード化された UI テストを作成する方法について説明します。

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

## <a name="create-a-uwp-app-to-test"></a>テストする UWP アプリの作成

最初の手順では、テストを実行する簡単な UWP アプリを作成します。

1. Visual Studio で、Visual C# または Visual Basic の **[空のアプリ (ユニバーサル Windows)]** テンプレートを使用して、新しいプロジェクトを作成します。

   ::: moniker range="vs-2017"

   ![[空のアプリ (ユニバーサル Windows)] テンプレート](../test/media/blank-uwp-app-template.png)

   ::: moniker-end

1. **[新しいユニバーサル Windows プラットフォーム プロジェクト]** ダイアログで、 **[OK]** を選択して既定のプラットフォーム バージョンをそのまま使用します。

1. **ソリューション エクスプローラー**で、*MainPage.xaml* を開きます。

   **XAML デザイナー**でファイルが開きます。

1. ボタン コントロールとテキスト ボックス コントロールを、 **[ツールボックス]** からデザイン サーフェイスにドラッグします。

     ![UWP アプリをデザインする](../test/media/toolbox-controls.png)

1. コントロールに名前を付けます。 テキスト ボックス コントロールを選択し、**[プロパティ]** ウィンドウの **[名前]** フィールドに「**textBox**」と入力します。 ボタン コントロールを選択し、**[プロパティ]** ウィンドウの **[名前]** フィールドに「**button**」と入力します。

1. ボタン コントロールをダブルクリックし、次のコードを `Button_Click` メソッドの本文に追加します。 後で作成するコード化された UI テストで確認するため、このコードでは単にテキスト ボックスのテキストをボタン コントロールの名前に設定します。

   ```csharp
   this.textBox.Text = this.button.Name;
   ```

   ```vb
   Me.textBox.Text = Me.button.Name
   ```

1. **Ctrl**+**F5** キーを押してアプリを実行します。 次のように表示されます。

   ![ボタンとテキスト ボックスがある UWP アプリ](media/uwp-app.png)

## <a name="create-a-coded-ui-test"></a>コード化された UI テストの作成

1. ソリューションにテスト プロジェクトを追加するには、**ソリューション エクスプローラー**でソリューションを右クリックして、 **[追加]**  >  **[新しいプロジェクト]** の順に選択します。

1. **[コード化された UI テスト プロジェクト (ユニバーサル Windows)]** テンプレートを検索して選択します。

   ::: moniker range="vs-2017"

   ![新しいコード化された UI テスト プロジェクト](../test/media/coded-ui-test-project-uwp-template.png)

   ::: moniker-end

   > [!NOTE]
   > **[コード化された UI テスト プロジェクト (ユニバーサル Windows)]** テンプレートが表示されない場合は、[コード化された UI テスト コンポーネントをインストールする](../test/use-ui-automation-to-test-your-code.md#install-the-coded-ui-test-component)必要があります。

1. **[コード化された UI テストのコードの生成]** ダイアログで、 **[テストを手動で編集]** を選択します。

   ![[コード化された UI テストのコードの生成] ダイアログ](../test/media/manually-edit-the-test.png)

1. UWP アプリがまだ実行されていない場合は、**Ctrl**+**F5** キーを押して起動します。

1. `CodedUITestMethod1` メソッドにカーソルを置き、**[テスト]** > **[コード化された UI テストのコードの生成]** > **[コード化された UI テスト ビルダー]** の順に選択して、**[コード化された UI テスト ビルダー]** ダイアログを開きます。

1. UI コントロール マップにコントロールを追加します。 **[コード化された UI テスト ビルダー]** の十字線ツールを使用して、UWP アプリのボタン コントロールを選択します。 **[アサーションの追加]** ダイアログで、必要に応じて **[UI コントロール マップ]** ウィンドウを展開し、 **[コントロールの UI コントロール マップへの追加]** を選択します。

     ![UI マップにコントロールを追加](../test/media/add-control-to-ui-control-map.png)

1. 前の手順を繰り返して、テキスト ボックス コントロールを UI コントロール マップに追加します。

1. **[コード化された UI テスト ビルダー]** ダイアログで、 **[コードの生成]** を選択するか、**Ctrl**+**G** キーを押します。 次に、 **[生成]** を選択し、UI コントロール マップの変更に対応するコードを作成します。

     ![UI マップのコードを生成](../test/media/generate-code-dialog.png)

1. ボタンがクリックされたときにテキスト ボックス内のテキストが **button** に変更されることを確認するには、ボタンをクリックします。

     ![ボタン コントロールをクリックして TextBox 値を設定する](../test/media/uwp-app-button-textbox.png)

1. テキスト ボックス コントロールのテキストを検証するアサーションを追加します。 十字線ツールを使用してテキスト ボックス コントロールを選択し、**[アサーションの追加]** ダイアログで **[Text]** プロパティを選択します。 次に、 **[アサーションの追加]** を選択するか、**Alt**+**A** キーを押します。 **[アサーション エラーのメッセージ]** ボックスに、「**テキスト ボックス値は予期されていません。** 」などと入力し、 **[OK]** を選択します。

     ![十字線ツールでテキスト ボックスを選択し、アサーションを追加する](../test/media/add-assertion-for-text.png)

1. アサーションのテスト コードを生成します。 **[コード化された UI テスト ビルダー]** ダイアログで、 **[コードの生成]** を選択します。 **[コードの生成]** ダイアログで、 **[追加と生成]** を選択します。

     ![TextBox アサーションのコードを生成する](../test/media/add-and-generate-assert-method.png)

   **ソリューション エクスプローラー**で、*UIMap.Designer.cs* を開き、Assert メソッドとコントロール用に追加されたコードを表示します。

   > [!TIP]
   > Visual Basic を使用している場合は、*CodedUITest1.vb* を開きます。 次に、`CodedUITestMethod1()` テスト メソッド コードで、Assert メソッド `Me.UIMap.AssertMethod1()` の呼び出しを右クリックし、 **[定義に移動]** を選択します。 コード エディターで *UIMap.Designer.vb* が開き、Assert メソッドとコントロール用に追加されたコードを確認できます。

    > [!WARNING]
    > *UIMap.designer.cs* ファイルや *UIMap.Designer.vb* ファイルは直接変更しないでください。 変更しても、その変更内容はテストの生成時に上書きされます。

    Assert メソッドは次のようになります。

    ```csharp
    public void AssertMethod1()
    {
        #region Variable Declarations
        XamlEdit uITextBoxEdit = this.UIUWPAppWindow.UITextBoxEdit;
        #endregion

        // Verify that the 'Text' property of 'textBox' text box equals 'button'
        Assert.AreEqual(this.AssertMethod1ExpectedValues.UITextBoxEditText, uITextBoxEdit.Text, "Textbox value is unexpected.");
    }
    ```

    ```vb
    Public Sub AssertMethod1()
        Dim uITextBoxEdit As XamlEdit = Me.UIApp2Window.UITextBoxEdit

        'Verify that the 'Text' property of 'textBox' text box equals 'button'
        Assert.AreEqual(Me.AssertMethod1ExpectedValues.UITextBoxEditText, uITextBoxEdit.Text, "Textbox value is unexpected.")
    End Sub
    ```

1. 次に、テストする UWP [アプリ](#create-a-uwp-app-to-test)の **AutomationId** を取得する必要があります。 Windows の **[スタート]** メニューを開き、アプリのタイルを表示します。 その後、十字線ツール ![ターゲット アイコン](media/target-icon.png) を **[コード化された UI テスト ビルダー]** ダイアログからアプリのタイルにドラッグします。 タイルが青色のボックスで囲まれている場合は、マウスを放します。

   ![十字線ツール](media/cross-hair-tool.png)

   **[アサーションの追加]** ダイアログ ボックスが開き、アプリの **AutomationId** が表示されます。 **AutomationId** を右クリックし、 **[値をクリップボードにコピー]** を選択します。

   ![[アサーションの追加] ダイアログの AutomationID](../test/media/automation-id.png)

1. UWP アプリを起動するコードをテスト メソッドに追加します。 **ソリューション エクスプローラー**で、*CodedUITest1.cs* または *CodedUITest1.vb* を開きます。 `AssertMethod1` の呼び出しの上に、UWP アプリを起動するコードを追加します。

   ```csharp
   XamlWindow.Launch("af5ecd75-f252-45a1-9e7e-c6f1d8f054ff_0q1pp7qrjexbp!App")
   ```

   ```vb
   XamlWindow myAppWindow = XamlWindow.Launch("af5ecd75-f252-45a1-9e7e-c6f1d8f054ff_0q1pp7qrjexbp!App");
   ```

   コード例のオートメーション ID を、前の手順でクリップボードにコピーした値に置き換えます。

   > [!IMPORTANT]
   > オートメーション ID の先頭をトリミングし、**P~** などの文字を削除します。 これらの文字をトリミングしないと、テストで、アプリを起動しようとしたときに `Microsoft.VisualStudio.TestTools.UITest.Extension.PlaybackFailureException` がスローされます。

1. 次に、ボタンをクリックするコードをテスト メソッドに追加します。 `XamlWindow.Launch` の後の行に、ボタン コントロールをタップするジェスチャを追加します。

   ```csharp
   Gesture.Tap(this.UIMap.UIUWPAppWindow.UIButtonButton);
   ```

   ```vb
   Gesture.Tap(Me.UIMap.UIUWPAppWindow.UIButtonButton)
   ```

   コードを追加すると、`CodedUITestMethod1` テスト メソッドは次のようになります。

   ```csharp
   [TestMethod]
   public void CodedUITestMethod1()
   {
       XamlWindow.Launch("af5ecd75-f252-45a1-9e7e-c6f1d8f054ff_0q1pp7qrjexbp!App");

       Gesture.Tap(this.UIMap.UIUWPAppWindow.UIButtonButton);

       // To generate code for this test, select "Generate Code for Coded UI Test" from the shortcut menu and select one of the menu items.
       this.UIMap.AssertMethod1();
   }
   ```

   ```vb
   <CodedUITest(CodedUITestType.WindowsStore)>
   Public Class CodedUITest1

       <TestMethod()>
       Public Sub CodedUITestMethod1()

           ' Launch the app.
           XamlWindow.Launch("af5ecd75-f252-45a1-9e7e-c6f1d8f054ff_0q1pp7qrjexbp!App")

           '// Tap the button.
           Gesture.Tap(Me.UIMap.UIUWPAppWindow.UIButtonButton)

           Me.UIMap.AssertMethod1()
       End Sub
   ```

1. テスト プロジェクトをビルドし、**[テスト]** > **[Windows]** > **[テスト エクスプローラー]** の順に選択して、**テスト エクスプローラー**を開きます。

1. **[すべて実行]** を選択してテストを実行します。

   アプリが開き、ボタンがタップされ、テキスト ボックスの **Text** プロパティが設定されます。 Assert メソッドでは、テキスト ボックスの **Text** プロパティが検証されます。

   テストの完了後、テストが成功したことが**テスト エクスプローラー**に表示されます。

   ![成功したテストがテスト エクスプローラーに表示される](../test/media/test-explorer-coded-ui-test-passed.png)

## <a name="q--a"></a>Q & A

### <a name="q-why-dont-i-see-the-option-to-record-my-coded-ui-test-in-the-generate-code-for-a-coded-ui-test-dialog"></a>Q:[コード化された UI テスト] ダイアログの [コードの生成] に、コード化された UI テストを記録するオプションが表示されないのはなぜですか?

**A**:記録するオプションは、UWP アプリではサポートされません。

### <a name="q-can-i-create-a-coded-ui-test-for-my-uwp-apps-based-on-winjs"></a>Q:WinJS ベースの UWP アプリのコード化された UI テストを作成できますか?

**A**:いいえ。サポートされるのは XAML ベースのアプリのみです。

### <a name="q-why-cant-i-modify-the-code-in-the-uimapdesigner-file"></a>Q:UIMap.Designer ファイルでコードを変更できないのはなぜですか?

**A**:*UIMapDesigner.cs* ファイルでコードを変更しても、 **[コード化された UI テスト ビルダー]** を使用してコードを生成するたびに変更内容が上書きされます。 記録されたメソッドを変更する必要がある場合は、メソッドを *UIMap.cs* ファイルにコピーし、メソッド名を変更します。 *UIMap.cs* ファイルを使用すると、*UIMapDesigner.cs* ファイルのメソッドやプロパティをオーバーライドできます。 *CodedUITest.cs* ファイルの元のメソッドへの参照を削除し、変更したメソッド名に置き換えます。

## <a name="see-also"></a>関連項目

- [UI オートメーションを使用してコードをテストする](../test/use-ui-automation-to-test-your-code.md)
- [UWP コントロールの一意のオートメーション プロパティを設定する](../test/set-a-unique-automation-property-for-windows-store-controls-for-testing.md)
