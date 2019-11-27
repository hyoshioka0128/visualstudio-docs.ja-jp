---
title: 'UML Use Case Diagrams: Guidelines | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- diagrams - modeling, use case
- UML, use case diagrams
- diagrams - modeling, UML use case
- use case diagrams
- UML diagrams, use case
ms.assetid: b1ae8ed0-d00b-4f9b-8e23-733e09e81e9b
caps.latest.revision: 38
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7c9ccd5285f9a2744704c0ee13094a1dac31c53b
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74302837"
---
# <a name="uml-use-case-diagrams-guidelines"></a>UML ユース ケース図: ガイドライン
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

In Visual Studio, you can draw a *use case diagram* to summarize who uses your application or system, and what they can do with it. To create a UML use case diagram, on the **Architecture** menu, click **New UML or Layer Diagram**.

 For a video demonstration, see [Organizing Features into Use Cases](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-2-organizing-features-into-use-cases).

 この機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

 ユース ケース図は、次の情報を検討および伝達するのに役立ちます。

- システムまたはアプリケーションが人、組織、または外部システムと対話するシナリオ。

- ユース ケース図でこれらのアクターが達成する目的。

- システムの範囲。

  ユース ケース図には、ユース ケースの詳細は示されません。ユース ケース、アクター、およびシステムの間のいくつかの関係を要約したものにすぎません。 特に、この図では、それぞれのユース ケースの目的を達成するために実行される各ステップの順序は示されません。 これらの詳細は、各ユース ケースにリンクできる他の図やドキュメントに記述できます。 For more information, see [Describing Use Cases in Detail](#Details) in this topic.

  ユース ケースの記述では、システムが運用されるドメインに関連するいくつかの用語 ("販売"、"メニュー"、"顧客" など) を使用します。 これらの用語とその関係を明確に定義することが重要になりますが、これは、UML クラス図を利用することで可能になります。 For more information, see [UML Class Diagrams: Guidelines](../modeling/uml-class-diagrams-guidelines.md).

  ユース ケースでは、システムの機能要求のみを扱います。 ビジネス ルール、サービス品質要求、および制約の実装などの他の要求は別途記述する必要があります。 アーキテクチャと内部の詳細も、別途記述する必要があります。 For more information about how to define user requirements, see [Model user requirements](../modeling/model-user-requirements.md).

  このトピックでは、顧客が近所のレストランに料理を注文できる Web サイトに関する例を使用します。

  ![Elements in a use case diagram](../modeling/media/uml-ucovactor.png "UML_UCOvActor")

- An *actor* (1) is a class of person, organization, device, or external software component that interacts with your system. Example actors are **Customer**, **Restaurant**, **Temperature Sensor**, **Credit Card Authorizer.**

- A *use case* (2) represents the actions that are performed by one or more actors in the pursuit of a particular goal. Example use cases are **Order Meal**, **Update Menu**, **Process Payment**.

   ユース ケース図では、ユース ケースを、ユース ケースを実行するアクターと関連付けます (3)。

- Your *system (4)* is whatever you are developing. システムは、アクターが他のソフトウェア コンポーネントにすぎない小さなソフトウェア コンポーネントである場合もあれば、1 つの完全なアプリケーションであったり、多数のコンピューターとデバイスに展開される大規模な分散アプリケーション スイートであったりする場合もあります。 Example subsystems are **Meal Ordering Website**, **Meal Delivery Business**, **Website Version 2**.

   ユース ケース図では、システムまたはそのサブシステムでサポートされるユース ケースを表すことができます。

## <a name="BasicSteps"></a> Basic Steps for Drawing Use Case Diagrams

> [!NOTE]
> Detailed steps for creating any of the modeling diagrams are described in [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md).

#### <a name="to-create-a-new-use-case-diagram"></a>新しいユース ケース図を作成するには

1. On the **Architecture** menu, click **New UML or Layer Diagram**.

2. Under **Templates**, click **UMLUse Case Diagram**.

3. 図に名前を付けます。

4. In **Add to Modeling Project**, select an existing modeling project in your solution, or **Create a New Modeling Project**, and then click **OK**.

#### <a name="to-draw-a-use-case-diagram"></a>ユース ケース図を描画するには

1. Drag **Subsystem** boundaries from the toolbox onto the diagram, to represent either your whole system or its major components.

    - どのユース ケースがシステムまたはそのコンポーネントによってサポートされるかを記述しない場合は、システム境界なしでユース ケース図を描画できます。

    - 必要に応じて、システムの隅をドラッグしてサイズを大きくします。

    - 名前を適切に変更します。

2. Drag **Actors** from the toolbox onto the diagram (placing them outside any system boundary).

    - アクターは、このシステムと対話するユーザー、組織、および外部システムのクラスを表します。

    - 各アクターの名前を変更します。 For example: **Customer, Restaurant, Credit card agency.**

3. Drag **Use Cases** from the toolbox onto the appropriate systems.

    - ユース ケースは、アクターがこのシステムを利用して実行するアクティビティを表します。

    - 各アクティビティの名前を、アクターが理解できるタイトルに変更します。 コードに関係するタイトルは使用しないでください。 For example: **Order Meal, Pay for Meal, Deliver Meal**.

    - Begin with major transactions such as **Order Meal**, leaving until later smaller interactions such as **Select Menu Item**.

    - システムおよびそのシステムをサポートする主なサブシステムに各ユース ケースを配置します (ユーザーへの接続にのみ関係するファサードやコンポーネントはすべて無視します)。

    - ユース ケースをシステム境界の外側に描画して、(特定のバージョンやリリースの) システムでサポートされないことを示すことができます。

4. Click **Association** on the toolbox, then a use case, and then an actor that participates in the use case. このようにして、各アクターをそのユース ケースにリンクします。

5. Structure the use cases with the **Include**, **Extend** and **Generalization** relationships. これらのリンクを作成するには、ツールをクリックし、ソースのユース ケースをクリックしてから、ターゲットのユース ケースをクリックします。 See the following section titled [Structuring Use Cases](#Structuring).

6. ユース ケースを詳細に記述します。 See the following section titled [Describing Use Cases in Detail](#Details).

7. サブシステムまたは関連するユース ケース グループごとに、それぞれをフォーカスした図を描画します。 1 つのモデリング プロジェクトのすべての図は、同じモデルのビューです。

## <a name="Actors"></a> Drawing Actors and Use Cases
 ユース ケース図の主な目的は、システムと対話するユーザーと、ユーザーがシステムを使用して実現する主要なゴールを示すことにあります。

- Create **Actors** to represent classes of people, organizations, other systems, software or devices that interact with your system or subsystem.

  - To learn how to draw actors and other elements, see [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md).

  - それぞれの目的のセットに対して、種類またはロールに基づいてアクターを指定します。実際には同じ人間またはエンティティになることがある場合でも、区別します。 たとえば、"レストラン" と "顧客" は、レストランの従業員が顧客になる場合があったとしても、別のアクターです。

- Create **Use Cases** for each of the goals that each actor seeks to achieve with the system.

  - 実装のための用語ではなく、アクターが理解できる表現でユース ケースに名前をつけて記述します。

- Use **Associations** to link actors to use cases.

### <a name="inheritance-between-actors"></a>アクター間での継承
 ![Use case diagram showing inheritance](../modeling/media/uml-ucguideinherit.png "UML_UCGuideInherit")

 You can draw a **Generalization** link between Actors. 特化されたアクター (この例の "会員の顧客" など) は、汎化されたアクター ("顧客" など) のユース ケースを継承します。 矢じりで、より一般的なアクター ("顧客" など) を指し示す必要があります。 リンクを作成する際は、先に、より特化されたアクターをポイントします。

 特化されたアクターは、汎化されたアクターにはない追加のユース ケースを独自に持つことができます。

> [!CAUTION]
> アクターがアクター自体を汎化することになる汎化関係のループを作成しないでください。 ループによってエラーが発生する場合があります。

### <a name="alternative-actor-icons"></a>代替アクター アイコン
 標準の棒人形の代わりに、カスタム アイコンを使用してアクターを表すことができます。 たとえば、デバイス、レストラン、銀行などに見えるようにアイコンを変更できます。

##### <a name="to-change-the-appearance-of-an-actor"></a>アクターの外観を変更するには

1. Right-click the actor and then click **Properties**.

     **[プロパティ]** ウィンドウが表示されます。

2. Set the **Image Path** property to the location of an image file.

    - いくつかのイメージ形式 (.gif、.jpg、.bmp など) を使用できます。

    - ソリューションまたはプロジェクトのソース管理に含まれているファイルを使用して、ソリューションが移動またはコピーされた場合にも使用できるようにします。

3. この外観を他のユース ケース図に複製するには、アクターをコピーして別の図に貼り付けます。

    - イメージに対する変更は、特定の図のビューにしか適用されません。 この変更は、基になるモデル要素には適用されません。 このアクターを [UML モデル エクスプ ローラー] から別の図にドラッグした場合は、標準の棒人形として表示されます。

### <a name="multiplicities-between-actors-and-use-cases"></a>アクターとユース ケース間の多重度
 The association between an actor and a use case can show a *multiplicity* at each end.

 ![Use case one to one with actor](../modeling/media/uml-ucguidemulti1.png "UML_UCGuideMulti1")

> [!NOTE]
> The multiplicities of an association on a use case diagram are hidden if they are both **1**.

 By default, each multiplicity is **1**. このモデルの厳密な解釈では、多重度 1 は、たとえば、ある料理を注文できる顧客は 1 人だけで、1 人の顧客は一度に料理を 1 つだけ注文できることを意味します。

 これらの多重度は変更できます。

 (例:

 ![Use case showing many to many multiplicity](../modeling/media/uml-ucguidemulti2.png "UML_UCGuideMulti2")

- To state that several actors of the same class can take part in a single occurrence of a use case, set the multiplicity at the actor end of the association to **1..\*** .

   この図では、1 つ以上のレストランが同じ料理の注文を受けることができます。

- To show that each actor can participate at the same time in several occurrences of a use case, set the multiplicity at the use case end of the association to **\*** .

   この図では、各レストランは一度に複数の注文に対応できます。

##### <a name="to-set-multiplicities-on-an-association"></a>関連付けの多重度を設定するには

1. Right-click the association and then click **Properties**.

2. Expand either **First Role** or **Second Role**.

    *Role* means the element at one end of the association.

3. 多重度プロパティを次の一覧から選択して設定します。

   - **1** to state that exactly one instance of this role participates in each link.

   - **1..\*** to state that one or more instance of this role participate in each link.

   - **0..1** to state that participation is optional.

   - **\*** to state that zero or more instances of this role participate in the link.

> [!NOTE]
> チームの多くがユース ケース図に多重度の情報を設定せず、多重度を既定値の 1 のままにしておきます。 代わりに、そのユース ケースの別の説明にこの情報を記述します。 その場合、ユース ケース図のすべての多重度が非表示になります。

### <a name="using-an-actor-or-use-case-on-multiple-diagrams"></a>1 つのアクターまたはユース ケースを複数の図で使用する
 同じアクターとユース ケースを複数の図に表示できます。 (例:

- 1 つのアクターが関係している異なるユース ケースを異なる図に記述できます

- ユース ケースが関連付けられているアクターおよびサブシステムを 1 つの図に示し、このユース ケースを、包含されるユース ケースと拡張されるユース ケースにどのように構成するかを別の図に示すことができます。

##### <a name="to-show-the-same-actor-or-use-case-on-different-diagrams"></a>同じアクターまたはユース ケースを異なる図に表示するには

1. アクターまたはユース ケースを 1 つの図に作成します。

2. 別のユース ケース図を作成します。

3. Drag an actor or use case off **Model Explorer** onto the new diagram.

    > [!NOTE]
    > 既に関連付けられているアクターとユース ケースを新しい図に配置すると、それらの間の関連付けが新しい図に自動的に表示されます。

## <a name="Details"></a> Describing use cases in detail
 ユース ケースは次のことを表します。

- A goal of an actor in using the system, such as **Buy a Meal**; and

- One or more *scenarios*, that is, sequences of steps performed in pursuing the goal, such as: {**Order Meal, Pay, Deliver**}. In addition to success scenarios, there might be several exception or failure scenarios, such as **Credit Card Rejected**.

  1 つのユース ケースは、さまざまな詳細レベルで記述できます。 設計の初期段階では、ユース ケース図の名前だけで十分です。  シナリオの詳細な説明は後で記述できます。

  Visual Studio Ultimate では、ユース ケースをさまざまな方法で記述して、別個に使用したり、組み合わせて使用したりできます。

- ユース ケースをプロジェクト内の別の図 (1 つまたは複数) にリンクする。

  - アクティビティ図は、ループ、分岐、および並列スレッドを含むより複雑なプロセスを説明するのに便利です。 プロセスの個々の部分の間のデータ フローを示すこともできます。 For more information, see [UML Activity Diagrams: Guidelines](../modeling/uml-activity-diagrams-guidelines.md).

  - シーケンス図は、さまざまなアクター間で行われる一連の複雑な対話を説明するのに便利です。 シーケンス図を使用して、各ユース ケースに対してシステム内部で発生する処理を示すこともできます。 For more information, see [UML Sequence Diagrams: Guidelines](../modeling/uml-sequence-diagrams-guidelines.md).

- ユース ケースを詳細に記述した OneNote のページ、セクション、または段落にユース ケースをリンクする。

- テキスト、スクリーン ショットなどを使用してユース ケースのシナリオを記述した Word 文書に、ユース ケースをリンクする。 For more information, see [Model user requirements](../modeling/model-user-requirements.md).

#### <a name="to-link-a-use-case-to-a-diagram-or-file-in-the-same-solution"></a>ユース ケースを、同じソリューション内の図またはファイルにリンクするには

1. シーケンス図やアクティビィティ図を描画して、ユース ケースのシナリオを例示します。

2. ユース ケース図に戻ります。

3. 図またはファイルを、ソリューション エクスプローラーからユース ケース図の空白部分にドラッグします。

4. Connect from the artifact to the use case using a **Dependency**.

#### <a name="to-link-to-a-solution-file-such-as-a-word-document-or-powerpoint-presentation"></a>Word 文書や PowerPoint プレゼンテーションなどのソリューション ファイルにリンクするには

1. テキスト、スクリーン ショットなどを使用してユース ケースのシナリオを説明するドキュメントを記述します。

2. このドキュメントをソリューションに追加します。

    1. Word 文書をソリューションとして、同じ Windows フォルダーに移動します。

    2. In Solution Explorer, right-click the solution, point to **Add**, and then click **Existing Item**.

    3. Navigate to the Word document and click **Add**.

         ソリューション エクスプローラーのソリューション フォルダーに、Word 文書が表示されます。

3. Word 文書を、ソリューション エクスプローラーからユース ケース図の空白部分にドラッグします。

     新しい成果物が表示されます。

4. Connect from the artifact to the use case using a **Dependency**.

#### <a name="to-link-to-a-shared-document-onenote-element-or-web-page"></a>共有ドキュメント、OneNote 要素、または Web ページにリンクを設定するには

1. 共有要素の URL を取得します。 This can be, for example, a network file path beginning '\\\\', or a web page or Sharepoint URL beginning 'http://', or a link to a OneNote section, page, or paragraph beginning 'onenote:'.

2. In the Toolbox, click **Artifact** and then click in the use case diagram.

3. With the new artifact selected, type or paste the URL into the **Hyperlink** property.

> [!NOTE]
> 成果物をダブルクリックして、成果物のリンク先の図またはドキュメントを開くことができます。

### <a name="linking-use-cases-to-work-items"></a>ユース ケースを作業項目にリンクする
 If your project uses [!INCLUDE[vstsTfsRosarioLong](../includes/vststfsrosariolong-md.md)] and you have [!INCLUDE[esprtfc](../includes/esprtfc-md.md)], you can link each use case to a work item in [!INCLUDE[esprfound](../includes/esprfound-md.md)]. To learn how to make these links, see [Link model elements and work items](../modeling/link-model-elements-and-work-items.md).

 このリンクを使用すると、次のことができます。

- リンクされた作業項目でユース ケースについて説明する。 特に、プロジェクトで Visual Studio の正式なプロセス テンプレートを使用している場合、ユース ケースの作業項目にリンクできます。 この種の作業項目には、ユース ケースの目的とシナリオを記述するためのフィールドが用意されています。

- テスト ケースをユース ケースにリンクして、開発中のコードにどの程度ユース ケースが実装されているかのレポートを取得できます。

- タスクをユース ケースにリンクして、開発作業の進捗状況を追跡できます。

## <a name="Structuring"></a> Structuring Use Cases
 システムの動作の記述には、少数の主要なユース ケースだけを使用してください。 それぞれの主要なユース ケースでは、"製品を購入する"、"(ベンダーの視点から) 販売用の製品を提供する" など、アクターが実現する主要な目的を定義します。

 これらの目的を明確にしたら、それぞれの目的を達成する方法、および基本の目的のバリエーションについての詳細に進むことができます。

 ユース ケースを細かく分解しすぎないようにしてください。 ユース ケースは、システムの内部動作ではなく、システムに関するユーザーのエクスペリエンスを表します。 また、一般的には、早い段階でコードの試作版を作成する方が、詳細なユース ケースを構成するために時間を費やすよりも生産的です。

 主要なユース ケースと詳細なユース ケースの間の関係はユース ケース図に要約できます。 以下の各セクションでは、このことについて説明します。

- [Showing the details of a use case with Include](#Include)

- [Sharing goals with Generalization](#Inheritance)

- [Separating out variant cases with Extend](#Extend)

### <a name="Include"></a> Showing the details of a use case with Include
 Use an **Include** relation to show that one use case describes some of the detail of another. In the illustration, **Order a Meal** includes **Pay**, **Choose Menu**, and **Choose Menu Item**. 包含されている側のより詳細なユース ケースのそれぞれは、包含している側のユース ケースの全体的なゴールを達成するためにアクターが実行する必要があるステップを表しています。 より詳細な、包含される側のユース ケースを矢印で指し示す必要があります。

> [!CAUTION]
> ユース ケースがユース ケース自体を包含することになる包含関係のループを作成しないでください。 ループによってエラーが発生する可能性があります。

 包含される側のユース ケースは共有できます。 In the example, the **Order a Meal** and **Subscribe to Reviews** use cases both include **Pay**.

 ![Use cases decomposed with include](../modeling/media/uml-ucguideinclude.png "UML_UCGuideInclude")

 包含される側のユース ケースの目的とシナリオは、後で設計されたユース ケースで包含できるように、単独で意味を成している必要があります。

 ユース ケースを、包含する部分と包含される部分に分けることで、次の目的を達成するのが容易になります。

- ユース ケースの記述を異なる詳細レイヤーに構成する。

- 共有のシナリオを複数のユース ケースで繰り返すことを防ぐ。

#### <a name="Steps"></a> Defining the order of the detailed steps
 ユース ケース図では、より詳細なステップを実行する順序や、各ステップを必ず実行する必要があるかどうかは示されません。

 To make the order of the steps clear, you can use an **Artifact** to attach a separate document to the including use case. 次の例では、アクティビティ図が "料理を注文する" ユース ケースにアタッチされています。 代わりに、ステップの一覧や一連のスクリーン ショットが含まれたテキスト ドキュメントを使用することもできます。 For more information, see [Describing Use Cases in Detail](#Details).

 アクティビティ図を使用する場合は、次の名前付け規則に注意してください。

- アクティビティ全体の名前が、包含する側のユース ケースの名前と同じである。

- アクティビティ図内のアクションに、包含される側のユース ケースと同じ名前が付いている。

  For more information, see [UML Activity Diagrams: Guidelines](../modeling/uml-activity-diagrams-guidelines.md).

  ![Use case steps shown in linked activity diagram](../modeling/media/uml-ucguidesteps.png "UML_UCGuideSteps")

### <a name="Inheritance"></a> Sharing goals with Generalization
 Use a Generalization relation to show that a *specialized* use case is a particular way to achieve the goals expressed by another *general* use case. 白抜きの矢じりで、より一般的なユース ケースを指し示す必要があります。

 ![Use cases showing the generalization relation](../modeling/media/uml-ucguidegeneral.png "UML_UCGuideGeneral")

 For example, **Pay** generalizes **Pay by Credit Card** and **Pay by Cash**.

> [!CAUTION]
> アクターがアクター自体を汎化することになる汎化関係のループを作成しないでください。 ループによってエラーが発生する場合があります。

 特化されたユース ケースによって、同じゴールを実現するためにシステムが実行できる異なる方法を示すことができます。

 特化されたユース ケースは、一般的なユース ケースの目的およびアクターを継承するものと見なされます。 一般的なユース ケースに独自のシナリオが含まれている必要はありません。特化によって、目的を達成するための異なる方法を記述します。

##### <a name="to-refactor-common-goals-from-two-or-more-use-cases"></a>共通の目的を 2 つ以上のユース ケースからリファクタリングするには

1. 新しい一般的なユース ケースを作成し、名前を付けます。

2. Create a **Generalization** relation with the large arrow pointing at the new general use case.

    1. Click **Generalization** in the toolbox.

    2. Click a specialized use case (**Pay by Credit Card** in the example).

    3. Click the general use case (**Pay** in the example).

3. 特化されたユース ケースの目的を記述したら、共通部分を一般的なユース ケースの記述に移動します。

4. 特化されたユース ケース間で共有されるアクターは、一般的なユース ケースに移動できます。

### <a name="Extend"></a> Separating variant cases with Extend
 特定の状況下においてあるユース ケースが別のユース ケースに機能を追加できることを示すには、拡張リンクを使用します。 メインの拡張される側のユース ケースを、矢印で指し示す必要があります。

 ![One use case extending another](../modeling/media/uml-ucguideextend.png "UML_UCGuideExtend")

> [!CAUTION]
> アクターがアクター自体を汎化することになる拡張関係のループを作成しないでください。 ループによってエラーが発生する場合があります。

 For example, the **Login** use case of a typical Web site can include **Register New User** - but only when the user does not already have an account.

##### <a name="to-separate-a-use-case-into-main-and-extending-parts"></a>1 つのユース ケースを主な部分と拡張する部分に分割するには

1. 新しい拡張ユース ケースを作成し、名前を付けます。

2. Create an **Extend** relation with the arrow pointing at the extended use case.

   1. Click **Extend** in the toolbox.

   2. Click the extending use case (**Register New User** in the example).

   3. Click the extended use case (**Login** in the example).

       > [!NOTE]
       > 図に拡張関係ループを作成することは避けてください。 ユース ケースをそれ自体の拡張にすることはできません。

3. 拡張される側のユース ケースのシナリオを既に作成した場合は、関連するステップを拡張のシナリオに移動します。

4. The description of the extension (**Register New User** in the example) should include details of where in the main use case scenarios it will occur, and under what circumstances. 拡張は、メインのケースの説明を変更したものと考えてください。

   拡張ユース ケースは、メインのユース ケースのシナリオとなるようなシナリオ ステップを表します。 拡張のシナリオおよび目的は、必ず、メインのユース ケースのコンテキストで読み取られます。したがって、これらが単独で機能する必要はありません。

   拡張の分離は、次のような状況の記述に役立ちます。

- 拡張ユース ケースにのみ関わる追加のアクターが存在する場合。 たとえば、Web サイトの顧客登録の承認には管理者が必要です。

- 拡張ユース ケースが別のサブシステムで処理される場合。

- この拡張を利用できるのがシステムの特定のバージョンに限られる場合。 ユース ケース図で、各バージョンを別個のサブシステムとして示すことができます。

## <a name="Subsystems"></a> Using Subsystem Boundaries
 サブシステム境界を使用して、システムの範囲内にあるユース ケースを示します。

#### <a name="to-draw-a-subsystem-boundary"></a>サブシステム境界を描画するには

1. In the toolbox, click **Subsystem**, then click the diagram.

    サブシステムが図上に表示されます。

2. サブシステムのサイズを調整するには、そのサブシステムの隅をドラッグします。

3. サブシステムの内容を調整するには、既存のユース ケースをサブシステムの内側または外側にドラッグします。

   \- または

   To create a new use case directly in a subsystem, click **Use Case** in the toolbox, then click inside the subsystem.

> [!NOTE]
> The **Subjects** property of a use case indicates what subsystem it is contained within.

### <a name="use-cases-outside-the-system-scope"></a>システムの範囲外のユース ケース
 ビジネスの一部に含まれているユース ケースであれば、開発中のシステムで処理されないものであっても、図に含めておくと便利です。 これにより、開発者は自分たちの作業のコンテキストを理解できます。 たとえば、"料理を配達する" を、アクターの "レストラン" と "顧客" が関わるけれども "料理の注文 Web サイト" の責任の範囲外であるユース ケースとして示すことができます。

### <a name="multiple-subsystems"></a>複数のサブシステム
 複数のサブシステム境界を作成すると、システムの異なるコンポーネントで異なるユース ケースが処理されることを示すことができます。 For example, **Add Restaurant Appraisal** may be dealt with on a separate forum Web site. ユース ケース図では、ユーザーに表示するものを扱う必要があります。 システムで社内の職務の分担について記述したい場合は、コンポーネント図の使用を検討します。

### <a name="system-versions"></a>システムのバージョン
 複数のサブシステム境界を使用して、システムの異なるバージョンを示すことができます。 For example, the Pay use case might be included in Website Version 2 but not in Version 1.This implies that the system helps customers make their orders. ただし、顧客は代金をレストランに直接支払う必要があります。

 Use **Dependency** relations to link subsystems representing different versions or variants.

 ![Subsystems show different versions of a system](../modeling/media/uml-ucguidesystem.png "UML_UCGuideSystem")

## <a name="see-also"></a>参照
 [Model user requirements](../modeling/model-user-requirements.md) [UML Sequence Diagrams: Guidelines](../modeling/uml-sequence-diagrams-guidelines.md) [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md) [UML Use Case Diagrams: Reference](../modeling/uml-use-case-diagrams-reference.md) [UML Class Diagrams: Reference](../modeling/uml-class-diagrams-reference.md) [UML Component Diagrams: Reference](../modeling/uml-component-diagrams-reference.md) [UML Activity Diagrams: Guidelines](../modeling/uml-activity-diagrams-guidelines.md) [Video: Organizing Features into Use Cases](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-2-organizing-features-into-use-cases)
