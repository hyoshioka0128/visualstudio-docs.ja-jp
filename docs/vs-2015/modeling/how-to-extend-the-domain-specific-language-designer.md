---
title: '方法: ドメイン固有言語デザイナーを拡張する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: fa807f1b-2780-491e-925b-abbfd31b2bfa
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 33a7f5a0f183030f9de021df328f8c5e50f5fd5a
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300895"
---
# <a name="how-to-extend-the-domain-specific-language-designer"></a>方法: ドメイン固有言語デザイナーを拡張する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

DSL 定義を編集するために使用するデザイナーの拡張機能を作成できます。 拡張の種類としては、メニューコマンドの追加、ドラッグアンドクリックによるジェスチャのハンドラーの追加、特定の種類の値や関係が変更されたときにトリガーされるルールなどがあります。 拡張機能は、Visual Studio Integration Extension (VSIX) としてパッケージ化し、他のユーザーに配布することができます。

 サンプルコードとこの機能の詳細については、「Visual Studio の[視覚化およびモデリング SDK (VMSDK)」 Web サイト](https://go.microsoft.com/fwlink/?LinkID=186128)を参照してください。

## <a name="setting-up-the-solution"></a>ソリューションの設定
 拡張機能のコードを含むプロジェクトと、プロジェクトをエクスポートする VSIX プロジェクトを設定します。 ソリューションには、同じ VSIX に組み込まれている他のプロジェクトを含めることができます。

#### <a name="to-create-a-dsl-designer-extension-solution"></a>DSL デザイナー拡張機能ソリューションを作成するには

1. クラスライブラリプロジェクトテンプレートを使用して、新しいプロジェクトを作成します。 **[新しいプロジェクト]** ダイアログボックスで、 **[ C#ビジュアル**] をクリックし、中央のウィンドウで **[クラスライブラリ]** をクリックします。

     このプロジェクトには、拡張機能のコードが含まれます。

2. VSIX プロジェクトテンプレートを使用して、新しいプロジェクトを作成します。 **[新しいプロジェクト]** ダイアログボックスで、 **[ C#ビジュアル**] を展開し、 **[機能拡張]** をクリックします。次に、中央のウィンドウで **[VSIX プロジェクト]** を選択します。

     **[ソリューションに追加]** を選択します。

     Source.extension.vsixmanifest が VSIX マニフェストエディターで開きます。

3. コンテンツ フィールドの上にある **コンテンツの追加** をクリックします。

4. **[コンテンツの追加]** ダイアログボックスで、 **[コンテンツの種類**を**MEF コンポーネント**に選択] を設定し、 **[プロジェクト]** をクラスライブラリプロジェクトに設定します。

5. **[エディションの選択]** をクリックし、 **Visual Studio Enterprise**がオンになっていることを確認します。

6. VSIX プロジェクトがソリューションのスタートアッププロジェクトであることを確認します。

7. クラスライブラリプロジェクトで、次のアセンブリへの参照を追加します。

     Microsoft.VisualStudio.CoreUtility

     Microsoft.VisualStudio.Modeling.Sdk.11.0

     Microsoft.VisualStudio.Modeling.Sdk.Diagrams.11.0

     Microsoft.VisualStudio.Modeling.Sdk.DslDefinition.11.0

     Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0

     System.ComponentModel.Composition

     System.Drawing

     System.Drawing.Design

     System.Windows.Forms

## <a name="testing-and-deployment"></a>テストと展開
 このトピックのすべての拡張機能をテストするには、ソリューションをビルドして実行します。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の実験用のインスタンスが開きます。 このインスタンスでは、DSL ソリューションを開きます。 DslDefinition ダイアグラムを編集します。 拡張機能の動作を確認できます。

 拡張機能をメイン [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]、および他のコンピューターに展開するには、次の手順を実行します。

1. Vsix のインストールファイルを検索するには、vsix プロジェクトの bin\\*\\\*.vsix を使用します。

2. このファイルを対象のコンピュータにコピーし、Windows エクスプローラ (またはファイルエクスプローラー) でダブルクリックします。

    [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 拡張機能マネージャーが開き、拡張機能がインストールされていることを確認できます。

   拡張機能をアンインストールするには、次の手順を実行します。

3. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]で、 **[ツール]** メニューの **[拡張機能マネージャー]** をクリックします。

4. 拡張機能を選択して削除します。

## <a name="adding-a-shortcut-menu-command"></a>ショートカットメニューコマンドの追加
 DSL デザイナー画面または DSL エクスプローラーウィンドウにショートカットメニューコマンドを表示するには、次のようなクラスを記述します。

 クラスは `ICommandExtension` を実装し、属性 `DslDefinitionModelCommandExtension`を持つ必要があります。

```
using System.Collections.Generic;
using System.ComponentModel.Composition;
using System.Linq;
using Microsoft.VisualStudio.Modeling.Diagrams;
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling.DslDefinition;
using Microsoft.VisualStudio.Modeling.DslDefinition.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling.DslDesigner;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;

namespace Fabrikam.SimpleDslDesignerExtension
{
  /// <summary>
  /// Command extending the DslDesigner.
  /// </summary>
  [DslDefinitionModelCommandExtension]
  public class MyDslDesignerCommand : ICommandExtension
  {
    /// <summary>
    /// Selection Context for this command
    /// </summary>
    [Import]
    IVsSelectionContext SelectionContext { get; set; }

    /// <summary>
    /// Is the command visible and active?
    /// This is called when the user right-clicks.
    /// </summary>
    public void QueryStatus(IMenuCommand command)
    {
      command.Visible = true;
      // Is there any selected DomainClasses in the Dsl explorer?
      command.Enabled =
        SelectionContext.AtLeastOneSelected<DomainClass>();

      // Is there any selected ClassShape on the design surface?
      command.Enabled |=
        (SelectionContext.GetCurrentSelection<ClassShape>()
                .Count() > 0);
    }
    /// <summary>
    /// Executes the command
    /// </summary>
    /// <param name="command">Command initiating this action</param>
    public void Execute(IMenuCommand command)
    {
      ...
    }
    /// <summary>
    /// Label for the command
    /// </summary>
    public string Text
    {
      get { return "My Command"; }
    }
  }
}
```

## <a name="handling-mouse-gestures"></a>マウスジェスチャの処理
 このコードは、メニューコマンドのコードに似ています。

```
[DslDefinitionModelGestureExtension]
 class MouseGesturesExtensions : IGestureExtension
 {
  /// <summary>
  /// Double-clicking on a shape representing a Domain model element displays this model element in a dialog box
  /// </summary>
  /// <param name="targetElement">Shape element on which the user has clicked</param>
  /// <param name="diagramPointEventArgs">event args for this double-click</param>
  public void OnDoubleClick(ShapeElement targetElement,
       DiagramPointEventArgs diagramPointEventArgs)
  {
   ModelElement modelElement = PresentationElementHelper.
        GetDslDefinitionModelElement(targetElement);
   if (modelElement != null)
   {
    MessageBox.Show(string.Format(
      "Double clicked on {0}", modelElement.ToString()),
      "Model element double-clicked");
   }
  }

  /// <summary>
  /// Tells if the DslDesigner can consume the to-be-dropped information
  /// </summary>
  /// <param name="targetMergeElement">Shape on which we try to drop</param>
  /// <param name="diagramDragEventArgs">Drop event</param>
  /// <returns><c>true</c> if we can consume the to be dropped data, and <c>false</c> otherwise</returns>
  public bool CanDragDrop(ShapeElement targetMergeElement,
        DiagramDragEventArgs diagramDragEventArgs)
  {
   if (diagramDragEventArgs.Data.GetDataPresent(DataFormats.FileDrop))
   {
    diagramDragEventArgs.Effect = DragDropEffects.Copy;
    return true;
   }
   return false;
  }

  /// <summary>
  /// Processes the drop by displaying the dropped text
  /// </summary>
  /// <param name="targetMergeElement">Shape on which we dropped</param>
  /// <param name="diagramDragEventArgs">Drop event</param>
  public void OnDragDrop(ShapeElement targetDropElement, DiagramDragEventArgs diagramDragEventArgs)
  {
   if (diagramDragEventArgs.Data.GetDataPresent(DataFormats.FileDrop))
   {
    string[] droppedFiles =
      diagramDragEventArgs.Data.
               GetData(DataFormats.FileDrop) as string[];
    MessageBox.Show(string.Format("Dropped text {0}",
        string.Join("\r\n", droppedFiles)), "Dropped Text");
   }
  }
 }
```

## <a name="responding-to-value-changes"></a>値の変更への対応
 このハンドラーでは、ドメインモデルを正常に動作させる必要があります。 単純なドメインモデルを提供します。

```
using System.Diagnostics;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.DslDefinition;
namespace Fabrikam.SimpleDslDesignerExtension
{
  /// <summary>
  /// Rule firing when the type of a domain model property is changed. The change is displayed
  /// in the debugger (Output window of the Visual Studio instance debugging this extension)
  /// </summary>
  [RuleOn(typeof(PropertyHasType))]
  public class DomainPropertyTypeChangedRule : RolePlayerChangeRule
  {
    /// <summary>
    /// Method called when the Type of a Domain Property
    /// is changed by the user in a DslDefinition
    /// </summary>
    /// <param name="e"></param>
    public override void RolePlayerChanged(RolePlayerChangedEventArgs e)
    {
      // We are only interested in the type
      if (e.DomainRole.Id == PropertyHasType.TypeDomainRoleId)
      {
        PropertyHasType relationship =
           e.ElementLink as PropertyHasType;
        DomainType newType = e.NewRolePlayer as DomainType;
        DomainType oldType = e.OldRolePlayer as DomainType;
        DomainProperty property = relationship.Property;

         // We write about the Type change in the debugguer
        Debug.WriteLine(string.Format("The type of the Domain property '{0}' of domain class '{1}' changed from '{2}' to '{3}'",
          property.Name,
          property.Class.Name,
          oldType.GetFullName(false),
          newType.GetFullName(false))
} }  }  );
```

 次のコードは、単純なモデルを実装しています。 新しい GUID を作成して、プレースホルダーを置き換えます。

```
using System;
using System.ComponentModel.Composition;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.DslDefinition;
namespace Fabrikam.SimpleDslDesignerExtension
{
    /// <summary>
    /// Simplest possible domain model
    /// needed only for extension rules.
    /// </summary>
    [DomainObjectId(SimpleDomainModelExtension.DomainModelId)]
    public class SimpleDomainModelExtension : DomainModel
    {
        // Id of this domain model extension
        // Please replace this with a new GUID:
        public const string DomainModelId =
                  "00000000-0000-0000-0000-000000000000";

        /// <summary>
        /// Constructor for the domain model extension
        /// </summary>
        /// <param name="store">Store in which the domain model will be loaded</param>
        public SimpleDomainModelExtension(Store store)
            : base(store, new Guid(SimpleDomainModelExtension.DomainModelId))
        {

        }

        /// <summary>
        /// Rules brought by this domain model extension
        /// </summary>
        /// <returns></returns>
        protected override System.Type[] GetCustomDomainModelTypes()
        {
            return new Type[] {
                     typeof(DomainPropertyTypeChangedRule)
                              };
        }
    }

    /// <summary>
    /// Provider for the DomainModelExtension
    /// </summary>
    [Export(typeof(DomainModelExtensionProvider))]    [ProvidesExtensionToDomainModel(typeof(DslDefinitionModelDomainModel))]
    public class SimpleDomainModelExtensionProvider
          : DomainModelExtensionProvider
    {
        /// <summary>
        /// Extension model type
        /// </summary>
        public override Type DomainModelType
        {
            get
            {
                return typeof(SimpleDomainModelExtension);
            }
        }

    }
}
```
