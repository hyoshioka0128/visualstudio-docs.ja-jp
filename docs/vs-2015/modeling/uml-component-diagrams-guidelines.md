---
title: 'UML Component Diagrams: Guidelines | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML diagrams, component
- diagrams - modeling, component
- diagrams - modeling, UML component
- UML, component diagrams
- component diagrams
ms.assetid: 6c1bdd60-369e-477e-83ed-7f6fe75c9f0b
caps.latest.revision: 37
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 99f2b67d264edcaab5272d0224d4450ee2e8a6f6
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297154"
---
# <a name="uml-component-diagrams-guidelines"></a>UML コンポーネント図: ガイドライン
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

In Visual Studio, you can draw a *component diagram* to show the structure a software system. For a video demonstration, see [Designing the Physical Structure by using Component Diagrams](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-6-designing-a-projects-physical-structure).

 この機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

 To create a UML component diagram, on the **Architecture** menu, click **New UML or Layer Diagram**.

 コンポーネントとは、環境内で置き換えることのできるモジュール式のユニットのことです。 Its internals are hidden, but it has one or more well-defined *provided interfaces* through which its functions can be accessed. A component can also have *required interfaces*. 要求インターフェイスは、他のコンポーネントに対して要求する機能またはサービスを定義します。 複数のコンポーネントの提供インターフェイスと要求インターフェイスを接続することで、より大規模なコンポーネントを構築できます。 完全なソフトウェア システムを 1 つのコンポーネントとして見なすことができます。

 コンポーネント図を描画することには、次のような利点があります。

- 設計を主要なブロックの観点から考察することは、開発チームが既存の設計を理解したり、新しい設計を生成したりするのに役立ちます。

- 正しく定義された提供インターフェイスおよび要求インターフェイスを持つコンポーネントのコレクションとしてシステムを見なすことで、それぞれのコンポーネントをより明確に分離して取り扱うことができます。 その結果、理解しやすい設計を実現でき、要求が変更されたときに容易に変更を加えることができるようになります。

  コンポーネント図を使用すると、設計で使用されている、または将来使用される予定の言語またはプラットフォームに関係なく、設計を表すことができます。

## <a name="OtherDiagrams"></a> Relationship to Other Diagrams
 コンポーネント図は他の図と共に使用できます。

|図の種類|確認できる設計の側面|
|-------------------|--------------------------------------------------------------------|
|UML シーケンス図|-   Interactions between a system's components<br />-   Interactions and between the parts inside a component.<br /><br /> For more information, see [UML Sequence Diagrams: Guidelines](../modeling/uml-sequence-diagrams-guidelines.md).|
|UML クラス図|-   The interfaces of a component. クラス図を使用すると、インターフェイスのメソッドを詳しく示すことができます。<br />-   The data sent in parameters across the components' interfaces.<br /><br /> For more information, see [UML Class Diagrams: Guidelines](../modeling/uml-class-diagrams-guidelines.md).|
|アクティビティ図|-   The internal processing performed by a component in response to incoming messages.<br /><br /> For more information, see [UML Activity Diagrams: Guidelines](../modeling/uml-activity-diagrams-guidelines.md).|
|レイヤー図|-   Logical architectural tiers for your components.<br /><br /> For more information, see [Layer Diagrams: Reference](../modeling/layer-diagrams-reference.md).|

