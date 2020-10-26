---
title: レイヤー図にコマンドおよびジェスチャを追加するMicrosoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- layer diagrams, adding custom commands
- layer diagrams, adding custom gestures
ms.assetid: ac9c417b-0b40-4a90-86f5-ee3cbdce030b
caps.latest.revision: 40
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7b0c54975cdd5bc86f77dddbd5ca1a56c1896394
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72655310"
---
# <a name="add-commands-and-gestures-to-layer-diagrams"></a>レイヤー図にコマンドおよびジェスチャを追加する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio でレイヤー図のコンテキスト メニュー コマンドやジェスチャ ハンドラーを定義できます。 これらの拡張機能を Visual Studio Integration Extension (VSIX) にパッケージ化し、他の Visual Studio ユーザーに配布できます。

 必要に応じて、複数のコマンドおよびジェスチャ ハンドラーを同じ Visual Studio プロジェクトで定義できます。 また、複数のプロジェクトを組み合わせて 1 つの VSIX に含めることもできます。 たとえば、レイヤー コマンド、特定領域言語、および UML 図用のコマンドを含む単一の VSIX を定義できます。

> [!NOTE]
> ユーザーのソース コードをレイヤー図と比較する、アーキテクチャの検証をカスタマイズすることもできます。 アーキテクチャの検証は、別の Visual Studio プロジェクトで定義する必要があります。 それを他の拡張機能と同じ VSIX に追加できます。 詳細については、「 [レイヤー図へのカスタムアーキテクチャ検証の追加](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)」を参照してください。

