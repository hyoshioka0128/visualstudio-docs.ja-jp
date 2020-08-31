---
title: Windows フォーム デザイナー チュートリアル
ms.date: 08/09/2019
ms.topic: tutorial
helpviewer_keywords:
- Windows Forms Designer, get started
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 831e0216bcecff2e9ac6551184ddbfda56a4b525
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88801296"
---
# <a name="tutorial-get-started-with-windows-forms-designer"></a>チュートリアル: Windows フォーム デザイナーを使ってみる

Windows フォーム デザイナーでは、Windows フォーム アプリケーションを構築するための多くのツールが提供されています。 この記事では、デザイナーによって提供されるさまざまなツールを使用して、以下のようなタスクなど、アプリを構築する方法について説明します。

- スナップ線を使用してコントロールを配置します。
- スマート タグを使用してデザイナー タスクを実行します。
- コントロールの余白とパディングを設定します。
- <xref:System.Windows.Forms.TableLayoutPanel> コントロールを使用してコントロールを配置します。
- <xref:System.Windows.Forms.SplitContainer> コントロールを使用してコントロールのレイアウトをパーティション分割します。
- [ドキュメント アウトライン] ウィンドウでレイアウト内を移動します。
- サイズと位置の情報を表示してコントロールを配置します。
- プロパティ ウィンドウを使用してプロパティの値を設定します。

完了すると、Windows フォーム デザイナーで利用できる多くのレイアウト機能を使って組み立てられたカスタム コントロールができあがります。 このコントロールでは、簡単な電卓用のユーザー インターフェイス (UI) が実装されています。 次の図では、電卓コントロールの一般的なレイアウトを示します。

![ガイド付きツアーの電卓の UI](media/calculator-ui.gif)

## <a name="create-the-custom-control-project"></a>カスタム コントロール プロジェクトを作成する

最初のステップでは、DemoCalculator コントロール プロジェクトを作成します。

1. Visual Studio を開き、新しい **Windows フォーム コントロール ライブラリ** プロジェクトを作成します。 プロジェクトの名前を **DemoCalculatorLib** にします。

   ::: moniker range=">=vs-2019"

   ![Visual Studio 2019 の Windows フォーム コントロール ライブラリ テンプレート](media/windows-forms-control-library-template.png)

   ::: moniker-end

2. ファイルの名前を変更するには、**ソリューション エクスプローラー**で **UserControl1.vb** または **UserControl1.cs** を右クリックし、 **[名前の変更]** を選択して、ファイル名を DemoCalculator.vb または DemoCalculator.cs に変更します。 コード要素 "UserControl1" へのすべての参照の名前を変更するかどうかをたずねられたら、 **[はい]** を選択します。

Windows フォーム デザイナーに、DemoCalculator コントロールのデザイナー画面が表示されます。 このビューでは、[ツールボックス] でコントロールとコンポーネントを選択し、デザイナー画面に配置することで、コントロールの外観をグラフィカルにデザインできます。 カスタム コントロールについて詳しくは、「[さまざまなカスタム コントロール](/dotnet/framework/winforms/controls/varieties-of-custom-controls)」をご覧ください。

## <a name="design-the-control-layout"></a>コントロールのレイアウトをデザインする

DemoCalculator コントロールには、いくつかの Windows フォーム コントロールが含まれています。 この手順では、Windows フォーム デザイナーを使ってコントロールを配置します。

1. Windows フォーム デザイナーで、右下隅にあるサイズ変更ハンドルを選択して右下方にドラッグし、DemoCalculator コントロールを大きなサイズに変更します。 Visual Studio の右下隅に表示されているコントロールのサイズと位置の情報を確認します。 サイズ情報を見ながらコントロールのサイズを変更して、コントロールのサイズを幅 500 および高さ 400 に設定します。

