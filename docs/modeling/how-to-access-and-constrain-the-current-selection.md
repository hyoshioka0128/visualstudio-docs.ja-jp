---
title: '方法: 現在の選択項目を表示および制限する'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Domain-Specific Language, accessing the current selection
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b1f5aaa106e00f9b10eb88892bcc978b92a01c79
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545692"
---
# <a name="how-to-access-and-constrain-the-current-selection"></a>方法: 現在の選択項目を表示および制限する

ドメイン固有言語のコマンドまたはジェスチャハンドラーを記述する場合は、ユーザーが右クリックした要素を確認できます。 また、一部の図形またはフィールドが選択されないようにすることもできます。 たとえば、ユーザーがアイコンデコレータをクリックしたときに、そのアイコンが含まれている図形が選択されていることを示すことができます。 この方法で選択を制限すると、記述する必要があるハンドラーの数が減ります。 また、デコレータを避けなくても、図形内の任意の場所をクリックできるようになります。

## <a name="access-the-current-selection-from-a-command-handler"></a>コマンドハンドラーから現在の選択項目にアクセスする

ドメイン固有言語のコマンドセットクラスには、カスタムコマンドのコマンドハンドラーが含まれています。 <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>ドメイン固有言語のコマンドセットクラスが派生するクラスは、現在の選択項目にアクセスするためのいくつかのメンバーを提供します。

コマンドハンドラーでは、コマンドに応じて、モデルデザイナー、モデルエクスプローラー、またはアクティブウィンドウでの選択が必要になる場合があります。

### <a name="to-access-selection-information"></a>選択情報にアクセスするには

1. クラスは、 <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> 現在の選択にアクセスするために使用できる次のメンバーを定義します。

    |メンバー|説明|
    |-|-|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsAnyDocumentSelectionCompartment%2A> メソッド|`true`モデルデザイナーで選択されているいずれかの要素がコンパートメントシェイプの場合はを返します。それ以外の場合はを返します `false` 。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsDiagramSelected%2A> メソッド|`true`モデルデザイナーでダイアグラムが選択されている場合はを返します。それ以外の場合はを返します `false` 。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsSingleDocumentSelection%2A> メソッド|`true`モデルデザイナーで要素が1つだけ選択されている場合はを返します。それ以外の場合はを返します `false` 。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsSingleSelection%2A> メソッド|`true`アクティブウィンドウで要素が1つだけ選択されている場合はを返します。それ以外の場合はを返します `false` 。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.CurrentDocumentSelection%2A> プロパティ|モデルデザイナーで選択されている要素の読み取り専用のコレクションを取得します。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.CurrentSelection%2A> プロパティ|アクティブウィンドウで選択されている要素の読み取り専用のコレクションを取得します。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.SingleDocumentSelection%2A> プロパティ|モデルデザイナーで選択のプライマリ要素を取得します。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.SingleSelection%2A> プロパティ|アクティブウィンドウ内の選択範囲のプライマリ要素を取得します。|

2. <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet.CurrentDocView%2A>クラスのプロパティは、 <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> モデルデザイナーウィンドウを表すオブジェクトへのアクセスを提供 <xref:Microsoft.VisualStudio.Modeling.Shell.DiagramDocView> し、モデルデザイナーで選択した要素に追加のアクセスを提供します。

3. さらに、生成されたコードでは、ドメイン固有言語用のコマンドセットクラスにエクスプローラーツールウィンドウプロパティとエクスプローラー選択プロパティが定義されています。

    - エクスプローラーのツールウィンドウプロパティは、ドメイン固有言語のエクスプローラーツールウィンドウクラスのインスタンスを返します。 エクスプローラーツールウィンドウクラスはクラスから派生 <xref:Microsoft.VisualStudio.Modeling.Shell.ModelExplorerToolWindow> し、ドメイン固有言語のモデルエクスプローラーを表します。

    - プロパティは、 `ExplorerSelection` ドメイン固有言語の [モデルエクスプローラー] ウィンドウで選択されている要素を返します。

## <a name="determine-which-window-is-active"></a>アクティブなウィンドウを確認する

インターフェイスには、 <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService> シェルの現在の選択状態へのアクセスを提供するメンバーが定義されています。 <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService> `MonitorSelection` 各の基本クラスで定義されているプロパティを使用して、ドメイン固有言語のパッケージクラスまたはコマンドセットクラスからオブジェクトを取得できます。 パッケージクラスはクラスから派生 <xref:Microsoft.VisualStudio.Modeling.Shell.ModelingPackage> し、コマンドセットクラスはクラスから派生し <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> ます。

### <a name="to-determine-from-a-command-handler-what-type-of-window-is-active"></a>コマンドハンドラーから、どの種類のウィンドウがアクティブであるかを判断するには

1. <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.MonitorSelection%2A>クラスのプロパティは、 <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> シェルの <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService> 現在の選択状態へのアクセスを提供するオブジェクトを返します。

2. インターフェイスのプロパティは、アクティブな <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService.CurrentSelectionContainer%2A> <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService> 選択コンテナーを取得します。アクティブなウィンドウとは異なる場合があります。

