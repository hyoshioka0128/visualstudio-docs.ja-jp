---
title: Windows フォーム ツールボックス コントロールを作成する |マイクロソフトドキュメント
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- winforms
- toolbox
- windows forms
ms.assetid: 0be6ffc1-8afd-4d02-9a5d-e27dde05fde6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d7e7749302252c5d56f21c58de9b6ac23f898572
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739588"
---
# <a name="create-a-windows-forms-toolbox-control"></a>Windows フォーム ツールボックス コントロールを作成する

Visual Studio の機能拡張ツール (VS SDK) に含まれている Windows フォーム ツールボックス コントロール項目テンプレートを使用すると、拡張機能のインストール時に自動的に追加される**ツールボックス**コントロールを作成できます。 このチュートリアルでは、テンプレートを使用して、他のユーザーに配布できる単純なカウンター コントロールを作成する方法を示します。

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-the-toolbox-control"></a>ツールボックス コントロールを作成する

Windows フォーム ツールボックス コントロール テンプレートは、未定義のユーザー コントロールを作成し、**コントロールをツールボックス**に追加するために必要なすべての機能を提供します。

### <a name="create-an-extension-with-a-windows-forms-toolbox-control"></a>Windows フォーム ツールボックス コントロールを使用して拡張機能を作成する

1. という名前`MyWinFormsControl`の VSIX プロジェクトを作成します。 VSIX プロジェクト テンプレートは、"vsix" を検索して [**新しいプロジェクト**] ダイアログで見つけることができます。