## <a name="requirements"></a>必要条件
 「 [要件](../modeling/extend-layer-diagrams.md#prereqs)」を参照してください。

## <a name="defining-a-command-or-gesture-in-a-new-vsix"></a>新しい VSIX でコマンドまたはジェスチャを定義する
 最も簡単に拡張機能を作成するには、プロジェクト テンプレートを使用します。 この方法では、コードと VSIX マニフェストが同じプロジェクトに配置されます。

#### <a name="to-define-an-extension-by-using-a-project-template"></a>プロジェクト テンプレートを使用して拡張機能を定義するには

1. **[ファイル]** メニューの **[新しいプロジェクト]** を使用して、新しいソリューションにプロジェクトを作成します。

2. **[新しいプロジェクト]** ダイアログ ボックスの **[モデリング プロジェクト]** で、 **[Layer Designer Command Extension]** (レイヤー デザイナー コマンド拡張機能) または **[Layer Designer Gesture Extension]**(レイヤー デザイナー ジェスチャ拡張機能) を選択します。

    このテンプレートでは、動作する小さい例を含むプロジェクトが作成されます。

3. 拡張機能をテストするには、 **Ctrl キーを押しながら F5** キーを押すか、 **F5**キーを押します。

    [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の実験用のインスタンスが開始します。 このインスタンスで、レイヤー図を作成します。 独自のコマンドまたはジェスチャ拡張機能が、この図で動作します。

4. 実験用のインスタンスを閉じて、サンプル コードを変更します。 詳細については、「 [プログラムコードでのレイヤーモデルの移動と更新](../modeling/navigate-and-update-layer-models-in-program-code.md)」を参照してください。

5. 同じプロジェクトに、さらにコマンドまたはジェスチャ ハンドラーを追加できます。 詳細については、次のいずれかのセクションを参照してください。

    [メニュー コマンドを定義する](#command)

    [ジェスチャ ハンドラーを定義する](#gesture)

6. のメインインスタンスまたは別のコンピューターに拡張機能をインストールするには、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] *bin \\ *で **.vsix**ファイルを見つけます。 このファイルをインストール先のコンピューターにコピーして、ダブルクリックします。 拡張機能をアンインストールするには、 **[ツール]** メニューの **[拡張機能と更新プログラム]** を使用します。

## <a name="adding-a-command-or-gesture-to-a-separate-vsix"></a>別の VSIX にコマンドまたはジェスチャを追加する
 コマンド、レイヤー検証コントロール、および他の拡張機能を含む 1 つの VSIX を作成する場合は、VSIX を定義するプロジェクトとハンドラー用のプロジェクトを分けることをお勧めします。 その他の種類のモデリング拡張機能については、「 [UML モデルと図の拡張](../modeling/extend-uml-models-and-diagrams.md)」を参照してください。

#### <a name="to-add-layer-extensions-to-a-separate-vsix"></a>レイヤー拡張機能を別の VSIX に追加するには

1. 新規または既存の Visual Studio ソリューションでクラス ライブラリ プロジェクトを作成します。 **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** をクリックし、 **[クラス ライブラリ]** をクリックします。 このプロジェクトに、コマンドまたはジェスチャ ハンドラーのクラスを格納します。

    > [!NOTE]
    > コマンドまたはジェスチャ ハンドラーのクラスは 1 つのクラス ライブラリに複数定義できますが、レイヤー検証クラスは別のクラス ライブラリで定義する必要があります。

2. ソリューションで VSIX プロジェクトを特定または作成します。 VSIX プロジェクトには、 **source.extension.vsixmanifest**という名前のファイルが含まれます。 VSIX プロジェクトを追加するには:

    1. **[新しいプロジェクト]** ダイアログ ボックスで **[Visual C#]** を展開し、 **[拡張機能]** をクリックして **[VSIX Project]**(VSIX プロジェクト) をクリックします。

    2. ソリューション エクスプローラーで、VSIX プロジェクトを右クリックし、 **[スタートアップ プロジェクトに設定]** をクリックします。

    3. **[Select Editions]** (エディションの選択) をクリックし、 **Visual Studio** がオンになっていることを確認します。

3. **source.extension.vsixmanifest**の **[アセット]** で、コマンドまたはジェスチャ ハンドラーのプロジェクトを MEF コンポーネントとして追加します。

    1. **[アセット]** タブで、 **[新規]** をクリックします。

    2. **[種類]** で、 **[Microsoft.VisualStudio.MefComponent]** をクリックします。

    3. **[ソース]** で、 **[Project in current solution]** (現在のソリューション内のプロジェクト) をクリックし、コマンドまたはジェスチャ ハンドラーのプロジェクトの名前を選択します。

    4. ファイルを保存します。

4. コマンドまたはジェスチャ ハンドラーのプロジェクトに戻り、以下のプロジェクト参照を追加します。

|**リファレンス**|**実行できる操作**|
|-------------------|------------------------------------|
|Program Files\Microsoft Visual Studio [バージョン]\Common7\IDE\Extensions\Microsoft\Architecture Tools\ExtensibilityRuntime\Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.dll|レイヤーを作成および編集する|
|Microsoft.VisualStudio.Uml.Interfaces|レイヤーを作成および編集する|
|Microsoft.VisualStudio.ArchitectureTools.Extensibility|図で図形を変更する|
|System.ComponentModel.Composition|MEF (Managed Extensibility Framework) を使用してコンポーネントを定義する|
|Microsoft.VisualStudio.Modeling.Sdk.[バージョン]|モデリング拡張機能を定義する|
|Microsoft.VisualStudio.Modeling.Sdk.Diagrams.[バージョン]|図形と図を更新する|

1. 拡張機能のコードを含むように、C# クラス ライブラリ プロジェクトのクラス ファイルを編集します。 詳細については、次のいずれかのセクションを参照してください。

     [メニュー コマンドを定義する](#command)

     [ジェスチャ ハンドラーを定義する](#gesture)

     「 [プログラムコードでのレイヤーモデルの移動と更新](../modeling/navigate-and-update-layer-models-in-program-code.md)」も参照してください。

2. 機能をテストするには、Ctrl キーを押しながら F5 キーを押すか、または F5 キーを押します。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の実験用のインスタンスが開きます。 このインスタンスで、レイヤー図を作成または開きます。

3. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]のメイン インスタンスまたは別のコンピューターに拡張機能をインストールするには、 **bin\*** ディレクトリで **bin** ファイルを探します。 このファイルを、VSIX をインストールするコンピューターにコピーします。 Windows エクスプローラー (Windows 8 のエクスプローラー) で VSIX ファイルをダブルクリックします。

     拡張機能をアンインストールするには、 **[ツール]** メニューの **[拡張機能と更新プログラム]** を使用します。

## <a name="defining-a-menu-command"></a><a name="command"></a> メニューコマンドの定義
 ジェスチャまたはコマンドの既存のプロジェクトに、さらにメニュー コマンド定義を追加できます。 各コマンドは、次のような特徴を持つクラスによって定義されます。

- クラスは次のように宣言されます。

   `[LayerDesignerExtension]`

   `[Export(typeof(ICommandExtension))]`

   `public class`  *MyLayerCommand*  `: ICommandExtension { ... }`

- クラスの名前空間と名前は重要ではありません。

- `ICommandExtension` を実装するメソッドは次のとおりです。

  - `string Text {get;}` : メニューに表示されるラベルです。

  - `void QueryStatus(IMenuCommand command)` : ユーザーが図を右クリックすると呼び出され、ユーザーの現在の選択に対してコマンドを表示して有効にする必要があるかどうかを判定します。

  - `void Execute(IMenuCommand command)` : ユーザーがコマンドを選択すると呼び出されます。

- 現在の選択項目を特定するには、 `IDiagramContext`をインポートします。

   `[Import]`

   `public IDiagramContext DiagramContext { get; set; }`

   `...`

   `DiagramContext.CurrentDiagram.SelectedShapes.Count()...`

  詳細については、「 [プログラムコードでのレイヤーモデルの移動と更新](../modeling/navigate-and-update-layer-models-in-program-code.md)」を参照してください。

  新しいコマンドを追加するには、以下のサンプルを含む新しいコード ファイルを作成します。 その後、テストして編集します。

```
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
using System.ComponentModel.Composition;
using System.Linq;

namespace MyLayerExtension // Change to your preference.
{
  // This is a feature for Layer diagrams:
  [LayerDesignerExtension]
  // This feature is a menu command:
  [Export(typeof(ICommandExtension))]
  // Change the class name to your preference:
  public class MyLayerCommand : ICommandExtension
  {
    [Import]
    public IDiagramContext DiagramContext { get; set; }

    [Import]
    public ILinkedUndoContext LinkedUndoContext { get; set; }

    // Menu command label:
    public string Text
    {
      get { return "Duplicate layers"; }
    }

    // Called when the user right-clicks the diagram.
    // Defines whether the command is visible and enabled.
    public void QueryStatus(IMenuCommand command)
    {
      command.Visible =
      command.Enabled = DiagramContext.CurrentDiagram
        .SelectedShapes.Count() > 0;
    }

    // Called when the user selects the command.
    public void Execute(IMenuCommand command)
    {
      // A selection of starting points:
      IDiagram diagram = this.DiagramContext.CurrentDiagram;
      ILayerModel lmodel = diagram.GetLayerModel();
      foreach (ILayer layer in lmodel.Layers)
      { // All layers in model.
      }
      // Updates should be performed in a transaction:
      using (ILinkedUndoTransaction t =
        LinkedUndoContext.BeginTransaction("copy selection"))
      {
        foreach (ILayer layer in
          diagram.SelectedShapes
            .Select(shape=>shape.GetLayerElement())
            .Where(element => element is ILayer))
        {
          ILayer copy = lmodel.CreateLayer(layer.Name + "+");
          // Position the shapes:
          IShape originalShape = layer.GetShape();
          copy.GetShape().Move(
            originalShape.XPosition + originalShape.Width * 1.2,
            originalShape.YPosition);
        }
        t.Commit();
      }
    }
  }
}
```

## <a name="defining-a-gesture-handler"></a><a name="gesture"></a> ジェスチャハンドラーの定義
 ジェスチャ ハンドラーは、ユーザーがレイヤー図に項目をドラッグしたとき、およびユーザーが図の任意の場所をダブルクリックしたときに応答します。

 コマンドまたはジェスチャ ハンドラーの既存の VSIX プロジェクトに対し、ジェスチャ ハンドラーが定義されているコード ファイルを追加できます。

```
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
using System.ComponentModel.Composition;
using System.Linq;
namespace MyLayerExtensions // change to your preference
{
  [LayerDesignerExtension]
  [Export(typeof(IGestureExtension))]
  public class MyLayerGestureHandler : IGestureExtension
  {
  }
}
```

 ジェスチャ ハンドラーについては次の点に注意してください。

- `IGestureExtension` のメンバーは次のとおりです。

   **OnDoubleClick** : ユーザーが図のどこかをダブルクリックすると呼び出されます。

   **CanDragDrop** : ユーザーがアイテムを図にドラッグするときにマウスを移動すると繰り返し呼び出されます。 すばやく動作する必要があります。

   **OnDragDrop** : ユーザーが図にアイテムをドロップすると呼び出されます。

- 各メソッドの最初の引数は、レイヤー要素を取得できる `IShape`です。 次に例を示します。

  ```
  public void OnDragDrop(IShape target, IDataObject data)
  {
      ILayerElement element = target.GetLayerElement();
      if (element is ILayer)
      {
          // ...
      }
  }
  ```

- ドラッグされるアイテムの種類によっては、ハンドラーが既に定義されています。 たとえば、ユーザーはソリューション エクスプローラーからレイヤー図にアイテムをドラッグできます。 このような種類のアイテムに対しては、ドラッグ ハンドラーを定義できません。 その場合、 `DragDrop` メソッドは呼び出されません。

  他の項目を図にドラッグしたときにデコードする方法の詳細については、「 [モデリング図でジェスチャハンドラーを定義](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)する」を参照してください。

## <a name="see-also"></a>参照
 [プログラムコードでレイヤーモデルを移動および更新](../modeling/navigate-and-update-layer-models-in-program-code.md)[するカスタムアーキテクチャ検証をレイヤー図に追加する](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)[モデリング拡張機能を定義してインストール](../modeling/define-and-install-a-modeling-extension.md)する
