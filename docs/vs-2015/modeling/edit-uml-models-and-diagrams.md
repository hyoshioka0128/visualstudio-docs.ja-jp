---
title: Edit UML models and diagrams | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.teamarch.modelingproject
- vs.teamarch.UMLModelExplorer
- vs.teamarch.UMLModelExplorer.rootnode
helpviewer_keywords:
- diagrams - modeling
- UML, copy and paste
- UML, models
- UML model
- UML, element properties
- UML
- UML, diagrams
ms.assetid: 87affd40-8127-4ee9-9d3a-ad977abe2ed6
caps.latest.revision: 86
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 00ac30cc7e9ee3aff0dd64f015a4b4954972c09a
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295528"
---
# <a name="edit-uml-models-and-diagrams"></a>UML モデルおよびダイアグラムの編集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML モデルは、いくつかの異なる種類の図によって提供されるビューを使用して作成および編集できます。 図を使用することにより、システムを異なる角度から検討できるため、システムの設計と要件のさまざまな側面について理解し、話し合うのに役立ちます。 Visual Studio には、最も一般的に使用される 5 種類の UML 図のテンプレートが用意されています。

 この機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

 このトピックでは、各種の図に共通のモデルを編集する方法について説明します。 For more information that is specific to particular types of diagrams, see [Create models for your app](../modeling/create-models-for-your-app.md).

## <a name="in-this-topic"></a>このトピックの内容

