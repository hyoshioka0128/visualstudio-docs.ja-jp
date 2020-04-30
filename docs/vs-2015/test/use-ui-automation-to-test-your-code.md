---
title: UI オートメーションを使用してコードをテストする | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
f1_keywords:
- vs.codedUITest
- vs.codedUITest.recorder
- vs.codedUITest.testbuilder
- vs.codedUITest.addAssertions
- vs.codedUITest.createdialog
helpviewer_keywords:
- automated tests, testing UI interface
- coded UI test
ms.assetid: ad9e3eaa-ab86-436e-95b8-dc20eb1f8b2a
caps.latest.revision: 87
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e054909bb8f020ed496185f0ba64aafec016358b
ms.sourcegitcommit: da5ebc29544fdbdf625ab4922c9777faf2bcae4a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "82586451"
---
# <a name="use-ui-automation-to-test-your-code"></a>UI オートメーションを使用してコードをテストする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ユーザー インターフェイス (UI) を介してアプリケーションを実行する自動テストは、*コード化された UI テスト* (CUIT) と呼ばれます。 これらのテストには、UI コントロールの機能テストが含まれます。 これらのテストで、アプリケーション全体が、ユーザー インターフェイスを含めて正しく機能していることを検証できます。 コード化された UI テストは、Web ページなど、ユーザー インターフェイスに検証やその他のロジックがある場合に特に有用です。 また、既存の手動テストを自動化するために頻繁に使用されます。

 次の図に示すように、一般的な開発環境では、最初はアプリケーションをビルドし (F5 キー)、いくつかの UI コントロールをクリックして正しく動作していることを確認するだけです。 次に、アプリケーションを手動でテストし続けなくてもよいように、コード化されたテストを作成しようとするでしょう。 アプリケーションでテストする特定の機能に応じて、機能テストまたは統合テストのコードを記述できます。テストには、UI レベルでのテストが含まれている場合も含まれていない場合もあります。 一部のビジネス ロジックに直接アクセスするだけの場合は、単体テストのコードを記述することができます。 ただし、特定の状況下では、アプリケーションのさまざまな UI コントロールのテストを含める方が有益な場合があります。 コード化された UI テストでは、最初の (F5 キー) シナリオを自動化でき、コード チャーンがアプリケーションの機能に影響を与えないことを検証できます。

 ![アプリケーション開発中のテスト](../test/media/cuit-overview.png "CUIT_Overview")

 コード化された UI テストの作成は簡単です。 CUIT テスト ビルダーをバックグラウンドで実行中に、テストを手動で実行します。 特定のフィールドに表示する値を指定することもできます。 CUIT テスト ビルダーは操作を記録し、それらの記録からコードを生成します。 テストの作成後、特殊なエディターでテストを編集して、操作のシーケンスを変更することができます。

 または、Microsoft Test Manager に記録されたテスト ケースがある場合は、それからコードを生成できます。 詳細については、「[手動テストの記録と再生](/azure/devops/test/mtm/record-play-back-manual-tests)」をご覧ください。

 コーディングよりテストに集中している場合でも、特殊な CUIT テスト ビルダーとエディターによって、コード化された UI テストの作成および編集が容易になります。 ただし、開発者がより高度な方法でこのテストを拡張する場合に備え、コードは簡単にコピーして適応できるように構造化されています。 たとえば、Web サイトで 1 つの商品を購入するテストを記録した後、生成されたコードを編集することにより、複数の商品を購入するループを追加することができます。

 **必要条件**

- Visual Studio Enterprise

  コード化された UI テストでサポートされているプラットフォームと構成の詳細については、「[コード化された UI テストと操作の記録でサポートされている構成とプラットフォーム](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)」をご覧ください。

  **このトピックの内容**

