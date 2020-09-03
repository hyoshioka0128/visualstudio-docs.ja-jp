---
title: UML 図をイメージファイルにエクスポートする |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: b29ce2a5-0ee3-4ab7-9aa3-13ca9c6b37a2
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c095291cd02d591d9e493601b598a63c1ccb6f5b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72669655"
---
# <a name="export-uml-diagrams-to-image-files"></a>UML 図をイメージ ファイルにエクスポートする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

から、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プログラムコントロールの下にあるイメージに UML ドキュメントをエクスポートできます。 たとえば、このエクスポートをドキュメントの自動生成の一部として実行できます。

 ドキュメントをイメージに手動でエクスポートする場合は、図から図形をコピーして Word などの他のプログラムに貼り付けることができます。 ドキュメントを XPS 形式にして印刷することもできます。 詳細については、「 [イメージとしてダイアグラムをエクスポート](../modeling/export-diagrams-as-images.md)する」を参照してください。

## <a name="saving-an-image"></a>イメージの保存
 次のコードでは、イメージをファイルに保存するショートカット メニュー コマンド ("コンテキスト メニュー コマンド" とも呼ばれる) を定義しています。

> [!NOTE]
> このコードをメニュー コマンドとして機能させるには、このコードを MEF コンポーネントに組み込む必要があります。 詳細については、「 [モデリング図のメニューコマンドの定義](../modeling/define-a-menu-command-on-a-modeling-diagram.md)」を参照してください。

 このコードでは、まず [Ishape. GetObject](/previous-versions/ee789371(v=vs.140)) を使用して、 <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram> 基になる実装のを取得します。 この型には <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram.CreateBitmap%2A> メソッドがあります。

```
namespace SaveToImage
{
  using System.ComponentModel.Composition; // for [Import], [Export]
  using System.Drawing; // for Bitmap
  using System.Drawing.Imaging; // for ImageFormat
  using System.Linq; // for collection extensions
  using System.Windows.Forms; // for SaveFileDialog
  using Microsoft.VisualStudio.Modeling.Diagrams;
    // for Diagram
  using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
    // for IGestureExtension, ICommandExtension, ILinkedUndoContext
  using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
    // for IDiagramContext
  using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
    // for designer extension attributes

  /// <summary>
  /// Called when the user clicks the menu item.
  /// </summary>
  // Context menu command applicable to any UML diagram
  [Export(typeof(ICommandExtension))]
  [ClassDesignerExtension]
  [UseCaseDesignerExtension]
  [SequenceDesignerExtension]
  [ComponentDesignerExtension]
  [ActivityDesignerExtension]
  class CommandExtension : ICommandExtension
  {
    [Import]
    IDiagramContext Context { get; set; }

    public void Execute(IMenuCommand command)
    {
      // Get the diagram of the underlying implementation.
      Diagram dslDiagram = Context.CurrentDiagram.GetObject<Diagram>();
      if (dslDiagram != null)
      {
        string imageFileName = FileNameFromUser();
        if (!string.IsNullOrEmpty(imageFileName))
        {
          Bitmap bitmap = dslDiagram.CreateBitmap(
           dslDiagram.NestedChildShapes,
           Diagram.CreateBitmapPreference.FavorClarityOverSmallSize);
          bitmap.Save(imageFileName, GetImageType(imageFileName));
        }
      }
    }

    /// <summary>
    /// Called when the user right-clicks the diagram.
    /// Set Enabled and Visible to specify the menu item status.
    /// </summary>
    /// <param name="command"></param>
    public void QueryStatus(IMenuCommand command)
    {
      command.Enabled = Context.CurrentDiagram != null
        && Context.CurrentDiagram.ChildShapes.Count() > 0;
    }

    /// <summary>
    /// Menu text.
    /// </summary>
    public string Text
    {
      get { return "Save To Image..."; }
    }

    /// <summary>
    /// Ask the user for the path of an image file.
    /// </summary>
    /// <returns>image file path, or null</returns>
    private string FileNameFromUser()
    {
      SaveFileDialog dialog = new SaveFileDialog();
      dialog.AddExtension = true;
      dialog.DefaultExt = "image.bmp";
      dialog.Filter = "Bitmap ( *.bmp )|*.bmp|JPEG File ( *.jpg )|*.jpg|Enhanced Metafile (*.emf )|*.emf|Portable Network Graphic ( *.png )|*.png";
      dialog.FilterIndex = 1;
      dialog.Title = "Save Diagram to Image";
      return dialog.ShowDialog() == DialogResult.OK ? dialog.FileName : null;
    }

    /// <summary>
    /// Return the appropriate image type for a file extension.
    /// </summary>
    /// <param name="fileName"></param>
    /// <returns></returns>
    private ImageFormat GetImageType(string fileName)
    {
      string extension = System.IO.Path.GetExtension(fileName).ToLowerInvariant();
      ImageFormat result = ImageFormat.Bmp;
      switch (extension)
      {
        case ".jpg":
          result = ImageFormat.Jpeg;
          break;
        case ".emf":
          result = ImageFormat.Emf;
          break;
        case ".png":
          result = ImageFormat.Png;
          break;
      }
      return result;
    }
  }
}
```

## <a name="see-also"></a>参照
 [図をイメージとしてエクスポート](../modeling/export-diagrams-as-images.md)[するモデリング図のメニューコマンドを定義](../modeling/define-a-menu-command-on-a-modeling-diagram.md)する
