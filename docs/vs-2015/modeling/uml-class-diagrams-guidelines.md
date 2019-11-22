---
title: 'UML Class Diagrams: Guidelines | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.teamarch.logicalclassdiagram.overrideoperationsdialog
helpviewer_keywords:
- UML diagrams, class
- diagrams - modeling, class
- UML, class diagrams
- class diagrams - UML
- diagrams - modeling, UML class
ms.assetid: 94dbfd55-b300-4b49-9049-0831ed849486
caps.latest.revision: 56
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c170827825d772f4d97cd22f0b5754232e8d2257
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297283"
---
# <a name="uml-class-diagrams-guidelines"></a>UML クラス図: ガイドライン
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

In Visual Studio, you can use a *UML class diagram* to describe data types and their relationships separately from their implementation. 図は、実装ではなく、クラスの論理的な側面に注目するために使用されます。

 To create a UML class diagram, on the **Architecture** menu, choose **New UML Diagram or Layer Diagram**.

 この機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

> [!NOTE]
> このトピックでは、UML クラス図について説明します。 このほか、プログラム コードを作成して視覚化するために使用されるクラス図もあります。 See [Designing and Viewing Classes and Types](https://go.microsoft.com/fwlink/?LinkId=142231).

## <a name="Using"></a> Using UML Class Diagrams
 UML クラス図は、さまざまな用途に使用できます。

- システムで使用され、コンポーネント間で受け渡される型の、実装に依存しない説明を提供する。

     たとえば、ビジネス層の .NET コード、コンポーネント間のインターフェイスの XML、データベースの SQL、およびユーザー インターフェイスの HTML で、Meal Order 型が実装されているとします。 これらの実装は細部が異なりますが、Meal Order と他の型 (Menu や Payment) の間の関係は常に同じです。 UML クラス図を使用することにより、これらの関係について、実装を考慮することなく話し合うことができます。

- アプリケーションとそのユーザーの間の通信、およびユーザーのニーズの記述において使用される用語を明確にする。 See [Model user requirements](../modeling/model-user-requirements.md).

     たとえば、レストラン用アプリケーションのユーザー ストーリー、ユース ケース、またはその他の要求の記述について考えてみましょう。 通常、このような記述には、"メニュー"、"注文"、"料理"、"価格"、"支払い" などの用語が使用されます。 UML クラス図を使用すると、これらの用語の間の関係を定義できます。 これにより、要求の記述、ユーザー インターフェイス、およびヘルプ ドキュメントに不整合が発生する可能性を抑えることができます。

### <a name="relationship-to-other-diagrams"></a>他の図との関係
 通常、UML クラス図は、使用する型の記述を提供するために、他のモデル図と共に描画します。 それぞれの場合において、型の物理的表現はいずれの図においても暗示されません。

 アクティビティ図

 オブジェクト ノードを通過するデータの型。

 入力ピン、出力ピン、およびアクティビティ パラメーター ノードの種類。

 See [UML Activity Diagrams: Guidelines](../modeling/uml-activity-diagrams-guidelines.md).

 シーケンス図

 パラメーターの型およびメッセージの戻り値。

 生存線の種類。 生存線のクラスには、受信できるすべてのメッセージの操作が含まれている必要があります。

 See [UML Sequence Diagrams: Guidelines](../modeling/uml-sequence-diagrams-guidelines.md).

 コンポーネント図

 コンポーネントのインターフェイスとその操作。

 See [UML Component Diagrams: Guidelines](../modeling/uml-component-diagrams-guidelines.md).

 ユース ケース図

 ユース ケースの目標と手順の説明で言及されている型。

 See [UML Use Case Diagrams: Guidelines](../modeling/uml-use-case-diagrams-guidelines.md).

## <a name="BasicSteps"></a> Basic Steps for Drawing Class Diagrams
 For reference information about the elements on UML class diagrams, see [UML Class Diagrams: Reference](../modeling/uml-class-diagrams-reference.md).

> [!NOTE]
> Detailed steps for creating any of the modeling diagrams are described in [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md).

#### <a name="to-create-a-uml-class-diagram"></a>UML クラス図を生成するには

1. On the **Architecture** menu, choose **New UML or Layer Diagram**.

2. Under **Templates**, choose **UML Class Diagram**.

3. 図に名前を付けます。

4. In **Add to Modeling Project**, select an existing modeling project in your solution, or **Create a New Modeling Project**, and then choose **OK**.

     A new class diagram appears with the **UMLClass Diagram** Toolbox. ツールボックスには、必要な要素および関係が含まれています。

#### <a name="to-draw-a-uml-class-diagram"></a>UML クラス図を描画するには

1. To create a type, choose the **Class**, **Interface** or **Enumeration** tool on the Toolbox, and then click a blank part of the diagram. (ツールボックスが表示されない場合は、Ctrl + Alt + X を押します。)

2. To add attributes or operations to the types, or literals to an enumeration, choose the **Attributes**, **Operations** or **Literals** heading in the type, and press ENTER.

     `f(x:Boolean):Integer` のようなシグニチャを記述できます。 See [Attributes and Operations](#AttributesAndOperations).

     複数の項目をすばやく追加するには、各項目の末尾で Enter キーを 2 回押します。 方向キーを使用して、リスト内を上下に移動できます。

3. 型を展開する、または折りたたむには、左上隅のシェブロン アイコンをクリックします。 You can also expand and collapse the **Attributes** and **Operations** section of a class or interface.

4. 型間の関連、継承、または依存関係リンクを描画するには、適切なツールをクリックし、ソース型をクリックしてから、ターゲット型をクリックします。

5. To create types in a package, create a package using the **Package** tool, and then create new types and packages within the package. また、コピー コマンドを使用して型をコピーし、パッケージに貼り付けることもできます。

6. すべての図は、同じプロジェクト内の他の図との間で共有されるモデル上のビューです。 To see a tree view of the complete model, choose **View**, **Other Windows**, **UML Model Explorer**.

## <a name="UsingTypes"></a> Using Classes, Interfaces, and Enumerations
 ツールボックスには、3 種類の標準的な分類子が用意されています。 These are referred to as *types* throughout this document.

 ![A class, an enumeration, and an interface](../modeling/media/uml-classguidetypes.png "UML_ClassGuideTypes")

- Use **Classes** (1) to represent data or object types for most purposes.

- Use **Interfaces** (2) in a context where you have to differentiate between pure interfaces and concrete classes that have internal implementations. この差別化は、図の目的がソフトウェア実装を記述することである場合に便利です。 しかし、受動的なデータをモデリングする場合、またはユーザー要求を記述するための概念を定義する場合には、それほど効果的ではありません。

- Use an **Enumeration** (3) to represent a type that has a limited number of literal values, for example `Stop` and `Go`.

  - リテラル値を列挙に追加します。 それぞれに別個の名前を指定します。

  - 必要に応じて、それぞれのリテラル値に数値を指定することもできます。 Open the shortcut menu for the literal in the enumeration, choose **Properties**, and then type a number in the **Value** field in the **Properties** window.

  それぞれの型に一意な名前を付けます。

### <a name="getting-types-from-other-diagrams"></a>他の図からの型の取得
 他の図にある型を自分の UML クラス図に表示できます。

 UML クラス図

 1 つのクラスを複数の UML クラス図に表示できます。 When you have created a class on one diagram, drag the class from **UML Model Explorer** onto the other diagram.

 この機能は、それぞれの図で特定の関係のグループに重点を置いて作業する場合に便利です。

 たとえば、"料理の注文" とレストランの "メニュー" の間の関連を 1 つの図に示し、"隆理の注文" と "支払い" の間の関連を別の図に示すことができます。

 コンポーネント図

 If you have defined interfaces on the components in a component diagram, you can drag an interface from **UML Model Explorer** onto the class diagram. クラス図で、インターフェイスに含まれるメソッドを定義できます。

 See [UML Component Diagrams: Guidelines](../modeling/uml-component-diagrams-guidelines.md).

 UML シーケンス図

 You can create classes and interfaces from lifelines in a sequence diagram, and then drag the class from **UML Model Explorer** to a UML class diagram. シーケンス図における各生存線は、オブジェクト、コンポーネント、またはアクターのインスタンスを表します。

 To create a class from a lifeline, open the shortcut menu for the lifeline, and then choose **Create Class** or **Create Interface**. See [UML Sequence Diagrams: Guidelines](../modeling/uml-sequence-diagrams-guidelines.md).

## <a name="AttributesAndOperations"></a> Attributes and Operations
 属性 (4) は、型のすべてのインスタンスが持つことができる名前付きの値です。 属性にアクセスしても、インスタンスの状態は変更されません。

 操作 (5) は、型のインスタンスが実行できるメソッドまたは関数です。 操作は、値を返すことができます。 If its **isQuery** property is true, it cannot change the state of the instance.

 To add an attribute or operation to a type, open the shortcut menu for the type, choose **Add**, and then choose **Attribute** or **Operation**.

 To see its properties, open the shortcut menu for the attribute or operation, and then choose **Properties**. The properties appear in the **Properties** window.

 To see the properties of an operation's parameters, choose <strong>[…]</strong>in the **Parameters** property. 新しいプロパティ ダイアログ ボックスが表示されます。

 設定できるすべてのプロパティの詳細については、次のトピックを参照してください。

- [UML クラス図の属性のプロパティ](../modeling/properties-of-attributes-on-uml-class-diagrams.md)

- [UML クラス ダイアグラムの操作のプロパティ](../modeling/properties-of-operations-on-uml-class-diagrams.md)

### <a name="types-of-attributes-and-operations"></a>属性および操作の型
 Each *Type* of an attribute or operation, and each parameter type, can be one of the following:

- **(none)** - You can leave a type unspecified in the signature by omitting the preceding colon (`:`).

- One of the standard primitive types: **Boolean**, **Integer**, **String**.

- モデルで定義されている型。

- A parameterized value of a template type, written Template\<Parameter>. See [Template Types](#Templates).

  モデルでまだ定義していない型の名前を書くこともできます。 The name will be listed under **Unspecified Types** in UML Model Explorer.

> [!NOTE]
> その後、モデル内でその名前のクラス、またはインターフェイスを定義すると、以前の属性と操作は引き続き未指定型の要素を参照します。 新規クラスを参照するように変更するには、それぞれの属性や操作について、ドロップダウン メニューから新規クラスを選択し、型を 1 つずつリセットする必要があります。

#### <a name="multiple-types"></a>複数の型
 任意の属性、操作、またはパラメーター型の多重度を設定できます。

 許可値は次のとおりです。

 `[1]`

 指定された型の 1 つの値。 既定値です。

 `[0..1]`

 **Null** or a value of the given type.

 `[*]`

 任意の数の指定された型のインスタンスが含まれるコレクション。

 `[1..*]`

 1 つ以上の指定された型のインスタンスが含まれるコレクション。

 `[n..m]`

 `n` ～ `m` 個の指定された型のインスタンスが含まれるコレクション。

 多重度が 1 を超える場合は、以下のプロパティも設定できます。

- **IsOrdered** - If true, the collection has a defined order.

- **IsUnique** - If true, there are no duplicate values in the collection.

### <a name="visibility"></a>可視性
 *Visibility* indicates whether the attribute or operation can be accessed outside the class definition. 許可値は次のとおりです。

 **Public**

 **+**

 他のすべての型からアクセスできます。

 **Private**

 **-**

 この型の内部定義からのみアクセスできます。

 **パッケージ**

 **~**

 この型を含むパッケージ内、および明示的に型をインポートするすべてのパッケージ内でアクセスできます。 See [Defining Namespaces and Packages](#Packages).

 **Protected**

 **#**

 この型、およびこの型を継承する型からのみアクセスできます。 See [Inheritance](#Inheritance).

### <a name="setting-the-signature-of-an-attribute-or-an-operation"></a>属性または操作のシグニチャの設定
 属性または操作のシグニチャは、可視性、名前、(操作の) パラメーター、および型を含むプロパティのコレクションです。

 シグニチャは、図に直接記述できます。 属性または操作をクリックして選択し、もう一度クリックします。

 シグニチャは、次の形式で記述します。

```
visibility attribute-name : Type
```

 \- または

```
visibility operation-name (parameter1 : Type1, ...) : Type
```

 (例:

```
+ AddItem (item : MenuItem, quantity : Integer) : Boolean
```

 可視性については省略形を使用します。 既定値は `+` (public) です。

 それぞれの型には、モデルで定義した型、Integer や String などの標準型、またはまだ定義していない新しい型の名前を使用できます。

> [!NOTE]
> パラメーター リストに名前のみを記述して型を省略した場合、その名前は、パラメーターの型ではなく名前と見なされます。 この例では、MenuItem と Integer は、型が指定されていない 2 つのパラメーターの名前になります。
>
> `AddItem(MenuItem, Integer) /* parameter names, not types! */`

 シグニチャで型の多重度を設定するには、次の例に示すように、型の名前に続けて多重度を角かっこで囲んで指定します。

```
+ AddItems (items : MenuItem [1..*])
+ MenuContent : MenuItem [*]
```

 属性または操作が静的な場合、その名前はシグニチャ内で下線付きで表示されます。 属性または操作が抽象型の場合、その名前は斜体で表示されます。

 However, you can only set the **Is Static** and **Is Abstract** properties in the **Properties** window.

#### <a name="full-signature"></a>完全なシグニチャ
 属性または操作のシグニチャを編集するときに、行の末尾および各パラメーターの後に追加のプロパティが表示されることがあります。 これらのプロパティは、中かっこ {...} で囲まれて表示されます。 これらのプロパティは、編集または追加できます。 (例:

```
+ AddItems (items: MenuItem [1..*] {unique, ordered})
+ GetItems (filter: String) : MenuItem [*] {ordered, query}
```

 選択できるプロパティは次のとおりです。

 `unique`

 **Is Unique**

 コレクション内に重複する値は存在しません。 多重度が 1 を超える型に適用されます。

 `ordered`

 **Is Ordered**

 コレクションは順序付けられています。 false の場合、1 番目の項目は確定されません。 多重度が 1 を超える型に適用されます。

 `query`

 **Is Query**

 操作によってインスタンスの状態が変更されることはありません。 操作にのみ適用されます。

 `/`

 **Is Derived**

 属性は、他の属性または関連の値から計算されます。

 "/" は、属性の名前の前に表示されます。 (例:

```
/TotalPrice: Integer
```

 通常、完全なシグニチャは、編集中の図にのみ表示されます。 編集が完了すると、追加のプロパティは非表示になります。 If you want to see the full signature all the time, open the shortcut menu for the type, and then choose **Show Full Signature**.

## <a name="Associations"></a> Drawing and Using Associations
 関連は、ソフトウェアでリンクがどのように実装されるかに関係なく、2 つの要素間のあらゆる種類のリンクを表すために使用します。 たとえば、関連を使用して、C# のポインター、データベースにおけるリレーションシップ、または XML ファイルのある部分から別の部分への相互参照を表すことができます。 関連を使用することで、地球と太陽のような、現実世界のオブジェクト間の関連を表すことができます。 関連は、リンクがどのように表されているかを示すものではなく、その情報が存在することのみを示します。

### <a name="properties-of-an-association"></a>関連のプロパティ
 関連を生成したら、次にそのプロパティを設定します。 Open the shortcut menu for the association, and then choose **Properties**.

 In addition to the properties of the association as a whole, each *role*, that is, each end of the association, has some properties of its own. To view them, expand the **First Role** and **Second Role** properties.

 各ロールのいくつかのプロパティは、図に直接表示されます。 それらは次のとおりです。

- ロールの名前。 図内の関連の適切な端部に表示されます。 You can set it either on the diagram or in the **Properties** window.

- **Multiplicity**, which defaults to **1**. 図内の関連の適切な端部にも表示されます。

- **Aggregation**. コネクタの一方の端部に菱形で表されます。 集約ロール側のインスタンスがもう一方の側のインスタンスを所有または包含していることを示すために使用します。

- **Is Navigable**. 1 つのロールに対してのみ true の場合、誘導可能な方向に矢印が表示されます。 これを使用して、ソフトウェアのリンクの誘導可能性とデータベースのリレーションシップを示すことができます。

  For the full details of these and other properties, see [Properties of associations on UML class diagrams](../modeling/properties-of-associations-on-uml-class-diagrams.md).

### <a name="navigability"></a>誘導可能性
 関連を描画すると、関連を移動できる方向を示す矢印が片方の末尾に付きます。 これは、クラス図がソフトウェア クラスを表し、関連がポインターまたは参照を表す場合に役立ちます。 ただし、クラス図を使用してエンティティと関係またはビジネス概念を表す場合は、誘導可能性との関連性は小さくなります。 この場合は、矢印を使用しないで関連を描画することをお勧めします。 You can do so by setting the **Is Navigable** property on both ends of the association to True.

### <a name="attributes-and-associations"></a>属性と関連
 関連は、属性を視覚的に示す方法の 1 つです。 たとえば、Menu 型の属性を持つ Restaurant クラスを生成する代わりに、Restaurant から Menu への関連を描画できます。

 それぞれの属性名はロール名となります。 属性名は、関連の所有している型から反対側の端部に表示されます。 図の `myMenu` に注目してください。

 通常は、基本型のような図中に描画しない型に関してのみ、属性を使用することをお勧めします。

 ![Equivalent association and attributes](../modeling/media/uml-classguideattrib.png "UML_ClassGuideAttrib")

## <a name="Inheritance"></a> 継承
 Use the **Inheritance** tool to create the following relationships:

- A *generalization* relationship between a specialized type and a general type

   \- または

- A *realization* relation between a class and an interface that it implements.

  継承関係内にループを生成することはできません。

### <a name="generalization"></a>汎化
 汎化とは、一般的な型または基本型の属性、操作、および関連を特化型または派生型が継承することを表します。

 一般的な型は、関係の矢じり付きの端部に表示されます。

 通常、継承された操作および属性は、特化型には表示されません。 ただし、継承された操作を特化型の操作リストに追加することができます。 この機能は、操作の特定のプロパティを特化型内でオーバーライドする場合、または実装コードでそのような操作を行う必要があることを示す場合に便利です。

##### <a name="to-override-an-operations-definition-in-a-specializing-type"></a>操作の定義を特化型内でオーバーライドするには

1. 汎化関係をクリックします。

    関係が強調表示され、アクション タグがその近くに表示されます。

2. Click the Action tag, and then click **Override Operations**.

    The **Override Operations** dialog box appears.

3. Select the operations that you want to appear in the specializing type, and then click **OK**.

   選択した操作が特化型に表示されます。

### <a name="realization"></a>実現
 実現とは、インターフェイスによって指定された属性および操作をクラスで実装することを表します。 インターフェイスは、コネクタの矢印端に示されます。

 実現コネクタを生成すると、インターフェイスの操作が自動的に実現クラスに複製されます。 インターフェイスに新しい操作を追加すると、その操作はその実現クラスに複製されます。

 実現関係を生成した後、それをロリポップ表記に変換できます。 Right-click the relationship and choose **Show as Lollipop**.

 これにより、実現リンクでクラス図が煩雑になることもなく、クラスで実装するインターフェイスを表示できます。 また、インターフェイスとそれを実現するクラスを別個の図に表示することもできます。

 ![Realization shown with conector and lollipop](../modeling/media/uml-classguiderealize.png "UML_ClassGuideRealize")

## <a name="Templates"></a> Template Types
 他の型または値でパラメーター化できるジェネリック型またはテンプレート型を定義できます。

 たとえば、キー型と値型でパラメーター化されたジェネリックな Dictionary を生成できます。

 ![Template class with two parameters](../modeling/media/uml-classguidetemplate1.png "UML_ClassGuideTemplate1")

#### <a name="to-create-a-template-type"></a>テンプレート型を生成するには

1. クラスまたはインターフェイスを生成します。 これがテンプレート型になります。 適切な名前 (たとえば、`Dictionary`) を付けます。

2. Open the shortcut menu for the new type, and then choose **Properties**.

3. In the **Properties** window, click **[…]** in the **Template Parameters** field.

    The **Template Parameter Collection Editor** dialog box appears.

4. **[追加]** をクリックします。

5. 名前プロパティをテンプレート型のパラメーター名 (たとえば、`Key`) に設定します。

6. Set **Parameter Kind**. The default is **Class**.

7. If you want the parameter to accept only derived classes of a particular base class, set **Constrained Value** to the base class that you want.

8. Add as many parameters as you need, then choose **OK**.

9. 他のクラスの場合と同様に、属性と操作をテンプレート型に追加します。

     You can use parameters whose kind is **Class**, **Interface** or **Enumeration** in the definition of attributes and operations. たとえば、`Key` と `Value` のパラメーター クラスを使用して、この操作を `Dictionary` で定義できます。

     `Get(k : Key) : Value`

     You can use a parameter whose kind is **Integer** as a bound in a multiplicity. たとえば、パラメーター整数 max を使用して、属性の多重度を `[0..max]` として定義できます。

   テンプレート型を生成した後は、これを使用してテンプレート バインディングを定義できます。

   ![A  class bound from the Dictionary template](../modeling/media/uml-classguidetemplate2.png "UML_ClassGuideTemplate2")

#### <a name="to-use-a-template-type"></a>テンプレート型を使用するには

1. 新しい型 (たとえば、`AddressTable`) を生成します。

2. Open the shortcut menu for the new type, and then choose **Properties**.

3. In the **Template Binding** property, select the template type, for example `Dictionary`, from the drop-down list.

4. Expand the **Template Binding** property.

     テンプレート型のそれぞれのパラメーターに対して行が表示されます。

5. それぞれのパラメーターを適切な値に設定します。 たとえば、`Key` パラメーターを `Name` クラスに設定します。

## <a name="Packages"></a> Packages
 UML クラス図では、パッケージを表示できます。 パッケージは、他のモデル要素のコンテナーです。 パッケージ内には任意の要素を生成できます。 図において、パッケージを移動すると、パッケージ内の要素も移動されます。

 展開/折りたたみコントロールを使用して、パッケージの内容の表示/非表示を切り替えることができます。

 See [Define packages and namespaces](../modeling/define-packages-and-namespaces.md).

## <a name="generating"></a> Generating Code from UML Class Diagrams
 UML クラス図でクラスの実装を開始するには、C# コードを生成するか、またはコード生成用テンプレートをカスタマイズすることができます。 用意された C のテンプレートを使用してコードの生成を開始する場合:

- Open the shortcut menu for the diagram or an element, choose **Generate Code**, and then set the necessary properties.

     For more information about how to set these properties and customize the provided templates, see [Generate code from UML class diagrams](../modeling/generate-code-from-uml-class-diagrams.md).

## <a name="see-also"></a>参照
 [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md) [UML Class Diagrams: Reference](../modeling/uml-class-diagrams-reference.md) [Model user requirements](../modeling/model-user-requirements.md) [UML Component Diagrams: Reference](../modeling/uml-component-diagrams-reference.md) [UML Sequence Diagrams: Reference](../modeling/uml-sequence-diagrams-reference.md) [UML Use Case Diagrams: Reference](../modeling/uml-use-case-diagrams-reference.md) [UML Component Diagrams: Reference](../modeling/uml-component-diagrams-reference.md)