- [コード化された UI テストの作成](#VerifyingCodeUsingCUITCreate)

  - [Main プロシージャ](#VerifyingCodeUsingCUITCreate)

  - [アプリケーションを開始および停止する](#starting)

  - [UI コントロールのプロパティの検証](#VerifyingCodeUsingCUITGenerateAssertions)

- [コード化された UI テストをカスタマイズする](#VerifyingCodeCUITModify)

  - [生成されたコード](#generatedCode)

  - [UI コントロールの操作とプロパティのコーディング](#actions)

  - [デバッグ](#debugging)

- [次の内容](#VerifyCodeUsingCUITWhatsNext)

## <a name="creating-coded-ui-tests"></a><a name="VerifyingCodeUsingCUITCreate"></a>コード化された UI テストの作成

1. **コード化された UI テストプロジェクトを作成します。**

    コード化された UI テストは、コード化された UI テスト プロジェクトに含まれている必要があります。 コード化された UI テスト プロジェクトをまだ作成していない場合は、プロジェクトを作成します。 ソリューションのショートカット メニューの **[ソリューション エクスプローラー]** で、**[追加]**、**[新しいプロジェクト]** を選択し、**[Visual Basic]** または **[Visual C#]** を選択します。 次に、**[テスト]**、**[コード化された UI テスト]** を選択します。

   - <em>**[コード化された UI テスト]</em>* プロジェクト テンプレートが表示されません。*

      コード化された UI テストをサポートしないバージョンの Visual Studio を使用している可能性があります。 コード化された UI テストを作成するには、Visual Studio Enterprise を使用する必要があります。

2. **コード化された UI テストファイルを追加します。**

    コード化された UI プロジェクトを作成した場合は、最初の CUIT ファイルが自動的に追加されます。 別のテスト ファイルを追加するには、コード化された UI テスト プロジェクトのショートカット メニューを開き、**[追加]** をポイントし、**[コード化された UI テスト]** を選択します。

    ![コード化された UI テストを作成する](../test/media/codedui-create.png "CodedUI_Create")

    **[コード化された UI テストのコードの生成]** ダイアログ ボックスで、**[操作の記録、UI マップの編集、またはアサーションの追加]** を選択します。

    ![操作の記録の選択](../test/media/codedui-codegendialogb.png "CodedUI_CodeGenDialogB")

    コード化された UI テスト ビルダーが表示され、Visual Studio は最小化されます。

    ![コード化された UI テスト ビルダー](../test/media/codedui-testbuilder.png "CodedUI_TestBuilder")

3. 一連**のアクションを記録**します。

    **記録を開始するには**、 **[記録する]** アイコンをクリックします。 必要に応じて、アプリケーションの起動など、アプリケーションでテストする操作を実行します。

    たとえば、Web アプリケーションをテストする場合は、ブラウザーを起動し、Web サイトに移動し、アプリケーションにログインします。

    受信メールを処理する場合などに、**記録を一時停止するには**、 **[一時停止]** を選択します。

   > [!WARNING]
   > デスクトップ上で実行されるすべてのアクションが記録されます。 機密データが記録される可能性のあるアクションを実行する場合には、記録を一時停止します。

    間違って記録した**操作を削除するには**、**[Edit Actions]**(操作の編集) を選択します。

    アクションをレプリケートする**コードを生成するに**は、[**コードの生成**] アイコンを選択し、コード化された UI テストメソッドの名前と説明を入力します。

4. **テキストボックスなどの UI フィールドの値を確認**します。

    コード化された UI テストビルダーで [**アサーションの追加**] を選択し、実行中のアプリケーションで UI コントロールを選択します。 表示されるプロパティの一覧で、テキスト ボックスの **Text** などのプロパティを選択します。 ショートカット メニューで、 **[アサーションの追加]** をクリックします。 ダイアログ ボックスで、比較演算子、比較対象値、およびエラー メッセージを選択します。

    アサーション ウィンドウを閉じ、 **[コードの生成]** を選択します。

    ![要素を対象としたコード化された UI テスト](../test/media/codedui-1.png "CodedUI_1")

   > [!TIP]
   > 操作の記録と値の検証を交互に行います。 操作または検証の各シーケンスの最後にコードを生成します。 必要に応じて、後で新しい操作と検証を挿入できます。

    詳細については、「[UI コントロールのプロパティを検証する](#VerifyingCodeUsingCUITGenerateAssertions)」をご覧ください。

5. **生成されたテストコードを表示**します。

    生成されたコードを表示するには、UI テスト ビルダー ウィンドウを閉じます。 コードで、各ステップに付けた名前を確認できます。 コードは作成した CUIT ファイルに記録されます。

   ```csharp
   [CodedUITest]
   public class CodedUITest1
   { ...
     [TestMethod]
     public void CodedUITestMethod1()
     {
         this.UIMap.AddTwoNumbers();
         this.UIMap.VerifyResultValue();
         // To generate more code for this test, select
         // "Generate Code" from the shortcut menu.
     }
   }
   ```

6. **アクションとアサーションをさらに追加**します。

    次に、テスト メソッド内の適切な位置にカーソルを置き、ショートカット メニューで、 **[コード化された UI テストのコードの生成]** を選択します。 新しいコードがカーソルの位置に挿入されます。

7. **テストアクションとアサーションの詳細を編集**します。

    UIMap.uitest を開きます。 このファイルはコード化された UI テスト エディターで開かれます。ここで、記録した操作のシーケンスやアサーションを編集できます。

    ![コード化された UI テスト エディター](../test/media/cuit-editor-edit.png "CUIT_Editor_edit")

    詳細については、「[コード化された UI テスト エディターを使用したコード化された UI テストの編集](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)」をご覧ください。

8. **テストを実行**します。

    テスト エクスプローラーを使用するか、テスト メソッドでショートカット メニューを開き、 **[テストの実行]** を選択します。 テストの実行方法の詳細については、このトピックの最後にある「 [[次へ]](#VerifyCodeUsingCUITWhatsNext)セクション」の「[テストエクスプローラーを使用して単体テストを実行](../test/run-unit-tests-with-test-explorer.md)する」および「*コード化された UI テストを実行するための追加オプション*」を参照してください。

   このトピックの残りのセクションでは、このプロシージャ内の各ステップについてさらに詳しく説明します。

   詳細な例については、「[チュートリアル: コード化された UI テストの作成、編集、および保守](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)」を参照してください。 このチュートリアルでは、簡単な Windows Presentation Foundation (WPF) アプリケーションを作成して、コード化された UI テストの作成、編集、および保守を行う方法について説明します。 また、さまざまなタイミングの問題やコントロールのリファクタリングによって機能が損なわれたテストを修正するための解決策を示します。

### <a name="starting-and-stopping-the-application-under-test"></a><a name="starting"></a> テスト対象のアプリケーションを開始および停止する
 *テストごとにアプリケーション、ブラウザー、またはデータベースを個別に起動および停止したくありません。操作方法回避するには、*

- ![Prerequsite](../test/media/prereq.png "前提条件")テスト対象のアプリケーションを開始するための操作を記録しない場合は、[**レコード**] アイコンを選択する前にアプリケーションを起動する必要があります。

- ![Prerequsite](../test/media/prereq.png "前提条件")テストの終了時に、テストを実行するプロセスが終了します。 テストでアプリケーションを起動した場合、アプリケーションは通常は閉じます。  終了時にテストがアプリケーションを閉じないようにするには、ソリューションに .runsettings ファイルを追加し、`KeepExecutorAliveAfterLegacyRun` オプションを使用する必要があります。 詳細については、「[.runsettings ファイルを使用して単体テストを構成する](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)」をご覧ください。

- ![Prerequsite](../test/media/prereq.png "前提条件")[TestInitialize] 属性で識別されるテスト初期化メソッドを追加できます。このメソッドは、各テストメソッドの開始時にコードを実行します。 たとえば、TestInitialize メソッドからアプリケーションを起動することができます。

- ![Prerequsite](../test/media/prereq.png "前提条件")[TestCleanup] 属性で識別されるテストクリーンアップメソッドを追加して、各テストメソッドの最後にコードを実行できます。 たとえば、アプリケーションを終了するメソッドは、TestCleanup メソッドから呼び出すことができます。

### <a name="validating-the-properties-of-ui-controls"></a><a name="VerifyingCodeUsingCUITGenerateAssertions"></a> UI コントロールのプロパティを検証する
 **コード化された UI テスト ビルダー**を使用すると、テストの [UIMap](/previous-versions/dd580454(v=vs.140)) にユーザー インターフェイス (UI) を追加したり、UI コントロールのアサーションを使用する検証メソッドのコードを生成したりできます。

 UI コントロールのアサーションを作成するには、コード化された UI テスト ビルダーの**アサーションの追加**ツールを選択し、正しいかどうかを検証するテスト対象アプリケーションのコントロールにドラッグします。 コントロールが枠で囲まれたら、マウス ボタンを離します。 コントロール クラス コードがすぐに `UIMap.Designer.cs` ファイルに作成されます。

 ![要素を対象としたコード化された UI テスト](../test/media/codedui-1.png "CodedUI_1")

 これで、このコントロールのプロパティが **[アサーションの追加]** ダイアログ ボックスに表示されます。

 特定のコントロールに移動するには、矢印 **(<<)** を選択して **[UI コントロール マップ]** のビューを展開する方法もあります。 親、兄弟、子の各コントロールを見つけるには、マップのどこかをクリックし、方向キーを使用してツリー内を移動します。

 ![コード化された UI テストのプロパティ](../test/media/codedui-2.png "CodedUI_2")

- *アプリケーションでコントロールを選択してもプロパティが表示されません、または UI コントロール マップにコントロールが表示されません。*

   アプリケーション コードで、検証するコントロールは、HTML ID 属性や WPF UId などの一意の ID を持っている必要があります。 これらの ID を追加するために、アプリケーション コードの更新が必要になる場合があります。

  次に、検証する UI コントロールのプロパティのショートカット メニューで、 **[アサーションの追加]** をポイントします。 **[アサーションの追加]** ダイアログ ボックスで、アサーションの **[比較子]** (<xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.AreEqual%2A> など) を選択し、 **[比較対象値]** にアサーションの値を入力します。

  ![コード化された UI テストのアサーション](../test/media/codedui-3.png "CodedUI_3")

  テスト用のアサーションをすべて追加したら、 **[OK]** を選択します。

  アサーションのコードを生成し、コントロールを UI マップに追加するために、 **[コードの生成]** アイコンを選択します。 コード化された UI テスト メソッドの名前と説明を入力します。これらはメソッドのコメントとして追加されます。 **[追加と生成]** を選択します。 次に、 **[閉じる]** アイコンをクリックして、 **[コード化された UI テスト ビルダー]** を閉じます。 これで、次のようなコードが生成されます。 たとえば、入力した名前が `AssertForAddTwoNumbers` の場合、コードは次の例のようになります。

- コード化された UI テスト ファイルのテスト メソッドに、AssertForAddTwoNumbers という Assert メソッドの呼び出しを追加します。

  ```
  [TestMethod]
  public void CodedUITestMethod1()
  {
      this.UIMap.AddTwoNumbers();
      this.UIMap.AssertForAddTwoNumbers();
  }
  ```

   このファイルを編集して、ステップとアサーションの順序を変更するか、新しいテスト メソッドを作成することができます。 さらにコードを追加するには、テスト メソッドにカーソルを置き、ショートカット メニューの **[コード化された UI テストのコードの生成]** を選択します。

- UI マップ (UIMap.uitest) に `AssertForAddTwoNumbers` という名前のメソッドを追加します。 このファイルはコード化された UI テスト エディターで開かれ、そこでアサーションを編集できます。

   ![コード化された UI テストエディターを使用したアサートの編集](../test/media/cuit-editor-assert.png "CUIT_Editor_assert")

   詳細については、「[コード化された UI テスト エディターを使用したコード化された UI テストの編集](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)」をご覧ください。

   UIMap.Designer.cs で、アサーション メソッドの生成されたコードを表示することもできます。 ただし、このファイルは編集しないでください。 適合させたバージョンのコードを作成する場合は、メソッドを UIMap.cs などの別のファイルにコピーし、メソッドの名前を変更し、メソッドを編集します。

  ```
  public void AssertForAddTwoNumbers()
  {
      ...
  }
  ```

  *コード化された UI テストビルダーから [アサーションの追加] ツールを選択しようとすると、選択したコントロールがフォーカスを失い、表示されなくなります。コントロールを選択操作方法には*
  **キーボードを使用して非表示のコントロールを選択**する

  [コントロールを追加し、プロパティを検証する](#VerifyingCodeUsingCUITGenerateAssertions)とき、キーボードが必要になる場合もあります。 たとえば、コンテキスト メニュー コントロールを使用するコード化された UI テストを記録するとき、コード化された UI テスト ビルダーの [アサーションの追加] ツールで選択しようとすると、コントロールのメニュー項目の一覧がフォーカスを失い、非表示になります。 これを次の図に示します。Internet Explorer で、[アサーションの追加] ツールでコンテキスト メニューを選択しようとすると、メニューはフォーカスを失い、非表示になります。

  ![CodedUITest&#95;SelectControlKeyboard](../test/media/codeduitest-selectcontrolkeyboard.png "CodedUITest_SelectControlKeyboard")

  キーボードを使用して UI コントロールを選択するには、マウスをコントロールの上に置きます。 次に、**Ctrl** キーと **I** キーを同時に押します。 キーを離します。 コントロールは、コード化された UT のテスト ビルダーによって記録されます。

> [!WARNING]
> Microsoft Lync を使用している場合は、コード化された UI テスト ビルダーを起動する前に Lync を閉じる必要があります。 Microsoft Lync は、**Ctrl + I** のキーボード ショートカットに干渉します。

 *コントロール上のマウスホバーを記録できません。これを回避する方法はありますか。*
 **マウス ホバーを手動で記録する**

 状況によっては、コード化された UI テストで使用される特定のコントロールで、キーボードを使用してマウス ホバー イベントを手動で記録することが必要な場合があります。 たとえば、Windows フォームまたは Windows Presentation Foundation (WPF) アプリケーションをテストするとき、カスタム コードが使用されている場合があります。 または、マウスが置かれたときにツリー ノードを展開するなど、コントロールの上にマウスが置かれたときに特別な動作が定義されている場合もあります。 このような状況をテストするには、定義済みのキーボードのキーを押して、コントロールの上にマウスを置いていることをコード化された UI テスト ビルダーに手動で通知する必要があります。

 コード化された UI テストを実行するとき、コントロール上にマウスを置きます。 そして、キーボードの Ctrl キーを押しながら、Shift キーと R キーを押したままにします。 キーを離します。 コード化された UT のテスト ビルダーによって、マウス ホバー イベントが記録されます。

 ![CodedUI&#95;ホバー](../test/media/codedui-hover.png "CodedUI_Hover")

 テスト メソッドを生成すると、次の例のようなコードが UIMap.Desinger.cs ファイルに追加されます。

```csharp
// Mouse hover '1' label at (87, 9)
Mouse.Hover(uIItem1Text, new Point(87, 9));

```

 *マウスホバーイベントをキャプチャするためのキーの割り当ては、環境内の他の場所で使用されています。既定のキーの割り当てを変更できますか。*
 **マウス ホバーのキーボード割り当てを構成する**

 必要に応じて、コード化された UI テストでマウス ホバー イベントを適用するために使用される既定のキーボード割り当て Ctrl + Shift + R は、異なるキーを使用するように構成できます。

> [!WARNING]
> 通常は、マウス ホバー イベントのキーボードの割り当てを変更する必要はありません。 キーボードの割り当てを再設定するときは注意してください。 選択したキーボードの割り当ては、既に Visual Studio またはテスト中のアプリケーション内の他の場所で使用されている可能性もあります。

 キーボードの割り当てを変更するには、次の構成ファイルを変更する必要があります:

 `<drive letter:>\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\CodedUITestBuilder.exe.config`

 構成ファイルで、`HoverKeyModifier` および `HoverKey` キーの値を変更して、キーボードの割り当てを変更します。

```
<!-- Begin : Background Recorder Settings -->
<!-- HoverKey to use. -->
<add key="HoverKeyModifier" value="Control, Shift"/>
<add key="HoverKey" value="R"/>

```

 *Web サイトでのマウスホバーの記録に問題があります。この修正プログラムもありますか。*
 **Web ブラウザーの暗黙のマウス ホバーを設定する**

 多くの Web サイトでは、特定のコントロールの上にマウスを置くと、そのコントロールが展開され、追加の詳細情報が表示されます。 通常、これらはデスクトップ アプリケーションのメニューのように見えます。 これが一般的なパターンであるため、コード化された UI テストでは Web 参照に対する暗黙のホバーが有効になります。 たとえば、Internet Explorer でホバーを記録すると、イベントが発生します。 これらのイベントによって、ホバーが重複して記録されることがあります。 このため、暗黙のホバーは UI テスト構成ファイルで `ContinueOnError` が `true` に設定された状態で記録されます。 これによって、ホバー イベントが失敗した場合でも再生は続行されます。

 Web ブラウザーで暗黙のホバーの記録を有効にするには、構成ファイルを開きます。

 `<drive letter:>\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\CodedUITestBuilder.exe.config`

 次の例に示すように、構成ファイルでキー `RecordImplicitiHovers` が `true` の値に設定されていることを確認します。

```
<!--Use this to enable/disable recording of implicit hovers.-->
<add key="RecordImplicitHover" value="true"/>

```

## <a name="customizing-your-coded-ui-test"></a><a name="VerifyingCodeCUITModify"></a>コード化された UI テストのカスタマイズ
 コード化された UI テストの作成後、Visual Studio で次のいずれかのツールを使用してテストを編集できます。

- **コード化された UI テスト ビルダー:** コード化された UI テスト ビルダーを使用して、テストにコントロールや検証を追加します。 このトピックの「[コントロールを追加し、プロパティを検証する](#VerifyingCodeUsingCUITGenerateAssertions)」セクションをご覧ください。

- **コード化された UI テスト エディター:** コード化された UI テスト エディターを使用すると、コード化された UI テストを簡単に変更できます。 Coded UI Test Editor (コード化された UI テスト エディター) を使用すると、テスト メソッドを検索、表示、および編集できます。 また、UI コントロール マップ内の UI 操作および関連コントロールを編集することもできます。 詳細については、「[コード化された UI テスト エディターを使用したコード化された UI テストの編集](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)」をご覧ください。

- **コード エディター:**

  - このトピックの「[UI コントロールの操作とプロパティのコーディング](#actions)」セクションで説明しているように、テストのコントロールのコードを手動で追加します。

  - コード化された UI テストを作成した後、データ ドリブンになるようにテストを変更できます。 詳細については、「[データ ドリブンのコード化された UI テストの作成](../test/creating-a-data-driven-coded-ui-test.md)」をご覧ください。

  - コード化された UI テストの再生では、テストに対して指示することで、ウィンドウの表示やプログレス バーの非表示などの特定のイベントが発生するまで待機することができます。 これを行うには、適切な UITestControl.WaitForControlXXX() メソッドを追加します。 使用できるメソッドの完全な一覧については、「[再生中に特定のイベントを待機するようにコード化された UI テストを設定](../test/making-coded-ui-tests-wait-for-specific-events-during-playback.md)」をご覧ください。 WaitForControlEnabled メソッドを使用してコントロールが有効になるまで待機するコード化された UI テストの例については、「[チュートリアル: コード化された Ui テストの作成、編集、および保守](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)」を参照してください。

  - コード化された UI テストには、Internet Explorer 9 と Internet Explorer 10 に含まれる HTML5 コントロールの一部のサポートが含まれます。 詳細については、「コード化された[UI テストでの HTML5 コントロールの使用](../test/using-html5-controls-in-coded-ui-tests.md)」を参照してください。

  - **コード化された UI テストのコーディング ガイダンス:**

    - [コード化された UI テストの構造](../test/anatomy-of-a-coded-ui-test.md)

    - [コード化された UI テストのベストプラクティス](../test/best-practices-for-coded-ui-tests.md)

    - [複数の UI マップでの大規模アプリケーションのテスト](../test/testing-a-large-application-with-multiple-ui-maps.md)

    - [コード化された UI テストと操作の記録でサポートされる構成とプラットフォーム](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)

### <a name="the-generated-code"></a><a name="generatedCode"></a>生成されたコード
 **[コードの生成]** を選択すると、いくつかのコードが作成されます。

- **テスト メソッド内の行。**

  ```csharp
  [CodedUITest]
  public class CodedUITest1
  { ...
    [TestMethod]
    public void CodedUITestMethod1()
    {
        this.UIMap.AddTwoNumbers();
        // To generate more code for this test, select
        // "Generate Code" from the shortcut menu.      }
  }
  ```

   このメソッド内で右クリックして、記録された操作および検証をさらに追加します。 メソッドを手動で編集して、コードを拡張または変更することもできます。 たとえば、コードの一部をループで囲むことができます。

   また、新しいテスト メソッドを追加し、同様にそれらにコードを追加できます。 各テスト メソッドは、`[TestMethod]` 属性を持っている必要があります。

- **UIMap. uitest のメソッド**

   このメソッドには、記録した操作または検証した値の詳細が含まれます。 UIMap.uitest を開いて、このコードを編集できます。 これは特殊なエディターで開かれ、記録された操作を削除またはリファクタリングできます。

   また、UIMap.Designer.cs で生成されたメソッドを表示できます。 このメソッドによって、テストの実行時に記録した操作が実行されます。

  ```csharp
  // File: UIMap.Designer.cs
  public partial class UIMap
  {
    /// <summary>
    /// Add two numbers
    /// </summary>
    public void AddTwoNumbers()
    { ...   }
  }
  ```

  > [!WARNING]
  > このファイルはさらにテストを作成すると再生成されるため、ファイルを編集しないでください。

   これらのメソッドを UIMap.cs にコピーして、メソッドの適合させたバージョンを作成できます。 たとえば、テスト メソッドから呼び出すことができるパラメーター化されたバージョンを作成できます。

  ```csharp
  // File: UIMap.cs
  public partial class UIMap // Same partial class
  {
    /// <summary>
    /// Add two numbers – parameterized version
    /// </summary>
    public void AddTwoNumbers(int firstNumber, int secondNumber)
    { ...   // Code modified to use parameters.
    }
  }
  ```

- **Uitest の宣言**

   これらの宣言は、テストで使用されるアプリケーションの UI コントロールを表します。 これらは、コントロールの操作とプロパティへのアクセスのために、生成されたコードによって使用されます。

   独自のコードを記述する場合も、これらを使用できます。 たとえば、テスト メソッドで Web アプリケーションのハイパーリンクの選択やテキスト ボックスへの値の入力を実行したり、フィールドの値に基づいて分岐して別のテスト操作を行ったりすることができます。

   大規模なアプリケーションのテストを容易にするために、複数のコード化された UI テストと複数の UI マップ オブジェクトおよびファイルを追加できます。 詳細については、「[複数の UI マップを使用した大規模なアプリケーションのテスト](../test/testing-a-large-application-with-multiple-ui-maps.md)」を参照してください。

  生成されるコードの詳細については、「コード化された[UI テストの構造](../test/anatomy-of-a-coded-ui-test.md)」を参照してください。

### <a name="coding-ui-control-actions-and-properties"></a><a name="actions"></a>UI コントロールの操作とプロパティのコーディング
 コード化された UI テストで UI テストのコントロールを使用する場合、コントロールは操作とプロパティの 2 つに分類されます。

- 最初の部分は、UI テストのコントロールで実行できる操作で構成されます。 たとえば、コード化された UI テストでは、UI テストのコントロールでのマウス クリックをシミュレートしたり、UI テストのコントロールに影響を与えるキーボードでのキー入力をシミュレートしたりすることができます。

- 2 番目の部分では、UI テストのコントロールのプロパティの取得や設定を行うことができます。 たとえば、コード化された UI テストでは、`ListBox` 内の項目数を取得したり、`CheckBox` をオンの状態に設定したりできます。

  **UI テストのコントロールの操作へのアクセス**

  UI テストのコントロールにマウス クリックやキー操作などの操作を実行するには、<xref:Microsoft.VisualStudio.TestTools.UITesting.Mouse> クラスおよび <xref:Microsoft.VisualStudio.TestTools.UITesting.Keyboard> クラスのメソッドを使用します。

- マウスのクリックなど、マウスを使用した操作を実行するには、<xref:Microsoft.VisualStudio.TestTools.UITesting.Mouse.Click%2A> を使用します。

   `Mouse.Click(buttonCancel);`

- エディット コントロールへの入力など、キーボードを使用した操作を実行するには、<xref:Microsoft.VisualStudio.TestTools.UITesting.Keyboard.SendKeys%2A> を使用します。

   `Keyboard.SendKeys(textBoxDestination, @"C:\Temp\Output.txt");`

  **UI テストのコントロールのプロパティへのアクセス**

  UI コントロールの特定のプロパティ値を取得および設定するには、コントロールのプロパティ値を直接取得または設定するか、取得または設定する特定のプロパティの名前と共に <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A?displayProperty=fullName> メソッドおよび <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.SetProperty%2A?displayProperty=fullName> メソッドを使用します。

  <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A> は、適切な <xref:System.Type> にキャストできるオブジェクトを返します。 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.SetProperty%2A> は、プロパティの値が格納されているオブジェクトを受け取ります。

##### <a name="to-get-or-set-properties-from-ui-test-controls-directly"></a>UI テストのコントロールからプロパティを直接取得または設定するには

- T:Microsoft.VisualStudio.TestTools.UITesting.HtmlControls.HtmlList や T:Microsoft.VisualStudio.TestTools.UITesting.WinControls.WinComboBox など、T:Microsoft.VisualStudio.TestTools.UITesting.UITestControl から派生するコントロールの場合は、次のように、プロパティ値を直接取得または設定できます。

    ```
    int i = myHtmlList.ItemCount;
    myWinCheckBox.Checked = true;
    ```

##### <a name="to-get-properties-from-ui-test-controls"></a>UI テストのコントロールからプロパティを取得するには

- コントロールからプロパティ値を取得するには、<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A> を使用します。

- 取得するコントロールのプロパティを指定するには、`PropertyNames` に対し、パラメーターとして各コントロールの <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A> クラスからの適切な文字列を使用します。

- <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A> は適切なデータ型を返しますが、この戻り値は <xref:System.Object> としてキャストされます。 戻り値 <xref:System.Object> は適切な型としてキャストされる必要があります。

     例:

     `int i = (int)GetProperty(myHtmlList.PropertyNames.ItemCount);`

##### <a name="to-set-properties-for-ui-test-controls"></a>UI テストのコントロールのプロパティを設定するには

- コントロールのプロパティを設定するには、<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.SetProperty%2A> を使用します。

- 設定するコントロールのプロパティを指定するには、`PropertyNames` に対し、最初のパラメーターとして <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.SetProperty%2A> クラスからの適切な文字列を使用します。2 番目のパラメーターにはプロパティ値を指定します。

     例:

     `SetProperty(myWinCheckBox.PropertyNames.Checked, true);`

### <a name="debugging"></a><a name="debugging"></a>デバッギング
 コード化された UI テスト ログを使用して、コード化された UI テストを分析できます。 コード化された UI テスト ログは、コード化された UI テストの実行に関する重要な情報にフィルターを適用して記録します。 ログは、問題をすばやくデバッグできるような形式で記録されます。 詳細については、「[コード化された UI テスト ログを使用したコード化された UI テストの分析](../test/analyzing-coded-ui-tests-using-coded-ui-test-logs.md)」をご覧ください。

## <a name="whats-next"></a><a name="VerifyCodeUsingCUITWhatsNext"></a>次は何ですか?
 **コード化された UI テストを実行するための追加オプション:** コード化された UI テストは、このトピックで既に説明したように、Visual Studio から直接実行できます。 また、[!INCLUDE[TCMext](../includes/tcmext-md.md)] または [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] から自動化された UI テストを実行できます。 コード化された UI テストを自動化すると、テストは他の自動テストとは異なって実行時にデスクトップと対話する必要があります。

- [方法: Microsoft Visual Studio からテストを実行する](https://msdn.microsoft.com/library/1a1207a9-2a33-4a1e-a1e3-ddf0181b1046)

- [Microsoft テスト マネージャーでの自動テストの実行](https://msdn.microsoft.com/0632f265-63fe-4859-a413-9bb934c66835)

- [方法: アプリケーションのビルド後にスケジュールされているテストを構成および実行する](https://msdn.microsoft.com/32acfeb1-b1aa-4afb-8cfe-cc209e6183fd)

- [ビルド プロセスでのテストの実行](https://msdn.microsoft.com/library/d05743a1-c5cf-447e-bed9-bed3cb595e38)

- [コマンド ラインからの自動テストの実行](https://msdn.microsoft.com/library/f18179c6-b688-4e41-9898-8aca130c4fc3)

- [方法: テストエージェントを設定して、デスクトップと対話するテストを実行する](/visualstudio/test/how-to-set-up-your-test-agent-to-run-tests-that-interact-with-the-desktop?view=vs-2015)

- [&#91;廃版&#93; ロード テストでのコード化された UI テストの使用](https://msdn.microsoft.com/library/704339ff-7da7-4d5f-acb3-c3b23f4acb43)

  **カスタムコントロールのサポートの追加:** コード化された UI テストフレームワークは、可能なすべての UI をサポートしているわけではなく、テスト対象の UI をサポートしていない場合もあります。 たとえば、[!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] の UI について、コード化された UI テストはすぐに作成できません。 しかし、コード化された UI テスト フレームワークの拡張性を活用すると、カスタム コントロールをサポートするようにすることができます。

- [コントロールのコード化された UI テストを有効にする](../test/enable-coded-ui-testing-of-your-controls.md)

- [コード化された UI テストと操作の記録を拡張して Microsoft Exce をサポート](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)

  コード化された UI テストは、手動テストを自動化するためによく使用されます。 追加のガイダンスについては、「[Testing for Continuous Delivery with Visual Studio 2012 – Chapter 5: Automating System Tests (Visual Studio 2012 を使用した継続的デリバリーのためのテスト – 第 5 章: システム テストの自動化)](https://msdn.microsoft.com/library/jj159335.aspx)」をご覧ください。 手動テストの詳細については、「[&#91;廃版&#93; Microsoft Test Manager を使用した手動テスト ケースの作成](https://msdn.microsoft.com/library/9989e184-c8e4-444b-998d-a1a5ec94461e)」をご覧ください。 自動化されたシステム テストの詳細については、「[Microsoft Test Manager を使用した自動テストの作成](https://msdn.microsoft.com/7b5075ee-ddfe-411d-b1d4-94283550a5d0)」をご覧ください。

## <a name="external-resources"></a>外部リソース

### <a name="guidance"></a>ガイダンス
- [Visual Studio 2012 を使用した継続的デリバリーのためのテスト – 第 2 章: 単体テスト: 内部のテスト](https://msdn.microsoft.com/library/jj159340.aspx)

- [Visual Studio 2012 を使用した継続的デリバリーのためのテスト–第5章: システムテストの自動化](https://msdn.microsoft.com/library/jj159335.aspx)

### <a name="faq"></a>よく寄せられる質問
- [Coded UI Tests FAQ - 1 (コード化された UI テストの FAQ - 1)](https://docs.microsoft.com/archive/blogs/mathew_aniyan/content-index-for-coded-ui-test)

- [Coded UI Tests FAQ - 2 (コード化された UI テストの FAQ - 2)](https://social.msdn.microsoft.com/Forums/en-US/vsautotest/thread/3a74dd2c-cef8-4923-abbf-7a91f489e6c4)

### <a name="forum"></a>フォーラム
- [Visual Studio の UI オートメーションのテスト (CodedUI を含む)](https://social.msdn.microsoft.com/Forums/en-US/vsautotest)

## <a name="see-also"></a>関連項目

- [UIMap](/previous-versions/dd580454(v=vs.140))
- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert>
- [コード品質の向上](https://msdn.microsoft.com/library/73baa961-c21f-43fe-bb92-3f59ae9b5945)
- [チュートリアル: コード化された UI テストの作成、編集、および保守](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)
- [コード化された UI テストの構造](../test/anatomy-of-a-coded-ui-test.md)
- [コード化された UI テストのベストプラクティス](../test/best-practices-for-coded-ui-tests.md)
- [複数の UI マップでの大規模アプリケーションのテスト](../test/testing-a-large-application-with-multiple-ui-maps.md)
- [コード化された UI テスト エディターを使用したコード化された UI テストの編集](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)
- [コード化された UI テストと操作の記録でサポートされる構成とプラットフォーム](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)
- [Visual Studio 2010 からのコード化された UI テストのアップグレード](../test/upgrading-coded-ui-tests-from-visual-studio-2010.md)
- [既存の操作の記録からのコード化された UI テストの生成](https://msdn.microsoft.com/library/56736963-9027-493b-b5c4-2d4e86d1d497)