## <a name="Basics"></a> Basic Steps for Drawing Component Diagrams
 For reference information about the elements on component diagrams, see [UML Component Diagrams: Reference](../modeling/uml-component-diagrams-reference.md).

 For more information about how to use component diagrams in the process of design, see [Model your app's architecture](../modeling/model-your-app-s-architecture.md).

> [!NOTE]
> Detailed steps for creating any of the modeling diagrams are described in [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md).

#### <a name="to-create-a-component-diagram"></a>コンポーネント図を生成するには

1. On the **Architecture** menu, click **New UML or Layer Diagram**.

2. Under **Templates**, click **UML Component Diagram**.

3. 図に名前を付けます。

4. In **Add to Modeling Project**, select an existing modeling project in your solution, or **Create a New Modeling Project**, and then click **OK**..

     A new component diagram appears with the UML **Component Diagram** toolbox. ツールボックスには、必要な要素および関係が含まれています。

### <a name="drawing-components"></a>コンポーネントの描画
 ![Components with interfaces](../modeling/media/uml-compdrawing.png "UML_CompDrawing")

 Create a *component* (1) for each major functional unit in your system or application.

 たとえば、アプリケーション、ハードウェア デバイス、Web サービス、.NET アセンブリ、プログラム クラス、クラス グループ、プログラムの分離可能なセグメントなどがこれに該当します。

##### <a name="to-create-components"></a>コンポーネントを生成するには

1. Click **Component** in the toolbox, and then click a blank part of the diagram.

     \- または

     既存のコンポーネントをコピーし、貼り付けます。

    1. Find an existing component in a diagram or in **UML Model Explorer**.

    2. Right-click the component and then click **Copy**.

    3. コピーしたコンポーネントを貼り付ける図を開きます。

    4. Right-click a blank part of the diagram and then click **Paste**.

         新しい名前が付けられたコンポーネントが表示されます。

2. コンポーネントの名前をクリックし、変更します。

3. コンポーネントのヘッダーのみを表示するには、シェブロン (5) をクリックします。

### <a name="showing-the-ports-of-a-component"></a>コンポーネントのポートの表示
 A *port* (2, 3) represents a group of messages or operation calls that pass either into or out of a component. このグループは、ポートの型を定義するインターフェイスによって記述されます。 ポートは、インターフェイスを提供するか、またはインターフェイスを要求することができます。

 A port with a *provided interface* (2) supplies operations that are implemented by the component, and that can be used by other components.

 たとえば、ユーザー インターフェイス、Web サービス、.NET インターフェイス、任意のプログラミング言語の関数のコレクションなどがこれに該当します。

 A port with a *required interface* (3) represents a component's requirement for a group of operations or services to be provided by other components or external systems.

 たとえば、Web ブラウザーの場合は Web サーバーが求められ、アプリケーション アドインの場合はアプリケーションからのサービスが求められます。

 1 つのコンポーネントは任意の数のポートを持つことができます。

##### <a name="to-add-ports-to-a-component"></a>ポートをコンポーネントに追加するには

1. In the toolbox, click **Provided Interface** or **Required Interface**.

2. ポートを追加するコンポーネントをクリックします。

    コンポーネントの境界上にポートが表示されます。

    新しいインターフェイスがポートの型として生成されます。 This interface appears in **UML Model Explorer**.

3. コンポーネント境界上でポートをドラッグして、目的の位置に配置します。

4. ポートのラベルをドラッグしてその位置を調整します。

5. ラベルをクリックし、変更します。 ラベルは、インターフェイスの名前を示します。 ラベルを変更することは、インターフェイスの名前を変更することになります。

   インターフェイスの属性と操作を一覧表示する場合は、UML モデル エクスプローラーのインターフェイスに追加すると表示できます。 または、UML モデル エクスプローラーからインターフェイスをクラス図にドラッグし、そこで操作と属性を追加することもできます。

### <a name="linking-between-components"></a>コンポーネント間のリンクの設定
 依存関係 (4) は、あるコンポーネントの要求を他のコンポーネントによって提供される操作またはサービスで満たすことができることを示すために使用します。

##### <a name="to-show-that-a-provided-interface-can-satisfy-a-required-interface"></a>提供インターフェイスが要求インターフェイスの要求を満たすことを示すには

1. In the toolbox, click **Dependency**.

2. 最初に操作またはサービスを要求するコンポーネント上の要求インターフェイスを持つポートをクリックし、次に操作またはサービスを提供するコンポーネントの提供インターフェイスを持つポートをクリックします。

   グループ内のすべてのコンポーネントが他のすべてのコンポーネントに依存するような依存関係ループを設計しないように注意してください。

##### <a name="to-add-a-port-for-an-existing-interface-to-a-component"></a>既存のインターフェイスのポートをコンポーネントに追加するには

- Find the interface in **UML Model Explorer** and then drag it from there onto the component.

     -または-

- インターフェイスへの参照を図からコピーし、貼り付けます。

    1. On a class diagram or a component diagram, right-click the interface and then click **Copy**.

    2. On the component diagram, right-click the component, and then click **Paste Reference**.

         提供インターフェイスがコンポーネント上に表示されます。 隣にアクション タグが表示されます。

        > [!NOTE]
        > If you use **Paste** instead of **Paste Reference**, a new interface that has a new name will be created.

    3. If you wanted to create a required interface, click the Action tag and then click **Convert to Required Interface**.

## <a name="Parts"></a> Showing the Internal Parts of a Component
 ![Component diagram showing internal parts](../modeling/media/uml-compshowing.png "UML_CompShowing")

 コンポーネントが相互に対話するより小規模なコンポーネントから構成されることを示すために、パート (3) をコンポーネント (1) 内に配置できます。

 この例の図は、Dinner Now Web Service 型のすべてのインスタンスに、Customer Server の 1 つのインスタンスと Kitchen Server の 1 つのインスタンスが含まれていることを示しています。

 パートは、通常のクラスに属する属性に似た、親コンポーネントのプロパティです。 パートは、独自の型を持ちます。通常はこれもコンポーネントです。 パートのラベルは、通常の属性と同じ形式を持ちます。

 `+ partName : TypeName`

 親コンポーネント内の各パートは、その型 (4、5) に対して定義されている提供インターフェイスおよび要求インターフェイスを示します。 あるパートで必要とされる操作またはサービスを別のパートが提供できます。 You can use **Part Assembly** connectors to show how parts are connected with one another (6).

 また、親コンポーネントのインターフェイスがそのいずれかのパートによって実際に提供または要求されることを示すこともできます。 You can connect a port of the parent to a port of an internal part using a **Delegation** relation (9). 2 つのポートは同じ種類 (提供ポートまたは要求ポート) である必要があり、インターフェイス型に互換性がある必要があります。

 新しい型または既存の型の新しいパートを生成できます。

#### <a name="to-add-parts-to-a-component"></a>パートをコンポーネントに追加するには

1. 親コンポーネントの構成要素と考える主要な機能ユニットごとにパートを生成します。

    1. Click **Component** in the toolbox, and then click inside the parent component (1).

         親コンポーネントの内側に新しいパート (3) が表示されます。

         A new component is created in **UML Model Explorer**. これが、新しいパートの型です。

         \- または

         既存のコンポーネントを UML モデル エクスプローラーから親コンポーネント上にドラッグします。

         親コンポーネントの内側に新しいパート (3) が表示されます。 その型は、UML モデル エクスプローラーからドラッグしたコンポーネントです。

         \- または

         Right-click a component, either in a diagram or in UML Model Explorer, and then click **Copy**.

         Right-click on the parent component, and then click **Paste Reference**.

         親コンポーネントの内側に新しいパート (3) が表示されます。 その型は、コピーしたコンポーネントです。

    2. 新しいパートの名前をクリックし、変更します。 型を変更することはできません。

    3. 提供インターフェイスと要求インターフェイス (4、5) を新しいパートに追加できます。 Click the **Provided Interface** or **Required Interface** tool, and then click in the part.

         \- または

         Drag an existing interface from **UML Model Explorer** onto the part.

         インターフェイスがパートの型に追加され、パート上に表示されます。 必要に応じて、親コンポーネントのサイズが調整されます。

2. パートを相互に接続します。

    - Use the **Dependency** tool to connect the ports of different parts (6).

3. パートを親コンポーネントのポートに接続します。

    1. 親コンポーネント上に 1 つ以上のポート (7) を生成します。 Click **Required Interface** or **Provided Interface** on the toolbox, and then click the parent component.

    2. ポートを 1 つ以上のパートに委譲 (9) します。 Click the **Delegation** tool, then a port on the parent component, and then a port on a part. 同じ方法で、インターフェイスを提供または要求するポートを接続できます。

### <a name="showing-the-parts-of-a-part"></a>パートの内部パートの表示
 コンポーネントをパートに分解した後、各パート型をそれに固有の内部パートに分解できます。

 各層の分解を別々のコンポーネント図で行うと作業が簡単です。 最初に、パートの型を見つける必要があります。 たとえば、この図の 1 つのパートは `DNCustomerServer` という名前を持ち、その型は `CustomerServer` という名前のコンポーネントです。 この型を UML モデル エクスプローラー内で見つけ、別の図に配置することができます。 これにより、それに固有の内部パートを生成できます。

##### <a name="to-place-a-parts-type-on-a-diagram"></a>パートの型を図に配置するには

1. パートの型の完全修飾名を確認します。

     Right-click the part and then click **Properties**.

     The type name appears in the **Type** field of the Properties window.

2. Locate the part's type in **UML Model Explorer**.

     Click **View**, point to **Other Windows**, and then click **UML Model Explorer**.

     プロジェクトを展開し、必要に応じて型が属しているパッケージを展開します。

     The type will be listed as a **Component**.

     必要に応じて、ここで名前を変更できます。

3. 別のコンポーネント図を開くかまたは生成します。

4. UML モデル エクスプローラーから図上に型をドラッグします。

     型のビューが、図内でコンポーネントとして表示されます。

     これは、パートに対して定義したのと同じインターフェイスを持ちます。

     この段階で、その内部にパートを追加できます。

## <a name="Designing"></a> Designing the Component

### <a name="describing-how-the-parts-collaborate"></a>パートのコラボレーションの記述
 シーケンス図を描画して、親コンポーネントが受信するメッセージに対する応答においてパートがどのように連携して動作するかを示すことができます。

 これらの図は、既存のコンポーネントを説明するため、および新しいコンポーネントを設計するために使用できます。

 コンポーネントを設計している途中であれば、配置するパートを決定する前にシーケンス図を描画できます。 シーケンス図を使用して、さまざまなパート、要求インターフェイス、およびメッセージ シーケンスを試すことができます。 最も頻繁に発生する最も重要な受信メッセージを対象に、シーケンス図を描画します。 これにより、決定した生存線に対応するパートをコンポーネント内に生成できます。

 シーケンス図を使用して、どのようにシステムの処理を複数の異なるコンポーネントに配分するかを評価します。

- 1 つのパートが担当する処理があまりに多い場合、処理を均等に配分した場合に比べて、アプリケーションの更新が困難になります。

- 処理を少しずつ多数の相互作用に配分した場合、システムのパフォーマンスが低下し、システムを理解するのが困難になります。

  ![Sequence diagram showing collaborating parts](../modeling/media/uml-compdescparts.png "UML_CompDescParts")

##### <a name="to-draw-a-sequence-diagram-that-shows-collaboration-between-parts"></a>パート間のコラボレーションを示すシーケンス図を描画するには

1. 新しいシーケンス図を生成します。

     For more information, see [UML Sequence Diagrams: Guidelines](../modeling/uml-sequence-diagrams-guidelines.md).

2. このコンポーネントにメッセージを送信する外部コンポーネント、ユーザー、デバイス、またはその他のアクター (1) の生存線を生成します。

     You can set the **Actor** property of this lifeline to true, to indicate that it is external to the component under consideration. 生存線の上にスティック図形が表示されます。

3. 選択したアクターからメッセージが送信されるこのコンポーネントの提供インターフェイス (2) の生存線を生成します。

4. コンポーネントの各パート (3) の生存線を生成します。

5. コンポーネントの要求インターフェイス (4) の生存線を生成します。

6. 外部アクター (5) からのメッセージを描画します。 メッセージがどのようにパートに渡されるか、およびパートがどのように連携してメッセージに応答するかを示します。

7. 必要に応じて、要求インターフェイス (6) に送信されるメッセージを示します。 メッセージの実行の詳細は省略してください。

### <a name="is-the-component-more-than-its-parts"></a>コンポーネントとそのパートの役割の重要性の相違
 場合によっては、コンポーネントはパートのコレクションに与えられた名前にすぎません。 すべての処理はパートによって実行され、実行時にはコンポーネントを表すコードまたはその他の成果物はありません。

 You can indicate this in the model by setting the **Is Indirectly Instantiated** property of the component. この場合、すべてのコンポーネントのインターフェイスがポート上にあり、内部パートへの委譲が設定されている必要があります。

### <a name="describing-the-process-inside-each-part"></a>各パート内のプロセスの記述
 アクティビティ図を使用すると、コンポーネントがそれぞれの受信メッセージをどのように処理するかを示すことができます。 For more information, see [UML Activity Diagrams: Guidelines](../modeling/uml-activity-diagrams-guidelines.md).

 ![Activity diagram with data buffer](../modeling/media/uml-compdescribingproc.png "UML_CompDescribingProc")

 イベント受理アクション (1) を使用して、受信メッセージによって新しいスレッドが開始されることを示します。

 オブジェクト ノードおよび入出力ピンを使用して、情報の流れと、情報が格納される場所を示します。 この例のオブジェクト ノード (2) は、スレッド間でバッファリングされる項目を示します。

### <a name="defining-data-and-classes"></a>データおよびクラスの定義
 UML クラス図を使用することで、次の項目の詳細な内容を記述できます。

- コンポーネントのインターフェイス。 必要な、または用意されているポートをコンポーネントに追加すると、インターフェイスが UML モデル エクスプローラーに表示されます。 これを UML クラス図にドラッグまたはコピーして、その属性と操作、および他のインターフェイスとの関係を示すことができます。

- インターフェイスの操作のパラメーターで渡されるデータ。

- アクティビティ図のオブジェクト フローに示されるようなコンポーネントに格納されているデータ。

### <a name="general-dependencies-between-components"></a>コンポーネント間の一般的な依存関係
 コンポーネント図を使用して、設計の主要な構成要素とその相互依存関係のみを示すことができます。

 ![A dependency between components](../modeling/media/uml-compdepend.png "UML_CompDepend")

 Use the **Dependency** tool to draw a dependency. これは、あるコンポーネントの設計が他のコンポーネントに依存することを示します。

 依存関係の代表的な例を次に示します。

- あるコンポーネントが、他のコンポーネント内のコードを呼び出す。

- あるコンポーネントが、他のクラス内で定義されているクラスをインスタンス化する。

- あるコンポーネントが、他のコンポーネントによって生成された情報を使用する。

  依存関係矢印の名前を使用して、特定の用途を表すことができます。 To set the name, right-click the arrow, then click **Properties**, and set the **Name** field in the properties window.

## <a name="see-also"></a>参照
 [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md) [UML Component Diagrams: Reference](../modeling/uml-component-diagrams-reference.md) [UML Sequence Diagrams: Reference](../modeling/uml-sequence-diagrams-reference.md) [UML Use Case Diagrams: Reference](../modeling/uml-use-case-diagrams-reference.md) [UML Class Diagrams: Reference](../modeling/uml-class-diagrams-reference.md) [UML Component Diagrams: Reference](../modeling/uml-component-diagrams-reference.md) [Video: Designing the Physical Structure by using Component Diagrams](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-6-designing-a-projects-physical-structure)
