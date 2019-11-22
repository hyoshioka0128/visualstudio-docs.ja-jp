---
title: Create layer diagrams from your code | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- architecture, layer diagrams
- layer diagrams
- diagrams - modeling, layer
- constraints, architectural
ms.assetid: 58c3ea71-2dbc-4963-bf82-40f1924cf973
caps.latest.revision: 64
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3e6cd77e785adb59fc8b2cf3b28724ed0efe1ae3
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300278"
---
# <a name="create-layer-diagrams-from-your-code"></a>コードからのレイヤー図の作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

To visualize your software system's high-level, logical architecture, create a *layer diagram* in Visual Studio. コードがこの設計と一致していることを確認するには、レイヤー図を使用してコードを検証します。 Visual C# .NET と Visual Basic .NET のプロジェクトのレイヤー図を作成できます。 To see which versions of Visual Studio support this feature, see [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)

 ![Create a layer diagram](../modeling/media/layerdiagramvisualizecode.png "LayerDiagramVisualizeCode")

 A layer diagram lets you organize Visual Studio solution items into logical, abstract groups called *layers*. レイヤーを使用して、これらの成果物が実行する主要タスク、またはシステムの主要コンポーネントを示すことができます。 各レイヤーには、より詳細なタスクを示す別のレイヤーを含めることができます。 You can also specify the intended or existing *dependencies* between layers. 矢印で表されるこれらの依存関係は、どのレイヤーが、他のレイヤーが表す機能を使用できるか、または現在使用しているかを示します。 コードのアーキテクチャ コントロールを保持するには、目的の依存関係を図で示し、図と照らし合わせてコードを検証します。

## <a name="CreateDiagram"></a> Create a layer diagram
 レイヤー図を作成する前に、ソリューションにモデリング プロジェクトがあることを確認します。 See [Create UML modeling projects and diagrams](../modeling/create-uml-modeling-projects-and-diagrams.md).

> [!IMPORTANT]
> モデリング プロジェクトから別のモデリング プロジェクトまたはソリューション内の別の場所への既存のレイヤー図の追加、ドラッグ、コピーは、いずれも実行しないでください。 これで、図を変更しても、元の図からの参照が保持されます。 また、これによってレイヤー検証が正しく機能しないため、要素が欠落したり、図を開こうとすると他のエラーが発生するなど、別の問題が生じる可能性があります。
>
> 代わりに、新しいレイヤー図をモデリング プロジェクトに追加してください。 元の図から新しい図へ要素をコピーします。 モデリング プロジェクトと新しいレイヤー図の両方を保存します。

#### <a name="to-add-a-new-layer-diagram-to-a-modeling-project"></a>新しいレイヤー図をモデリング プロジェクトに追加するには

1. On the **Architecture** menu, choose **New UML or Layer Diagram**.

2. Under **Templates**, choose **Layer Diagram**.

3. 図に名前を付けます。

4. In **Add to Modeling Project**, browse to and select an existing modeling project in your solution.

     -または-

     Choose **Create a new modeling project** to add a new modeling project to the solution.

    > [!NOTE]
    > レイヤー図はモデリング プロジェクト内に存在している必要があります。 ただし、ソリューション内のどの場所にある項目にもリンクできます。

5. 必ず、モデリング プロジェクトとレイヤー図の両方を保存してください。

