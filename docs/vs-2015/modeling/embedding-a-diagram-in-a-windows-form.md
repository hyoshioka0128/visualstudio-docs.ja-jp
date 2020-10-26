---
title: Windows フォームでのダイアグラムの埋め込み |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: fa6cd040-7c88-4329-b9c3-2a80b312610f
caps.latest.revision: 3
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 487105350fe5c62a9451bccc5713c6506c76bf1f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72669703"
---
# <a name="embedding-a-diagram-in-a-windows-form"></a>Windows フォームでのダイアグラムの埋め込み
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows コントロールに DSL 図を埋め込むことができます。これは、ウィンドウに表示され [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。

## <a name="embedding-a-diagram"></a>ダイアグラムの埋め込み

#### <a name="to-embed-a-dsl-diagram-in-a-windows-control"></a>Windows コントロールに DSL 図を埋め込むには

1. 新しい **ユーザーコントロール** ファイルを DslPackage プロジェクトに追加します。

2. パネルコントロールをユーザーコントロールに追加します。 このパネルには DSL の図が表示されます。

     必要なその他のコントロールを追加します。

     コントロールのアンカープロパティを設定します。

3. ソリューションエクスプローラーで、ユーザーコントロールファイルを右クリックし、[ **コードの表示**] をクリックします。 次のコンストラクターと変数をコードに追加します。

    ```csharp

    internal UserControl1(MyDSLDocView docView, Control content)
      : this()
    {
      panel1.Controls.Add(content);
      this.docView = docView;
    }
    private MyDSLDSLDocView docView;

    ```

4. 次の内容を使用して、DslPackage プロジェクトに新しいファイルを追加します。

    ```
    using System.Windows.Forms;
    namespace Company.MyDSL
    {
      partial class MyDSLDocView
      {
        private UserControl1 container;
        public override IWin32Window Window
        {
          get
          {
            if (container == null)
            {
              // Put our own form inside the DSL window:
              container = new UserControl1(this,
                (Control)base.Window);
            }
            return container;
    } } } }

    ```

5. DSL をテストするには、F5 キーを押してサンプルモデルファイルを開きます。 この図はコントロール内に表示されます。 ツールボックスとその他の機能は正常に動作します。

#### <a name="updating-the-form-using-store-events"></a>ストアイベントを使用したフォームの更新

1. フォームデザイナーで、という名前の **リストボックス** を追加 `listBox1` します。 これにより、モデル内の要素の一覧が表示されます。 このモデルは、 *ストアイベント*を使用してモデルと共に synchronism に保持されます。 詳細については、「 [イベントハンドラーによって変更がモデル外に反映される](../modeling/event-handlers-propagate-changes-outside-the-model.md)」を参照してください。

2. カスタムコードファイルで、DocView クラスにさらにメソッドをオーバーライドします。

    ```

    partial class MyDSLDocView
    {
     /// <summary>
     /// Register store event listeners.
     /// This method is called when the model and diagram
     /// have completed loading.
     /// </summary>
     protected override bool LoadView()
      {
        bool result = base.LoadView();
        Store store = this.DocData.Store;
        EventManagerDirectory emd = store.EventManagerDirectory;
        DomainClassInfo componentClass = store.DomainDataDirectory.FindDomainClass(typeof(ExampleElement));
        emd.ElementAdded.Add(componentClass, new EventHandler<ElementAddedEventArgs>(AddElement));
        emd.ElementDeleted.Add(componentClass, new EventHandler<ElementDeletedEventArgs>(RemoveElement));

        // Do the initial parts list:
        container.SetUpFormFromModel();
        return result;
      }
     /// <summary>
     /// Listener method called on creation of each instance of
     /// the ExampleElement class or its subclasses.
     /// </summary>
     private void AddElement(object sender, ElementAddedEventArgs e)
     {
       container.Add(e.ModelElement as ExampleElement);
     }
     /// <summary>
     /// Listener method called after deletion of each instance of
     /// the ExampleElement class or its subclasses.
     /// </summary>
     private void RemoveElement(object sender, ElementDeletedEventArgs e)
     {
       container.Remove(e.ModelElement as ExampleElement);
     }

    ```

3. ユーザーコントロールの背後にあるコードで、追加および削除された要素をリッスンするメソッドを挿入します。

    ```

          public partial class UserControl1 : UserControl { ...

    private ExampleModel modelRoot;

    internal void Add(ExampleElement e) { UpdatePartsList(); }
    internal void Remove(ExampleElement e) { UpdatePartsList(); }

    internal void SetUpFormFromModel()
    {
      modelRoot = this.docView.CurrentDiagram.ModelElement as ExampleModel;
      UpdatePartsList();
    }

    private void UpdatePartsList()
    {
      StringBuilder builder = new StringBuilder();
      listBox1.Items.Clear();
      foreach (ExampleElement c in modelRoot.Elements)
      {
        listBox1.Items.Add(c.Name);
      }
    }

    ```

4. DSL をテストするには、F5 キーを押し、の実験用インスタンスで [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] サンプルモデルファイルを開きます。

     リストボックスには、モデル内の要素の一覧が表示され、追加または削除した後、[元に戻す] と [やり直し] の後に適切であることがわかります。

## <a name="see-also"></a>参照
 [プログラムコード内のモデルの移動と更新コード](../modeling/navigating-and-updating-a-model-in-program-code.md)を記述して [ドメイン固有言語をカスタマイズする](../modeling/writing-code-to-customise-a-domain-specific-language.md)
