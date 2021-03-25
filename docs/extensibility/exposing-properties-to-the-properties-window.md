---
title: プロパティウィンドウへのプロパティの公開 |Microsoft Docs
description: オブジェクトのパブリックプロパティについて説明します。 これらのプロパティに加えた変更は、プロパティウィンドウに反映されます。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- properties [Visual Studio SDK], exposing in Property Browser
- properties [Visual Studio SDK]
- Property Browser, exposing properties
ms.assetid: 47f295b5-1ca5-4e7b-bb52-7b926b136622
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b9de86e956fe6a4d7841d519d7252b75ae216229
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075251"
---
# <a name="expose-properties-to-the-properties-window"></a>プロパティをプロパティウィンドウに公開する

このチュートリアルでは、オブジェクトのパブリックプロパティを [ **プロパティ** ] ウィンドウに公開します。 これらのプロパティに加えた変更は、[ **プロパティ** ] ウィンドウに反映されます。

## <a name="prerequisites"></a>前提条件

Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="expose-properties-to-the-properties-window"></a>プロパティをプロパティウィンドウに公開する

このセクションでは、カスタムツールウィンドウを作成し、[ **プロパティ** ] ウィンドウで、関連付けられているウィンドウペインオブジェクトのパブリックプロパティを表示します。

### <a name="to-expose-properties-to-the-properties-window"></a>プロパティをプロパティウィンドウに公開するには

1. すべての Visual Studio 拡張機能は、拡張機能アセットを含む VSIX デプロイプロジェクトから開始されます。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]という名前の VSIX プロジェクトを作成 `MyObjectPropertiesExtension` します。 VSIX プロジェクトテンプレートは、"vsix" を検索することで、[ **新しいプロジェクト** ] ダイアログで見つけることができます。

