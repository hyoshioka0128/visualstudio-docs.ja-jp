---
title: Windows フォームツールボックスコントロールの作成 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- winforms
- toolbox
- windows forms
ms.assetid: 0be6ffc1-8afd-4d02-9a5d-e27dde05fde6
caps.latest.revision: 20
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 03fcc73c58baa1482c53e104a9946ffaa354f1a0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65698964"
---
# <a name="creating-a-windows-forms-toolbox-control"></a>Windows フォーム ツールボックス コントロールの作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio Extensibility Tools (VS SDK) に含まれている Windows フォームツールボックスコントロール項目テンプレートを使用すると、拡張機能のインストール時に自動的に **ツールボックス** に追加されるコントロールを作成できます。 このトピックでは、テンプレートを使用して、他のユーザーに配布できる単純なカウンターコントロールを作成する方法について説明します。  
  
## <a name="prerequisites"></a>前提条件  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
## <a name="creating-a-windows-forms-toolbox-control"></a>Windows フォーム ツールボックス コントロールの作成  
 Windows フォームツールボックスコントロールテンプレートは、未定義のユーザーコントロールを作成し、コントロールを **ツールボックス**に追加するために必要なすべての機能を提供します。  
  
#### <a name="create-an-extension-with-a-windows-forms-toolbox-control"></a>Windows フォームツールボックスコントロールを使用して拡張機能を作成する  
  
