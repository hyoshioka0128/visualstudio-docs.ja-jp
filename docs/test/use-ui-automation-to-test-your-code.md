---
title: コード化された UI テスト
ms.date: 12/04/2018
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: eaa1e284394bda78c6892647ce9eca20d372a362
ms.sourcegitcommit: 754133c68ad841f7d7962e0b7a575e133289d8a8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91928096"
---
# <a name="use-coded-ui-test-to-test-your-code"></a>コード化された UI テストを使用してコードをテストする

コード化された UI テスト (CUITs) では、ユーザー インターフェイス (UI) を介してアプリケーションが実行されます。 これらのテストには、UI コントロールの機能テストが含まれます。 これらのテストで、アプリケーション全体が、ユーザー インターフェイスを含めて正しく機能していることを検証できます。 コード化された UI テストは、Web ページなど、ユーザー インターフェイスに検証やその他のロジックがある場合に便利です。 また、既存の手動テストを自動化するために頻繁に使用されます。

Visual Studio では、コード化された UI テストを簡単に作成できます。 **コード化された UI テスト ビルダー**をバックグラウンドで実行しているときに、テストを手動で実行するだけです。 特定のフィールドに表示する値を指定することもできます。 **コード化された UI テスト ビルダー**では、操作が記録され、それらの記録からコードを生成します。 テストの作成後、特殊なエディターでテストを編集して、操作のシーケンスを変更することができます。

コーディングよりテストのほうが得意な方でも、特殊な**コード化されたテスト ビルダー**とエディターによって、簡単にコード化された UI テストを作成および編集できます。 ただし、開発者がより高度な方法でこのテストを拡張する場合に備え、コードは簡単にコピーして適応できるように構造化されています。 たとえば、Web サイトで 1 つの商品を購入するテストを記録した後、生成されたコードを編集することにより、複数の商品を購入するループを追加することができます。

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

## <a name="requirements"></a>必要条件

- Visual Studio Enterprise
- コード化された UI テストのコンポーネント

コード化された UI テストでサポートされているプラットフォームと構成の詳細については、「[コード化された UI テストと操作の記録でサポートされている構成とプラットフォーム](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)」をご覧ください。

## <a name="install-the-coded-ui-test-component"></a>コード化された UI テストのコンポーネントをインストールする

コード化された UI テストのツールとテンプレートにアクセスするには、Visual Studio の**コード化された UI テスト** コンポーネントをすべてインストールします。

1. **[ツール]**  >  **[ツールと機能を取得]** を選択して **Visual Studio インストーラー**を起動します。

1. **Visual Studio インストーラー**で **[個別のコンポーネント]** タブを選択し、下にスクロールして **[デバッグとテスト]** セクションを表示します。 **コード化された UI テスト**のコンポーネントを選択します。

   ![コード化された UI テストのコンポーネント](media/coded-ui-test-component.png)

1. **[変更]** を選択します。

## <a name="create-a-coded-ui-test"></a>コード化された UI テストの作成