2. **[ツールボックス]** で、 **[コンテナー]** ノードを選択して開きます。 **SplitContainer** コントロールを選択し、デザイナー画面にドラッグします。

   `SplitContainer` が、DemoCalculator コントロールのデザイナー画面に配置されます。

    > [!TIP]
    > `SplitContainer` コントロールのサイズは、DemoCalculator コントロールのサイズに合わせて自動的に調整されます。 **[プロパティ]** ウィンドウで、`SplitContainer` コントロールのプロパティ設定を確認します。 <xref:System.Windows.Forms.SplitContainer.Dock%2A> プロパティを見つけます。 その値は [DockStyle.Fill](xref:System.Windows.Forms.DockStyle.Fill) であり、これは `SplitContainer` コントロールのサイズが常に DemoCalculator コントロールの境界に合わせて自動的に変更されることを意味します。 DemoCalculator コントロールのサイズを変更して、この動作を確認します。

3. **[プロパティ]** ウィンドウで、<xref:System.Windows.Forms.SplitContainer.Dock%2A> プロパティの値を `None` に変更します。

    `SplitContainer` コントロールは既定のサイズに縮小され、DemoCalculator コントロールのサイズに従って変化しなくなります。

4. `SplitContainer` コントロールの右上隅にあるスマート タグ グリフ (![スマート タグ グリフ](media/smart-tag-glyph.gif)) を選択します。 **[親コンテナーにドッキングする]** を選択して、`Dock` プロパティを `Fill` に設定します。

    `SplitContainer` コントロールが、DemoCalculator コントロールの境界にドッキングされます。

    > [!NOTE]
    > いくつかのコントロールでは、デザインを容易にするスマート タグが提供されています。 詳細については、「[チュートリアル:Windows フォーム コントロールのスマート タグを使用した共通タスクの実行](/dotnet/framework/winforms/controls/performing-common-tasks-using-smart-tags-on-wf-controls)」をご覧ください。

5. パネル間の垂直方向の境界線を選択し、右にドラッグして、領域の大部分が左側のパネルによって使用されるようにします。

    `SplitContainer` により、DemoCalculator コントロールは、移動可能な境界線で 2 つのパネルに分割されます。 左側のパネルには電卓のボタンと表示が保持され、右側のパネルにはユーザーが実行した算術演算の記録が表示されます。

6. **[プロパティ]** ウィンドウで、`BorderStyle` プロパティの値を `Fixed3D` に変更します。

7. **[ツールボックス]** で、 **[コモン コントロール]** ノードを選択して開きます。 `ListView` コントロールを選択し、`SplitContainer` コントロールの右側のパネルにドラッグします。

8. `ListView` コントロールのスマート タグ グリフを選択します。 スマート タグ パネルで、`View` の設定を `Details` に変更します。

9. スマート タグ パネルで、 **[列の編集]** を選択します。

   **[ColumnHeader コレクション エディター]** ダイアログ ボックスが表示されます。

10. **[ColumnHeader コレクション エディター]** ダイアログ ボックスで、 **[追加]** を選択して `ListView` コントロールに列を追加します。 列の `Text` プロパティの値を「**History**」に変更します。 **[OK]** を選択して列を作成します。

11. スマート タグ パネルで、 **[親コンテナーにドッキングする]** を選択してから、スマート タグ グリフを選択してスマート タグ パネルを閉じます。

12. **[コンテナー]** ノードの **[ツールボックス]** から、`TableLayoutPanel` コントロールを `SplitContainer` コントロールの左側のパネルにドラッグします。

    `TableLayoutPanel` コントロールがデザイナー画面に表示され、そのスマート タグ パネルが開きます。 `TableLayoutPanel` コントロールの子コントロールが、グリッドに配置されます。 `TableLayoutPanel` コントロールには、DemoCalculator コントロールの表示とボタンが保持されます。 詳細については、「[チュートリアル:TableLayoutPanel を使用してコントロールを配置する](/dotnet/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel)」をご覧ください。

13. スマート タグ パネルで **[行および列の編集]** を選択します。

    **[列と行のスタイル]** ダイアログ ボックスが表示されます。

14. 5 列表示されるまで **[追加]** ボタンを選択します。 5 列すべてを選択し、 **[サイズの型]** ボックスで **[パーセント]** を選択します。 **[パーセント]** の値を **20** に設定します。 これにより、各列が同じ幅に設定されます。