- [UML Diagrams are Views of a UML Model](#Views)

- [Creating UML Modeling Diagrams](#Creating)

- [Drawing UML Modeling Diagrams](#Drawing)

- [Editing Shapes and Connectors](#Editing)

- [Undoing Changes to the Model](#Undo)

- [Sharing Elements between Diagrams](#Sharing)

- [Copying Elements and Groups of Related Elements](#Copying)

- [Deleting a Model Element or its Views](#Deleting)

- [Searching text in a diagram](#Searching)

- [Preparing a Diagram for Presentation](#presentation)

- [Extending the UML Designers](#extensions)

## <a name="Views"></a> UML Diagrams are Views of a UML Model
 UML 図は、モデリング プロジェクトでのみ作成および使用できます。 For more information about how to create diagrams and projects, see [Create UML modeling projects and diagrams](../modeling/create-uml-modeling-projects-and-diagrams.md).

- モデリング プロジェクトには UML モデルが 1 つ存在します。 プロジェクト内の UML 図はすべて UML モデルのビューです。

- You can see the model in **UML Model Explorer**. On the **Architecture** menu, point to **Windows**, and then click **UML Model Explorer**.

- 図の中のシェイプはすべてモデル内の要素のビューです。 図に新しいシェイプを配置するということは、そのモデルに新しい要素を作成するということです。

- When you save any diagram, Visual Studio saves the whole model, all its diagrams, and the modeling project file.

## <a name="Creating"></a> Creating UML Modeling Diagrams

1. On the **Architecture** menu in Visual Studio, click **New UML or Layer Diagram**.

2. 図を選択し、名前を付けます。

3. In **Add to modeling project**, select an existing modeling project, or select **Create a new modeling project**.

   > [!NOTE]
   > モデリング図はモデリング プロジェクト内に存在している必要があります。

   ソリューション エクスプローラーで既存のモデリング プロジェクトに図を追加することもできます。 Right-click the modeling project, point to **Add**, and then click **New Item**.

#### <a name="to-create-an-empty-uml-modeling-project"></a>空の UML モデリング プロジェクトを作成するには

- On the **File** menu, point to **New**, click **Project**, and in the **New Project** dialog box, double-click **Modeling Projects**.

  For more information about how to manage modeling projects, see [Create UML modeling projects and diagrams](../modeling/create-uml-modeling-projects-and-diagrams.md).

## <a name="Drawing"></a> Drawing UML Modeling Diagrams
 モデリング図には、関係によってリンクされたモデル要素のコレクションが表示されます。 それぞれの要素はシェイプとして表示され、それぞれの関係は 2 つのシェイプをつなぐコネクタとして表示されます。

 要素用と関係用の 2 種類のツールが存在します。 For example, in the UML class diagram Toolbox, **Class** is an element tool, and **Association** is a relationship tool.

> [!NOTE]
> If you want information that is specific to particular diagram types, see [Create models for your app](../modeling/create-models-for-your-app.md).

#### <a name="to-create-elements-and-relationships-in-a-uml-modeling-diagram"></a>UML モデリング図の要素および関係を作成するには

1. モデル要素を作成するには、ツールボックスで要素ツールをクリックし、その表示場所となる図をクリックします。 要素を作成したら、そのハンドルをドラッグしてサイズと形状を調整します。

    場合によっては、新しい要素を別の要素内に配置することができます。 たとえば、UML クラス図では、パッケージ内にクラスを配置できます。

   > [!NOTE]
   > If you cannot see the toolbox, click **Toolbox** on the **View** menu.

2. 関係を作成するには、関係ツールをクリックし、関係の起点となる要素をクリックしてから、終点となる要素をクリックします。

    起点および終点として選択できる要素の種類は関係の種類によって異なります。 たとえば、UML クラス図では、Comment 要素を起点または終点とする Association の関係は作成できません。

   > [!NOTE]
   > 同じツールを複数回使用するには、ツールをダブルクリックします。 When you have finished, click the **Pointer** tool.

   一部の種類の図では、単純なシェイプを描画することもできます。 これらのシェイプはモデルの一部ではありませんが、図のパーツを強調したり、図を複数の領域に分割したりするために使用できます。

## <a name="Editing"></a> Editing Shapes and Connectors
 シェイプのサイズ変更または色付けを行ったり、コネクタのルートを変更したりしても、基になるモデルは影響を受けません。 ただし、図または UML モデル エクスプローラーでシェイプの名前を変更すると、対応する要素の名前が UML モデル エクスプローラー内およびその要素を表示するその他の図の中でも変更されます。

> [!NOTE]
> ツールボックス アイテムを使用すると、要素のグループを作成したり、独自に選んだプロパティを持つ要素を作成したりできます。新しいツールボックス アイテムは簡単に作成できます。 For more information, see [Define a custom modeling toolbox item](../modeling/define-a-custom-modeling-toolbox-item.md).

 次の図は、シェイプのサイズまたは名前を変更する方法を示しています。

 ![Adjusting a model element](../modeling/media/uml-drawadjust1.png "UML_DrawAdjust1")

> [!TIP]
> 組み込みコマンドには、図形をきれいに整列させるためのコマンドは含まれていません。 However, you can easily create your own alignment command by copying the code in the example in [Display a UML model on diagrams](../modeling/display-a-uml-model-on-diagrams.md).

 次の図は、コネクタまたはそのラベルのルートと位置を調整する方法を示しています。

 ![Adjusting a connector](../modeling/media/uml-drawadjust2.png "UML_DrawAdjust2")

#### <a name="to-move-one-end-of-a-connector-to-another-shape"></a>コネクタの片端を別のシェイプに移動するには

1. 次のいずれかの操作を行います。

   - Press **CTRL** and move the end.

     \- または

   - Right-click the connector and then click **Reconnect**.

2. 移動するコネクタの端をクリックします。

3. コネクタの移動先のシェイプをクリックします。

#### <a name="to-change-color-or-other-properties-of-an-element-relationship-or-diagram"></a>要素、関係、または図の色およびその他のプロパティを変更するには

- Click the element and set the fields in the **Properties** window.

     If you cannot see the **Properties** window, right-click the element, and then click **Properties.**

#### <a name="to-zoom-in-and-out-on-a-modeling-diagram"></a>モデリング図を拡大または縮小するには

- Press and hold the **CTRL** key while you rotate the mouse wheel.

     \- または

- Press and hold **CTRL+SHIFT**, and then click the left or right mouse button.

     \- または

- On the **Architecture Designers** toolbar, click the plus sign ( **+** ) or minus sign ( **-** ), or choose a zoom level.

## <a name="Searching"></a> Searching in a Diagram
 図のアイテムを検索するには、クイック検索機能を使用します。 You must set **Look in:** to **Current Document**.

#### <a name="to-search-for-text-in-a-modeling-diagram"></a>モデリング図内のテキストを検索するには

1. Press **CTRL+F**.

     \- または

     On the **Edit** menu, point to **Find and Replace**, and then click **Quick Find**.

    > [!NOTE]
    > In the **Find and Replace** dialog box, you must leave the **Look in** field set to **Current Document**. その他のオプションはサポートされていません。

2. Type the text that you want to find, and then click **Find Next**.

    > [!NOTE]
    > 検索したテキストが折りたたまれたシェイプ内にある場合、シェイプが強調表示されます。 Expand the shape, and then click **Find Next** again.

## <a name="Undo"></a> Undoing Changes to the Model
 You can undo and redo changes that you have made to the model and diagrams by using the **Undo** and **Redo** commands on the **Edit** menu.

 **Each modeling project has a single stack of changes.** モデルおよび図に対して行った変更はすべてこのスタックに記録されます。 スタックには図から図へのフォーカスの切り替えも含まれます。 [元に戻す] コマンドは、このスタックに記録された変更を逆にたどることによって実行されます。

 たとえば、Diagram1 に変更を加え、フォーカスを Diagram 2 に切り替えてから、Diagram2 に変更を加えたとします。 ここで、[元に戻す] コマンドを 3 回実行すると、1 回目には最後の変更が取り消され、2 回目にはフォーカスが Diagram1 に戻され、3 回目には Diagram1 に対する変更が取り消されます。

 **Closing a diagram truncates the stack of changes.** 図を閉じると、その図に対して実行した変更は元に戻せなくなります。また、それ以前にモデルまたはその図に対して加えた変更も元に戻せなくなります。

 **You cannot undo while you are editing a property.** プロパティ ウィンドウでプロパティを編集しているとき、または図のラベルのプロパティを編集しているときは、そのプロパティに対する変更しか元に戻すことができません。 Enter キーを押してプロパティの変更を確定するか、Esc キーを押して変更を取り消してください。 これで、モデルおよび図に対する変更を元に戻すことができるようになります。

 **Closing a diagram without saving might not have the effect you expect.** 図に変更を加えた後にその図を保存せずに閉じても、変更内容はモデルで保持されます。 図を保存せずに閉じる必要がある場合は、モデル全体を閉じることをお勧めします。

## <a name="Sharing"></a> Sharing Elements between Diagrams
 モデル要素の特定のインスタンスが複数の図に表示されるようにすることができます。 クラス、インターフェイス、コンポーネント、ユース ケース、およびアクターがこれに該当します。

 この機能は、図ごとに異なる関係のグループを表示する必要がある場合に便利です。 たとえば、ある図の中で Customer クラスと Address クラスとの間の関連を表示し、 別の図では、同じ Address クラスを Postal Area クラスに関連付けて表示できます。

 名前などのモデル要素のプロパティは、任意の図でそのビューのいずれかを選択するか、UML モデル エクスプローラーでそれを選択することによって変更できます。

 それぞれの図の種類で表示できるモデル要素の種類は限られています。 たとえば、コンポーネント図にユース ケースを表示することはできません。 したがって、モデル要素と図の組み合わせによっては、以下の手順を使用できない場合があります。

#### <a name="to-add-a-new-view-of-a-model-element-by-using-uml-model-explorer"></a>UML モデル エクスプローラーを使用してモデル要素の新しいビューを追加するには

1. To open **UML Model Explorer**, on the **Architecture** menu, point to **Windows**, and then click **UML Model Explorer**.

2. Drag the model element from **UML Model Explorer** to a compatible diagram in the same project.

     モデル要素のビューを表すシェイプが表示されます。これは、他の図または同じ図のビューに追加される形で表示される場合があります。

    > [!NOTE]
    > クラスまたはコンポーネントをシーケンス図にドラッグした場合、結果は異なります。 その場合は、そのクラスまたはコンポーネントと同じ型の新しい生存線が作成されます。 For more information, see [UML Sequence Diagrams: Guidelines](../modeling/uml-sequence-diagrams-guidelines.md).

#### <a name="to-add-a-new-view-of-a-model-element-by-using-paste-reference"></a>[参照の貼り付け] を使用してモデル要素の新しいビューを追加するには

1. Right-click an existing element, and then click **Copy**.

    - 複数の要素を同時にコピーすることができます。 Hold down the CTRL key while you click each element, right-click one of them, and then click **Copy**.

2. Right-click an empty part of a compatible diagram, and then click **Paste Reference**.

     同じ要素のもう 1 つのビューが表示されます。

    > [!NOTE]
    > This differs from the **Paste** command, which creates a new element in the model. For more information, see [Copying Elements and Groups of Related Elements](#Copying).

> [!NOTE]
> 既に特定の関係で接続されている 2 つのモデル要素から成る図のビューに対して追加した場合、その関係のビューも図に表示されます。 このビューを削除するには、要素の 1 つを図から削除するか、要素間の関係をモデルから削除します。

## <a name="Copying"></a> Copying Elements and Groups of Related Elements
 モデル要素はコピーして貼り付けることができます。また、要素のグループをその要素間の関係も含めてコピーして貼り付けることもできます。

> [!NOTE]
> The **Paste** and **Paste Reference** commands have different effects. **Paste** creates new elements whose properties are like those of the copied elements. **Paste Reference** creates new views of the same elements.

#### <a name="to-copy-elements-and-their-relationships"></a>要素とその関係をコピーするには

1. コピーする要素がある図で、1 つ以上の要素を選択します。

    > [!NOTE]
    > 要素のグループから関係だけを切り離してコピーすることはできません。

2. On the **Edit** menu, click **Copy**.

3. 要素を別の図にコピーする場合は、新しい図を作成するか、既存の図を開きます。

4. On the **Edit** menu, click **Paste**.

    - 要素のコピーが、要素間に存在するすべての関係のコピーと共に表示されます。

    - それぞれの新しい要素には、自動的に生成された新しい名前が付けられます。

5. 新しい要素と関係の位置や名前などのプロパティを調整します。

> [!NOTE]
> 2 つのモデルが同じソリューションに存在する場合などに、モデル間でモデル要素をコピーすることはできません。 しかし、1 つの図と別の図との間で要素をコピーすることはできます。

#### <a name="to-copy-an-entire-diagram"></a>図全体をコピーするには

1. 新しい図を作成します。

2. 既存の図のすべての要素を選択し、それらをコピーして、新しい図に貼り付けます。

   図の複製は、ソリューション エクスプローラーでコピーと貼り付けをして行うことはできません。

## <a name="Deleting"></a> Deleting a Model Element or its Views
 分類子などの特定の種類の要素は、モデルからは削除せず、図からのみ削除することができます。 分類子は、クラス図、コンポーネント図、およびユース ケース図に表示される主要な要素です。 複数の図に表示される場合もあります。 For these types of elements, there are two separate commands: **Remove from Diagram** and **Delete from Model**.

 一方、図から関係を削除すると、その関係は自動的にモデルからも削除されます。

> [!NOTE]
> UML 図の特定の種類の要素にはラベルがあります。 要素の周囲に四角形を描画して選択すると、ラベルを選択することはできますが、そのラベルを所有する要素は選択できません。 この方法で選択された要素のサブセットの削除はサポートされていません。 To select a subset of these elements, press and hold the **CTRL** key while you click each element.

#### <a name="to-remove-a-classifiers-view-from-a-diagram"></a>分類子のビューを図から削除するには

- Right-click the element on the diagram, and then click **Remove from Diagram**.

  \- または

- Click the element on the diagram and then press the **DELETE** key.

  - この要素のビューが削除されます。 However, the element remains in the model, and you can still find it in **UML Model Explorer**. 同じ要素の他のビューもすべて残っています。

  - このシェイプに接続されているコネクタはすべて図から削除されますが、それが表している関係はモデル内に残ります。 You can see the relationship in **UML Model Explorer** under **Relationships**, under each element that it connects.

#### <a name="to-delete-an-element-from-the-model"></a>モデルから要素を削除するには

- Right-click the element either in **UML Model Explorer** or on a diagram, and then click **Delete from Model**.

  - 要素は、表示されていたすべての図から削除されます。

  - この要素に接続されている関係もすべてモデルから削除されます。

#### <a name="to-delete-a-relationship-from-the-model"></a>モデルから関係を削除するには

- Right-click the relationship on a diagram or in **UML Model Explorer**, and then click **Delete from Model**.

    > [!CAUTION]
    > 関係をモデルからは削除せずに図からのみ削除することはできません。

     関係がモデルから削除され、それが表示されていたすべての図からも削除されます。

## <a name="presentation"></a> Preparing a Diagram for Presentation
 次に示す機能は、図の特定のパーツを強調する場合や、説明を追加する場合、または 1 つの図を複数の関心領域に分割する場合に役立ちます。

- 図の任意のパーツを Word や PowerPoint などのドキュメントにコピーできます。 Select the shapes and connectors you want, right-click and then click **Copy**.

- 任意のシェイプまたはコネクタの色を変更できます。 Select one or more shapes and change the **Color** property. **[プロパティ]** ウィンドウが表示されない場合は、**F4** キーを押します。

- On diagrams of some kinds, you can draw lines, rectangles and ellipses from the **Simple Shapes** section of the Toolbox. これらのシェイプは UML モデルの一部を形成するものではありません。

- To label an area, you can drag a Comment from the Toolbox and then set its **Transparent** property to **True**. 単純なシェイプと同様に、コメントは UML モデルの一部を形成するものではないため、UML モデル エクスプローラーには表示されません。

- モデル要素にメモおよび説明を追加するには、コメントを作成し、要素にリンクします。

### <a name="to-export-a-diagram-as-an-image"></a>ダイアグラムをイメージとしてエクスポートするには
 For more information, see [Export diagrams as images](../modeling/export-diagrams-as-images.md).

## <a name="extensions"></a> Extending the UML Designers
 UML ツールに新しい機能を追加し、各自のニーズに合わせてダイアグラムの表記を調整できます。 For more information, see [Extend UML models and diagrams](../modeling/extend-uml-models-and-diagrams.md).

## <a name="see-also"></a>参照
 [Create UML modeling projects and diagrams](../modeling/create-uml-modeling-projects-and-diagrams.md) [Analyzing and Modeling Architecture](../modeling/analyze-and-model-your-architecture.md) [Create models for your app](../modeling/create-models-for-your-app.md)