3. 次のプロパティをドメイン固有言語のコマンドセットクラスに追加して、アクティブなウィンドウの種類を判別します。

    ```csharp
    // using Microsoft.VisualStudio.Modeling.Shell;

    // Returns true if the model designer is the active selection container;
    // otherwise, false.
    protected bool IsDesignerActive
    {
        get
        {
            return (this.MonitorSelection.CurrentSelectionContainer
                is DiagramDocView);
        }
    }

    // Returns true if the model explorer is the active selection container;
    // otherwise, false.
    protected bool IsExplorerActive
    {
        get
        {
            return (this.MonitorSelection.CurrentSelectionContainer
                is ModelExplorerToolWindow);
        }
    }
    ```

## <a name="constrain-the-selection"></a>選択範囲を制限する

選択規則を追加することにより、ユーザーがモデル内の要素を選択したときにどの要素を選択するかを制御できます。 たとえば、ユーザーが複数の要素を1つの単位として扱うことができるようにするには、選択ルールを使用します。

### <a name="to-create-a-selection-rule"></a>選択ルールを作成するには

1. DSL プロジェクトでカスタムコードファイルを作成する

2. クラスから派生した選択規則クラスを定義 <xref:Microsoft.VisualStudio.Modeling.Diagrams.DiagramSelectionRules> します。

3. 選択 <xref:Microsoft.VisualStudio.Modeling.Diagrams.DiagramSelectionRules.GetCompliantSelection%2A> 条件を適用するには、選択規則クラスのメソッドをオーバーライドします。

4. ClassDiagram クラスの部分クラス定義をカスタムコードファイルに追加します。

     クラスは、 `ClassDiagram` クラスから派生 <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram> し、DSL プロジェクトの生成されたコードファイル Diagram.cs で定義されます。

5. クラスのプロパティをオーバーライドして、 <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram.SelectionRules%2A> `ClassDiagram` カスタム選択規則を返します。

     プロパティの既定の実装では、選択を <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram.SelectionRules%2A> 変更しない選択ルールオブジェクトを取得します。

### <a name="example"></a>例

次のコードファイルは、選択範囲を拡張して、最初に選択された各ドメイン図形のすべてのインスタンスを含む選択規則を作成します。

```csharp
using System;
using System.Collections.Generic;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;

namespace CompanyName.ProductName.GroupingDsl
{
    public class CustomSelectionRules : DiagramSelectionRules
    {
        protected Diagram diagram;
        protected IElementDirectory elementDirectory;

        public CustomSelectionRules(Diagram diagram)
        {
            if (diagram == null) throw new ArgumentNullException();

            this.diagram = diagram;
            this.elementDirectory = diagram.Store.ElementDirectory;
        }

        /// <summary>Called by the design surface to allow selection filtering.
        /// </summary>
        /// <param name="currentSelection">[in] The current selection before any
        /// ShapeElements are added or removed.</param>
        /// <param name="proposedItemsToAdd">[in/out] The proposed DiagramItems to
        /// be added to the selection.</param>
        /// <param name="proposedItemsToRemove">[in/out] The proposed DiagramItems
        /// to be removed from the selection.</param>
        /// <param name="primaryItem">[in/out] The proposed DiagramItem to become
        /// the primary DiagramItem of the selection. A null value signifies that
        /// the last DiagramItem in the resultant selection should be assumed as
        /// the primary DiagramItem.</param>
        /// <returns>true if some or all of the selection was accepted; false if
        /// the entire selection proposal was rejected. If false, appropriate
        /// feedback will be given to the user to indicate that the selection was
        /// rejected.</returns>
        public override bool GetCompliantSelection(
            SelectedShapesCollection currentSelection,
            DiagramItemCollection proposedItemsToAdd,
            DiagramItemCollection proposedItemsToRemove,
            DiagramItem primaryItem)
        {
            if (currentSelection.Count == 0 && proposedItemsToAdd.Count == 0) return true;

            HashSet<DomainClassInfo> itemsToAdd = new HashSet<DomainClassInfo>();

            foreach (DiagramItem item in proposedItemsToAdd)
            {
                if (item.Shape != null)
                    itemsToAdd.Add(item.Shape.GetDomainClass());
            }
            proposedItemsToAdd.Clear();
            foreach (DomainClassInfo classInfo in itemsToAdd)
            {
                foreach (ModelElement element
                    in this.elementDirectory.FindElements(classInfo, false))
                {
                    if (element is ShapeElement)
                    {
                        proposedItemsToAdd.Add(
                            new DiagramItem((ShapeElement)element));
                    }
                }
            }

            return true;
        }
    }

    public partial class ClassDiagram
    {
        protected CustomSelectionRules customSelectionRules = null;

        protected bool multipleSelectionMode = true;

        public override DiagramSelectionRules SelectionRules
        {
            get
            {
                if (multipleSelectionMode)
                {
                    if (customSelectionRules == null)
                    {
                        customSelectionRules = new CustomSelectionRules(this);
                    }
                    return customSelectionRules;
                }
                else
                {
                    return base.SelectionRules;
                }
            }
        }
    }
}
```

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>
- <xref:Microsoft.VisualStudio.Modeling.Shell.ModelingPackage>
- <xref:Microsoft.VisualStudio.Modeling.Shell.DiagramDocView>
- <xref:Microsoft.VisualStudio.Modeling.Shell.ModelExplorerToolWindow>
- <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService>
- <xref:Microsoft.VisualStudio.Modeling.Diagrams.DiagramSelectionRules>
- <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram>