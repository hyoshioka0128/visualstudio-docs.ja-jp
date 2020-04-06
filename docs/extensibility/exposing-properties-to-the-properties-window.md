---
title: プロパティ ウィンドウへのプロパティの公開 |マイクロソフトドキュメント
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- properties [Visual Studio SDK], exposing in Property Browser
- properties [Visual Studio SDK]
- Property Browser, exposing properties
ms.assetid: 47f295b5-1ca5-4e7b-bb52-7b926b136622
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f84962628ae550676e2c2eeb10c0f3baeca1bb58
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711826"
---
# <a name="expose-properties-to-the-properties-window"></a>プロパティを [プロパティ] ウィンドウに公開する

このチュートリアルでは、オブジェクトのパブリック プロパティを **[プロパティ]** ウィンドウに公開します。 これらのプロパティに加えた変更は **、[プロパティ]** ウィンドウに反映されます。

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="expose-properties-to-the-properties-window"></a>プロパティを [プロパティ] ウィンドウに公開する

このセクションでは、カスタム ツール ウィンドウを作成し、関連付けられたウィンドウ ペイン オブジェクトのパブリック プロパティを **[プロパティ]** ウィンドウに表示します。

### <a name="to-expose-properties-to-the-properties-window"></a>プロパティを [プロパティ] ウィンドウに公開するには

1. すべての Visual Studio 拡張機能は、拡張機能の資産を含む VSIX 配置プロジェクトで開始します。 という名前[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]`MyObjectPropertiesExtension`の VSIX プロジェクトを作成します。 VSIX プロジェクト テンプレートは、"vsix" を検索して **[新しいプロジェクト**] ダイアログで見つけることができます。