15. **[表示]** で、 **[行]** を選択します。

16. 5 行表示されるまで **[追加]** を選択します。 5 行すべてを選択し、 **[サイズの型]** ボックスで **[パーセント]** を選択します。 **[パーセント]** の値を **20** に設定します。 これにより、各行が同じ高さに設定されます。

17. **[OK]** を選択して変更を受け入れた後、スマート タグ グリフを選択してスマート タグ パネルを閉じます。

18. **[プロパティ]** ウィンドウで、`Dock` プロパティの値を `Fill` に変更します。

## <a name="populate-the-control"></a>コントロールを設定する

コントロールのレイアウトを設定したので、DemoCalculator コントロールにボタンと表示を設定できます。

1. **ツールボックス**で、`TextBox` コントロール アイコンを選択します。

   `TextBox` コントロールが、`TableLayoutPanel` コントロールの最初のセルに配置されます。

2. **[プロパティ]** ウィンドウで、`TextBox` コントロールの ColumnSpan プロパティの値を **5** に変更します。

   `TextBox` コントロールが、行の中央の位置に移動されます。

3. `TextBox` コントロールの `Anchor` プロパティの値を `Left`、`Right` に変更します。

   `TextBox` コントロールが、5 つの列すべてを占めるように水平方向に拡張されます。

4. `TextBox` コントロールの `TextAlign` プロパティの値を `Right`に変更します。

5. **[プロパティ]** ウィンドウで、`Font` プロパティを展開します。 `TextBox` コントロールの `Size` を **14** に設定し、`Bold` を **true** に設定します。

6. `TableLayoutPanel` コントロールを選択します。

7. **ツールボックス**で、`Button` アイコンを選択します。

   `Button` コントロールが、`TableLayoutPanel` コントロールの次の空いているセルに配置されます。

8. **ツールボックス**で `Button` アイコンをさらに 4 回クリックし、`TableLayoutPanel` コントロールの 2 行目を設定します。

9. **Shift** キーを押しながら選択して、5 つの `Button` コントロールをすべて選択します。 **Ctrl**+**C** キーを押して、`Button` コントロールをクリップボードにコピーします。

10. **Ctrl**+**V** キーを 3 回押して、`Button` コントロールのコピーを `TableLayoutPanel` コントロールの残りの行に貼り付けます。

11. **Shift** キーを押しながら選択して、20 個の `Button` コントロールをすべて選択します。

12. **[プロパティ]** ウィンドウで、`Dock` プロパティの値を `Fill` に変更します。

    すべての `Button` コントロールが、それらを含むセルにいっぱいにドッキングされます。

13. **[プロパティ]** ウィンドウで、`Margin` プロパティを展開します。 `All` の値を **5** に設定します。

    すべての `Button` コントロールのサイズが小さくなり、それらの間に大きな余白が作成されます。

14. **button10** と **button20** を選択し、**Delete** キーを押してレイアウトから削除します。

15. **button5** と **button15** を選択し、それらの `RowSpan` プロパティの値を **2** に変更します。 これらは、DemoCalculator コントロールの **[Clear]** ボタンと **[=]** ボタンになります。

## <a name="use-the-document-outline-window"></a>[ドキュメント アウトライン] ウィンドウを使用する

コントロールまたはフォームに複数のコントロールが設定されている場合は、[ドキュメント アウトライン] ウィンドウでレイアウト内を移動する方が簡単な場合があります。

1. メニュー バーで **[表示]**  >  **[その他のウィンドウ]**  >  **[ドキュメント アウトライン]** の順に選択します。

   [ドキュメント アウトライン] ウィンドウには、DemoCalculator コントロールとその構成コントロールのツリー ビューが表示されます。 `SplitContainer` のようなコンテナー コントロールには、ツリー内のサブノードとして子コントロールが表示されます。 また、[ドキュメント アウトライン] ウィンドウを使用して、その場でコントロールの名前を変更することもできます。

