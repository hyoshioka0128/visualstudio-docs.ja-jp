---
title: Define a gesture handler on a modeling diagram | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML - extending, double-click
- UML - extending, drag and drop
ms.assetid: e5e1d70a-3539-4321-a3b1-89e86e4d6430
caps.latest.revision: 36
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: bf749d1073faf4cf22febafce716af36b47c6484
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299309"
---
# <a name="define-a-gesture-handler-on-a-modeling-diagram"></a>モデリング図にジェスチャ ハンドラーを定義する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio では、ユーザーが UML 図の項目をダブルクリックまたはドラッグしたときに実行されるコマンドを定義できます。 これらの拡張機能を[VSIX](https://go.microsoft.com/fwlink/?LinkId=160780)(Visual Studio Integration Extension) にパッケージ化して、他の Visual Studio ユーザーに配布できます。

 図の種類およびドラッグする要素の種類に対応する組み込みの動作が既に用意されている場合は、この動作を追加またはオーバーライドできない可能性があります。

## <a name="requirements"></a>［要件］
 「 [要件](../modeling/extend-uml-models-and-diagrams.md#Requirements)」を参照してください。

 この機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

## <a name="creating-a-gesture-handler"></a>ジェスチャ ハンドラーの作成
 UML デザイナーのジェスチャ ハンドラーを定義するには、ジェスチャ ハンドラーの振る舞いを定義するクラスを生成し、そのクラスを Visual Studio Integration Extension (VSIX) に埋め込む必要があります。 VSIX は、ハンドラーをインストールできるコンテナーとして機能します。 ジェスチャ ハンドラーを定義する方法は 2 つあります。

- **Create a gesture handler in its own VSIX using a project template.** これはより簡単な方法です。 ハンドラーの他の種類の拡張機能 (検証拡張機能、カスタム ツールボックス項目、メニュー コマンドなど) と組み合わせない場合は、この方法を使用します。

- **Create separate gesture handler and VSIX projects.** 複数の種類の拡張機能を同じ VSIX に組み合わせる場合は、この方法を使用します。 たとえば、ジェスチャ ハンドラーが特定の制約に従うモデルを必要とする場合は、そのモデルを検証メソッドとして同じ VSIX に埋め込むことができます。

#### <a name="to-create-a-gesture-handler-in-its-own-vsix"></a>ジェスチャ ハンドラーを独自の VSIX に生成するには

1. **[新しいプロジェクト]** ダイアログ ボックスの **[モデリング プロジェクト]** で、 **[ジェスチャ拡張機能]** をクリックします。

2. 新しいプロジェクトで **.cs** ファイルを開き、 `GestureExtension` クラスを変更してジェスチャ ハンドラーを実装します。

    詳細については、「 [ジェスチャ ハンドラーの実装](#Implementing)」を参照してください。

3. F5 キーを押してジェスチャ ハンドラーをテストします。 詳細については、「 [ジェスチャ ハンドラーの実行](#Executing)」を参照してください。

4. Install the gesture handler on another computer by copying the file **bin\\\*\\\*.vsix** that is built by your project. 詳細については、「 [拡張機能のインストールとアンインストール](#Installing)」を参照してください。

   次の手順も使用できます。

#### <a name="to-create-a-separate-class-library-dll-project-for-the-gesture-handler"></a>ジェスチャ ハンドラー用に別のクラス ライブラリ (DLL) プロジェクトを作成するには

1. 新規の [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューションまたは既存のソリューションにクラス ライブラリ プロジェクトを作成します。

   1. **[ファイル]** メニューで、 **[新規]** 、 **[プロジェクト]** をクリックします。

   2. **[インストールされたテンプレート]** の **[Visual C#]** または **[Visual Basic]** を展開し、中央の列で、 **[クラス ライブラリ]** をクリックします。

2. 以下の参照をプロジェクトに追加します。

    `Microsoft.VisualStudio.Modeling.Sdk.[version]`

    `Microsoft.VisualStudio.Modeling.Sdk.Diagrams.[version]`

    `Microsoft.VisualStudio.ArchitectureTools.Extensibility`

    `Microsoft.VisualStudio.Uml.Interfaces`

    `System.ComponentModel.Composition`

    `System.Windows.Forms`

    `Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer` – レイヤー図を拡張する場合にのみ必要になります。 For more information, see [Extend layer diagrams](../modeling/extend-layer-diagrams.md).

3. プロジェクトにクラス ファイルを追加し、その内容を次のコードに設定します。

   > [!NOTE]
   > 名前空間およびクラスの名前は必要に応じて変更してください。

   ```
   using System.ComponentModel.Composition;
   using System.Linq;
   using System.Collections.Generic;
   using Microsoft.VisualStudio.Modeling.Diagrams;
   using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;
   using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
   using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
   using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
   using Microsoft.VisualStudio.Uml.AuxiliaryConstructs;
   using Microsoft.VisualStudio.Modeling;
   using Microsoft.VisualStudio.Uml.Classes;
   // ADD other UML namespaces if required

   namespace MyGestureHandler // CHANGE
   {
     // DELETE any of these attributes if the handler
     // should not work with some types of diagram.
     [ClassDesignerExtension]
     [ActivityDesignerExtension]
     [ComponentDesignerExtension]
     [SequenceDesignerExtension]
     [UseCaseDesignerExtension]
     // [LayerDesignerExtension]

     // Gesture handlers must export IGestureExtension:
     [Export(typeof(IGestureExtension))]
     // CHANGE class name
     public class MyGesture1 : IGestureExtension
     {
       [Import]
       public IDiagramContext DiagramContext { get; set; }

       /// <summary>
       /// Called when the user double-clicks on the diagram
       /// </summary>
       /// <param name="targetElement"></param>
       /// <param name="diagramPointEventArgs"></param>
       public void OnDoubleClick(ShapeElement targetElement, DiagramPointEventArgs diagramPointEventArgs)
       {
         // CHANGE THIS CODE FOR YOUR APPLICATION.

         // Get the target shape, if any. Null if the target is the diagram.
         IShape targetIShape = targetElement.CreateIShape();

         // Do something...
       }

       /// <summary>
       /// Called repeatedly when the user drags from anywhere on the screen.
       /// Return value should indicate whether a drop here is allowed.
       /// </summary>
       /// <param name="targetMergeElement">References the element to be dropped on.</param>
       /// <param name="diagramDragEventArgs">References the element to be dropped.</param>
       /// <returns></returns>
       public bool CanDragDrop(ShapeElement targetMergeElement, DiagramDragEventArgs diagramDragEventArgs)
       {
         // CHANGE THIS CODE FOR YOUR APPLICATION.

         // Get the target element, if any. Null if the target is the diagram.
         IShape targetIShape = targetMergeElement.CreateIShape();

         // This example allows drag of any UML elements.
         return GetModelElementsFromDragEvent(diagramDragEventArgs).Count() > 0;
       }

       /// <summary>
       /// Execute the action to be performed on the drop.
       /// </summary>
       /// <param name="targetDropElement"></param>
       /// <param name="diagramDragEventArgs"></param>
       public void OnDragDrop(ShapeElement targetDropElement, DiagramDragEventArgs diagramDragEventArgs)
       {
         // CHANGE THIS CODE FOR YOUR APPLICATION.
       }

       /// <summary>
       /// Retrieves UML IElements from drag arguments.
       /// Works for drags from UML diagrams.
       /// </summary>
       private IEnumerable<IElement> GetModelElementsFromDragEvent
               (DiagramDragEventArgs dragEvent)
       {
         //ElementGroupPrototype is the container for
         //dragged and copied elements and toolbox items.
         ElementGroupPrototype prototype =
            dragEvent.Data.
            GetData(typeof(ElementGroupPrototype))
                 as ElementGroupPrototype;
         // Locate the originals in the implementation store.
         IElementDirectory implementationDirectory =
            dragEvent.DiagramClientView.Diagram.Store.ElementDirectory;

         return prototype.ProtoElements.Select(
           prototypeElement =>
           {
             ModelElement element = implementationDirectory
               .FindElement(prototypeElement.ElementId);
             ShapeElement shapeElement = element as ShapeElement;
             if (shapeElement != null)
             {
               // Dragged from a diagram.
               return shapeElement.ModelElement as IElement;
             }
             else
             {
               // Dragged from UML Model Explorer.
               return element as IElement;
             }
           });
       }

     }
   }

   ```

    メソッドに記述する内容の詳細については、「 [ジェスチャ ハンドラーの実装](#Implementing)」を参照してください。

   VSIX プロジェクトにメニュー コマンドを追加する必要があります。VSIX プロジェクトは、コマンドをインストールするためのコンテナーとして機能します。 必要に応じて、同じ VSIX に他のコンポーネントを追加できます。

#### <a name="to-add-a-separate-gesture-handler-to-a-vsix-project"></a>VSIX プロジェクトにジェスチャ ハンドラーを個別に追加するには

1. ジェスチャ ハンドラーを独自の VSIX と共に作成した場合、この手順は必要ありません。

2. ソリューションに既存の VSIX プロジェクトが存在しない場合は、新しく作成します。

    1. **ソリューション エクスプローラー**で、ソリューションのショートカット メニューを開き、 **[追加]** 、 **[新しいプロジェクト]** の順にクリックします。

    2. **[インストールされたテンプレート]** の **[Visual C#]** または **[Visual Basic]** を展開し、 **[機能拡張]** をクリックします。 中央の列で、 **[VSIX プロジェクト]** をクリックします。

3. VSIX プロジェクトをソリューションのスタートアップ プロジェクトとして設定します。

    - ソリューション エクスプローラーで、VSIX プロジェクトのショートカット メニューを開き、 **[スタートアップ プロジェクトに設定]** をクリックします。

4. **source.extension.vsixmanifest**で、ジェスチャ ハンドラーのクラス ライブラリ プロジェクトを MEF コンポーネントとして追加します。

    1. **[メタデータ]** タブで、VSIX の名前を設定します。

    2. **[インストールの対象]** タブで、Visual Studio のバージョンを対象として設定します。

    3. **[アセット]** タブで、 **[新規作成]** をクリックし、ダイアログ ボックスで次のように設定します。

         **[種類]**  = **MEF コンポーネント**

         **[ソース]**  = **現在のソリューション内のプロジェクト**

         **[プロジェクト]**  = *クラス ライブラリ プロジェクト*

## <a name="Executing"></a> Executing the Gesture Handler
 テストを行う場合は、ジェスチャ ハンドラーをデバッグ モードで実行します。

#### <a name="to-test-the-gesture-handler"></a>ジェスチャ ハンドラーをテストするには

1. **F5**キーを押すか、または **[デバッグ]** メニューの **[デバッグ開始]** をクリックします。

    [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の実験用のインスタンスが開始します。

    **トラブルシューティング**: 新しい [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] が起動しない場合:

   - 複数のプロジェクトがある場合は、VSIX プロジェクトがソリューションのスタートアップ プロジェクトとして設定されていることを確認してください。

   - ソリューション エクスプローラーで、スタートアップまたはプロジェクトのみのショートカット メニューを開き、[プロパティ] をクリックします。 In the project properties editor, choose the **Debug** tab. Make sure that the string in the **Start external program** field is the full pathname of [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], typically:

        `C:\Program Files\Microsoft Visual Studio [version]\Common7\IDE\devenv.exe`

2. 実験用の [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]で、モデリング プロジェクトを開くか、または生成し、モデリング図を開くか、または生成します。 ジェスチャ ハンドラー クラスの属性に表示されているいずれかの種類に含まれる図を使用してください。

3. 図上の任意の場所をダブルクリックします。 ダブルクリック ハンドラーが呼び出されます。

4. UML エクスプローラーから図上へ要素をドラッグします。 ドラッグ ハンドラーが呼び出されます。

   **トラブルシューティング**: ジェスチャ ハンドラーが動作しない場合は、次の点について確認してください。

- ジェスチャ ハンドラー プロジェクトは、VSIX プロジェクトの **source.extensions.manifest** の **[アセット]** タブに MEF コンポーネントとして表示される。

- すべての `Import` 属性と `Export` 属性のパラメーターが有効である。

- `CanDragDrop` メソッドが `false`を返さない。

- 使用するモデル図の種類 (UML クラス、シーケンスなど) が、ジェスチャ ハンドラー クラスの属性 ([ClassDesignerExtension]、[SequenceDesignerExtension] など) の 1 つとして表示される。

- この種類のターゲットおよびドロップ対象の要素に対して組み込みの機能が定義されていない。

## <a name="Implementing"></a> Implementing the Gesture Handler

### <a name="the-gesture-handler-methods"></a>ジェスチャ ハンドラーのメソッド
 ジェスチャ ハンドラー クラスは、<xref:Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement.IGestureExtension> を実装およびエクスポートします。 定義する必要のあるメソッドを次に示します。

|||
|-|-|
|`bool CanDragDrop (ShapeElement target, DiagramDragEventArgs dragEvent)`|`true` で参照されるソース要素をこのターゲット上にドロップすることを許可する場合は `dragEvent` を返します。<br /><br /> このメソッドによってモデルが変更されることはありません。 このメソッドは、マウスを動かしたときの矢印の状態を判断するために使用されるので、すばやい処理が必要です。|
|`void OnDragDrop (ShapeElement target, DiagramDragEventArgs dragEvent)`|`dragEvent`で参照されるソース オブジェクトに基づいてモデルを更新し、ターゲットを更新します。<br /><br /> ドラッグ後にマウスのボタンを離すと呼び出されます。|
|`void OnDoubleClick (ShapeElement target, DiagramPointEventArgs pointEvent)`|`target` は、ユーザーがダブルクリックした図形です。|

 UML だけでなく、ファイルや .NET クラス ビュー内のノードなど、他のさまざまな項目を受け取ることができるハンドラーを作成できます。 シリアル化形式の項目をデコードする `OnDragDrop` メソッドを記述すると、ユーザーはこれらの項目を UML 図にドラッグできます。 デコード メソッドは、項目の種類によって異なります。

 メソッドのパラメーターは次のとおりです。

- `ShapeElement target`. ユーザーが項目をドラッグした図形または図。

    `ShapeElement` は、UML モデリング ツールの基礎にある実装のクラスです。 UML モデルと図が不整合な状態になる可能性を低くするには、このクラスのメソッドを直接使用しないことをお勧めします。 Instead, wrap the element in an `IShape`, and then use the methods described in [Display a UML model on diagrams](../modeling/display-a-uml-model-on-diagrams.md).

  - `IShape`を取得するには

      ```
      IShape targetIShape = target.CreateIShape(target);
      ```

  - ドラッグまたはダブルクリック操作が対象とするモデル要素を取得するには

      ```
      IElement target = targetIShape.Element;
      ```

      これを要素のより具体的な種類にキャストできます。

  - UML モデルを格納する UML モデル ストアを取得するには

      ```
      IModelStore modelStore =
        targetIShape.Element.GetModelStore(); 
      ```

  - ホストおよびサービス プロバイダーへのアクセスを取得するには

      ```
      target.Store.GetService(typeof(EnvDTE.DTE)) as EnvDTE.DTE
      ```

- `DiagramDragEventArgs eventArgs`. このパラメーターは、ドラッグ操作の、シリアル化形式のソース オブジェクトを保持します。

    ```
    System.Windows.Forms.IDataObject data = eventArgs.Data;
    ```

     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]のさまざまな部分から、または Windows デスクトップから、さまざまな種類の要素を図にドラッグすることができます。 `IDataObject`では、多種多様な要素がさまざまな方法でエンコードされています。 情報を抽出する方法については、適切なオブジェクトの種類に関するドキュメントを参照してください。

     If your source object is a UML element dragged from UML Model Explorer or from another UML diagram, refer to [Get UML model elements from IDataObject](../modeling/get-uml-model-elements-from-idataobject.md).

### <a name="writing-the-code-of-the-methods"></a>メソッドのコードの記述
 モデルを読み取って更新するコードの記述の詳細については、「 [Programming with the UML API](../modeling/programming-with-the-uml-api.md)」を参照してください。

 For information about accessing model information in a drag operation, see [Get UML model elements from IDataObject](../modeling/get-uml-model-elements-from-idataobject.md).

 If you are dealing with a sequence diagram, see also [Edit UML sequence diagrams by using the UML API](../modeling/edit-uml-sequence-diagrams-by-using-the-uml-api.md).

 メソッドのパラメーターに加え、現在の図およびモデルにアクセスするためのクラスの、インポート済みプロパティを宣言することもできます。

```
[Import] public IDiagramContext DiagramContext { get; set; }
```

 `IDiagramContext` の宣言により、図、現在の選択項目、およびモデルにアクセスするメソッドにコードを記述することができます。

```
IDiagram diagram = this.DiagramContext.CurrentDiagram;
foreach (IShape<IElement> shape in diagram.GetSelectedShapes<IElement>)
{ IElement element = shape.Element; ... }
IModelStore modelStore = diagram.ModelStore;
IModel model = modelStore.Root;
foreach (IDiagram diagram in modelStore.Diagrams) {...}
foreach (IElement element in modelStore.AllInstances<IUseCase>) {...}
```

 For more information, see [Navigate the UML model](../modeling/navigate-the-uml-model.md).

## <a name="Installing"></a> Installing and uninstalling an extension
 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 拡張機能は、自分のコンピューターと他のコンピューターの両方にインストールできます。

#### <a name="to-install-an-extension"></a>拡張機能をインストールするには

1. 自分のコンピューターで、VSIX プロジェクトによってビルドされた **.vsix** ファイルを見つけます。

    1. **ソリューション エクスプローラー**で、VSIX プロジェクトのショートカット メニューを開き、 **[エクスプローラーでフォルダーを開く]** をクリックします。

    2. Locate the file **bin\\\*\\** _YourProject_ **.vsix**

2. 拡張機能をインストールするターゲット コンピューターに **.vsix** ファイルをコピーします。 自分のコンピューターでも別のコンピューターでもかまいません。

     The target computer must have one of the editions of [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] that you specified in **source.extension.vsixmanifest**.

3. ターゲット コンピューター上で、 **.vsix** ファイルを開きます。

     **Visual Studio 拡張機能インストーラー** が起動され、拡張機能がインストールされます。

4. [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]を起動または再起動します。

#### <a name="to-uninstall-an-extension"></a>拡張機能をアンインストールするには

1. **[ツール]** メニューの **[拡張機能と更新プログラム]** をクリックします。

2. **[インストール済みの拡張機能]** を展開します。

3. 拡張機能を選択し、 **[アンインストール]** をクリックします。

   拡張機能の障害が原因で読み込みが失敗し、エラー ウィンドウにレポートが生成されることがまれにありますが、それは拡張機能マネージャーには表示されません。 その場合は、以下の場所からファイルを削除して、拡張機能を削除します。

   *%LocalAppData%* **\Local\Microsoft\VisualStudio\\[version]\Extensions**

## <a name="DragExample"></a> 「例」
 コンポーネント図からドラッグされたコンポーネントのパートおよびポートに基づいて、シーケンス図に生存線を生成する方法を次の例に示します。

 テストするには、F5 キーを押します。 Visual Studio の実験用インスタンスが開きます。 このインスタンスで UML モデルを開き、コンポーネント図にコンポーネントを生成します。 このコンポーネントに、インターフェイスと内部コンポーネントのパートを追加します。 インターフェイスおよびパートを選択します。 次に、インターフェイスおよびパートをシーケンス図にドラッグします (Drag from the component diagram up to the tab for the sequence diagram, and then down into the sequence diagram.) A lifeline will appear for each interface and part.

 For more information about binding interactions to sequence diagrams, see [Edit UML sequence diagrams by using the UML API](../modeling/edit-uml-sequence-diagrams-by-using-the-uml-api.md).

```
using System.Collections.Generic;
using System.ComponentModel.Composition;
using System.Linq;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
using Microsoft.VisualStudio.Uml.AuxiliaryConstructs;
using Microsoft.VisualStudio.Uml.Classes;
using Microsoft.VisualStudio.Uml.Interactions;
using Microsoft.VisualStudio.Uml.CompositeStructures;
using Microsoft.VisualStudio.Uml.Components;

/// <summary>
/// Creates lifelines from component ports and parts.
/// </summary>
[Export(typeof(IGestureExtension))]
[SequenceDesignerExtension]
public class CreateLifelinesFromComponentParts : IGestureExtension
{
  [Import]
  public IDiagramContext Context { get; set; }

  /// <summary>
  /// Called by the modeling framework when
  /// the user drops something on a target.
  /// </summary>
  /// <param name="target">The target shape or diagram </param>
  /// <param name="dragEvent">The item being dragged</param>
  public void OnDragDrop(ShapeElement target,
           DiagramDragEventArgs dragEvent)
  {
    ISequenceDiagram diagram = Context.CurrentDiagram
            as ISequenceDiagram;
    IInteraction interaction = diagram.Interaction;
    if (interaction == null)
    {
      // Sequence diagram is empty: create an interaction.
      interaction = diagram.ModelStore.Root.CreateInteraction();
      interaction.Name = Context.CurrentDiagram.Name;
      diagram.Bind(interaction);
    }
    foreach (IConnectableElement connectable in
       GetConnectablesFromDrag(dragEvent))
    {
      ILifeline lifeline = interaction.CreateLifeline();
      lifeline.Represents = connectable;
      lifeline.Name = connectable.Name;
    }
  }

  /// <summary>
  /// Called by the modeling framework to determine whether
  /// the user can drop something on a target.
  /// Must not change anything.
  /// </summary>
  /// <param name="target">The target shape or diagram</param>
  /// <param name="dragEvent">The item being dragged</param>
  /// <returns>true if this item can be dropped on this target</returns>
  public bool CanDragDrop(ShapeElement target,
           DiagramDragEventArgs dragEvent)
  {
    IEnumerable<IConnectableElement> connectables = GetConnectablesFromDrag(dragEvent);
    return connectables.Count() > 0;
  }

  ///<summary>
  /// Get dragged parts and ports of an IComponent.
  ///</summary>
  private IEnumerable<IConnectableElement>
    GetConnectablesFromDrag(DiagramDragEventArgs dragEvent)
  {
    foreach (IElement element in
      GetModelElementsFromDragEvent(dragEvent))
    {
      IConnectableElement part = element as IConnectableElement;
      if (part != null)
      {
        yield return part;
      }
    }
  }

  /// <summary>
  /// Retrieves UML IElements from drag arguments.
  /// Works for drags from UML diagrams.
  /// </summary>
  private IEnumerable<IElement> GetModelElementsFromDragEvent
          (DiagramDragEventArgs dragEvent)
  {
    //ElementGroupPrototype is the container for
    //dragged and copied elements and toolbox items.
    ElementGroupPrototype prototype =
       dragEvent.Data.
       GetData(typeof(ElementGroupPrototype))
            as ElementGroupPrototype;
    // Locate the originals in the implementation store.
    IElementDirectory implementationDirectory =
       dragEvent.DiagramClientView.Diagram.Store.ElementDirectory;

    return prototype.ProtoElements.Select(
      prototypeElement =>
      {
        ModelElement element = implementationDirectory
          .FindElement(prototypeElement.ElementId);
        ShapeElement shapeElement = element as ShapeElement;
        if (shapeElement != null)
        {
          // Dragged from a diagram.
          return shapeElement.ModelElement as IElement;
        }
        else
        {
          // Dragged from UML Model Explorer.
          return element as IElement;
        }
      });
  }

  public void OnDoubleClick(ShapeElement targetElement, DiagramPointEventArgs diagramPointEventArgs)
  {
  }
}

```

 The code of `GetModelElementsFromDragEvent()` is described in [Get UML model elements from IDataObject](../modeling/get-uml-model-elements-from-idataobject.md).

## <a name="see-also"></a>参照
 [Define and install a modeling extension](../modeling/define-and-install-a-modeling-extension.md) [Extend UML models and diagrams](../modeling/extend-uml-models-and-diagrams.md) [Define a menu command on a modeling diagram](../modeling/define-a-menu-command-on-a-modeling-diagram.md) [Define validation constraints for UML models](../modeling/define-validation-constraints-for-uml-models.md) [Programming with the UML API](../modeling/programming-with-the-uml-api.md)