## <a name="CreateLayers"></a> Create layers from artifacts
 レイヤーは、プロジェクト、コード ファイル、名前空間、クラス、メソッドなど、Visual Studio ソリューションの項目から生成できます。 これにより、レイヤーと項目の間のリンクが自動的に作成され、レイヤー検証プロセスに含まれます。

 Word 文書や PowerPoint プレゼンテーションなどの検証をサポートしない項目にレイヤーをリンクすることもできます。こうすると、仕様や計画にレイヤーを関連付けることができます。 複数のアプリが共有するプロジェクトのファイルにレイヤーをリンクすることもできます。ただし、これらのレイヤーは検証プロセスには含まれず、"レイヤー 1"、"レイヤー 2" などの汎用名で表示されます。

 To see if a linked item supports validation, open **Layer Explorer** and examine the **Supports Validation** property of the item. See [Managing links to artifacts](#Managing).

|**目的**|**Follow these steps**|
|------------|----------------------------|
|1 つの成果物を表すレイヤーを生成する|<ol><li>以下のソースからレイヤー図上へ項目をドラッグします。<br /><br /> <ul><li>**ソリューション エクスプローラー**<br /><br />         ファイルやプロジェクトなどをドラッグできます。</li><li>コード マップ<br /><br />         See [Map dependencies across your solutions](../modeling/map-dependencies-across-your-solutions.md) and [Use code maps to debug your applications](../modeling/use-code-maps-to-debug-your-applications.md).</li><li>**Class View** or **Object Browser**</li></ul><br />     レイヤーが図に表示され、成果物にリンクされます。</li><li>レイヤーの名前を、関連するコードや成果物の役割を表す名前に変更します。</li></ol> **Important:**  Dragging binary files to the layer diagram does not automatically add their references to modeling project. 検証するバイナリ ファイルを手動でモデリング プロジェクトに追加する必要があります。 **To add binary files to the modeling project** <ol><li>In **Solution Explorer**, open the shortcut menu for the modeling project, and then choose **Add Existing Item**.</li><li>In the **Add Existing Item** dialog box, browse to the binary files, select them, and then choose **OK**.     バイナリ ファイルがモデリング プロジェクトに表示されます。</li><li>In **Solution Explorer**, choose a binary file that you added, and then press **F4** to open the **Properties** window.</li><li>On each binary file, set the **Build Action** property to **Validate**.</li></ol>|
|選択したすべての成果物を表す 1 つのレイヤーを生成する|すべての成果物を同時にレイヤー図へドラッグします。<br /><br /> レイヤーが図に表示され、すべての成果物にリンクされます。|
|選択した各成果物を表すレイヤーを生成する|Press and hold the **SHIFT** key while you drag all of the artifacts to the layer diagram at the same time. **Note:**  If you use the **SHIFT** key to select a range of items, release the key after you select the artifacts. 成果物を図にドラッグするときは、キーを再び押して、押したままにします。 <br /><br /> 各成果物を表すレイヤーが図に表示され、各成果物にリンクされます。|
|成果物をレイヤーに追加する|成果物をレイヤーにドラッグします。|
|リンクされない新しいレイヤーを生成する|In the **Toolbox**, expand the **Layer Diagram** section, and then drag a **Layer** to the layer diagram.<br /><br /> 複数のレイヤーを追加するには、ツールをダブルクリックします。 When you are finished, choose the **Pointer** tool or press the **ESC** key.<br /><br /> または<br /><br /> Open the shortcut menu for the layer diagram, choose **Add**, and then choose **Layer**.|
|入れ子になったレイヤーを生成する|既存のレイヤーを別のレイヤー上へドラッグします。<br /><br /> または<br /><br /> Open the shortcut menu for a layer, choose **Add**, and then choose **Layer**.|
|複数の既存レイヤーを含む新しいレイヤーを生成する|Select the layers, open the shortcut menu for your selection, and then choose **Group**.|
|レイヤーの色を変更する|Set its **Color** property to the color that you want.|
|レイヤーに関連付けられている成果物を、指定した名前空間に所属させることができないように指定する|Type the namespaces in the layer's **Forbidden Namespaces** property. Use a semicolon ( **;** ) to separate the namespaces.|
|レイヤーに関連付けられている成果物が、指定した名前空間に依存できないように指定する|Type the namespaces in the layer's **Forbidden Namespace Dependencies** property. Use a semicolon ( **;** ) to separate the namespaces.|
|レイヤーに関連付けられている成果物を、指定した名前空間のいずれかに必ず所属させるように指定する|Type the namespace in the layer's **Required Namespaces** property. Use a semicolon ( **;** ) to separate the namespaces.|

 レイヤーの数字は、レイヤーにリンクされている成果物の数を示します。 ただし、この数値を読み取るときには、次の点に注意してください。

- 1 つのレイヤーが他の成果物を含む 1 つの成果物にリンクされているが、他の成果物に直接リンクされていない場合、その数字にはリンクされた成果物のみが含まれます。 ただし、レイヤー検証時の分析にはそれらの他の成果物も含まれます。

     たとえば、1 つのレイヤーが 1 つの名前空間にリンクされている場合、その名前空間に複数のクラスが含まれていても、リンクされた成果物の数は 1 です。 レイヤーに名前空間の各クラスへのリンクもある場合、その数字にはリンクされたクラスが含まれます。

- 1 つのレイヤーに成果物にリンクされた他のレイヤーが含まれている場合は、そのコンテナー レイヤーの数字にそれらの成果物が含まれていなくても、コンテナー レイヤーはそれらの成果物にリンクされます。

## <a name="Managing"></a> Manage links between layers and artifacts

1. On the layer diagram, open the shortcut menu for the layer, and then choose **View Links**.

     **Layer Explorer** shows the artifact links for the selected layer.

2. これらのリンクを管理するには、次の操作を行います。

|**目的**|**In Layer Explorer**|
|------------|---------------------------|
|レイヤーと成果物のリンクを削除する|Open the shortcut menu for the artifact link, and then choose **Delete**.|
|リンクを別のレイヤーに移動する|成果物のリンクを図上の既存のレイヤーにドラッグします。<br /><br /> または<br /><br /> 1.  Open the shortcut menu for the artifact link, and then choose **Cut**.<br />2.  On the layer diagram, open the shortcut menu for the layer, and then choose **Paste**.|
|リンクを別のレイヤーにコピーする|1.  Open the shortcut menu for the artifact link, and then choose **Copy**.<br />2.  On the layer diagram, open the shortcut menu for the layer, and then choose **Paste**.|
|既存の成果物のリンクから新しいレイヤーを生成する|成果物のリンクを図上の空白領域にドラッグします。|
|リンクされた成果物がレイヤー図に対する検証をサポートしていることを確認する|Look at the **Supports Validation** column for the artifact link.|

## <a name="Discovering"></a> Reverse-engineer existing dependencies
 依存関係が存在するのは、あるレイヤーに関連付けられている成果物が、別のレイヤーに関連付けられている成果物を参照している場合です。 たとえば、あるレイヤー内のクラスが、別のレイヤー内のクラスを保持する変数を宣言する場合などです。 図のレイヤーにリンクされている成果物の既存の依存関係はリバース エンジニアリングできます。

> [!NOTE]
> 成果物の種類によっては、依存関係をリバース エンジニアリングできないものもあります。 たとえば、テキスト ファイルにリンクされているレイヤーから、またはそのレイヤーに対して依存関係をリバース エンジニアリングすることはできません。 To see which artifacts have dependencies that you can reverse-engineer, open the shortcut menu for one or multiple layers, and then choose **View Links**. In **Layer Explorer**, examine the **Supports Validation** column. Dependencies will not be reverse-engineered for artifacts for which this column shows **False**.

- Select one or multiple layers, open the shortcut menu for a selected layer, and then choose **Generate Dependencies**.

  通常は、不要な依存関係がいくつか見つかります。 これらの依存関係を編集して、目的の設計に準拠するようアラインできます。

## <a name="EditDependencies"></a> Edit layers and dependencies to show the intended design
 システムに追加予定の変更または目的のアーキテクチャを示すには、レイヤー図を編集します。

|**目的**|**Perform these steps**|
|------------|-----------------------------|
|依存関係の方向を変更または制限する|Set its **Direction** property.|
|新しい依存関係を生成する|Use the **Dependency** and **Bidirectional Dependency** tools.<br /><br /> 複数の依存関係を描画するには、ツールをダブルクリックします。 When you are finished, choose the **Pointer** tool or press the **ESC** key.|
|レイヤーに関連付けられている成果物が、指定した名前空間に依存できないように指定する|Type the namespaces in the layer's **Forbidden Namespace Dependencies** property. Use a semicolon ( **;** ) to separate the namespaces.|
|レイヤーに関連付けられている成果物を、指定した名前空間に所属させることができないように指定する|Type the namespaces in the layer's **Forbidden Namespaces** property. Use a semicolon ( **;** ) to separate the namespaces.|
|レイヤーに関連付けられている成果物を、指定した名前空間のいずれかに必ず所属させるように指定する|Type the namespace in the layer's **Required Namespaces** property. Use a semicolon ( **;** ) to separate the namespaces.|

## <a name="EditLayout"></a> Change how elements appear on the diagram
 プロパティを編集して、レイヤーのサイズ、形状、色、位置、または依存関係の色を変更できます。

## <a name="Codemaps"></a> Discover patterns and dependencies on a code map
 While creating layer diagrams, you might also create **code maps**. これらの図を利用することで、コードを検証するときに、パターンと依存関係を見つけやすくなります。 ソリューション エクスプローラー、クラス ビュー、またはオブジェクト ブラウザーを使用して、アセンブリ、名前空間、およびクラスを調べることができます。これらは、通常は既存のレイヤーに対応しています。 コード マップについての詳細は、次を参照してください。

- [ソリューション間の依存関係をマップする](../modeling/map-dependencies-across-your-solutions.md)

- [コード マップを使用してアプリケーションをデバッグする](../modeling/use-code-maps-to-debug-your-applications.md)

- [コード マップ アナライザーを使用して潜在的な問題を検索する](../modeling/find-potential-problems-using-code-map-analyzers.md)

## <a name="see-also"></a>参照
 [Channel 9 Video: Design and validate your architecture using layer diagrams](https://go.microsoft.com/fwlink/?LinkID=252073) [Layer Diagrams: Reference](../modeling/layer-diagrams-reference.md) [Layer Diagrams: Guidelines](../modeling/layer-diagrams-guidelines.md) [Validate code with layer diagrams](../modeling/validate-code-with-layer-diagrams.md) [Visualize code](../modeling/visualize-code.md)