2. **[ドキュメント アウトライン]** ウィンドウで、**button1** を右クリックして、 **[名前の変更]** を選択します。 名前を sevenButton に変更します。

3. **[ドキュメント アウトライン]** ウィンドウを使用して、`Button` コントロールの名前を、デザイナーで生成された名前から、次の一覧に従った運用環境の名前に変更します。

   - button1 を **sevenButton** に

   - button2 を **eightButton** に

   - button3 を **nineButton** に

   - button4 を **divisionButton** に

   - button5 を **clearButton** に

   - button6 を **fourButton** に

   - button7 を **fiveButton** に

   - button8 を **sixButton** に

   - button9 を **multiplicationButton** に

   - button11 を **oneButton** に

   - button12 を **twoButton** に

   - button13 を **threeButton** に

   - button14 を **subtractionButton** に

   - button15 を **equalsButton** に

   - button16 を **zeroButton** に

   - button17 を **changeSignButton** に

   - button18 を **decimalButton** に

   - button19 を **additionButton** に

4. **[ドキュメント アウトライン]** ウィンドウと **[プロパティ]** ウィンドウを使用して、各 `Button` コントロール名の `Text` プロパティの値を次の一覧のように変更します。

   - sevenButton コントロールの text プロパティを「**7**」に変更します

   - eightButton コントロールの text プロパティを「**8**」に変更します

   - nineButton コントロールの text プロパティを「**9**」に変更します

   - divisionButton コントロールの text プロパティを「 **/** 」 (スラッシュ) に変更します

   - clearButton コントロールの text プロパティを「**Clear**」に変更します

   - fourButton コントロールの text プロパティを「**4**」に変更します

   - fiveButton コントロールの text プロパティを「**5**」に変更します

   - sixButton コントロールの text プロパティを「**6**」に変更します

   - multiplicationButton コントロールの text プロパティを「 **\*** 」 (アスタリスク) に変更します

   - oneButton コントロールの text プロパティを「**1**」に変更します

   - twoButton コントロールの text プロパティを「**2**」に変更します

   - threeButton コントロールの text プロパティを「**3**」に変更します

   - subtractionButton コントロールの text プロパティを「 **-** 」 (ハイフン) に変更します

   - equalsButton コントロールの text プロパティを「 **=** 」 (等号) に変更します

   - zeroButton コントロールの text プロパティを「**0**」に変更します

   - changeSignButton コントロールの text プロパティを「 **+/-** 」に変更します

   - decimalButton コントロールの text プロパティを「 **.** 」 (ピリオド) に変更します

   - additionButton コントロールの text プロパティを「 **+** 」 (プラス記号) に変更します

5. デザイン画面で、**Shift** キーを押しながら選択して、`Button` コントロールをすべて選択します。

6. **[プロパティ]** ウィンドウで、`Font` プロパティを展開します。 すべての `Button` コントロールの `Size` を **14** に設定し、`Bold` を **true** に設定します。

これで、DemoCalculator コントロールのデザインは完了です。 残っているのは、電卓のロジックを提供することだけです。

## <a name="implement-event-handlers"></a>イベント ハンドラーを実装する

DemoCalculator コントロールのボタンには、電卓ロジックの多くを実装するために使用できるイベント ハンドラーがあります。 Windows フォーム デザイナーを使用すると、すべてのボタンのすべてのイベント ハンドラーのスタブを 1 回の選択で実装できます。

1. デザイン画面で、**Shift** キーを押しながら選択して、`Button` コントロールをすべて選択します。

2. いずれかの `Button` コントロールを選択します。

   コード エディターが開き、デザイナーによって生成されたイベント ハンドラーが表示されます。

## <a name="test-the-control"></a>コントロールをテストする

DemoCalculator コントロールは <xref:System.Windows.Forms.UserControl> クラスを継承しているので、**UserControl テスト コンテナー**を使用してその動作をテストできます。 詳細については、「[方法:UserControl の実行時の動作をテストする](/dotnet/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol)」をご覧ください。

1. **F5** キーを押し、**UserControl Test Container** で DemoCalculator コントロールをビルドして実行します。

2. `SplitContainer` のパネル間の境界線を選択し、左右にドラッグします。 `TableLayoutPanel` とそのすべての子コントロールのサイズが、使用可能なスペースに合わせて自動的に変更されます。

3. コントロールのテストが完了したら、 **[閉じる]** を選択します。

## <a name="use-the-control-on-a-form"></a>フォームでコントロールを使用する

DemoCalculator コントロールを他の複合コントロールまたはフォームで使用できます。 以下の手順ではその使用方法を説明します。

### <a name="create-the-project"></a>プロジェクトの作成

最初にアプリケーションのプロジェクトを作成します。 このプロジェクトを使用して、カスタム コントロールが表示されるアプリケーションをビルドします。

1. 新しい **Windows フォーム アプリケーション** プロジェクトを作成し、**DemoCalculatorTest** という名前を付けます。

2. **ソリューション エクスプローラー**で、**DemoCalculatorTest** プロジェクトを右クリックし、 **[参照の追加]** を選択して、 **[参照の追加]** ダイアログ ボックスを開きます。

3. **[プロジェクト]** タブに移動し、DemoCalculatorLib プロジェクトを選択して、テスト プロジェクトへの参照を追加します。

4. **ソリューション エクスプローラー**で、**DemoCalculatorTest** を右クリックし、 **[スタートアップ プロジェクトに設定]** を選択します。

5. Windows フォーム デザイナーで、フォームのサイズを約 **700 x 500** に増やします。

### <a name="use-the-control-in-the-forms-layout"></a>フォームのレイアウトでコントロールを使用する

アプリケーションで DemoCalculator コントロールを使用するには、フォーム上に配置する必要があります。

1. **[ツールボックス]** で、 **[DemoCalculatorLib コンポーネント]** ノードを展開します。

2. **DemoCalculator** コントロールを **[ツールボックス]** からフォームにドラッグします。 コントロールをフォームの左上隅に移動します。 コントロールがフォームの境界線の近づくと、*スナップ線*が表示されます。 スナップ線では、フォームの `Padding` プロパティとコントロールの `Margin` プロパティの距離が示されます。 スナップ線によって示される位置にコントロールを配置します。

   詳細については、「[チュートリアル:スナップ線を使用した Windows フォーム上のコントロールの配置](/dotnet/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines)」をご覧ください。

3. `Button`[ツールボックス]**から** コントロールをドラッグし、フォームにドロップします。

4. `Button` コントロールを DemoCalculator コントロール上であちこち移動して、スナップ線が表示される位置を確認します。 この機能を使用すると、コントロールを正確かつ簡単に配置できます。 終わったら `Button` コントロールを削除します。

5. DemoCalculator コントロールを右クリックし、 **[プロパティ]** を選択します。

6. `Dock` プロパティの値を `Fill` に変更します。

7. フォームを選択し、[`Padding` プロパティ] ノードを展開します。 **[All]** の値を **20** に変更します。

   フォームの新しい `Padding` の値に合わせて、DemoCalculator コントロールのサイズが縮小されます。

8. さまざまなサイズ変更ハンドルを別の位置にドラッグして、フォームのサイズを変更します。 DemoCalculator コントロールのサイズがどのように変化するかを確認します。

## <a name="next-steps"></a>次の手順

この記事では、簡単な電卓用のユーザー インターフェイスを作成する方法について説明しました。 続行するには、電卓ロジックを実装してその機能を拡張し、[ClickOnce を利用してアプリを公開](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)できます。 または、[Windows フォームを使用して画像ビューアーを作成する](../ide/tutorial-1-create-a-picture-viewer.md)別のチュートリアルに進んでもかまいません。

## <a name="see-also"></a>関連項目

- [Windows フォームのコントロール](/dotnet/framework/winforms/controls/)
- [Windows フォームのコントロールのアクセシビリティ](/dotnet/framework/winforms/controls/providing-accessibility-information-for-controls-on-a-windows-form)
- [ClickOnce を使用して公開する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