2. プロジェクトが開いたら、**という**名前`Counter`の Windows フォーム ツールボックス コントロール項目テンプレートを追加します。 ソリューション**エクスプローラ**で、プロジェクト ノードを右クリックし、[**Add** > **新しい項目**の追加] を選択します。 [**新しい項目の追加]** ダイアログ**で、[Visual C#** > **の機能拡張**] に移動し **、[Windows フォーム ツールボックス コントロール**] を選択します。

3. これにより、ユーザー コントロール、`ProvideToolboxControlAttribute`<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute>**ツールボックス**にコントロールを配置する、配置用の VSIX マニフェストに**Microsoft.VisualStudio.ToolboxControl**資産エントリが追加されます。

### <a name="build-a-user-interface-for-the-control"></a>コントロールのユーザー インターフェイスを構築する

コントロール`Counter`には、現在のカウントを表示<xref:System.Windows.Forms.Label>する a と、カウントを<xref:System.Windows.Forms.Button>0 にリセットする 2 つの子コントロールが必要です。 呼び出し元がプログラムでカウンターをインクリメントするため、他の子コントロールは必要ありません。

#### <a name="to-build-the-user-interface"></a>ユーザー インターフェイスを作成するには

1. **ソリューション エクスプローラー**で *、Counter.cs*をダブルクリックしてデザイナーで開きます。

2. **ここをクリック**を削除 ! Windows フォーム ツールボックス コントロールの項目テンプレートを追加するときに既定で含まれるボタンです。

3. **ツールボックス**からコントロールを`Label`ドラッグし、その下`Button`のコントロールをデザイン 画面にドラッグします。

4. ユーザー コントロール全体のサイズを 150 ピクセル、50 ピクセルに変更し、ボタン コントロールのサイズを 50 ピクセル、20 ピクセルに変更します。

5. [**プロパティ]** ウィンドウで、デザイン サーフェイスのコントロールに次の値を設定します。

    |コントロール|プロパティ|値|
    |-------------|--------------|-----------|
    |`Label1`|**[テキスト]**|""|
    |`Button1`|**名前**|リセット|
    |`Button1`|**[テキスト]**|Reset|

### <a name="code-the-user-control"></a>ユーザー コントロールをコーディングする

コントロール`Counter`は、カウンターをインクリメントするメソッド、カウンタがインクリメントされるたびに発生するイベント **、Reset**ボタン、および現在のカウントを格納する 3 つのプロパティ、表示テキスト、および [**リセット**] ボタンの表示と非表示を切り替えます。 `ProvideToolboxControl` 属性は、 **[ツールボックス]** のどの場所に `Counter` コントロールが表示されるかを判断します。

#### <a name="to-code-the-user-control"></a>ユーザー コントロールをコーディングするには

1. フォームをダブルクリックして、コード ウィンドウで読み込みイベント ハンドラーを開きます。

2. イベント ハンドラー メソッドの上に、コントロール クラスでは、次の例に示すように、カウンター値を格納する整数と表示テキストを格納する文字列を作成します。

    ```csharp
    int currentValue;
    string displayText;
    ```

3. 次のパブリック プロパティ宣言を作成します。

    ```csharp
    public int Value {
        get { return currentValue; }
    }

    public string Message {
        get { return displayText; }
        set { displayText = value; }
    }

    public bool ShowReset {
        get { return btnReset.Visible; }
        set { btnReset.Visible = value; }
    }

    ```

    呼び出し元は、これらのプロパティにアクセスして、カウンタの表示テキストを取得および設定したり **、[Reset]** ボタンを表示または非表示にしたりできます。 呼び出し元は、読み取り専用`Value`プロパティの現在の値を取得できますが、値を直接設定することはできません。

4. コントロールのイベントに次の`Load`コードを記述します。

    ```csharp
    private void Counter_Load(object sender, EventArgs e)
    {
        currentValue = 0;
        label1.Text = Message + Value;
    }

    ```

    イベントで**Label**テキスト<xref:System.Windows.Forms.UserControl.Load>を設定すると、ターゲット プロパティを読み込んでから値を適用できます。 コンストラクタで**Label**テキストを設定すると **、ラベルが**空になります。

5. カウンタをインクリメントする次のパブリック メソッドを作成します。

    ```csharp
    public void Increment()
    {
        currentValue++;
        label1.Text = displayText + Value;
        Incremented(this, EventArgs.Empty);
    }

    ```

6. コントロール クラスにイベント`Incremented`の宣言を追加します。

    ```csharp
    public event EventHandler Incremented;
    ```

    呼び出し元は、カウンターの値の変更に応答するために、このイベントにハンドラーを追加できます。

7. デザイン ビューに戻り **、[Reset]** ボタンをダブルクリックして`btnReset_Click`イベント ハンドラを生成し、次の例に示すように入力します。

    ```csharp
    private void btnReset_Click(object sender, EventArgs e)
    {
        currentValue = 0;
        label1.Text = displayText + Value;
    }

    ```

8. すぐに、クラス定義の上、 `ProvideToolboxControl` 属性の宣言内で、最初のパラメーターの値を `"MyWinFormsControl.Counter"` から `"General"`に変更します。 これにより、 **[ツールボックス]** のコントロールをホストする項目グループの名前が設定されます。

    次の例では、 `ProvideToolboxControl` の属性と、調整されたクラス定義を示しています。

    ```csharp
    [ProvideToolboxControl("General", false)]
    public partial class Counter : UserControl
    ```

### <a name="test-the-control"></a>コントロールをテストする

 **ツールボックス**コントロールをテストするには、まず開発環境でテストし、コンパイル済みアプリケーションでテストします。

#### <a name="to-test-the-control"></a>コントロールをテストするには

1. **F5 キー**を押して**デバッグを開始**します。

    このコマンドは、プロジェクトをビルドし、コントロールがインストールされている Visual Studio の 2 番目の実験インスタンスを開きます。

2. Visual Studio の実験用インスタンスで **、Windows フォーム アプリケーション**プロジェクトを作成します。

3. **ソリューション エクスプローラー**で*Form1.csダブルクリックして*、デザイナーで開いていない場合は、デザイナーで開きます。

4. **ツールボックス**の [`Counter`**全般**] セクションにコントロールが表示されます。

5. フォームに`Counter`コントロールをドラッグし、選択します。 `Value`、 `Message`、および`ShowReset`プロパティが、 から継承されたプロパティと共に **[ プロパティ** <xref:System.Windows.Forms.UserControl>] ウィンドウに表示されます。

6. `Message` プロパティを `Count:` に設定します。

7. コントロールを<xref:System.Windows.Forms.Button>フォームにドラッグし、ボタンの名前とテキストのプロパティを に`Test`設定します。

8. ボタンをダブルクリックして *、コード*ビューでForm1.csを開き、クリック ハンドラを作成します。

9. クリック ハンドラで、`counter1.Increment()`を呼び出します。

10. コンストラクター関数で、 を呼び出`InitializeComponent`した後`counter1``.``Incremented +=`に、 を入力し **、Tab キー**を 2 回押します。

    Visual Studio は、イベントのフォーム レベル`counter1.Incremented`のハンドラーを生成します。

11. イベント`Throw`ハンドラでステートメントを強調表示し、「 `mbox`」と入力し **、Tab キー**を 2 回押して、mbox コード スニペットからメッセージ ボックスを生成します。

12. 次の`if`/`else`行に次のブロックを追加して、[**リセット**] ボタンの表示を設定します。

    ```csharp
    if (counter1.Value < 5) counter1.ShowReset = false;
    else counter1.ShowReset = true;
    ```

13. **F5**キーを押します。

    フォームが開きます。 コントロール`Counter`には、次のテキストが表示されます。

    **カウント: 0**

14. **[Test]** をクリックします。

    カウンタがインクリメントされ、Visual Studio にメッセージ ボックスが表示されます。

15. メッセージ ボックスを閉じます。

    [**リセット]** ボタンが消えます。

16. カウンタがメッセージ ボックスを閉じる**5**に達するまで**Test**をクリックします。

    リセット**ボタン**が再表示されます。

17. **[リセット]** をクリックします。

    カウンタは**0**にリセットされます。

## <a name="next-steps"></a>次の手順

**ツールボックス**コントロールをビルドすると、プロジェクトの \bin\debug\ フォルダーに*ProjectName.vsix*という名前のファイルが作成されます。 コントロールを展開するには *、.vsix*ファイルをネットワークまたは Web サイトにアップロードします。 ユーザーが *.vsix*ファイルを開くと、コントロールがインストールされ、ユーザーのコンピューター上の Visual Studio**ツールボックス**に追加されます。 または *、.vsix*ファイルを[Visual Studio マーケットプレース](https://marketplace.visualstudio.com/)にアップロードして、ユーザーが **[ツール** > **の拡張機能と更新プログラム**] ダイアログで参照して見つけることもできます。

## <a name="see-also"></a>関連項目

- [ビジュアル スタジオの他の部分を拡張します。](../extensibility/extending-other-parts-of-visual-studio.md)
- [WPF ツールボックス コントロールの作成](../extensibility/creating-a-wpf-toolbox-control.md)
- [ビジュアル スタジオの他の部分を拡張します。](../extensibility/extending-other-parts-of-visual-studio.md)
- [Windows フォーム コントロールの開発の基本](/dotnet/framework/winforms/controls/windows-forms-control-development-basics)
