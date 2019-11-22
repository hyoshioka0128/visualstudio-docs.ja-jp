---
title: 'UML Activity Diagrams: Guidelines | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML diagrams, activity
- diagrams - modeling, activity
- diagrams - modeling, UML activity
- activity diagrams
- UML, activity diagrams
ms.assetid: fe5dbe96-79ab-483a-b9bc-44d0d1d3efc2
caps.latest.revision: 50
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 692859008891439e4af3d751306bfd3ee6d351e8
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298989"
---
# <a name="uml-activity-diagrams-guidelines"></a>UML アクティビティ図: ガイドライン
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio では、アクティビティ図を描画することによって、ビジネス プロセスやソフトウェア アルゴリズムを一連のアクションのワークフローとして表すことができます。 ユーザー、ソフトウェア コンポーネント、またはデバイスが、これらのアクションを実行できます。 For a video demonstration, see: [Capture Business Workflows by using Activity Diagrams](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-4-capture-business-workflows).

 この機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

 To create a UML activity diagram, on the **Architecture** menu, click **New UML or Layer Diagram**.

 アクティビティ図は、以下のようなさまざまな目的に使用できます。

- ビジネス プロセス、またはユーザーとシステム間のワークフローを示す。 For more information, see [Model user requirements](../modeling/model-user-requirements.md).

- ユース ケースで実行される手順を示す。 For more information, see [UML Use Case Diagrams: Guidelines](../modeling/uml-use-case-diagrams-guidelines.md).

