---
title: プロパティウィンドウへのプロパティの公開 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- properties [Visual Studio SDK], exposing in Property Browser
- properties [Visual Studio SDK]
- Property Browser, exposing properties
ms.assetid: 47f295b5-1ca5-4e7b-bb52-7b926b136622
caps.latest.revision: 37
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c28a0520680951920ee19e91f3df098066f432dd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841460"
---
# <a name="exposing-properties-to-the-properties-window"></a>プロパティ ウィンドウへのプロパティの公開
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、オブジェクトのパブリックプロパティを [ **プロパティ** ] ウィンドウに公開します。 これらのプロパティに加えた変更は、[ **プロパティ** ] ウィンドウに反映されます。  
  
## <a name="prerequisites"></a>前提条件  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
## <a name="exposing-properties-to-the-properties-window"></a>プロパティ ウィンドウへのプロパティの公開  
 このセクションでは、カスタムツールウィンドウを作成し、[ **プロパティ** ] ウィンドウで、関連付けられているウィンドウペインオブジェクトのパブリックプロパティを表示します。  
  
#### <a name="to-expose-properties-to-the-properties-window"></a>プロパティをプロパティウィンドウに公開するには  
  
1. すべての Visual Studio 拡張機能は、拡張機能アセットを含む VSIX デプロイプロジェクトから開始されます。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]という名前の VSIX プロジェクトを作成 `MyObjectPropertiesExtension` します。 VSIX プロジェクトテンプレートは、[ **新しいプロジェクト** ] ダイアログボックスの [ **Visual C#]/[拡張機能**] で見つけることができます。  
  
2. という名前のカスタムツールウィンドウ項目テンプレートを追加して、ツールウィンドウを追加し `MyToolWindow` ます。 **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[追加]、[**新しい項目**] の順に選択します。 [ **新しい項目の追加] ダイアログ**で、[ **Visual C# の項目/機能拡張** ] にアクセスし、[ **カスタムツールウィンドウ**] を選択します。 ダイアログの下部にある [ **名前** ] フィールドで、ファイル名をに変更 `MyToolWindow.cs` します。 カスタムツールウィンドウを作成する方法の詳細については、「 [ツールウィンドウを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」を参照してください。  
  
3. MyToolWindow.cs を開き、次の using ステートメントを追加します。  
  
    ```  
    using System.Collections;  
    using System.ComponentModel;  
    using Microsoft.VisualStudio.Shell.Interop;  
    ```  
  
4. ここで、クラスに次のフィールドを追加し `MyToolWindow` ます。  
  
    ```csharp  
    private ITrackSelection trackSel;  
    private SelectionContainer selContainer;  
  
    ```  
  
5. MyToolWindow クラスに次のコードを追加します。  
  
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
  
    public void UpdateSelection()  
    {  
        ITrackSelection track = TrackSelection;  
        if (track != null)  
            track.OnSelectChange((ISelectionContainer)selContainer);  
    }  
  
    public void SelectList(ArrayList list)  
    {  
        selContainer = new SelectionContainer(true, false);  
        selContainer.SelectableObjects = list;  
        selContainer.SelectedObjects = list;  
        UpdateSelection();  
    }  
  
    public override void OnToolWindowCreated()  
    {  
        ArrayList listObjects = new ArrayList();  
        listObjects.Add(this);  
        SelectList(listObjects);  
    }  
    ```  
  
     `TrackSelection`プロパティはを使用して `GetService` `STrackSelection` サービスを取得します。これは、インターフェイスを提供 <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> します。 `OnToolWindowCreated`イベントハンドラーとメソッドを一緒に使うと、 `SelectList` ツールウィンドウペインのオブジェクト自体だけを含む選択したオブジェクトの一覧が作成されます。 メソッドは、[ `UpdateSelection` **プロパティ** ] ウィンドウに、ツールウィンドウペインのパブリックプロパティを表示するように指示します。  
  
6. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。  
  
7. [ **プロパティ** ] ウィンドウが表示されていない場合は、F4 キーを押して開きます。  
  
8. **MyToolWindow**ウィンドウを開きます。 これは、[ **表示]/[その他のウィンドウ**] で見つけることができます。  
  
     ウィンドウが開き、[ **プロパティ** ] ウィンドウにウィンドウペインのパブリックプロパティが表示されます。  
  
9. [**プロパティ**] ウィンドウの [**キャプション**] プロパティを **[マイオブジェクトのプロパティ**] に変更します。  
  
     MyToolWindow ウィンドウのキャプションが適宜変更されます。  
  
## <a name="exposing-tool-window-properties"></a>公開 (ツールウィンドウのプロパティを)  
 このセクションでは、ツールウィンドウを追加し、そのプロパティを公開します。 プロパティに対して行った変更は、[ **プロパティ** ] ウィンドウに反映されます。  
  
#### <a name="to-expose-tool-window-properties"></a>ツールウィンドウのプロパティを公開するには  
  
1. MyToolWindow.cs を開き、MyToolWindow クラスに IsChecked というパブリックブール型プロパティを追加します。  
  
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
  
     このプロパティは、後で作成する WPF チェックボックスから状態を取得します。  
  
2. MyToolWindowControl.xaml.cs を開き、MyToolWindowControl コンストラクターを次のコードに置き換えます。  
  
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
  
3. MyToolWindow.cs で、次の `MyToolWindow` ようにコンストラクターを変更します。  
  
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
  
     [ **プロパティ** ] ウィンドウで、ウィンドウのプロパティを探します。 **Ischecked**プロパティは、ウィンドウの下部の [ **My Properties** ] カテゴリの下に表示されます。  
  
10. [ **MyToolWindow** ] ウィンドウのチェックボックスをオンにします。 [**プロパティ**] ウィンドウの**Ischecked**が**True**に変更されます。 **MyToolWindow**ウィンドウのチェックボックスをオフにします。 [**プロパティ**] ウィンドウの**Ischecked**が**False**に変更されます。 [**プロパティ**] ウィンドウの [ **ischecked** ] の値を変更します。 [ **MyToolWindow** ] ウィンドウのチェックボックスは、新しい値と一致するように変更されます。  
  
    > [!NOTE]
    > [ **プロパティ** ] ウィンドウに表示されるオブジェクトを破棄する必要がある場合は、 `OnSelectChange` まず選択コンテナーを使用してを呼び出し `null` ます。 プロパティまたはオブジェクトを破棄した後は、更新された一覧とリストがある選択コンテナーに変更でき <xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectableObjects%2A> <xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectedObjects%2A> ます。  
  
## <a name="changing-selection-lists"></a>選択リストの変更  
 このセクションでは、基本プロパティクラスの選択リストを追加し、ツールウィンドウインターフェイスを使用して、表示する選択リストを選択します。  
  
#### <a name="to-change-selection-lists"></a>選択リストを変更するには  
  
1. MyToolWindow.cs を開き、という名前のパブリッククラスを追加し `Simple` ます。  
  
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
  
2. SimpleObject プロパティを MyToolWindow クラスに追加し、2つのメソッドを追加して、ウィンドウペインとオブジェクトの間で [ **プロパティ** ] ウィンドウの選択を切り替え `Simple` ます。  
  
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
  
3. MyToolWindowControl.cs で、チェックボックスハンドラーを次のコード行に置き換えます。  
  
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
  
6. [ **MyToolWindow** ] ウィンドウのチェックボックスをオンにします。 [ **プロパティ** ] ウィンドウには、 `Simple` オブジェクトのプロパティ、 **テキスト** 、および **読み取り専用**が表示されます。 チェック ボックスをオフにする ウィンドウのパブリックプロパティが [ **プロパティ** ] ウィンドウに表示されます。  
  
    > [!NOTE]
    > **テキスト**の表示名は **[マイテキスト**] です。  
  
## <a name="best-practice"></a>推奨事項  
 このチュートリアルで <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> は、選択可能なオブジェクトコレクションと選択されたオブジェクトコレクションが同じコレクションであるように、が実装されています。 選択したオブジェクトのみが [プロパティブラウザー] の一覧に表示されます。 ISelectionContainer の実装の詳細については、ToolWindow のサンプルを参照してください。  
  
 Visual Studio のツールウィンドウは、Visual Studio セッション間で保持します。 ツールウィンドウの状態の保持の詳細については、「」を参照してください <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 。  
  
## <a name="see-also"></a>参照  
 [プロパティとプロパティ ウィンドウの拡張](../extensibility/extending-properties-and-the-property-window.md)