1. という名前の VSIX プロジェクトを作成 `MyWinFormsControl` します。 VSIX プロジェクトテンプレートは、[ **新しいプロジェクト** ] ダイアログボックスの [ **Visual C#]/[拡張機能**] で見つけることができます。  
  
2. プロジェクトが開いたら、という名前の **Windows フォームツールボックスコントロール** 項目テンプレートを追加 `Counter` します。 **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[追加]、[**新しい項目**] の順に選択します。 [**新しい項目の追加**] ダイアログで、[ **Visual C#]/[機能拡張**] にアクセスし、[ **Windows フォームツールボックスコントロール**] を選択します。  
  
3. これにより、ユーザーコントロールが追加され、 `ProvideToolboxControlAttribute` <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> **ツールボックス**にコントロールが配置されます。また、展開用の VSIX マニフェストに**VisualStudio**アセットエントリが追加されます。  
  
### <a name="building-a-user-interface-for-the-control"></a>コントロールのユーザー インターフェイスの構築  
 コントロールには、 `Counter` 現在の数を表示するための2つの子コントロール <xref:System.Windows.Forms.Label> と、カウントを <xref:System.Windows.Forms.Button> 0 にリセットするためのが必要です。 呼び出し元はプログラムによってカウンターをインクリメントするため、他の子コントロールは必要ありません。  
  
##### <a name="to-build-the-user-interface"></a>ユーザー インターフェイスを作成するには  
  
1. **ソリューションエクスプローラー**で、Counter.cs をダブルクリックしてデザイナーで開きます。  
  
2. 「ここをクリック」を削除します。 Windows フォームツールボックスコントロール項目テンプレートを追加するときに既定で含まれる**ボタン**。  
  
3. [ **ツールボックス**] からコントロールをドラッグし、 `Label` `Button` その下にあるコントロールをデザインサーフェイスにドラッグします。  
  
4. ユーザーコントロール全体のサイズを150、50ピクセルに変更し、ボタンコントロールのサイズを50、20ピクセルに変更します。  
  
5. [ **プロパティ** ] ウィンドウで、デザインサーフェイス上のコントロールに対して次の値を設定します。  
  
    |コントロール|プロパティ|値|  
    |-------------|--------------|-----------|  
    |`Label1`|**Text**|""|  
    |`Button1`|**名前**|btnReset|  
    |`Button1`|**Text**|Reset|  
  
### <a name="coding-the-user-control"></a>ユーザー コントロールのコーディング  
 `Counter` コントロールは、カウンターをインクリメントするメソッド、カウンターがインクリメントされると発生するイベント、および `Reset` ボタンを公開します。また、現在のカウント、表示テキスト、および `Reset` ボタンの表示または非表示の状態を格納するための、3 つのプロパティも公開します。 `ProvideToolboxControl` 属性は、 **[ツールボックス]** のどの場所に `Counter` コントロールが表示されるかを判断します。  
  
##### <a name="to-code-the-user-control"></a>ユーザーコントロールをコーディングするには  
  
1. フォームをダブルクリックすると、その読み込みイベントハンドラーがコードウィンドウに表示されます。  
  
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
  
     呼び出し元は、これらのプロパティにアクセスして、カウンターの表示テキストを取得および設定したり、ボタンの表示と非表示を切り替えることができ `Reset` ます。 呼び出し元は、読み取り専用プロパティの現在の値を取得でき `Value` ますが、値を直接設定することはできません。  
  
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
  
7. デザインビューに戻り、ボタンをダブルクリックして `Reset` イベントハンドラーを生成し、 `btnReset_Click` 次の例に示すように入力します。  
  
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
  
### <a name="testing-the-control"></a>コントロールのテスト  
 **ツールボックス**コントロールをテストするには、まず開発環境でテストしてから、コンパイル済みアプリケーションでテストします。  
  
##### <a name="to-test-the-control"></a>コントロールをテストするには  
  
1. F5 キーを押す。  
  
     これにより、プロジェクトがビルドされ、コントロールがインストールされている Visual Studio の2番目の実験用インスタンスが開きます。  
  
2. Visual Studio の実験用インスタンスで、 **Windows フォームアプリケーション** プロジェクトを作成します。  
  
3. **ソリューションエクスプローラー**で、Form1.cs をダブルクリックしてデザイナーで開きます (まだ開いていない場合)。  
  
4. **ツールボックス**では、 `Counter` コントロールが **[全般**] セクションに表示されます。  
  
5. コントロールを `Counter` フォームにドラッグし、選択します。 、、およびの各プロパティは、 `Value` `Message` `ShowReset` から継承されたプロパティと共に [ **プロパティ** ] ウィンドウに表示され <xref:System.Windows.Forms.UserControl> ます。  
  
6. `Message` プロパティを `Count:`に設定します。  
  
7. コントロールを <xref:System.Windows.Forms.Button> フォームにドラッグし、ボタンの name プロパティと text プロパティをに設定し `Test` ます。  
  
8. ボタンをダブルクリックして、コードビューで Form1.cs を開き、クリックハンドラーを作成します。  
  
9. クリックハンドラーで、を呼び出し `counter1.Increment()` ます。  
  
10. コンストラクター関数で、の呼び出しの後に `InitializeComponent` 「」と入力し、 `counter1``.``Incremented +=` tab キーを2回押します。  
  
     Visual Studio によって、イベントのフォームレベルのハンドラーが生成さ `counter1.Incremented` れます。  
  
11. イベントハンドラーでステートメントを強調表示し、「」 `Throw` と入力し `mbox` ます。 tab キーを2回押すと、mbox コードスニペットからメッセージボックスが生成されます。  
  
12. 次の行で、次のブロックを追加して、 `if` / `else` ボタンの表示を設定し `Reset` ます。  
  
    ```csharp  
    if (counter1.Value < 5) counter1.ShowReset = false;  
    else counter1.ShowReset = true;  
    ```  
  
13. F5 キーを押す。  
  
     フォームが開きます。 コントロールには `Counter` 、次のテキストが表示されます。  
  
     **カウント: 0**  
  
14. **[Test]** をクリックします。  
  
     カウンターの値が増加し、Visual Studio によってメッセージボックスが表示されます。  
  
15. メッセージボックスを閉じます。  
  
     [ **リセット** ] ボタンが表示されなくなります。  
  
16. [ **テスト** ] をクリックすると、カウンターがメッセージボックスを閉じるたびに **5** に達します。  
  
     [ **リセット** ] ボタンが再度表示されます。  
  
17. **[リセット]** をクリックします。  
  
     カウンターが **0**にリセットされます。  
  
## <a name="next-steps"></a>次の手順  
 **[ツールボックス]** のコントロールを構築すると、Visual Studio によって、プロジェクトの \bin\debug\ フォルダーに *プロジェクト名*.vsix という名前のファイルが作成されます。 コントロールは、.vsix ファイルをネットワークや Web サイトにアップロードすることで展開できます。 ユーザーが .vsix ファイルを開くと、コントロールがインストールされ、ユーザーのコンピューターの Visual Studio **ツールボックス** に追加されます。 または、.vsix ファイルを [Visual Studio Marketplace](https://marketplace.visualstudio.com/) Web サイトにアップロードして、ユーザーが [ツール]、[ **拡張機能と更新プログラム** ] ダイアログを参照して検索できるようにすることもできます。  
  
## <a name="see-also"></a>参照  
 [ツールボックスの拡張](../misc/extending-the-toolbox.md)   
 [WPF ツールボックスコントロールの作成](../extensibility/creating-a-wpf-toolbox-control.md)   
 [Visual Studio のその他の部分の拡張](../extensibility/extending-other-parts-of-visual-studio.md)   
 [Windows フォーム コントロール開発の基本概念](https://msdn.microsoft.com/library/6277bb81-90f7-4c5b-9f4b-b02bb42dd316)