2. という名前のカスタムツールウィンドウ項目テンプレートを追加して、ツールウィンドウを追加し `MyToolWindow` ます。 **ソリューションエクスプローラー** で、プロジェクトノードを右クリックし、[新しい項目の **追加**] を選択し  >  ます。 [**新しい項目の追加] ダイアログ** で、[ **Visual C# 項目** の機能拡張] にアクセスし、  >   [**カスタムツールウィンドウ**] を選択します。 ダイアログの下部にある [ **名前** ] フィールドで、ファイル名を *MyToolWindow* に変更します。 カスタムツールウィンドウを作成する方法の詳細については、「 [ツールウィンドウで拡張機能を作成](../extensibility/creating-an-extension-with-a-tool-window.md)する」を参照してください。

3. *MyToolWindow* を開き、次の using ステートメントを追加します。

   ```csharp
   using System.Collections;
   using System.ComponentModel;
   using Microsoft.VisualStudio.Shell.Interop;
   ```

4. ここで、クラスに次のフィールドを追加し `MyToolWindow` ます。

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

    `TrackSelection`プロパティはを使用して `GetService` `STrackSelection` サービスを取得します。これは、インターフェイスを提供 <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> します。 `OnToolWindowCreated`イベントハンドラーとメソッドを一緒に使うと、 `SelectList` ツールウィンドウペインのオブジェクト自体だけを含む選択したオブジェクトの一覧が作成されます。 メソッドは、[ `UpdateSelection` **プロパティ** ] ウィンドウに、ツールウィンドウペインのパブリックプロパティを表示するように指示します。

6. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。

7. [ **プロパティ** ] ウィンドウが表示されていない場合は、 **F4** キーを押して開きます。

8. **MyToolWindow** ウィンドウを開きます。 [   >  **その他のウィンドウ** を表示] で見つけることができます。

    ウィンドウが開き、[ **プロパティ** ] ウィンドウにウィンドウペインのパブリックプロパティが表示されます。

9. [**プロパティ**] ウィンドウの [**キャプション**] プロパティを **[マイオブジェクトのプロパティ**] に変更します。

     MyToolWindow ウィンドウのキャプションが適宜変更されます。

## <a name="expose-tool-window-properties"></a>ツールウィンドウのプロパティを公開する

このセクションでは、ツールウィンドウを追加し、そのプロパティを公開します。 プロパティに対して行った変更は、[ **プロパティ** ] ウィンドウに反映されます。

### <a name="to-expose-tool-window-properties"></a>ツールウィンドウのプロパティを公開するには

1. *MyToolWindow* を開き、パブリックブール型プロパティ ischecked をクラスに追加します `MyToolWindow` 。

    ```csharp
    [Category("My Properties")]
    [Description("MyToolWindowControl properties")]
    public bool IsChecked
    {
        get {
            if (base.Content == null)  return false;
            return (bool)(( MyToolWindowControl) base.Content).checkBox.IsChecked;
        }
        set {
            ((MyToolWindowControl) base.Content).checkBox.IsChecked = value;
        }
    }
    ```

     このプロパティは、後で作成する WPF チェックボックスから状態を取得します。

2. *Mytoolwindowcontrol .xaml* を開き、mytoolwindowcontrol コンストラクターを次のコードに置き換えます。

    ```vb
    private MyToolWindow pane;
    public MyToolWindowControl(MyToolWindow pane)
    {
        InitializeComponent();
        this.pane = pane;
        checkBox.IsChecked = false;
    }
    ```

     これ `MyToolWindowControl` により、ペインにアクセスできるように `MyToolWindow` なります。

3. *MyToolWindow* で、次のように `MyToolWindow` コンストラクターを変更します。

    ```csharp
    base.Content = new MyToolWindowControl(this);
    ```

4. MyToolWindowControl のデザインビューに変更します。

5. ボタンを削除し、 **ツールボックス** から左上隅にチェックボックスを追加します。

6. Checked イベントと Unchecked イベントを追加します。 デザインビューでチェックボックスをオンにします。 [ **プロパティ** ] ウィンドウで、[イベントハンドラー] ボタン ([ **プロパティ** ] ウィンドウの右上) をクリックします。 チェックボックスを **オン** にして、テキストボックスに **checkbox_Checked** を入力し、[ **Unchecked** ] を見つけて、テキストボックスに「 **checkbox_Unchecked** 」と入力します。

7. チェックボックスのイベントハンドラーを追加します。

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

9. 実験用インスタンスで、[ **MyToolWindow** ] ウィンドウを開きます。

     [ **プロパティ** ] ウィンドウで、ウィンドウのプロパティを探します。 **Ischecked** プロパティは、ウィンドウの下部の [ **My Properties** ] カテゴリの下に表示されます。

10. [ **MyToolWindow** ] ウィンドウのチェックボックスをオンにします。 [**プロパティ**] ウィンドウの **Ischecked** が **True** に変更されます。 **MyToolWindow** ウィンドウのチェックボックスをオフにします。 [**プロパティ**] ウィンドウの **Ischecked** が **False** に変更されます。 [**プロパティ**] ウィンドウの [ **ischecked** ] の値を変更します。 [ **MyToolWindow** ] ウィンドウのチェックボックスは、新しい値と一致するように変更されます。

    > [!NOTE]
    > [ **プロパティ** ] ウィンドウに表示されるオブジェクトを破棄する必要がある場合は、 `OnSelectChange` まず選択コンテナーを使用してを呼び出し `null` ます。 プロパティまたはオブジェクトを破棄した後は、更新された一覧とリストがある選択コンテナーに変更でき <xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectableObjects%2A> <xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectedObjects%2A> ます。

## <a name="change-selection-lists"></a>選択リストの変更

 このセクションでは、基本プロパティクラスの選択リストを追加し、ツールウィンドウインターフェイスを使用して、表示する選択リストを選択します。

### <a name="to-change-selection-lists"></a>選択リストを変更するには

1. *MyToolWindow* を開き、という名前のパブリッククラスを追加し `Simple` ます。

    ```csharp
    public class Simple
    {
        private string someText = "";

        [Category("My Properties")]
        [Description("Simple Properties")]
        [DisplayName("My Text")]
        public string SomeText
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

2. クラスにプロパティを追加し、2つのメソッドを追加して、 `SimpleObject` `MyToolWindow` ウィンドウペインとオブジェクトの間で [ **プロパティ** ] ウィンドウの選択を切り替え `Simple` ます。

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

3. *Mytoolwindowcontrol .cs* で、チェックボックスハンドラーを次のコード行に置き換えます。

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

5. 実験用インスタンスで、[ **MyToolWindow** ] ウィンドウを開きます。

6. [ **MyToolWindow** ] ウィンドウのチェックボックスをオンにします。 [ **プロパティ** ] ウィンドウには、 `Simple` オブジェクトのプロパティ、 **テキスト** 、および **読み取り専用** が表示されます。 チェック ボックスをオフにする ウィンドウのパブリックプロパティが [ **プロパティ** ] ウィンドウに表示されます。

    > [!NOTE]
    > **テキスト** の表示名は **[マイテキスト**] です。

## <a name="best-practice"></a>ベスト プラクティス

このチュートリアルで <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> は、選択可能なオブジェクトコレクションと選択されたオブジェクトコレクションが同じコレクションであるように、が実装されています。 選択したオブジェクトのみが [プロパティブラウザー] の一覧に表示されます。 ISelectionContainer の実装の詳細については、ToolWindow のサンプルを参照してください。

Visual Studio のツールウィンドウは、Visual Studio セッション間で保持します。 ツールウィンドウの状態の保持の詳細については、「」を参照してください <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 。

## <a name="see-also"></a>こちらもご覧ください

- [プロパティとプロパティウィンドウの拡張](../extensibility/extending-properties-and-the-property-window.md)
