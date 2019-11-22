---
title: Customizing Tools and the Toolbox | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.dsltools.dsldesigner.selectiondialog
- vs.dsltools.dsldesigner.selecticondialog
- vs.dsltools.dsldesigner.selectcursordialog
helpviewer_keywords:
- Domain-Specific Language, toolbox
ms.assetid: 2a0d03d7-ebc6-4458-b9f4-d2cb8418a62d
caps.latest.revision: 28
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2a5e2a46a2326c123d6b7b4e85fa29908ede9fc9
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299333"
---
# <a name="customizing-tools-and-the-toolbox"></a>ツールおよびツールボックスのカスタマイズ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ユーザーがモデルに追加可能な要素についてツールボックス項目を定義する必要があります。 ツールには要素ツールと接続ツールの 2 種類があります。 生成されたデザイナーで、ユーザーは要素ツールを選択して図形を図へドラッグすることができ、接続ツールを選択して図形間のリンクを描画できます。 一般にユーザーは、要素ツールを使用するとドメイン クラスのインスタンスをモデルに追加することができ、接続ツールを使用するとドメイン リレーションシップのインスタンスを追加できます。

 このトピックの内容

- [How the Toolbox is Defined](#ToolboxDef)

- [要素ツールのカスタマイズ](#customizing)

- [Creating Groups of Elements from a Tool](#groups)

- [Customizing Connection Tools](#connections)

## <a name="ToolboxDef"></a> How the toolbox is defined
 DSL エクスプローラーで、エディター ノードとその下のノードを展開します。 一般に、次のような階層が表示されます。

```

Editor
     Toobox Tabs
        MyDsl          //a tab
           Tools
               ExampleElement      // an element tool
               ExampleRelationship // a connection tool

```

 DSL エクスプローラーのこの部分で、次の操作を実行できます。

- 新しいタブを作成します。 タブはツールボックス内のセクション見出しを定義します。

- 新しいツールを作成します。

- ツールをコピーして貼り付けます。

- 一覧内のツールを上下に移動します。

- タブとツールを削除します。

> [!IMPORTANT]
> DSL エクスプローラー内の項目を追加または貼り付けるには、新しいノードの親の親を右クリックします。 For example, to add a tool, right-click the tab, and not the **Tools** node. To add a tab, right-click the **Editor** node.

 The **Toolbox Icon** property of every tool references a 16x16 bitmap file. These files are usually kept in the **Dsl\Resources** folder.

 The **Class** property of an element tool refers to a concrete domain class. 既定では、ツールはこのクラスのインスタンスを作成します。 ただし、コードを作成して、ツールに要素のグループまたはさまざまな種類の要素を作成させることができます。

 The **Connection Builder** property of a connection tool refers to a connection builder, which defines what types of elements the tool can connect, and what relationships it creates between them. DSL エクスプローラーで、接続ビルダーはノードとして定義されます。 接続ビルダーは、ドメイン リレーションシップを定義すると自動的に作成されますが、コードを作成してカスタマイズできます。

#### <a name="to-add-a-tool-to-the-toolbox"></a>ツールボックスにツールを追加するには

1. 通常、図形クラスを作成し、それをドメイン クラスにマップした後で、要素ツールを作成します。

     通常、コネクタ クラスを作成し、それを参照リレーションシップにマップした後で、コネクタ ツールを作成します。

2. In DSL Explorer, expand the **Editor** node and the **Toolbox Tabs** node.

     Right-click a toolbox tab node, and then click **Add New Element Tool** or **Add New Connection Tool**.

3. Set the **Toolbox Icon** property to refer to a 16x16 bitmap.

     If you want to define a new icon, create a bitmap file in Solution Explorer in the **Dsl\Resources** folder. The file should have the following property values: **Build Action** = **Content**; **Copy to Output Directory** = **Do not copy**.

4. **For an element tool:** Set the **Class** property of the tool to refer to a concrete domain class that is mapped to a shape.

     **For a connector tool:** Set the **Connection Builder** property of the tool to one of the items that are offered in the drop-down list. 接続ビルダーは、コネクタをドメイン リレーションシップにマップすると、自動的に作成されます。 最近、コネクタを作成した場合、通常、関連する接続ビルダーを選択しています。

5. DSL をテストするには、F5 キーまたは CTRL+F5 キーを押し、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の実験用インスタンスでサンプル モデル ファイルを開きます。 ツールボックスに新しいツールが表示されます。 それを図の上にドラッグし、新しい要素が作成されることを確認します。

     ツールが表示されない場合、実験用の [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を停止します。 In the Windows **Start** menu, run **Reset the Microsoft Visual Studio 2010 Experimental Instance**. On the [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]**Build** menu, click **Rebuild Solution**. 再度 DSL をテストします。

## <a name="customizing"></a> Customizing Element Tools
 既定では、ツールは指定されたクラスの単一インスタンスを作成しますが、次の 2 つの方法で変更できます。

- 他のクラスで要素マージ ディレクティブを定義し、このクラスの新しいインスタンスが受け入れられ、新しい要素が作成されるときに追加のリンクが作成されるようにします。 たとえば、ユーザーが別の要素にコメントをドロップし、両者の間に参照リンクを作成可能にすることができます。

     これらのカスタマイズは、ユーザーが要素を貼り付けたりドラッグ アンド ドロップしたりするときに発生することにも影響します。

     For more information, see [Customizing Element Creation and Movement](../modeling/customizing-element-creation-and-movement.md).

- コードを作成して、ツールをカスタマイズし、要素のグループを作成可能にします。 ツールはオーバーライド可能な ToolboxHelper.cs 内のメソッドにより初期化されます。 For more information, see [Creating Groups of Elements from a Tool](#groups).

## <a name="groups"></a> Creating Groups of Elements from a Tool
 各要素ツールは作成する要素のプロトタイプを含みます。 既定では、各要素ツールは単一の要素を作成しますが、1 つのツールで関連するオブジェクトのグループを作成することも可能です。 そのためには、関連項目を含む <xref:Microsoft.VisualStudio.Modeling.ElementGroupPrototype> を使用してツールを初期化します。

 次の例は、型 Transistor がある DSL から取得しています。 各 Transistor には名前の付いた Terminal が 3 つあります。 Transistor の要素ツールは、4 つのモデル要素と 3 つのリレーションシップ リンクを含むプロトタイプを格納します。 ユーザーがツールを図の上にドラッグすると、プロトタイプはインスタンス化され、モデル ルートにリンクされます。

 This code overrides a method that is defined in **Dsl\GeneratedCode\ToolboxHelper.cs**.

 For more information about customizing the model by using program code, see [Navigating and Updating a Model in Program Code](../modeling/navigating-and-updating-a-model-in-program-code.md).

```
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;

  public partial class CircuitsToolboxHelper
  {
    /// <summary>
    /// Toolbox initialization, called for each element tool on the toolbox.
    /// This version deals with each Component subtype separately.
    /// </summary>
    /// <param name="store"></param>
    /// <param name="domainClassId">Identifies the domain class this tool should instantiate.</param>
    /// <returns>prototype of the object or group of objects to be created by tool</returns>
    protected override ElementGroupPrototype CreateElementToolPrototype(Store store, Guid domainClassId)
    {
        if (domainClassId == Transistor.DomainClassId)
        {
            Transistor transistor = new Transistor(store);

            transistor.Base = new ComponentTerminal(store);
            transistor.Collector = new ComponentTerminal(store);
            transistor.Emitter = new ComponentTerminal(store);

            transistor.Base.Name = "base";
            transistor.Collector.Name = "collector";
            transistor.Emitter.Name = "emitter";

            // Create an ElementGroup for the Toolbox.
            ElementGroup elementGroup = new ElementGroup(store.DefaultPartition);
            elementGroup.AddGraph(transistor, true);
            // AddGraph includes the embedded parts

            return elementGroup.CreatePrototype();
        }
        else
        {
            return base.CreateElementToolPrototype(store, domainClassId);
}  }    }

```

## <a name="connections"></a> Customizing Connection Tools
 通常、新しいコネクタ クラスを作成するときに要素ツールを作成します。 または、両端の種類でリレーションシップの種類を確認可能にすることで、1 つのツールをオーバーロードできます。 たとえば、Person-Person リレーションシップと Person-Town リレーションシップの両方を作成可能な 1 つの接続ツールを定義できます。

 接続ツールは接続ビルダーを呼び出します。 接続ビルダーを使用して、ユーザーが生成されたデザイナー内で要素をリンク可能な方法を指定します。 接続ビルダーは、リンク可能な要素と要素間に作成されるリンクの種類を指定します。

 ドメイン クラス間に参照リレーションシップを作成すると、接続ビルダーは自動的に作成されます。 接続ツールをマップするときにこの接続ビルダーを使用します。 For more information about how to create connection tools, see [Configuring the Toolbox](../modeling/customizing-tools-and-the-toolbox.md).

 既定の接続ビルダーを変更して、異なる範囲のソース型とターゲット型を扱い、異なる種類のリレーションシップを作成できます。

 接続ビルダー用にカスタム コードを作成し、接続用のソース クラスとターゲット クラスの指定、作成される接続の種類の定義、および接続の作成に関連するその他の処理を実行できます。

### <a name="the-structure-of-connection-builders"></a>接続ビルダーの構造
 接続ビルダーには 1 つ以上のリンク接続ディレクティブが含まれ、それによってドメイン リレーションシップとソース要素およびターゲット要素が指定されます。 For example, in the Task Flow solution template, you can see the **CommentReferencesSubjectsBuilder** in the **DSL Explorer**. This connection builder contains one link connect directive named **CommentReferencesSubjects**, which is mapped to the domain relationship **CommentReferencesSubjects**. このリンク接続ディレクティブには、`Comment` ドメイン クラスを指し示すソース ロール ディレクティブと `FlowElement` ドメイン クラスを指し示すターゲット ロール ディレクティブが含まれます。

### <a name="using-connection-builders-to-restrict-source-and-target-roles"></a>接続ビルダーを使用したソース ロールとターゲット ロールの制限
 接続ビルダーを使用して、指定されたドメイン リレーションシップのソース ロールまたはターゲット ロールのどちらかで、特定のクラスの出現を制限できます。 たとえば、別のドメイン クラスへのドメイン リレーションシップを伴う基底ドメイン クラスがあるが、そのリレーションシップにおいて、その基底クラスのすべての派生クラスのロールが同じロールになるのは望ましくないという場合があるかもしれません。 In the Task Flow solution, there are four concrete domain classes (**StartPoint**, **EndPoint**, **MergeBranch**, and **Synchronization**) that inherit directly from the abstract domain class **FlowElement**, and two concrete domain classes (**Task** and **ObjectInState**) that inherit indirectly from it. There is also a **Flow** reference relationship that takes **FlowElement** domain classes in both its source role and target role. However, an instance of an **EndPoint** domain class should not be the source of an instance of a **Flow** relationship, nor should an instance of a **StartPoint** class be the target of an instance of a **Flow** relationship. The **FlowBuilder** connection builder has a link connect directive named **Flow** that specifies which domain classes can play the source role (**Task**, **MergeBranch**, **StartPoint**, and **Synchronization**) and which can play the target role(**MergeBranch**, **Endpoint**, and **Synchronization**).

### <a name="connection-builders-with-multiple-link-connect-directives"></a>複数のリンク接続ディレクティブを持つ接続ビルダー
 接続ビルダーには複数のリンク接続ディレクティブを追加できます。 This can help you hide some of the complexities of the domain model from users and keep the **Toolbox** from getting too cluttered. 単一の接続ビルダーにいくつかの異なるドメイン リレーションシップのリンク接続ディレクティブを追加できます。 ただし、ほぼ同一の関数を実行するときはドメイン リレーションシップを結合する必要があります。

 In the Task Flow solution, the **Flow** connection tool is used to draw instances of both the **Flow** and the **ObjectFlow** domain relationships. The **FlowBuilder** connection builder has, in addition to the **Flow** link connect directive described earlier, two link connect directives named **ObjectFlow**. These directives specify that an instance of an **ObjectFlow** relationship may be drawn between instances of the **ObjectInState** domain class, or from an instance of an **ObjectInState** to an instance of a **Task**, but not between two instances of a **Task**, or from an instance of a **Task** to an instance of an **ObjectInState**. However, an instance of a **Flow** relationship may be drawn between two instances of a **Task**. If you compile and run the Task Flow solution, you can see that drawing a **Flow** from an instance of an **ObjectInState** to an instance of a **Task** creates an instance of an **ObjectFlow**, but drawing a **Flow** between two instances of a **Task** creates an instance of a **Flow**.

### <a name="custom-code-for-connection-builders"></a>接続ビルダーのカスタム コード
 ユーザー インターフェイスには接続ビルダーの異なる種類のカスタマイズを定義する 4 つのチェック ボックスがあります。

- the **Custom accept** check box on a source or target role directive

- the **Custom connect** check box on a source or target role directive

- the **Uses custom connect** check box on a connect directive

- the **Is Custom** property of the connection builder

  これらのカスタマイズを実施するためにプログラム コードを準備する必要があります。 どのようなコードを準備する必要があるのかを知るためには、これらのボックスのいずれかをチェックし、[すべてのテンプレートの変換] をクリックして、ソリューションをビルドします。 エラー レポートが生成されます。 エラー レポートをダブルクリックし、追加する必要があるコードを説明しているコメントを確認します。

> [!NOTE]
> カスタム コードを追加するには、GeneratedCode フォルダー内のコード ファイルとは別のコード ファイルに部分クラス定義を作成します。 作業内容を失わないために、生成されたコード ファイルを編集しないでください。 For more information, see [Overriding and Extending the Generated Classes](../modeling/overriding-and-extending-the-generated-classes.md).

#### <a name="creating-custom-connection-code"></a>カスタム接続コードの作成
 In each link connect directive, the **Source role directives** tab defines from what types you can drag. Similarly, the **Target role directives** tab defines to what types you can drag. For each type, you can further specify whether to allow the connection (for that link connect directive) by setting the **Custom Accept** flag and then supplying the extra code.

 接続が確立されたときに発生することをカスタマイズすることもできます。 たとえば、特定のクラスに対してドラッグが発生するただ 1 つのケース、あるリンク接続ディレクティブが規定するすべてのケース、または FlowBuilder 接続ビルダー全体をカスタマイズできます。 これらの各オプションについて、適切なレベルでカスタム フラグを設定できます。 すべてのテンプレートを変換し、ソリューションのビルドを試みると、エラー メッセージから生成されたコード内のコメントに誘導されます。 これらのコメントにより、提供する必要のあるものが特定されます。

 コンポーネント図のサンプルで、Connection ドメイン リレーションシップの接続ビルダーはポート間に作成可能な接続を制限するようにカスタマイズされています。 次の図は、`OutPort` 要素から `InPort` 要素への接続のみ可能であること、しかし互いの内部でコンポーネントを入れ子にすることが可能であることを示しています。

 **Connection Coming in to an OutPort from a Nested Component**

 ![Connection Builder](../modeling/media/connectionbuilder-3.png "ConnectionBuilder_3")

 したがって、入れ子になったコンポーネントから OutPort への接続が可能であることを指定するのが適切です。 To specify such a connection, you set **Uses Custom Accept** on the **InPort** type as source role and the **OutPort** type as target role in the **DSL Details** window as shown in the following illustrations:

 **Link Connect Directive in DSL Explorer**

 ![Connection builder image](../modeling/media/connectionbuilder-4a.png "ConnectionBuilder_4a")

 **Link Connect Directive in DSL Details Window**

 ![](../modeling/media/connectionbuilder-4b.png "ConnectionBuilder_4b")

 次に、ConnectionBuilder クラスにメソッドを入力する必要があります。

```
  public partial class ConnectionBuilder
  {
    /// <summary>
    /// OK if this component has children
    /// </summary>
    private static bool CanAcceptInPortAsSource(InPort candidate)
    {
       return candidate.Component.Children.Count > 0;
    }

    /// <summary>
    /// Only if source is on parent of target.
    /// </summary>
    private static bool CanAcceptInPortAndInPortAsSourceAndTarget                (InPort sourceInPort, InPort targetInPort)
    {
      return sourceInPort.Component == targetInPort.Component.Parent;
    }
// And similar for OutPorts…
```

 For more information about customizing the model by using program code, see [Navigating and Updating a Model in Program Code](../modeling/navigating-and-updating-a-model-in-program-code.md).

 たとえば、同様のコードを使用して、ユーザーによる親子リンクを含むループの作成を防ぐことができます。 これらの制限は、どんな場合でもユーザーが違反することができないため、「ハード」な制約と見なされます。 ユーザーが保存できない無効な構成を作成することにより、一時的に迂回可能な「ソフト」な検証チェックを作成することもできます。

### <a name="good-practice-in-defining-connection-builders"></a>接続ビルダーを定義する際の適切なプラクティス
 異なる種類のリレーションシップを作成するために、それらが概念的に関連する場合にのみ、1 つの接続ビルダーを定義する必要があります。 タスク フローのサンプルでは、同じビルダーを使用して、タスク間のフローのほか、タスクとオブジェクト間のフローも作成します。 ただし、コメントとタスク間のリレーションシップを作成するために同じビルダーを使用することは混乱を招くことがあります。

 複数の種類のリレーションシップに対して接続ビルダーを定義する場合、ソース オブジェクトとターゲット オブジェクトの同じペアから複数の型が一致しないことを確認する必要があります。 そうでない場合、結果は予測不可能になります。

 カスタム コードを使用して「ハード」な制約を適用できますが、ユーザーが一時的に無効な接続を確立できる必要があるかどうかを考慮してください。 その必要がある場合、制約を変更して、ユーザーが変更内容を保存しようとするまで、接続が検証されないようにすることができます。

## <a name="see-also"></a>参照
 [Customizing Element Creation and Movement](../modeling/customizing-element-creation-and-movement.md) [Customizing Copy Behavior](../modeling/customizing-copy-behavior.md) [How to: Add a Drag-and-Drop Handler](../modeling/how-to-add-a-drag-and-drop-handler.md) [Navigating and Updating a Model in Program Code](../modeling/navigating-and-updating-a-model-in-program-code.md)