2. という名前のカスタム ツール ウィンドウ項目テンプレートを追加して`MyToolWindow`、ツール ウィンドウを追加します。 ソリューション**エクスプローラ**で、プロジェクト ノードを右クリックし、[**Add** > **新しい項目**の追加] を選択します。 [**新しい項目の追加**] ダイアログ で **、[Visual C# アイテム** > **の機能拡張**] に移動し、[**カスタム ツール ウィンドウ**] を選択します。 ダイアログの下部にある [**名前]** フィールドで、ファイル名を *[MyToolWindow.cs*に変更します。 カスタム ツール ウィンドウを作成する方法の詳細については、「[ツール ウィンドウを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」を参照してください。

3. *MyToolWindow.cs*開き、次の using ステートメントを追加します。

   ```csharp
   using System.Collections;
   using System.ComponentModel;
   using Microsoft.VisualStudio.Shell.Interop;
   ```

4. 次のフィールドをクラスに`MyToolWindow`追加します。

   ```csharp
   private ITrackSelection trackSel;
   private SelectionContainer selContainer;

   ```

5. 次のコードを `MyToolWindow` クラスに追加します。

   ```csharp
   private ITrackSelection TrackSelection
   {
       get
       {
           if (trackSel == null)
               trackSel =
                  GetService(typeof(STrackSelection)) as ITrackSelection;
           return trackSel;
       }
   }

   public void UpdateSelection()
   {
       ITrackSelection track = TrackSelection;
       if (track != null)
           track.OnSelectChange((ISelectionContainer)selContainer);
   }

   public void SelectList(ArrayList list)
   {
       selContainer = new SelectionContainer(true, false);
       selContainer.SelectableObjects = list;
       selContainer.SelectedObjects = list;
       UpdateSelection();
   }

   public override void OnToolWindowCreated()
   {
       ArrayList listObjects = new ArrayList();
       listObjects.Add(this);
       SelectList(listObjects);
   }
   ```

    プロパティ`TrackSelection`は、`GetService`<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection>インターフェイスを提供`STrackSelection`するサービスを取得するために使用します。 イベント`OnToolWindowCreated`ハンドラーと`SelectList`メソッドを組み合わせて、ツール ウィンドウ ウィンドウ オブジェクト自体のみを含む選択したオブジェクトのリストを作成します。 この`UpdateSelection`メソッドは、ツール ウィンドウ ペインのパブリック プロパティを表示するように **[プロパティ]** ウィンドウに指示します。

6. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。

7. **[プロパティ]** ウィンドウが表示されていない場合は **、F4**キーを押して開きます。

8. **[マイツール ウィンドウ] ウィンドウを**開きます。 このウィンドウは、**他のウィンドウ**の**表示** > で確認できます。

    ウィンドウが開き、ウィンドウ ペインのパブリック プロパティが **[プロパティ]** ウィンドウに表示されます。

9. プロパティ ウィンドウの **[キャプション]** **プロパティ**を **[マイ オブジェクトのプロパティ]** に変更します。

     MyToolWindow ウィンドウのキャプションは、それに応じて変更されます。

## <a name="expose-tool-window-properties"></a>ツール ウィンドウのプロパティを公開する

このセクションでは、ツール ウィンドウを追加し、そのプロパティを公開します。 プロパティに加えた変更は **、[プロパティ]** ウィンドウに反映されます。

### <a name="to-expose-tool-window-properties"></a>ツール ウィンドウのプロパティを公開するには

1. *MyToolWindow.cs*を開き、クラスにパブリックブールプロパティ IsChecked`MyToolWindow`を追加します。

    ```csharp
    [Category("My Properties")]
    [Description("MyToolWindowControl properties")]
    public bool IsChecked
    {
        get {
            if (base.Content == null)  return false;
            return (bool)(( MyToolWindowControl) base.Content).checkBox.IsChecked;
        }
        set {
            ((MyToolWindowControl) base.Content).checkBox.IsChecked = value;
        }
    }
    ```

     このプロパティは、後で作成する WPF のチェック ボックスからその状態を取得します。

2. *MyToolWindowControl.xaml.cs*開き、MyToolWindowControl コンストラクターを次のコードに置き換えます。

    ```vb
    private MyToolWindow pane;
    public MyToolWindowControl(MyToolWindow pane)
    {
        InitializeComponent();
        this.pane = pane;
        checkBox.IsChecked = false;
    }
    ```

     これにより、`MyToolWindowControl``MyToolWindow`ペインにアクセスできます。

3. *MyToolWindow.cs*で、次のように`MyToolWindow`コンストラクタを変更します。

    ```csharp
    base.Content = new MyToolWindowControl(this);
    ```

4. コントロールのデザイン ビューに変更します。

5. ボタンを削除し、**ツールボックス**から左上隅にチェック ボックスを追加します。

6. [チェック済み] イベントと [未チェック] イベントを追加します。 デザインビューでチェックボックスを選択します。 **[プロパティ]** ウィンドウで、イベント ハンドラー ボタン (**プロパティ**ウィンドウの右上) をクリックします。 [**検索] チェック ボックス**をオンにしてテキスト ボックスに**checkbox_Checked**と入力し、[**オフ] を**見つけて、テキスト ボックスに **「checkbox_Unchecked」** と入力します。

7. チェック ボックスイベント ハンドラを追加します。

    ```csharp
    private void checkbox_Checked(object sender, RoutedEventArgs e)
    {
        pane.IsChecked = true;
        pane.UpdateSelection();
    }
    private void checkbox_Unchecked(object sender, RoutedEventArgs e)
    {
        pane.IsChecked = false;
        pane.UpdateSelection();
    }
    ```

8. プロジェクトをビルドし、デバッグを開始します。

9. 実験用インスタンスで **、MyToolWindow ウィンドウ**を開きます。

     [プロパティ] ウィンドウで、ウィンドウのプロパティを**探**します。 **IsChecked**プロパティは、ウィンドウの下部にある **[マイ プロパティ]** カテゴリに表示されます。

10. [**マイツール ウィンドウ**] ウィンドウのチェック ボックスをオンにします。 **[プロパティ]** ウィンドウで **[チェック]** が **[True]** に変わります。 [**マイツール ウィンドウ**] ウィンドウのチェック ボックスをオフにします。 **[プロパティ]** ウィンドウで **[チェック]** が **[False]** に変わります。 **[プロパティ**] ウィンドウで **[IsChecked]** の値を変更します。 **MyToolWindow**ウィンドウのチェック ボックスが、新しい値に一致するように変更されます。

    > [!NOTE]
    > **[プロパティ]** ウィンドウに表示されるオブジェクトを破棄する必要がある場合は`OnSelectChange`、最初`null`に選択コンテナーを呼び出します。 プロパティまたはオブジェクトを破棄した後、更新<xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectableObjects%2A>および<xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectedObjects%2A>リストが含まれる選択コンテナに変更できます。

## <a name="change-selection-lists"></a>選択リストの変更

 このセクションでは、基本的なプロパティ クラスの選択リストを追加し、ツール ウィンドウ インターフェイスを使用して、表示する選択リストを選択します。

### <a name="to-change-selection-lists"></a>選択リストを変更するには

1. *MyToolWindow.cs*を開き、 という名前`Simple`のパブリック クラスを追加します。

    ```csharp
    public class Simple
    {
        private string someText = "";

        [Category("My Properties")]
        [Description("Simple Properties")]
        [DisplayName("My Text")]
        public string SomeText
        {
            get { return someText; }
            set { someText = value; }
        }

        [Category("My Properties")]
        [Description("Read-only property")]
        public bool ReadOnly
        {
            get { return false; }
        }
    }
    ```

2. クラスに`SimpleObject`プロパティを`MyToolWindow`追加し、ウィンドウ ペインとオブジェクトの間で **[プロパティ]** ウィンドウの`Simple`選択を切り替える 2 つのメソッドを追加します。

    ```csharp
    private Simple simpleObject = null;
    public Simple SimpleObject
    {
        get
        {
            if (simpleObject == null) simpleObject = new Simple();
            return simpleObject;
        }
    }

    public void SelectSimpleList()
    {
        ArrayList listObjects = new ArrayList();
        listObjects.Add(SimpleObject);
        SelectList(listObjects);
    }

    public void SelectThisList()
    {
        ArrayList listObjects = new ArrayList();
        listObjects.Add(this);
        SelectList(listObjects);
    }
    ```

3. *MyToolWindowControl.cs*で、チェック ボックス ハンドラを次のコード行に置き換えます。

    ```csharp
    private void checkbox_Checked(object sender, RoutedEventArgs e)
     {
        pane.IsChecked = true;
        pane.SelectSimpleList();
        pane.UpdateSelection();
    }
    private void checkbox_Unchecked(object sender, RoutedEventArgs e)
    {
        pane.IsChecked = false;
        pane.SelectThisList();
        pane.UpdateSelection();
    }
    ```

4. プロジェクトをビルドし、デバッグを開始します。

5. 実験用インスタンスで **、MyToolWindow ウィンドウ**を開きます。

6. [**マイツール ウィンドウ**] ウィンドウのチェック ボックスをオンにします。 **[プロパティ]** ウィンドウ`Simple`には、オブジェクトのプロパティ**である SomeText**および**ReadOnly**が表示されます。 チェック ボックスをオフにします。 ウィンドウのパブリック プロパティが **[プロパティ]** ウィンドウに表示されます。

    > [!NOTE]
    > **SomeText**の表示名は **、マイ テキスト です**。

## <a name="best-practice"></a>ベスト プラクティス

このチュートリアルでは、<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>選択可能なオブジェクト コレクションと選択したオブジェクト コレクションが同じコレクションになるように実装されています。 選択したオブジェクトのみが[プロパティ ブラウザ]リストに表示されます。 より完全な ISelectionContainer 実装については、参照.ToolWindow サンプルを参照してください。

Visual Studio のツール ウィンドウは、Visual Studio セッション間で保持されます。 ツール ウィンドウの状態を永続化する方法の詳細については<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>、を参照してください。

## <a name="see-also"></a>関連項目

- [プロパティとプロパティ ウィンドウを拡張する](../extensibility/extending-properties-and-the-property-window.md)
