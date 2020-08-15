---
title: Windows フォームツールボックスコントロールの作成 |Microsoft Docs
ms.date: 3/16/2019
ms.topic: how-to
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
ms.openlocfilehash: cb0f0e66d623f53c641126f1e07edaa476d831ae
ms.sourcegitcommit: 577c905de52057a741e68c2ed168ea527813fda5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2020
ms.locfileid: "88248605"
---
# <a name="create-a-windows-forms-toolbox-control"></a>Windows フォームツールボックスコントロールを作成する

Visual Studio Extensibility Tools (VS SDK) に含まれている Windows フォームツールボックスコントロール項目テンプレートを使用すると、拡張機能のインストール時に自動的に追加される **ツールボックス** コントロールを作成できます。 このチュートリアルでは、テンプレートを使用して、他のユーザーに配布できる単純なカウンターコントロールを作成する方法について説明します。

## <a name="prerequisites"></a>前提条件

Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-the-toolbox-control"></a>ツールボックスコントロールを作成する

Windows フォームツールボックスコントロールテンプレートは、未定義のユーザーコントロールを作成し、コントロールを **ツールボックス**に追加するために必要なすべての機能を提供します。

### <a name="create-an-extension-with-a-windows-forms-toolbox-control"></a>Windows フォームツールボックスコントロールを使用して拡張機能を作成する

1. という名前の VSIX プロジェクトを作成 `MyWinFormsControl` します。 VSIX プロジェクトテンプレートは、"vsix" を検索することで、[ **新しいプロジェクト** ] ダイアログで見つけることができます。