1. コード化された UI テストを作成します。

   コード化された UI テストは、コード化された UI テスト プロジェクトに含まれている必要があります。 コード化された UI テスト プロジェクトをまだ作成していない場合は、プロジェクトを作成します。 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。 **[コード化された UI テスト プロジェクト]** プロジェクト テンプレートを検索して選択します。

   ::: moniker range="vs-2017"

   ![[新しいプロジェクト] ダイアログのコード化された UI テスト プロジェクトのテンプレート](media/coded-ui-test-project-template.png)

   ::: moniker-end

   > [!NOTE]
   > **[コード化された UI テスト プロジェクト]** テンプレートが表示されない場合は、[コード化された UI テスト コンポーネントをインストール](../test/use-ui-automation-to-test-your-code.md#install-the-coded-ui-test-component)する必要があります。

2. コード化された UI テスト ファイルを追加します。

     コード化された UI プロジェクトを作成した場合は、最初の CUIT ファイルが自動的に追加されます。 別のテスト ファイルを追加するには、**ソリューション エクスプローラー**でコード化された UI テスト プロジェクトのショートカット メニューを開き、 **[追加]** 、 **[コード化された UI テスト]** の順に選択します。

     **[コード化された UI テストのコードの生成]** ダイアログ ボックスで、 **[操作の記録]**  >  **[UI マップの編集またはアサーションの追加]** を選択します。

     ![[コード化された UI テストのコードの生成] ダイアログ ボックス](media/generate-code-for-coded-ui-test.png)

     **コード化された UI テスト ビルダー**が表示されます。

     ![コード化された UI テスト ビルダー](../test/media/codedui_testbuilder.png)

3. 操作のシーケンスを記録します。

     **記録を開始するには**、 **[記録する]** アイコンをクリックします。 必要に応じて、アプリケーションの起動など、アプリケーションでテストする操作を実行します。 たとえば、Web アプリケーションをテストする場合は、ブラウザーを起動し、Web サイトに移動し、アプリケーションにサインインします。

     受信メールを処理する場合などに、**記録を一時停止するには**、 **[一時停止]** を選択します。

    > [!WARNING]
    > デスクトップ上で実行されるすべてのアクションが記録されます。 機密データが記録される可能性のあるアクションを実行する場合には、記録を一時停止します。

     間違って記録した**操作を削除するには**、 **[Edit Steps]\(ステップの編集\)** を選択します。

     操作をレプリケートする**コードを生成するには**、 **[コードの生成]** アイコンを選択し、コード化された UI テスト メソッドの名前と説明を入力します。

4. テキスト ボックスなどの UI フィールドの値を検証します。

     **コード化された UI テスト ビルダー**で **[アサーションの追加]** を選択し、実行中のアプリケーションで UI コントロールを選択します。 表示されるプロパティの一覧で、テキスト ボックスの **Text** などのプロパティを選択します。 ショートカット メニューで、 **[アサーションの追加]** をクリックします。 ダイアログ ボックスで、比較演算子、比較対象値、およびエラー メッセージを選択します。

     アサーション ウィンドウを閉じ、 **[コードの生成]** を選択します。

     ![要素を対象としたコード化された UI テスト](../test/media/codedui_1.png)

    > [!TIP]
    > 操作の記録と値の検証を交互に行います。 操作または検証の各シーケンスの最後にコードを生成します。 必要に応じて、後で新しい操作と検証を挿入できます。

     詳細については、[コントロールのプロパティの検証](#validate-the-properties-of-ui-controls)に関するページをご覧ください。

5. 生成されたテスト コードを表示します。

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

6. さらに操作とアサーションを追加します。

   次に、テスト メソッド内の適切な位置にカーソルを置き、ショートカット メニューで、 **[コード化された UI テストのコードの生成]** を選択します。 新しいコードがカーソルの位置に挿入されます。

7. テストの操作とアサーションの詳細を編集します。

     *UIMap.uitest* を開きます。 このファイルは**コード化された UI テスト エディター**で開かれます。ここで、記録した操作のシーケンスやアサーションを編集できます。

     ![コード化された UI テスト エディター](../test/media/cuit_editor_edit.png)

     詳細については、「[コード化された UI テスト エディターを使用してコード化された UI テストを編集する](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)」をご覧ください。

8. テストを実行します。

   テスト エクスプローラーを使用するか、テスト メソッドでショートカット メニューを開き、 **[テストの実行]** を選択します。 テストの実行方法の詳細については、「[テスト エクスプローラーを使用した単体テストの実行](../test/run-unit-tests-with-test-explorer.md)」と、このトピックの最後の「[次の内容](#whats-next)」セクションの「*コード化された UI テストの実行の追加オプション*」をご覧ください。

このトピックの残りのセクションでは、このプロシージャ内の各ステップについてさらに詳しく説明します。

詳しい例については、「[チュートリアル:コード化された UI テストの作成、編集、および保守](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)」を参照してください。 このチュートリアルでは、簡単な Windows Presentation Foundation (WPF) アプリケーションを作成して、コード化された UI テストの作成、編集、および保守を行う方法について説明します。 また、さまざまなタイミングの問題やコントロールのリファクタリングによって機能が損なわれたテストを修正するための解決策を示します。

## <a name="start-and-stop-the-application-under-test"></a>テスト対象のアプリケーションを開始し、停止する

テストごとにアプリケーション、ブラウザー、データベースを開始/停止しない場合、次のいずれかを行います。

- テスト対象のアプリケーションの起動操作を記録しない場合は、 **[記録する]** アイコンを選択する前にアプリケーションを起動する必要があります。

- テストの終了時に、テストを実行するプロセスが終了します。 テストでアプリケーションを起動した場合、アプリケーションは通常は閉じます。  終了時にテストがアプリケーションを閉じないようにするには、ソリューションに *.runsettings* ファイルを追加し、`KeepExecutorAliveAfterLegacyRun` オプションを使用します。 詳細については、「[.runsettings ファイルを使用して単体テストを構成する](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)」をご覧ください。

- `[TestInitialize]` 属性で識別されるテスト初期化メソッドを追加します。このメソッドは、各テスト メソッドの開始時にコードを実行します。 たとえば、TestInitialize メソッドからアプリケーションを起動することができます。

- `[TestCleanup]` 属性で識別されるテスト クリーンアップ メソッドを追加します。このメソッドは、各テスト メソッドの開始時にコードを実行します。 たとえば、アプリケーションを終了するメソッドは、TestCleanup メソッドから呼び出すことができます。

## <a name="validate-the-properties-of-ui-controls"></a>UI コントロールのプロパティを検証する

**コード化された UI テスト ビルダー**を使用すると、テストの [UIMap](/previous-versions/dd580454(v=vs.140)) にユーザー インターフェイス (UI) を追加したり、UI コントロールのアサーションを使用する検証メソッドのコードを生成したりできます。

UI コントロールのアサーションを作成するには、**コード化された UI テスト ビルダー**の**アサーションの追加**ツールを選択し、正しいかどうかを検証するテスト対象アプリケーションのコントロールにドラッグします。 コントロールが枠で囲まれたら、マウス ボタンを離します。 コントロール クラス コードがすぐに *UIMap.Designer.cs* ファイルに作成されます。

![要素を対象としたコード化された UI テスト](../test/media/codedui_1.png)

これで、このコントロールのプロパティが **[アサーションの追加]** ダイアログ ボックスに表示されます。

特定のコントロールに移動するには、矢印 **(<<)** を選択して **[UI コントロール マップ]** のビューを展開する方法もあります。 親、兄弟、子の各コントロールを見つけるには、マップのどこかをクリックし、方向キーを使用してツリー内を移動します。

![コード化された UI テストのプロパティ](../test/media/codedui_2.png)

> [!TIP]
> アプリケーションでコントロールを選択してもプロパティが表示されない場合、または UI コントロール マップにコントロールが表示されない場合は、コントロールのアプリケーション コードに一意の ID が与えられていることを確認してください。 一意の ID には HTML ID 属性や WPF UId が使用されることがあります。

次に、検証する UI コントロールのプロパティのショートカット メニューで、 **[アサーションの追加]** をポイントします。 **[アサーションの追加]** ダイアログ ボックスで、アサーションの **[比較子]** (<xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.AreEqual%2A> など) を選択し、 **[比較対象値]** にアサーションの値を入力します。

![コード化された UI テストのアサーション](../test/media/codedui_3.png)

テスト用のアサーションをすべて追加したら、 **[OK]** を選択します。

アサーションのコードを生成し、コントロールを UI マップに追加するために、 **[コードの生成]** アイコンを選択します。 コード化された UI テスト メソッドの名前と説明を入力します。これらはメソッドのコメントとして追加されます。 **[追加と生成]** を選択します。 次に、 **[閉じる]** アイコンをクリックして、 **[コード化された UI テスト ビルダー]** を閉じます。 これで、次のようなコードが生成されます。 たとえば、入力した名前が `AssertForAddTwoNumbers` の場合、コードは次の例のようになります。

- コード化された UI テスト ファイルのテスト メソッドに、AssertForAddTwoNumbers という Assert メソッドの呼び出しを追加します。

    ```csharp
    [TestMethod]
    public void CodedUITestMethod1()
    {
        this.UIMap.AddTwoNumbers();
        this.UIMap.AssertForAddTwoNumbers();
    }
    ```

     このファイルを編集して、ステップとアサーションの順序を変更するか、新しいテスト メソッドを作成することができます。 さらにコードを追加するには、テスト メソッドにカーソルを置き、ショートカット メニューの **[コード化された UI テストのコードの生成]** を選択します。

- UI マップ (*UIMap.uitest*) に `AssertForAddTwoNumbers` という名前のメソッドを追加します。 このファイルを**コード化された UI テスト エディター**で開くことにより、アサーションの編集を行えます。

     ![コード化された UI テスト エディターを使用したアサートの編集](../test/media/cuit_editor_assert.png)

     詳細については、「[コード化された UI テスト エディターを使用してコード化された UI テストを編集する](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)」をご覧ください。

     生成されたアサーション メソッドのコードは、*UIMap.Designer.cs* で確認することもできます。 ただし、このファイルは編集しないでください。 適合させたバージョンのコードを作成する場合は、メソッドを *UIMap.cs* などの別のファイルにコピーし、メソッドの名前を変更し、メソッドを編集します。

    ```csharp
    public void AssertForAddTwoNumbers()
    {
        ...
    }
    ```

### <a name="select-a-hidden-control-using-the-keyboard"></a>キーボードを使用して非表示のコントロールを選択する

**コード化された UI テスト ビルダー**から **[アサーションの追加]** ツールを選択しようとすると、目的のコントロールがフォーカスを失い、表示されなくなる場合:

コントロールを追加し、プロパティを検証するとき、キーボードが必要になる場合もあります。 たとえば、右クリック メニュー コントロールを使用するコード化された UI テストを記録するとき、**コード化された UI テスト ビルダー**の **[アサーションの追加]** ツールで選択しようとすると、コントロールのメニュー項目の一覧がフォーカスを失い、非表示になります。 これを次の図に示します。Internet Explorer で、 **[アサーションの追加]** ツールで右クリック メニューを選択しようとすると、これはフォーカスを失い、表示されなくなります。

![CodedUITest&#95;SelectControlKeyboard](../test/media/codeduitest_selectcontrolkeyboard.png)

キーボードを使用して UI コントロールを選択するには、マウスをコントロールの上に置きます。 次に、**Ctrl** キーと **I** キーを同時に押します。 キーを離します。 コントロールは、**コード化された UI のテスト ビルダー**によって記録されます。

#### <a name="manually-record-mouse-hovers"></a>マウス ホバーを手動で記録する

コントロール上のマウス ホバーを記録できない場合:

状況によっては、コード化された UI テストで使用される特定のコントロールで、キーボードを使用してマウス ホバー イベントを手動で記録することが必要な場合があります。 たとえば、Windows フォームまたは Windows Presentation Foundation (WPF) アプリケーションをテストするとき、カスタム コードが使用されている場合があります。 または、マウスが置かれたときにツリー ノードを展開するなど、コントロールの上にマウスが置かれたときに特別な動作が定義されている場合もあります。 このような状況をテストするには、定義済みのキーボードのキーを押して、コントロールの上にマウスを置いていることを**コード化された UI テスト ビルダー**に手動で通知する必要があります。

コード化された UI テストを実行するとき、コントロール上にマウスを置きます。 そして、キーボードの **Ctrl** キーを押しながら、**Shift** キーと **R** キーを押したままにします。 キーを離します。 **コード化された UI のテスト ビルダー**によって、マウス ホバー イベントが記録されます。

![CodedUI&#95;Hover](../test/media/codedui_hover.png)

テスト メソッドを作成すると、次の例のようなコードが *UIMap.Designer.cs* ファイルに追加されます。

```csharp
// Mouse hover '1' label at (87, 9)
Mouse.Hover(uIItem1Text, new Point(87, 9));
```

### <a name="configure-mouse-hover-keyboard-assignments"></a>マウス ホバーのキーボード割り当てを構成する

マウス ホバー イベントをキャプチャするキーの割り当てが自分の環境内の他の場所で使用されている場合:

必要に応じて、コード化された UI テストでマウス ホバー イベントを適用するために使用される既定のキーボード割り当て **Ctrl**+**Shift**+**R** は、異なるキーを使用するように構成できます。

> [!WARNING]
> 通常は、マウス ホバー イベントのキーボードの割り当てを変更する必要はありません。 キーボードの割り当てを再設定するときは注意してください。 選択したキーボードの割り当ては、既に Visual Studio またはテスト中のアプリケーション内の他の場所で使用されている可能性もあります。

キーボードの割り当てを変更するには、次の構成ファイルを変更します。

*%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CodedUITestBuilder.exe.config*

構成ファイルで、`HoverKeyModifier` および `HoverKey` キーの値を変更して、キーボードの割り当てを変更します。

```xml
<!-- Begin : Background Recorder Settings -->
<!-- HoverKey to use. -->
<add key="HoverKeyModifier" value="Control, Shift"/>
<add key="HoverKey" value="R"/>
```

### <a name="set-implicit-mouse-hovers-for-the-web-browser"></a>Web ブラウザーの暗黙のマウス ホバーを設定する

Web サイトでマウス ホバーの記録に問題がある場合:

多くの Web サイトでは、特定のコントロールの上にマウスを置くと、そのコントロールが展開され、追加の詳細情報が表示されます。 通常、これらはデスクトップ アプリケーションのメニューのように見えます。 これが一般的なパターンであるため、コード化された UI テストでは Web の閲覧中の暗黙のホバーが有効になります。 たとえば、Internet Explorer でホバーを記録すると、イベントが発生します。 これらのイベントによって、ホバーが重複して記録されることがあります。 このため、暗黙のホバーは UI テスト構成ファイルで `ContinueOnError` が `true` に設定された状態で記録されます。 これによって、ホバー イベントが失敗した場合でも再生は続行されます。

Web ブラウザーで暗黙のホバーの記録を有効にするには、構成ファイルを開きます。

*%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CodedUITestBuilder.exe.config*

次の例に示すように、構成ファイルでキー `RecordImplicitiHovers` が `true` の値に設定されていることを確認します。

```xml
<!--Use this to enable/disable recording of implicit hovers.-->
<add key="RecordImplicitHover" value="true"/>
```

## <a name="customize-the-coded-ui-test"></a>コード化された UI テストのカスタマイズ

コード化された UI テストの作成後、Visual Studio で次のいずれかのツールを使用してテストを編集できます。

- **コード化された UI テスト ビルダー**を使用して、テストにコントロールや検証を追加します。 このトピックの[コントロールの追加およびプロパティの検証](#validate-the-properties-of-ui-controls)に関するセクションをご覧ください。

- **コード化された UI テスト エディター**では、コード化された UI テストを簡単に変更できます。 **コード化された UI テスト エディター**を使用すると、テスト メソッドを検索、表示、および編集できます。 また、UI コントロール マップ内の UI 操作および関連コントロールを編集することもできます。 詳細については、「[コード化された UI テスト エディターを使用してコード化された UI テストを編集する](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)」をご覧ください。

- **コード エディター:**

  - このトピックの「[コード化された UI コントロールの操作とプロパティ](#coded-ui-control-actions-and-properties)」セクションで説明しているように、テストのコントロールのコードを手動で追加します。

  - コード化された UI テストを作成した後、それをデータ ドリブンに変更できます。 詳細については、「[データ ドリブンのコード化された UI テストを作成する](../test/creating-a-data-driven-coded-ui-test.md)」を参照してください。

  - コード化された UI テストの再生では、テストに対して指示することで、ウィンドウの表示やプログレス バーの非表示などの特定のイベントが発生するまで待機することができます。 これを行うには、適切な UITestControl.WaitForControlXXX() メソッドを追加します。 使用できるメソッドの完全な一覧については、「[再生中に特定のイベントを待機するようにコード化された UI テストを設定](../test/making-coded-ui-tests-wait-for-specific-events-during-playback.md)」をご覧ください。 WaitForControlEnabled メソッドを使用して、コントロールが有効になるまで待機するコード化された UI テストの例については、「[チュートリアル:コード化された UI テストの作成、編集、および保守](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)」を参照してください。

  - コード化された UI テストには、Internet Explorer 9 と Internet Explorer 10 に含まれる HTML5 コントロールの一部のサポートが含まれます。 詳細については、「[コード化された UI テストでの HTML5 コントロールの使用](../test/using-html5-controls-in-coded-ui-tests.md)」をご覧ください。

  - コード化された UI テストのコーディング ガイダンス:

    - [コード化された UI テストの構造](../test/anatomy-of-a-coded-ui-test.md)

    - [コード化された UI テストのベスト プラクティス](../test/best-practices-for-coded-ui-tests.md)

    - [複数の UI マップで大規模アプリケーションをテストする](../test/testing-a-large-application-with-multiple-ui-maps.md)

    - [コード化された UI テストと操作の記録でサポートされている構成とプラットフォーム](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)

### <a name="the-generated-code"></a>生成されたコード

**[コードの生成]** を選択すると、いくつかのコードが作成されます。

- テスト メソッド内の行。

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

- *UIMap.uitest* 内のメソッド。

     このメソッドには、記録した操作または検証した値の詳細が含まれます。 *UIMap.uitest* を開いて、このコードを編集できます。 これは特殊なエディターで開かれ、記録された操作を削除またはリファクタリングできます。

     また、*UIMap.Designer.cs* で生成されたメソッドを表示できます。 このメソッドによって、テストの実行時に記録した操作が実行されます。

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

     これらのメソッドを *UIMap.cs* にコピーすることにより、メソッドを適合させたバージョンを作成できます。 たとえば、テスト メソッドから呼び出すことができるパラメーター化されたバージョンを作成できます。

    ```csharp
    // File: UIMap.cs
    public partial class UIMap // Same partial class
    {
      /// <summary>
      /// Add two numbers - parameterized version
      /// </summary>
      public void AddTwoNumbers(int firstNumber, int secondNumber)
      { ...   // Code modified to use parameters.
      }
    }
    ```

- *UIMap.uitest* 内の宣言。

    これらの宣言は、テストで使用されるアプリケーションの UI コントロールを表します。 これらは、コントロールの操作とプロパティへのアクセスのために、生成されたコードによって使用されます。

    独自のコードを記述する場合も、これらを使用できます。 たとえば、テスト メソッドで Web アプリケーションのハイパーリンクの選択やテキスト ボックスへの値の入力を実行したり、フィールドの値に基づいて分岐して別のテスト操作を行ったりすることができます。

    大規模なアプリケーションのテストを容易にするために、複数のコード化された UI テストと複数の UI マップ オブジェクトおよびファイルを追加できます。 詳細については、「[複数の UI マップでの大規模アプリケーションのテスト](../test/testing-a-large-application-with-multiple-ui-maps.md)」をご覧ください。

生成されるコードの詳細については、「[コード化された UI テストの構造](../test/anatomy-of-a-coded-ui-test.md)」をご覧ください。

## <a name="coded-ui-control-actions-and-properties"></a>コード化された UI コントロールの操作とプロパティ

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

### <a name="to-get-or-set-properties-from-ui-test-controls-directly"></a>UI テストのコントロールからプロパティを直接取得または設定するには

[HtmlList](xref:Microsoft.VisualStudio.TestTools.UITesting.HtmlControls.HtmlList) や [WinComboBox](xref:Microsoft.VisualStudio.TestTools.UITesting.WinControls.WinComboBox) などの、<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl>から派生するコントロールを使用して、プロパティ値を直接取得したり設定したりできます。 次のコードは、いくつかの例を示しています。

```csharp
int i = myHtmlList.ItemCount;
myWinCheckBox.Checked = true;
```

### <a name="to-get-properties-from-ui-test-controls"></a>UI テストのコントロールからプロパティを取得するには

- コントロールからプロパティ値を取得するには、<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A> を使用します。

- 取得するコントロールのプロパティを指定するには、`PropertyNames` に対し、パラメーターとして各コントロールの <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A> クラスからの適切な文字列を使用します。

- <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A> は適切なデータ型を返しますが、この戻り値は <xref:System.Object> としてキャストされます。 戻り値 <xref:System.Object> は適切な型としてキャストされる必要があります。

     例:

     `int i = (int)GetProperty(myHtmlList.PropertyNames.ItemCount);`

### <a name="to-set-properties-for-ui-test-controls"></a>UI テストのコントロールのプロパティを設定するには

- コントロールのプロパティを設定するには、<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.SetProperty%2A> を使用します。

- 設定するコントロールのプロパティを指定するには、`PropertyNames` に対し、最初のパラメーターとして <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.SetProperty%2A> クラスからの適切な文字列を使用します。2 番目のパラメーターにはプロパティ値を指定します。

     例:

     `SetProperty(myWinCheckBox.PropertyNames.Checked, true);`

## <a name="debug"></a>デバッグ

コード化された UI テスト ログを使用して、コード化された UI テストを分析できます。 コード化された UI テスト ログは、コード化された UI テストの実行に関する重要な情報にフィルターを適用して記録します。 ログは、問題をすばやくデバッグできるような形式で記録されます。 詳細については、「[コード化された UI テスト ログを使用したコード化された UI テストの分析](../test/analyzing-coded-ui-tests-using-coded-ui-test-logs.md)」をご覧ください。

## <a name="whats-next"></a>次の内容

::: moniker range="vs-2017"
**コード化された UI テストの実行の追加オプション:** このトピックで既に説明したように、コード化された UI テストを Visual Studio から直接実行できます。 さらに、Microsoft Test Manager から、または Azure Pipelines を使用して、自動化された UI テストを実行できます。 コード化された UI テストが自動化されている場合、他の自動テストとは異なり、実行時にデスクトップと対話する必要があります。
::: moniker-end
::: moniker range=">=vs-2019"
**コード化された UI テストの実行の追加オプション:** このトピックで既に説明したように、コード化された UI テストを Visual Studio から直接実行できます。 また、Azure Pipelines を使用して、自動化された UI テストを実行できます。 コード化された UI テストが自動化されている場合、他の自動テストとは異なり、実行時にデスクトップと対話する必要があります。
::: moniker-end

- [テスト エクスプローラーを使用して単体テストを実行する](../test/run-unit-tests-with-test-explorer.md)

- [ビルド プロセスでのテストの実行](/azure/devops/pipelines/test/getting-started-with-continuous-testing?view=vsts&preserve-view=true)

- [方法: テスト エージェントを設定して、デスクトップと対話するテストを実行する](/previous-versions/ee291332(v=vs.140))

**カスタム コントロールに対するサポートを追加する:** コード化された UI テスト フレームワークは使用可能な UI すべてをサポートしているわけではなく、テスト対象の UI をサポートしない場合もあります。 たとえば、Microsoft Excel の UI 用のコード化された UI テストをすぐに作成することはできません。 ただし、コード化された UI テスト フレームワークでカスタム コントロールをサポートするための拡張機能を作成することはできます。

- [コントロールのコード化された UI テストを有効化する](../test/enable-coded-ui-testing-of-your-controls.md)

- [コード化された UI テストと操作の記録を拡張する](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)

コード化された UI テストは、手動テストを自動化するためによく使用されます。 自動テストの詳細については、「[Visual Studio のテスト ツール](../test/improve-code-quality.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [手動テストの記録と再生](/azure/devops/test/mtm/record-play-back-manual-tests?view=vsts&preserve-view=true)
- [Xamarin.UITest](/appcenter/test-cloud/uitest/)
- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert>
- [チュートリアル: コード化された UI テストの作成、編集、保守](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)
- [UWP アプリをテストするためのコード化された UI テストの作成](test-uwp-app-with-coded-ui-test.md)
- [コード化された UI テストの構造](../test/anatomy-of-a-coded-ui-test.md)
- [コード化された UI テストのベスト プラクティス](../test/best-practices-for-coded-ui-tests.md)
- [複数の UI マップで大規模アプリケーションをテストする](../test/testing-a-large-application-with-multiple-ui-maps.md)