- ソフトウェアでのメソッド、関数、または操作を示す。 For more information, see [Model your app's architecture](../modeling/model-your-app-s-architecture.md).

  アクティビティ図を描画することは、プロセスの改善につながります。 既存のプロセスの図が非常に複雑であることが分かったら、どのようにすればプロセスを単純化できるかを検討してください。

  For reference information about the elements on activity diagrams, see [UML Activity Diagrams: Reference](../modeling/uml-activity-diagrams-reference.md).

## <a name="Relationships"></a> Relationship to Other Diagrams
 ビジネス プロセス、またはユーザーがシステムを使用する方法を表すアクティビティ図を描画する場合は、ユース ケース図を描画することにより、同じ情報を異なる観点で示すことができます。 ユース ケース図では、アクションをユース ケースとして描画します。 ユース ケースには、対応するアクションと同じ名前を付けます。 ユース ケース ビューのメリットは、次の操作ができることです。

- 大規模なアクション/ユース ケースが、小規模なアクション/ユース ケースでどのように構成されるかを、Includes リレーションシップを使用して 1 つの図で示す。

- 各アクション/ユース ケースを、その実行に関連するユーザーまたは外部システムに明示的に接続する。

- システムまたはその各主要コンポーネントでサポートされているアクション/ユース ケースの周囲に境界線を描画する。

  アクティビティ図を描画することにより、ソフトウェア操作の詳細設計を示すこともできます。

  アクティビティ図では、アクション間で渡されるデータのフローを示すことができます。 See the section on [Describing Data Flow](#DataFlows). ただし、アクティビティ図はデータの構造を表すわけではありません。 そのためには、UML クラス図を描画します。 For information see [UML Class Diagrams: Guidelines](../modeling/uml-class-diagrams-guidelines.md).

## <a name="BasicSteps"></a> Basic Steps for Drawing Activity Diagrams
 Detailed steps for creating any of the modeling diagrams are described in [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md).

#### <a name="to-draw-an-activity-diagram"></a>アクティビティ図を描画するには

1. On the **Architecture** menu, click **New UML or Layer Diagram**.

2. Under **Templates**, click **UML Activity Diagram**.

3. 図に名前を付けます。

4. In **Add to Modeling Project**, select an existing modeling project in your solution, or **Create a New Modeling Project**.

#### <a name="to-draw-elements-on-an-activity-diagram"></a>アクティビティ図の要素を描画するには、次のようにします。

1. ツールボックスから図へ要素をドラッグします。

     まず、図にメイン アクティビティを配置し、それらを接続した後、開始ノードや終了ノードなどの最後の仕上げを追加します。

    > [!NOTE]
    > UML モデル エクスプローラーから図へ既存の要素をドラッグすることはできません。

2. 要素を接続するには、次の手順に従います。

    1. In the **Activity Diagram** toolbox, click **Connector**.

    2. 図で、ソース要素をクリックします。

    3. ターゲット要素をクリックします。

        > [!NOTE]
        > ツールを複数回使用するには、ツールボックス内のツールをダブルクリックします。

#### <a name="to-move-an-activity-to-another-package"></a>アクティビティを別のパッケージに移動するには、次のようにします。

- In **UML Model Explorer**, drag the activity into a package.

     \- または

- In **UML Model Explorer**, right-click the activity and click **Cut**. Then right-click the package and click **Paste**.

    > [!NOTE]
    > アクティビティが UML モデル エクスプローラーに表示されるのは、最初の要素を図に追加するときのみです。

## <a name="SimpleControlFlow"></a> Describing Control Flow
 アクティビティ図は、ビジネス プロセスまたはソフトウェア アルゴリズムを一連のアクションとして表します。 コネクタの矢印は、あるアクションから次のアクションにどのように制御が連続的に渡されるかを示します。 通常、アクションは前のアクションが完了した後でなければ開始できません。

 次の図は、アクションのシーケンスをアクション、コネクタ、分岐、およびループでどのように示すことができるかという例です。 各要素については、後のセクションで詳しく説明します。

 ![A simple activity diagram](../modeling/media/uml-actguidectrl.png "UML_ActGuideCtrl")

 Activity diagrams use **Actions** and **Connectors** to describe your system or application as a series of actions with the control flowing sequentially from one action to the next.

- Create an **Action** (1) for each major task that is performed by a user, the system, or both in collaboration.

  > [!NOTE]
  > プロセスまたはアルゴリズムをごくわずかのアクションで記述するようにしてください。 You can use **Call Behavior Actions** to define each action in more detail in a separate diagram, as described in [Describing Sub-activities with Call Behavior Actions](#Subactivities).

- 各アクションのタイトルは、アクションによって通常得られることを明確に示すタイトルになるようにしてください。

- Link the actions in sequence with **Connectors** (2).

- それぞれのアクションが終了してから、制御フロー内の次のアクションが始まります。 If you want to describe actions that overlap, use a **Fork Node** as described in the section [Concurrent Flows](#Concurrent).

  図はアクションのシーケンスを表しますが、アクションの実行方法や、あるアクションから次のアクションへの制御の渡し方を示すわけではありません。 図を使用してビジネス プロセスを表す場合は、たとえば、あるユーザーが別のユーザーに電子メール メッセージを送信したら、制御を渡すことができます。 図を使用してソフトウェア設計を表す場合は、通常の実行フローによって、あるステートメントから次のステートメントに制御を渡すことができます。

### <a name="describing-decisions-and-loops"></a>判断とループの記述

- Use a **Decision Node** (3) to indicate a point where the outcome of a decision dictates the next step. 必要な数だけ出力パスを描画できます。

- アクティビティ図を使用してアプリケーションの一部を定義する場合は、各パスがいつ必要かが明確になるように、ガード (4) を定義する必要があります。 Right-click the connector, click **Properties**, and in the **Properties** window, type a value for the **Guard** field.

- ガードを常に定義する必要はありません。 たとえば、アクティビティ図を使用してビジネス プロセスまたは相互作用プロトコルを表す場合は、ユーザーまたは相互作用コンポーネントに対してオープンなオプションの範囲を分岐で定義します。

- Use a **Merge Node** (5) to bring together two or more alternative flows that branched at a **Decision Node**.

    > [!NOTE]
    > You should use a **Merge Node** to bring together alternative flows, instead of bringing the flows together at an action. In the example, it would not be correct to connect from the decision node directly back to **Choose Menu Item**. アクションが開始されるのは、その受信コネクタに制御のスレッドが到着してからになるためです。 そのため、アクションでまとめるのは、同時実行フローのみにする必要があります。 For more information, see [Concurrent Flows](#Concurrent).

- 例に示すように、分岐を使用してループを表します。

    > [!NOTE]
    > プログラム コードの場合と同様に、適切な構造でループを入れ子にしてください。 既存のビジネス プロセスを記述していくと、そのビジネス プロセスを改善できる機会がいくつか明らかになることがあります。

### <a name="starting-the-activity"></a>アクティビティの開始
 アクティビティへのエントリ ポイントを示すには、次の 2 とおりの方法があります。

- **Initial Node**

     Create one **Initial Node** (6) to indicate the first action of the activity.

     この方法は、サブアクティビティを記述するときや、何がアクティビティを開始するかを明示的に示す必要がない場合に最も有用です。 たとえば、"Order a Meal" というアクティビティは、顧客が空腹になったときに明確に開始されます。

- **Accept Event Node**

     Create **Accept Event Nodes**, as described in the section [Concurrent Flows](#Concurrent), to indicate the start of a thread that responds to a particular event, such as a user input. ノードに入力フローを接続しないでください。 入力フローを省略した場合は、イベントが発生するたびにスレッドが開始されることを示します。

     この方法は、特定の外部イベントへの応答を記述するときに最も有用です。

### <a name="ending-the-activity"></a>アクティビティの終了
 Use an **Activity Final Node** (7) to indicate the end of an activity.

- When a thread of control reaches an **Activity Final Node**, all the activity's concurrent actions and sub-activities terminate.

- アクティビティ終了ノードを複数使用することで、追加コネクタの煩雑さを軽減できます。

### <a name="interrupting-the-activity"></a>アクティビティの中断
 たとえば、ユーザーがプロセスを取り消すことにした場合、どうすればアクティビティの通常フローを中断できるかを記述するには、そのイベントをリッスンするイベント受理ノードを作成します。 For more information, see the section [Concurrent Flows](#Concurrent). それからアクティビティ終了ノード (7) への制御フローを作成します。

### <a name="swimlanes"></a>スイムレーン
 アクティビティのアクションを、アクションを実行する異なるオブジェクトまたはビジネス ロールに対応する領域に配置すると好都合な場合があります。 These areas are conventionally arranged in columns and are called *swimlanes*.

- Use lines or rectangles from the **Simple Shapes** section of the Toolbox to draw swimlanes or other areas.

- To label each swimlane, create a comment and set its **Transparent** property to **True**.

  単純なシェイプは UML モデルの一部を形成しないため、UML モデル エクスプローラーには表示されません。

## <a name="DataFlows"></a> Describing Data Flow
 アクティビティとの間のデータの受け渡しを、次の 2 とおりの方法のいずれかで記述できます。

- Use an **Object Node**. これは、アクティビティ間を流れる情報を記述する最も簡単な方法です。 オブジェクト ノードは、プログラムにおける変数のようなものです。 あるアクションから別のアクションへ渡される 1 つ以上の値を格納するものを表します。

- Use an **Output Pin** and an **Input Pin**. この方法を使用すると、あるアクションからの出力と別のアクションへの入力を別々に記述できます。 ピンはプログラムにおけるパラメーターのようなものです。 ピンは、オブジェクトがアクションに出入りできるポートを表します。

    > [!NOTE]
    > For an overview of the elements used in this section, see the Data Flows section of the topic see [UML Activity Diagrams: Reference](../modeling/uml-activity-diagrams-reference.md).

### <a name="describing-data-flow-with-object-nodes"></a>オブジェクト ノードを使用したデータ フローの記述
 ほとんどの制御フローはデータを運びます。 たとえば、"Customer provides details" アクションからの出力フローは、出荷先住所への参照を運びます。

 そのデータを図に記述するには、次の図に示すように、コネクタを 1 つのオブジェクト ノードと 2 つのコネクタに置き換えます。

 ![Object nodes can show data passed between actions](../modeling/media/uml-actguidedata.png "UML_ActGuideData")

 Dispatch Goods などの角が丸い四角形は、処理がなされるアクションを表します。 Shipment Address などの角が直角の四角形は、あるアクションから別のアクションへのオブジェクトのフローを表します。

 アクション間を流れるオブジェクトのコンジットまたはバッファーとしてのノードのロールを反映した名前を、オブジェクト ノードに付けます。

 You can set the **Type** of the object node in the Properties window. 型としては、整数などのプリミティブ型、またはクラス図で定義したクラス、インターフェイス、列挙を使用できます。 たとえば、Street Address、City などの属性を持つ Shipment Address というクラスを、Customer という名前の別のクラスへの関連付けと一緒に作成することもできます。 For more information, see [UML Class Diagrams: Guidelines](../modeling/uml-class-diagrams-guidelines.md).

> [!NOTE]
> If you type the name of a type that has not yet been defined, an item will be added under **Unspecified Types** in UML Model Explorer. その名前の型を後でクラス図で定義する場合は、新しい型を参照するようにオブジェクト ノードの型を再設定する必要があります。

#### <a name="buffering-data-in-object-nodes"></a>オブジェクト ノードでのデータのバッファリング
 オブジェクト ノードは、複数のオブジェクトのバッファーの働きをすることができます。 次の図の制御フローは、ユーザーは [choose more] ループ (1) を何度も回ることができ、その間 Chosen Menu Items オブジェクト ノード (2) はユーザーが選択したものを蓄積することを示しています。 最後に、ユーザーが自分の選択を完了すると、制御は Confirm Order アクション (3) に渡され、このアクションは選択された項目の完全なリストを Chosen Menu Items バッファーから受け取ります。

 ![Buffering data in object nodes](../modeling/media/uml-actguidebuffer.png "UML_ActGuideBuffer")

 オブジェクト ノードのプロパティを設定することにより、バッファー内の項目の格納方法を指定できます。次のようにします。

- Set the **Ordering** property:

  - **Unordered** to specify a random or unspecified order. (既定値。)

  - **Ordered** to specify an order according to a specific key.

  - **Fifo** to specify an order of first-in, first-out.

  - **Lifo** to specify an order of last-in, first-out.

- Set the **Upper Bound** property to specify the maximum number of objects that can be contained in the buffer. 既定値は * です。 これは、制限がないことを意味します。

### <a name="describing-data-flow-with-input-and-output-pins"></a>入力ピンと出力ピンを使用したデータ フローの記述
 Use an **Output Pin** and an **Input Pin** to separately describe the outputs from one action and the inputs to another.

 ![Input and output pins are action parameters](../modeling/media/uml-actguidepins.png "UML_ActGuidePins")

 To create a pin, click **Input Pin** or **Output Pin** on the toolbox and then click an action. その後、ピンをアクションの周囲に移動して、その名前を変更することができます。 You can create input and output pins on any kind of action, including **Call Behavior Actions**, **Call Operation Actions**, **Send Signal Actions**, and **Accept Event Actions**.

 2 つのピンの間のコネクタは、オブジェクト ノードへのフローやオブジェクト ノードからのフローと同じように、オブジェクト フローを表します。

 各ピンには、それが生成したり受け取ったりするオブジェクトのロールを示す、パラメーター名などの名前を付けます。

 You can set the type of objects transmitted in the **Type** property. これは、UML クラス図を作成した型であることが必要です。

 接続されたピンの間を流れる各オブジェクトには、何らかの形で互換性がなければなりません。 たとえば、出力ピンによって生成されたオブジェクトは、入力ピンの型の派生型に属するからです。

 もう 1 つの方法として、出力ピンの型と入力ピンの型の間でデータを変換する変換がオブジェクト フローに含まれることを指定することもできます。 この種の最も一般的な変換は、大きい方の型から適切な部分を抽出するだけです。 図の例は、注文の詳細から出荷先住所を抽出する変換の存在を示しています。

## <a name="Details"></a> Defining an Action in More Detail
 アクションの名前を使用してそのアクションによって通常得られるべき結果を明確にすることに加えて、さらに詳細をアクションに追加できる次の方法があります。

- Write a more detailed description in the **Body** property. たとえば、プログラム コードまたは擬似コードの一部や、得られる結果の詳細な説明を書き込むこともできます。

- アクションを振る舞い呼び出しアクションに置き換え、その詳細な振る舞いを別個のアクティビティ図内で記述する。 See [Describing Sub-activities with Call Behavior Actions](#Subactivities).

- Set the action's **Local Postconditions** and **Local Preconditions** properties to describe its outcome in more specific detail. For more information, see [Defining Postconditions and Preconditions](#Postcondition).

### <a name="Subactivities"></a> Describing Sub-activities with Call Behavior Actions
 別個のアクティビティ図を使用して、アクションの詳細な振る舞いを記述できます。 呼び出される振る舞いは、振る舞い呼び出しアクションによってメイン アクティビティ図に表されるアクティビティ図です。 振る舞い呼び出しアクションを使用して、異なるアクティビティ間で共有される振る舞いを記述することもできます。これにより、サブアクティビティを複数回描画する必要がなくなります。

 次の図において、図 1 は、振る舞い呼び出しアクションのあるアクティビティを示しており、図 2 は、呼び出される振る舞いを表すサブアクティビティ図を示しています。

 ![A separate activity diagram shows detailed actions](../modeling/media/uml-actguidedetail.png "UML_ActGuideDetail")

##### <a name="to-describe-a-sub-activity-with-a-call-behavior-action"></a>振る舞い呼び出しアクションを使用してサブアクティビティを記述するには

1. To create the diagram for the sub-activity, in **Solution Explorer**, right-click your modeling project, point to **Add**, and then click **New Item**.

2. In the **Add New Item** dialog box, under **Templates** click **Activity Diagram** and in the **Name** box type the name that you plan to give your **Call Behavior Action**.

3. サブアクティビティの詳細なワークフローを描画します。 これは、呼び出される振る舞いです。

    - In the called sub-activity diagram, the **Initial Node** indicates where control starts when the called behavior is invoked. The **Activity Final Node** shows where control should return to the parent activity.

4. Set the **Behavior** property of the **Call Behavior Action** to refer to the called behavior diagram.

    > [!NOTE]
    > The sub-activity diagram must have some elements on it or the diagram will not be available in the drop-down list for the **Behavior** property. Also, the trident icon will not appear on your **Call Behavior Action** shape until you set its **Behavior** property.

5. Set the **Is Synchronous** property of the action to indicate whether your activity waits for the called activity to complete.

    - If you set **Is Synchronous** to false, you are indicating that the flow can continue to the next action before the called activity finishes. 出力ピンは定義すべきではありません。定義すると、アクションから送信データが流れる結果となります。

### <a name="describing-data-flow-in-and-out-of-sub-activities"></a>サブアクティビティとの間のデータ フローの記述
 ソフトウェアでパラメーターを使用するのと同じように、サブアクティビティに出入りするデータを記述できます。

- 呼び出される振る舞いアクションに、アクションに出入りするデータごとに、入出力ピン (1) を作成します。 それぞれに適切な名前を付けます。

- In the sub-activity diagram, create an **Activity Parameter Node** (2) for each input and output pin on the calling action. 各ノードに、対応するピンと同じ名前を付けます。

  > [!NOTE]
  > アクティビティ パラメーター ノードは、オブジェクト ノードに似ています。 To check what type of node that you are looking at, right-click the node and then click **Properties**. [プロパティ] ウィンドウのヘッダーにノードの型が表示されます。

- サブアクティビティ図で、各アクティビティ パラメーター ノードに出入りするオブジェクトのフローを示すコネクタを描画します。

  ![Pins on Call Behavior map to activity parameters](../modeling/media/uml-actguidesub.png "UML_ActGuideSub")

### <a name="Postcondition"></a> Defining Postconditions and Preconditions
 You can use the **Local Postconditions** and **Local Preconditions** properties to specify in detail the outcome of an action. これらのプロパティは、どのようにして効果が得られるかを記述せずに、アクションの効果を記述します。

 To set these properties, right-click the action and then click **Properties**. [プロパティ] ウィンドウで、プロパティに値を入力します。

#### <a name="local-postconditions"></a>ローカル事後条件
 事後条件とは、アクションが完了したと見なされるために満たされなければならない条件のことです。 Confirm Order アクション例では、事後条件は次のような場合があります。

 顧客は、自分のクレジット カードを処理するために必要な、完全で有効な詳細を提供した。

 事後条件は、アクション実行前後の状態間のリレーションシップを表すことができます。 (例:

 利率は以前の 2 倍である。

 より形式的なスタイルで事後条件を作成することで、アクションで扱われるデータの特定の属性を表せます。 (例:

 `InvoiceTotal == Sum(OrderItem.MenuItem.Price)`

#### <a name="local-preconditions"></a>ローカル事前条件
 事前条件とは、アクションが開始可能状態になるために真でなければならない条件のことです。 たとえば、Confirm Order アクションの事前条件は、次のような場合があります。

 顧客はメニューから少なくとも 1 つの項目を選択した。

### <a name="describing-calls-to-operations"></a>操作の呼び出しの記述
 アクションは一般に、ユーザー、ソフトウェア、コンピューターのあらゆる組み合わせによって実行される作業を表します。 ただし、操作呼び出しアクションを使用して、特定のソフトウェア メソッドまたは関数の呼び出しを記述することができます。

- 操作呼び出しアクションの名前を、どのような操作がどのようなオブジェクトまたはコンポーネントに対して呼び出されるかを示すように設定します。

- 操作呼び出しアクションに入出力ピンを追加して、パラメーターと戻り値を記述します。

- You can set the **Is Synchronous** property of the action to indicate whether your activity waits for the operation to complete.

  - If you set **Is Synchronous** to false, you are indicating that the flow can continue to the next action before the called operation is complete. 出力ピンは定義すべきではありません。定義すると、アクションから送信データが流れる結果となります。

## <a name="Concurrent"></a> Concurrent Flows
 You can use the **Fork Node** and the **Join Node** to describe two or more threads of activities that can execute at the same time.

 ![The fork and join nodes show concurrent flows](../modeling/media/uml-actguideconcurrent.png "UML_ActGuideConcurrent")

 The effect of the **Fork Node** (1) is to divide the thread of control into two or more threads. 前のアクションが終了すると、フォークの出力側のすべてのアクションが開始可能になります。

 A **Join Node** (2) brings concurrent threads together. The action after the **Join Node** may not start until all the actions leading to the **Join Node** are complete.

### <a name="describing-signals-and-events"></a>シグナルとイベントの記述
 シグナルを送信するプロセス内のステップを、アクティビティ内のシグナル送信アクションとして示すことができます。 イベント受理アクションとして続行する前段階で、特定のシグナルやイベントを待機するステップを示すことができます。

 たとえば、注文を送信するステップと、その注文を受信してから処理しなければならない別のステップを示すこともできます。

#### <a name="sending-a-signal"></a>シグナルの送信
 ある種のシグナルまたはメッセージが他のアクティビティまたはプロセスに送信されることを示すには、シグナル送信アクション (3) を使用します。 アクションが送信するメッセージの種類を示すには、アクションの名前を使用します。

- 制御フロー内に次のアクションがあれば、制御がすぐに渡されます。

- 返された情報にプロセスがどのように応答するかを、シグナル送信アクションを使用して記述することはできません。 そうするには、別個のイベント受理アクションを使用します。

- シグナル送信アクションへの入力データ フローを使用して、送信メッセージとともに送信できるデータを示すことができます。 For more information, see [Describing Data Flow](#DataFlows).

#### <a name="waiting-for-a-signal-or-event"></a>シグナルまたはイベントの待機
 このアクティビティが何らかの外部イベントまたは受信メッセージを待機することを示すには、イベント受理アクション (4) を使用します。 アクションが待機するイベントの種類を示すには、アクションの名前を使用します。

- アクティビティがそのフロー内の特定のポイントで外部イベントまたはメッセージを待機することを示すには、アクティビティ内の適切な場所にイベント受理アクションを入力フローとともに描画します。

- アクティビティがいつでも外部イベントまたはメッセージに応答できることを示すには、入力フローなしのイベント受理アクションを描画します。 指定された外部イベントが発生すると、アクティビティ内のイベント受理アクションから、新しいスレッドが開始されます。

- シグナルの送信側に返される値を、イベント受理アクションを使用して記述することはできません。 そのためには、別個のシグナル送信アクションを使用します。

- アクションからの出力データ フローを示すことにより、シグナルで受信されたデータをアクティビティがどのように処理するかを示すことができます。 If you want to show more than one output flow, you should set the **IsUnmarshall** property of the Accept Event Action, which indicates that the action parses the incoming signal into its separate components. For more information, see [Describing Data Flow](#DataFlows).

### <a name="describing-multiple-data-flows"></a>複数のデータ フローの記述
 アクションから出てくる制御フローまたはオブジェクト フローを複数描画することにより、アクションが終了すると複数のスレッドが出現することを示すことができます。 この効果はフォークに似ていますが、制御フローとオブジェクト フローの組み合わせを使用することができます。

 次の例は、アクションに出入りする複数のフローを示しています。

 ![Parallel object flows](../modeling/media/uml-actguidemulti.png "UML_ActGuideMulti")

 "Customer provides details" アクションが完了すると、"Shipment address" と "Credit card details" の 2 つのオブジェクトが生成されます。 この 2 つのオブジェクトは、それぞれ異なるアクションによる処理に進みます。

 アクションの開始のためにはそのすべての入力がそろっていることが必要であるため、最後のアクションは、それにつながるすべてのアクションが完了するまで開始されません。

### <a name="streams"></a>ストリーム
 アクティビティ図を使用すると、パイプライン、つまり同時に実行されて、アクションが相互に連続的にデータを受け渡す一連のアクションを記述しやすくなります。

 次の例の意図は、各アクションはオブジェクトを生成して作業し続けることができるということです。 制御フローが存在しないので、各アクションはそれぞれの最初のオブジェクトを受け取ったらすぐに開始できます。

 この例のコネクタはオブジェクト フローであることに注意してください。それらすべてにおいて、アクティビティ パラメーター ノード、オブジェクト ノード、あるいは入力ピンまたは出力ピンに、末端が少なくとも 1 つあるからです。

 ![A data flow](../modeling/media/uml-actguidestream.png "UML_ActGuideStream")

 1. この例には、3 つのアクティビティ パラメーター ノードがあり、その入力と出力を表しています。

 2. オブジェクト ノード、入力ピン、出力ピンは、バッファーを表すことができます。 オブジェクト ノードの [上限] プロパティを設定することにより、バッファーに同時に入れることができるオブジェクトの数を示すことができます。

 3. デシジョン ノードを使用することにより、ストリームが分かれて各オブジェクトがそれぞれ異なる分岐に送信されることを示すことができます。 コメントまたはノードのタイトルを使用して、分割の基準を説明できます。

 4. フォーク ノードを使用することにより、オブジェクトのコピーが複数作成されて同時処理に送られることを示すことができます。

 5. ジョイン ノードを使用して、処理の 2 つのストリームが 1 つに再マージされることを示すことができます。

### <a name="selection-and-transformation"></a>選択と変換
 オブジェクト フロー内のオブジェクトが変換されることまたは選択されること、あるいはその両方であることを指定できます。 オブジェクト フローとは、ピンまたはオブジェクト ノードに出入りするフローのことです。

- 変換は、フローに入るオブジェクトが別の型にどのように変換されるかを表します。

- 選択は、どのようにしてフローに入るオブジェクトの一部だけが受信アクションに送信されるかを表します。

  例は、変換を示しています。 図 1 の最初のアクションは、出力ピンに郵便番号を生成します。 これは、2 番目のアクションの入力ピンに接続されています。 しかし、2 番目のアクションは、完全に指定された住所を必要としています。 ある型から別の型への変換は、2 番目のアクティビティ Address Lookup で指定されています。 これは、オブジェクトのフローの [変換] プロパティから参照されます。 Address Lookup アクティビティには、受信する郵便番号のためのアクティビティ パラメーター ノードと、送信する詳細住所のための別のアクティビティ パラメーター ノードが含まれています。

  ![Object transformation defined in another diagram](../modeling/media/uml-actguidetransform.png "UML_ActGuideTransform")

  変換または選択は、次の 2 とおりの方法で指定できます。

- 入力ピンまたは出力ピンにコメントをアタッチする。

  - To distinguish this description from a general comment, you can begin the comment with <\<**transformation**>> or <\<**selection**>>.

- 別個のアクティビティ図で変換または選択を詳細に指定する。

  - この方法を使用する場合も、コメントをアタッチします。こうすることで、変換が定義されていることが読み手にとって明確になります。

##### <a name="to-specify-a-transformation-or-selection-in-a-separate-activity-diagram"></a>別個のアクティビティ図で変換または選択を指定するには

1. 変換フローまたは選択フローを記述する新しいアクティビティ図を作成します。

   - In **Solution Explorer**, right-click your project, point to **Add**, click **New Item**, and then click **Activity Diagram**. 変換フローまたは選択フローにふさわしい名前を図に付けます。 **[追加]** をクリックします。

2. 新しい図で、次のようにします。

   1. アクティビティ パラメーター ノードを 2 つ作成します。1 つは入力フロー用、もう 1 つは出力用です。

   2. オブジェクト フローと相互接続されるアクションを作成します。 これは、変換または選択の動作を示します。

3. 変換または選択を使用する図で、次のようにします。

   1. オブジェクト フロー (入力ピンまたは出力ピンのコネクタ、オブジェクト ノード、またはアクティビティ パラメーター ノード) を作成します。

   2. Right-click the object flow and then click **Properties**.

   3. In the **Transformation** or **Selection** property, select the diagram where you specified the transformation or selection flow.

   オブジェクト ノード、および個々の入力ピンと出力ピンに対して、選択を定義することもできます。 Define a selection activity as in the previous procedure, and then set the **Selection** property of the object node, or input or output pin.

## <a name="see-also"></a>参照
 [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md) [UML Sequence Diagrams: Reference](../modeling/uml-sequence-diagrams-reference.md) [UML Component Diagrams: Reference](../modeling/uml-component-diagrams-reference.md) [UML Use Case Diagrams: Reference](../modeling/uml-use-case-diagrams-reference.md) [UML Class Diagrams: Reference](../modeling/uml-class-diagrams-reference.md) [UML Component Diagrams: Reference](../modeling/uml-component-diagrams-reference.md) [Video: Capture Business Workflows by using Activity Diagrams](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-4-capture-business-workflows)