2. プロジェクトが開いたら、という名前の **Windows フォームツールボックスコントロール** 項目テンプレートを追加 `Counter` します。 **ソリューションエクスプローラー**で、プロジェクトノードを選択して保持 (または右クリック) し、 **Add**[  >  **新しい項目**の追加] を選択します。 [**新しい項目の追加**] ダイアログで、[ **Visual C#** の  >  **機能拡張**] にアクセスし、[ **Windows フォームツールボックスコントロール**] を選択します。

3. これにより、ユーザーコントロールが追加され、 `ProvideToolboxControlAttribute` <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> **ツールボックス**にコントロールが配置されます。また、展開用の VSIX マニフェストに **VisualStudio** アセットエントリが追加されます。

### <a name="build-a-user-interface-for-the-control"></a>コントロールのユーザーインターフェイスを作成する

コントロールには、 `Counter` 現在の数を表示するための2つの子コントロール <xref:System.Windows.Forms.Label> と、カウントを <xref:System.Windows.Forms.Button> 0 にリセットするためのが必要です。 呼び出し元はプログラムによってカウンターをインクリメントするため、他の子コントロールは必要ありません。

#### <a name="to-build-the-user-interface"></a>ユーザー インターフェイスを作成するには

1. **ソリューションエクスプローラー**で、 *Counter.cs*をダブルタップするか、ダブルクリックしてデザイナーで開きます。

2. ここを **クリックしてください。** Windows フォームツールボックスコントロール項目テンプレートを追加するときに既定で含まれるボタン。

3. [ **ツールボックス**] からコントロールをドラッグし、 `Label` `Button` その下にあるコントロールをデザインサーフェイスにドラッグします。

4. ユーザーコントロール全体のサイズを150、50ピクセルに変更し、ボタンコントロールのサイズを50、20ピクセルに変更します。

5. [ **プロパティ** ] ウィンドウで、デザインサーフェイス上のコントロールに対して次の値を設定します。

    |コントロール|プロパティ|[値]|
    |-------------|--------------|-----------|
    |`Label1`|**[テキスト]**|""|
    |`Button1`|**名前**|btnReset|
    |`Button1`|**[テキスト]**|Reset|

### <a name="code-the-user-control"></a>ユーザーコントロールのコーディング

コントロールは、 `Counter` カウンターをインクリメントするメソッド、カウンターがインクリメントされるたびに発生するイベント、 **リセット** ボタン、および現在のカウント、表示テキスト、および **リセット** ボタンを表示するか非表示にするかを指定する3つのプロパティを公開します。 `ProvideToolboxControl` 属性は、 **[ツールボックス]** のどの場所に `Counter` コントロールが表示されるかを判断します。

#### <a name="to-code-the-user-control"></a>ユーザーコントロールをコーディングするには

1. フォームをダブルタップまたはダブルクリックすると、その読み込みイベントハンドラーがコードウィンドウに表示されます。

2. イベントハンドラーメソッドの上にあるコントロールクラスで、次の例に示すように、カウンター値を格納する整数と表示テキストを格納する文字列を作成します。

    ```csharp
    int currentValue;
    string displayText;
    ```

3. 次のパブリックプロパティ宣言を作成します。

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

    呼び出し元は、これらのプロパティにアクセスして、カウンターの表示テキストを取得および設定したり、 **リセット** ボタンの表示と非表示を切り替えることができます。 呼び出し元は、読み取り専用プロパティの現在の値を取得でき `Value` ますが、値を直接設定することはできません。

4. コントロールのイベントに次のコードを追加 `Load` します。

    ```csharp
    private void Counter_Load(object sender, EventArgs e)
    {
        currentValue = 0;
        label1.Text = Message + Value;
    }

    ```

    イベントの **ラベル** テキストを設定する <xref:System.Windows.Forms.UserControl.Load> と、対象のプロパティの値が適用される前に読み込むことができます。 コンストラクターで **ラベル** のテキストを設定すると、空の **ラベル**が生成されます。

5. 次のパブリックメソッドを作成して、カウンターをインクリメントします。

    ```csharp
    public void Increment()
    {
        currentValue++;
        label1.Text = displayText + Value;
        Incremented(this, EventArgs.Empty);
    }

    ```

6. イベントの宣言を `Incremented` コントロールクラスに追加します。

    ```csharp
    public event EventHandler Incremented;
    ```

    呼び出し元は、このイベントにハンドラーを追加して、カウンターの値の変更に応答することができます。

7. デザインビューに戻り、[ **リセット** ] ボタンをダブルタップまたはダブルクリックして、イベントハンドラーを生成し `btnReset_Click` ます。 次に、次の例に示すように入力します。

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

 **ツールボックス**コントロールをテストするには、まず開発環境でテストしてから、コンパイル済みアプリケーションでテストします。

#### <a name="to-test-the-control"></a>コントロールをテストするには

1. **F5**キーを押して**デバッグを開始**します。

    このコマンドは、プロジェクトをビルドし、コントロールがインストールされている Visual Studio の2番目の実験用インスタンスを開きます。

2. Visual Studio の実験用インスタンスで、 **Windows フォームアプリケーション** プロジェクトを作成します。

3. **ソリューションエクスプローラー**で、 *Form1.cs*をダブルタップするか、ダブルクリックしてデザイナーで開きます (まだ開いていない場合)。

4. **ツールボックス**では、 `Counter` コントロールが **[全般**] セクションに表示されます。

5. コントロールを `Counter` フォームにドラッグし、選択します。 、、およびの各プロパティは、 `Value` `Message` `ShowReset` から継承されたプロパティと共に [ **プロパティ** ] ウィンドウに表示され <xref:System.Windows.Forms.UserControl> ます。

6. `Message` プロパティを `Count:`に設定します。

7. コントロールを <xref:System.Windows.Forms.Button> フォームにドラッグし、ボタンの name プロパティと text プロパティをに設定し `Test` ます。

8. ボタンをダブルタップまたはダブルクリックして、コードビューで *Form1.cs* を開き、クリックハンドラーを作成します。

9. クリックハンドラーで、を呼び出し `counter1.Increment()` ます。

10. コンストラクター関数で、の呼び出しの後に `InitializeComponent` 「」と入力し、 `counter1``.``Incremented +=` **tab** キーを2回押します。

    Visual Studio によって、イベントのフォームレベルのハンドラーが生成さ `counter1.Incremented` れます。

11. イベントハンドラーでステートメントを強調表示し、「」 `Throw` と入力し `mbox` ます。 **tab** キーを2回押すと、mbox コードスニペットからメッセージボックスが生成されます。

12. 次の行で、次のブロックを追加して `if` / `else` 、[**リセット**] ボタンの表示を設定します。

    ```csharp
    if (counter1.Value < 5) counter1.ShowReset = false;
    else counter1.ShowReset = true;
    ```

13. **F5**キーを押します。

    フォームが開きます。 コントロールには `Counter` 、次のテキストが表示されます。

    **カウント: 0**

14. **[Test]** を選択します。

    カウンターの値が増加し、Visual Studio によってメッセージボックスが表示されます。

15. メッセージボックスを閉じます。

    [ **リセット** ] ボタンが表示されなくなります。

16. [ **テスト** ] を選択すると、カウンターがメッセージボックスを閉じるたびに **5** に達します。

    [ **リセット** ] ボタンが再び表示されます。

17. **[リセット]** を選択します。

    カウンターが **0**にリセットされます。

## <a name="next-steps"></a>次のステップ

**ツールボックス**コントロールをビルドすると、Visual Studio によってプロジェクトの \bin\debug\ フォルダーに*ProjectName*という名前のファイルが作成されます。 コントロールを配置するには、 *.vsix* ファイルをネットワークまたは Web サイトにアップロードします。 ユーザーが *.vsix* ファイルを開くと、コントロールがインストールされ、ユーザーのコンピューターの Visual Studio **ツールボックス** に追加されます。 または、 *.vsix*ファイルを[Visual Studio Marketplace](https://marketplace.visualstudio.com/)にアップロードして、ユーザーが [**ツール**  >  ] [**拡張機能と更新プログラム**] ダイアログで参照して検索できるようにすることもできます。

## <a name="see-also"></a>関連項目

- [Visual Studio の他の部分を拡張する](../extensibility/extending-other-parts-of-visual-studio.md)
- [WPF ツールボックスコントロールの作成](../extensibility/creating-a-wpf-toolbox-control.md)
- [Visual Studio の他の部分を拡張する](../extensibility/extending-other-parts-of-visual-studio.md)
- [Windows フォームコントロールの開発の基礎](/dotnet/framework/winforms/controls/windows-forms-control-development-basics)
