---
title: How to Define a Domain-Specific Language | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.dsltools.dsldesigner.domainrelationship
- vs.dsltools.dsldesigner.domainclass
- vs.dsltools.dsldesigner.domaintype
helpviewer_keywords:
- Domain-Specific Language, domain class
- Domain-Specific Language, external types
- Domain-Specific Language, relationships
- Domain-Specific Language, domain properties
ms.assetid: d1772463-0eb1-40a5-b7c0-9a008bc76760
caps.latest.revision: 45
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b4bcd1f1f023c9e439fb870c9e31f07aa5be215d
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299552"
---
# <a name="how-to-define-a-domain-specific-language"></a>方法: ドメイン固有言語を定義する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ドメイン固有言語 (DSL) を定義するには、テンプレートから [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューションを作成します。 ソリューションの主要な機能は DSL 定義図です。これは DslDefinition.dsl に保存されています。 DSL 定義は、DSL のクラスとシェイプを定義します。 これらの要素を変更および追加した後で、プログラム コードを追加して DSL を詳細にカスタマイズできます。

 If you are new to DSLs, we recommend that you work through the **DSL Tools Lab**, which you can find in this site: [Visualizaton and Modeling SDK](https://go.microsoft.com/fwlink/?LinkID=186128)

## <a name="templates"></a> Selecting a Template Solution
 DSL を定義するには、以下のコンポーネントをインストールしておく必要があります。

|||
|-|-|
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]|[http://go.microsoft.com/fwlink/?LinkId=185579](https://go.microsoft.com/fwlink/?LinkId=185579)|
|[!INCLUDE[vssdk_current_short](../includes/vssdk-current-short-md.md)]|[http://go.microsoft.com/fwlink/?LinkId=185580](https://go.microsoft.com/fwlink/?LinkId=185580)|
|Visual Studio Visualization and Modeling SDK|[http://go.microsoft.com/fwlink/?LinkID=186128](https://go.microsoft.com/fwlink/?LinkID=186128)|

 ドメイン固有言語を新規に作成するには、ドメイン固有言語プロジェクト テンプレートを使用して新しい [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューションを作成します。

#### <a name="to-create-a-dsl-solution"></a>DSL ソリューションを作成するには

1. Create a solution with the **Domain-Specific Language** template, which can be found under **Other Project Types/Extensibility** in the **New Project** dialog box.

    ![Create DSL dialog](../modeling/media/create-dsldialog.png "Create_DSLDialog")

    When you click **OK**, the **Domain-Specific Language Wizard** opens and displays a list of template DSL solutions.

2. 各テンプレートをクリックして説明を参照します。 作成したい内容に最も近いソリューションを選択します。

    各 DSL テンプレートは、機能する基本的な DSL を定義します。 この DSL を編集して、各自の要件に合わせて調整します。

    詳細については、各サンプルをクリックしてください。

   - Select **Task Flow** to create a DSL that has swimlanes. スイムレーンとは、図上の垂直方向または水平方向のパーティションです。

   - Select **Component Models** to create a DSL that has ports. ポートとは、大きなシェイプの境界上にある小さなシェイプです。

   - Select **Class Diagrams** to define a DSL that has compartment shapes. コンパートメント シェイプには、項目のリストが含まれています。

   - Select **Minimal Language** in other cases, or if you are uncertain.

       > [!NOTE]
       > クラス図またはコンポーネント図を作成する場合は、UML モデルの使用を検討してください。 UML モデリング ツールには、1 つのモデルの周りで統合される図のセットが用意されています。 これらの図は拡張可能であり、ModelBus を使用して DSL と統合できます。 For more information, see [Create models for your app](../modeling/create-models-for-your-app.md).

   - Select **Minimal WinForm Designer** or **Minimal WPF Designer** to create a DSL that is displayed on a Windows Forms or WPF surface. エディターを定義するコードを記述する必要があります。 詳細については、以下のトピックを参照してください。

        [Windows フォームに基づくドメイン固有言語の作成](../modeling/creating-a-windows-forms-based-domain-specific-language.md)

        [WPF に基づくドメイン固有言語の作成](../modeling/creating-a-wpf-based-domain-specific-language.md)

3. 該当するウィザード ページに DSL のファイル名拡張子を入力します。 これは、DSL インスタンスを含むファイルに使用される拡張子です。

   - ご使用のコンピューター、または DSL をインストールするコンピューター上のどのアプリケーションにも関連付けられていないファイル名拡張子を選択してください。 For example, **docx** and **htm** would be unacceptable file name extensions.

   - 入力した拡張子が DSL として使用されている場合は、ウィザードから警告が出されます。 別のファイル名拡張子の使用を検討してください。 また、古い実験デザイナーをクリアするために Visual Studio SDK 実験用インスタンスをリセットできます。 Click **Start**, click **All Programs**, **Microsoft Visual Studio 2010 SDK**, **Tools**, and then **Reset the Microsoft Visual Studio 2010 Experimental instance**.

4. 他のページの設定を調整するか、または既定値のままにしておくことができます。

5. **[完了]** をクリックします。

    ウィザードにより、2 つまたは 3 つのプロジェクトを含むソリューションが作成され、DSL 定義からコードが生成されます。

   ユーザー インターフェイスは次の図のようになります。

   ![DSL デザイナー](../modeling/media/dsl-designer.png "dsl_designer")

   このソリューションはドメイン固有言語を定義します。 For more information, see [Overview of the Domain-Specific Language Tools User Interface](../modeling/overview-of-the-domain-specific-language-tools-user-interface.md).

### <a name="test-the-solution"></a>ソリューションのテスト
 テンプレート ソリューションは、機能する DSL を提供します。この DSL を変更するか、またはそのまま使用できます。

 ソリューションをテストするには、F5 キーを押すか、または Ctrl キーを押しながら F5 キーを押します。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の新しいインスタンスが実験モードで開きます。

 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の新しいインスタンスのソリューション エクスプローラーで Sample ファイルを開きます。 このファイルは図として開き、ツールボックスが表示されます。

 If you run a solution that you have created from the **Minimal Language** template, your experimental [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] will resemble the following example:

 ![](../modeling/media/dsl-min.png "DSL_min")

 ツールを試してみます。 要素を作成して接続します。

 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の実験用インスタンスを閉じます。

> [!NOTE]
> DSL を変更した場合は、Sample テスト ファイルにシェイプが表示されなくなります。 ただし、新しい要素を作成できます。

### <a name="modifying-the-template-dsl"></a>テンプレート DSL の変更
 テンプレート DSL 定義のすべてまたは一部のドメイン クラスとシェイプ クラスの名前を変更して保持します。 新しいクラス名として、スペースと句読点のない有効な CLR 名を使用してください。

 これは特に次のクラスを保持するときに役立ちます。

- The root class appears at the upper-left of the DSL Definition diagram, under **Classes and Relationships**. その名前を変更し、DSL とは異なる名前を付けてください。 For example, a DSL named **MusicLibrary** might have a root class named **Music**.

- The diagram class appears at the lower right of the DSL Definition diagram, in the **Diagram Elements** column. この列を表示するために、右へスクロールしなければならない場合があります。 It is typically named _YourDsl_**Diagram**.

- If you used the **Task Flow** template and you want to create diagrams with swimlanes, keep and rename the Actor domain class and ActorSwimlane shape.

  その他のクラスは、実際の要件に合わせて削除または名前変更します。

## <a name="patterns"></a> Patterns for Defining a DSL
 DSL を開発するときには、一度に 1 ～ 2 つの機能を追加または調整することをお勧めします。 機能を追加し、DSL を実行してテストしてから、1 つまたは 2 つの機能を追加します。 DSL の一般的な機能は次のようになります。

- ドメイン クラス、要素をモデルに接続する埋め込みリレーションシップ、ドメイン クラスの要素を図に表示するために必要なシェイプ、およびユーザーが要素を作成するための要素ツール。

- ドメイン クラスのドメイン プロパティと、シェイプにそれらを表示するデコレータ。

- 参照リレーションシップ、図に参照リレーションシップを表示するコネクタ、ユーザーがリンクを作成するためのコネクタ ツール。

- プログラム コードを必要とするカスタマイズ (検証制約やメニュー コマンドなど)。

  以降のセクションでは、最も有用な DSL 機能の作成方法について説明します。 DSL を作成できるパターンは他にもありますが、これらは最もよく使用されるパターンです。

> [!NOTE]
> After adding a feature, do not forget to click **Transform All Templates** in the toolbar of Solution Explorer before you build and running your DSL.

 次の図に、このトピックで例として使用する DSL のクラスとリレーションシップの部分を示します。

 ![Embedding and Reference relationships](../modeling/media/music-classes.png "Music_Classes")

 次の図は、この DSL のモデル例です。

 ![Instance model of generated DSL](../modeling/media/music-instance.png "Music_Instance")

> [!NOTE]
> "モデル" は、ユーザーが作成する DSL のインスタンスを指し、通常は図として表示されます。 このトピックでは、DSL を使用するときに表示される DSL 定義図とモデル図の両方について説明します。

## <a name="classes"></a> Defining Domain Classes
 ドメイン クラスは DSL の概念を表します。 The instances are *model elements*. For example in a **MusicLibrary** DSL you might have Domain Classes named **Album** and **Song**.

 To create a domain class, you can drag from the **Named Domain Class** tool to the diagram, and then rename the class.

 For more information, see [Properties of Domain Classes](../modeling/properties-of-domain-classes.md).

### <a name="create-an-embedding-relationship-for-each-domain-class"></a>ドメイン クラスごとに埋め込みリレーションシップを作成します。
 ルート クラス以外のすべてのドメイン クラスは、1 つ以上の埋め込みリレーションシップのターゲットであるか、または埋め込みリレーションシップのターゲットであるクラスから継承しているクラスである必要があります。

 モデルのすべてのモデル要素は、埋め込みリレーションシップの単一ツリー内のノードです。 埋め込みリレーションシップのソースとターゲットは、親と子と呼ばれることがよくあります。

 ドメイン クラスの親の選択は、要素の有効期間を他の要素にどのように依存させるかによります。 ツリーのノードが削除されると、そのサブツリーも通常削除されます。 したがって独立した要素のクラスは、ルート クラスの直下に埋め込まれます。

 通常、表示する要素が別の要素内部に含まれている場合は、所有者リレーションシップを示すことがあります。 この場合、最も適切な親クラスはコンテナーのクラスです。 例外として、コンテナー内部に含まれている項目が、実際には独立要素への参照リンクである場合があります。 この場合、コンテナーを削除すると参照も削除されますが、参照のターゲットは削除されません。

 このトピックで説明する DSL 定義パターンでは、コンテナーが削除されるとコンテナー内部に表示される要素も削除されることを前提としています。 より複雑な構成も可能です。そのためには規則を定義します。

|要素の表示方法|親 (埋め込み) クラス|DSL ソリューション テンプレートの例|
|------------------------------|--------------------------------|--------------------------------------|
|図のシェイプ。<br /><br /> スイムレーン。|DSL のルート クラス。|最小言語。<br /><br /> タスク フロー: Actor クラス。|
|スイムレーンのシェイプ。|スイムレーンとして表示される要素のドメイン クラス。|タスク フロー: Task クラス。|
|シェイプ内のリストの項目。コンテナーが削除されると、項目も削除されます。<br /><br /> シェイプの境界上のポート。|コンテナー シェイプにマップされるドメイン クラス。|クラス図: Attribute クラス。<br /><br /> コンポーネント図: Port クラス。|
|リストの項目。コンテナーが削除されても、項目は削除されません。|DSL のルート クラス。<br /><br /> リストには参照リンクが表示されます。||
|直接表示されません。|パーツを構成するクラス。||

 Music Library の例では、Album は四角形として表示され、この四角形の中に Song のタイトルがリストされます。 したがって Album の親がルート クラス Music であり、Song の親が Album です。

 To create a domain class and its embedding at the same time, click the **Embedding Relationship** tool, then click the parent class, and then click on a blank part of the diagram.

 埋め込みリレーションシップの名前とそのロールは、クラス名を自動的に追跡するため、通常はこれらの名前とロールを調整する必要はありません。

 For more information, see [Properties of Domain Relationships](../modeling/properties-of-domain-relationships.md) and [Properties of Domain Roles](../modeling/properties-of-domain-roles.md).

> [!NOTE]
> 埋め込みは継承とは異なります。 埋め込みリレーションシップの子は、親の機能を継承しません。

### <a name="add-domain-properties-to-each-domain-class"></a>各ドメイン クラスへのドメイン プロパティの追加
 ドメイン プロパティには値が格納されます。 例えば、Name、Title、Publication Date などです。

 Click **Domain Properties** in the class, press the ENTER key, and then type the name of a property. ドメイン プロパティの既定の型は String です。 If you want to change the type, select the domain property, and set the **Type** in the **Properties** window. If the type that you want is not in the drop-down list, see [Adding Property Types](#addTypes).

 **Set an Element Name property.** Select a domain property that can be used to identify elements in the language explorer. たとえば Song ドメイン クラスでは Title ドメイン プロパティを選択できます。 In the **Properties** window, set **Is Element Name** to `true`.

### <a name="create-derived-domain-classes"></a>派生ドメイン クラスの作成
 ドメイン クラスに、そのプロパティとリレーションシップを継承するバリアントを作成するには、そのドメイン クラスから派生するクラスを作成します。 たとえば Album には WMA、MP3 といった派生クラスを作成できます。

 Create the derived class using the **Domain Class** tool.

 Click the **Inheritance** tool, click the derived class, and then click the base class.

 Consider setting the **Inheritance Modifier** of the base class to **abstract**. 基底クラスのインスタンスが必要であると思われる場合は、それらのインスタンスに対して個別の派生クラスを作成することを検討してください。

 派生クラスは基底クラスのプロパティとロールを継承します。

### <a name="tidy-the-dsl-definition-diagram"></a>DSL 定義図の整理
 リレーションシップを追加すると、いくつかのクラスが複数の個所に表示されます。 To reduce the number of appearances and make the diagram wider, right-click the target class of a relationship, and then click **Bring Tree Here**. For the opposite effect, right-click the target class of a relationship and click **Split Tree**. メニュー コマンドが表示されない場合は、ドメイン クラスだけが選択されていることを確認してください。

 ドメイン クラスとシェイプ クラスを移動するには、CTRL+Up と CTRL+Down を使用します。

### <a name="test-the-domain-classes"></a>ドメイン クラスのテスト

##### <a name="to-test-the-new-domain-classes"></a>新しいドメイン クラスをテストするには

1. **Click Transform All Templates** in the toolbar of Solution Explorer, to generate the DSL designer code. このステップは自動化できます。 For more information, see [How to Automate Transform All Templates](https://msdn.microsoft.com/b63cfe20-fe5e-47cc-9506-59b29bca768a).

2. **Build and run the DSL.** Press F5 or CTRL+F5 to run a new instance of [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] in experimental mode. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の実験用インスタンスで、DSL のファイル名拡張子が付いているファイルを開くかまたは作成します。

3. **Open the Explorer.** At the side of the diagram is the language explorer window, which is usually named *YourLanguage* Explorer. このウィンドウが表示されない場合は、ソリューション エクスプローラーの下のタブに表示されている可能性があります。 If you cannot find it, on the **View** menu, point to **Other Windows**, and then click _YourLanguage_**Explorer**.

     エクスプローラーにはモデルのツリー ビューが表示されます。

4. **Create new elements.** Right-click the root node at the top, and then click **Add New**_YourClass_.

     クラスの新しいインスタンスが言語エクスプローラーに表示されます。

5. 新しいインスタンスを作成するときに、各インスタンスに異なる名前が付いていることを確認します。 This will occur only if you have set the **Is Element Name** flag on a domain property.

6. **Examine the domain properties. With an instance of your class selected,** inspect the Properties window. このドメイン クラスに定義したドメイン プロパティが表示されます。

7. **Save the file, close it, and re-open it**. ノードを展開すると、作成したすべてのインスタンスがエクスプローラーに表示されるはずです。

## <a name="shapes"></a> Defining Shapes on the Diagram
 図に四角形、楕円、またはアイコンとして表示する要素のクラスを定義できます。

#### <a name="to-define-a-class-of-elements-that-appear-as-shapes-on-a-diagram"></a>図にシェイプとして表示する要素のクラスを定義するには

1. **Define and test a domain class as described in**  [Defining Domain Classes](#classes) **.**

   - クラスの親はルート クラスである必要があります。 つまり、ルート クラスと新しいドメイン クラスの間に埋め込みリレーションシップが存在している必要があります。

   - 図にスイムレーンがある場合は、スイムレーンにマップされるドメイン クラスを親にすることができます。 Before continuing with this procedure, see [Defining a DSL that has Swimlanes](#swimlanes).

2. **Add a shape class** to represent the elements on the model diagram. 次のいずれかのツールから DSL 定義図にドラッグします。

   - **Geometry Shape** provides a rectangle or ellipse.

   - **Image Shape** displays an image that you provide.

   - **Compartment Shape** is a rectangle that contains one or more lists of items.

     シェイプ クラスの名前を変更します。シェイプ クラスは DSL 定義図の右側、[Shapes and Connectors] (シェイプとコネクタ) の下に表示されます。

3. **Define an image, if you created an image shape**.

   1. 任意のサイズのイメージ ファイルを作成します。 BMP、JPEG、GIF、および EMF 形式がサポートされています。

   2. ソリューション エクスプローラーで、Dsl\Resources の下のソリューションにファイルを追加します。

   3. DSL 定義図に戻り、新しいイメージ シェイプ クラスを選択します。

   4. In the Properties window, click the **Image** property.

   5. In the **Select Image** dialog box, click the drop-down menu under **File name**, and select the image.

4. **Add text decorators to the shape, to display the domain properties.**

    モデル要素の名前またはタイトルを表示するには、少なくとも 1 つのテキスト デコレータを追加する必要があります。

    Right-click the header of the shape class, point to **Add**, and then click **Text Decorator**. Set the name of the decorator, and in the Properties window set its **Position**.

5. **Connect each shape with a Diagram Element Map to the domain class that it should display**.

    Click the **Diagram Element Map** tool, then click the domain class, then click the shape class.

6. **Map the properties to the text decorators.**

   1. ドメイン クラスとシェイプ クラスの間の、図要素マップを表す灰色の線を選択します。

   2. In the **DSL Details** window, click the **Decorator Maps** tab. If you do not see the **DSL Details** window, on the **View** menu, point to **Other Windows** and then click **DSL Details**. すべての内容を確認するために、頻繁にこのウィンドウの上部を引き上げる必要があります。

   3. デコレータの名前を選択します。 Under **Display property**, select the name of a property of the domain class. デコレータごとにこの手順を繰り返します。

       If you want to display a property of a related element, click the drop-down tree navigator under **Path to display property**.

   4. 各デコレータ名の横にチェック マークが表示されていることを確認します。

      ![Shape Mappings and DSL Details window](../modeling/media/dsldetailswindow.png "DslDetailsWindow")

7. **Make a toolbox item for creating elements of the domain class.**

   1. In **DSL Explorer**, expand the **Editor** node and all its sub-nodes.

   2. Right-click the node under **Toolbox Tabs** that has the same name as your DSL, for example MusicLibrary. Click **Add Element Tool**.

       > [!NOTE]
       > If you right-click the **Tools** node, you will not see **Add Element Tool**. 代わりに、その上のノードをクリックします。

   3. In the Properties window with the new element tool selected, set **Class** to the domain class that you have recently added.

   4. Set **Caption** and **Tooltip**.

   5. Set **Toolbox Icon** to an icon that will appear in the toolbox. 別のツールで既に使用されているアイコンまたは新しいアイコンに設定できます。

        To create a new icon, open Dsl\Resources in **Solution Explorer**. 既存の要素ツールの BMP ファイルのいずれかをコピーして貼り付けます。 貼り付けたコピーの名前を変更して、ダブルクリックして編集します。

        Return to the DSL Definition diagram, select the tool, and in the Properties window click **[...]** in **Toolbox Icon**. In the **Select Bitmap** dialog box, select your .BMP file from the drop-down menu.

   For more information, see [Properties of Geometry Shapes](../modeling/properties-of-geometry-shapes.md) and [Properties of Image Shapes](../modeling/properties-of-image-shapes.md).

#### <a name="to-test-shapes"></a>シェイプをテストするには

1. **Click Transform All Templates** in the toolbar of Solution Explorer, to generate the DSL designer code.

2. **Build and run the DSL.** Press F5 or CTRL+F5 to run a new instance of [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] in experimental mode. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の実験用インスタンスで、DSL のファイル名拡張子が付いているファイルを開くかまたは作成します。

3. **Verify that the element tools appear on the toolbox.**

4. **Create shapes** by dragging from a tool onto the model diagram.

5. **Verify that each text decorator appears,** and that:

   1. You can edit it, unless you have set the **Is UI Read Only** flag on the domain property.

   2. [プロパティ] ウィンドウまたはデコレータでプロパティを編集すると、他のビューが更新される。

   シェイプを初めてテストした後に、シェイプのプロパティをいくつか調整し、拡張機能を追加する必要がある場合があります。 For more information, see [Customizing and Extending a Domain-Specific Language](../modeling/customizing-and-extending-a-domain-specific-language.md).

## <a name="references"></a> Defining Reference Relationships
 ソース ドメイン クラスとターゲット ドメイン クラスの間に参照リレーションシップを定義できます。 通常、参照リレーションシップは図ではコネクタ (シェイプ間の線) として表示されます。

 たとえば音楽の Album と Artist が図上にシェイプとして表示される場合、Artist と、そのアーティストが参加した Album を関連付ける ArtistsAppearedOnAlbums というリレーションシップを定義できます。 次の図に示す例を参照してください。

 ![Instance model of generated DSL](../modeling/media/music-instance.png "Music_Instance")

 参照リレーションシップは、同じ型の要素をリンクすることもできます。 たとえば家系図を表す DSL で、親とその子の間のリレーションシップは、Person から Person への参照リレーションシップです。

### <a name="define-a-reference-relationship"></a>参照リレーションシップを定義する
 [Reference Relationship] (参照リレーションシップ) ツール、リレーションシップのソース ドメイン クラス、ターゲット ドメイン クラスの順にクリックします。 ターゲット クラスとソース クラスを同一にできます。

 各リレーションシップには 2 つのロールがあり、各ロールはリレーションシップ ボックスの各側から伸びる線として表現されます。 各ロールを選択し、[プロパティ] ウィンドウでロールのプロパティを設定できます。

 **Consider renaming the roles**. たとえば、Person と Person の間のリレーションシップでは、既定の名前を Parents と Children、Manager と Subordinates、Teacher と Student などに変更することができます。

 **Adjust the multiplicities of each role**, if it is necessary. 各 Person に最大で １ つの Manager を設定するには、図の [Manager] ラベルの下に表示される多重度を 0..1 に設定します。

 **Add domain properties to the relationship.** In the figure, the Artist-Album relationship has a property of role.

 **Set the Allows Duplicates property of the relationship,** if more than one link of the same class can exist between the same pair of model elements. たとえば、Teacher が同一 Student に複数の Subject を指導できるように設定できます。

 ![Shape maps for connectors](../modeling/media/music-connector.png "Music_Connector")

 For more information, see [Properties of Domain Relationships](../modeling/properties-of-domain-relationships.md) and [Properties of Domain Roles](../modeling/properties-of-domain-roles.md).

### <a name="define-a-connector-to-display-the-relationship"></a>リレーションシップを表示するコネクタの定義
 コネクタは、モデル図の 2 つのシェイプを結ぶ線を表示します。

 Drag the **Connector** tool onto the DSL definition diagram.

 コネクタにラベルを表示する場合は、テキスト デコレータを追加します。 それらの位置を設定します。 To let the user move a text decorator, set its **Is Moveable** property.

 Use the **Diagram Element Map** tool to link the connector to the reference relationship.

 With the diagram element map selected, open the **DSL Details** window, and open the **Decorator Maps** tab.

 Select each **Decorator** and set **Display property** to the correct domain property.

 Make sure that a check mark appears next to each item in the **Decorators** list.

### <a name="define-a-connection-builder-tool"></a>接続ビルダー ツールを定義する
 In the **DSL Explorer** window, expand the **Editor** node and all its subnodes.

 Right-click the node that has the same name as your DSL, and then click **Add New Connection Tool**.

 新しいツールが選択されている状態で、[プロパティ] ウィンドウで次の操作を行います。

- Set the **Caption** and **Tooltip**.

- Click **Connection Builder** and select the appropriate builder for the new relationship.

- Set **Toolbox Icon** to the icon that you want to appear in the toolbox. 別のツールで既に使用されているアイコンまたは新しいアイコンに設定できます。

     To create a new icon, open Dsl\Resources in **Solution Explorer**. 既存の要素ツールの BMP ファイルのいずれかをコピーして貼り付けます。 貼り付けたコピーの名前を変更して、ダブルクリックして編集します。

     Return to the DSL Definition diagram, select the tool, and in the Properties window click **[...]** in **Toolbox Icon**. In the **Select Bitmap** dialog box, select your .BMP file from the drop-down menu.

##### <a name="to-test-a-reference-relationship-and-connector"></a>参照リレーションシップとコネクタをテストするには

1. **Click Transform All Templates** in the toolbar of Solution Explorer, to generate the DSL designer code.

2. **Build and run the DSL.** Press F5 or CTRL+F5 to run a new instance of [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] in experimental mode. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の実験用インスタンスで、DSL のファイル名拡張子が付いているファイルを開くかまたは作成します。

3. **Verify that the connection tool appears on the toolbox.**

4. **Create shapes** by dragging from a tool onto the model diagram.

5. **Create connections** between the shapes. 接続ツールをクリックし、シェイプをクリックし、別のシェイプをクリックします。

6. **Verify that you cannot create connections between inappropriate classes.** For example, if your relationship is between Albums and Artists, verify that you cannot link Artists to Artists.

7. **Verify that the multiplicities are correct. For example, verify that you cannot connect a Person to more than one manager.**

8. **Verify that each text decorator appears,** and that:

   1. You can edit it, unless you have set the **Is UI Read Only** flag on the domain property.

   2. [プロパティ] ウィンドウまたはデコレータでプロパティを編集すると、他のビューが更新される。

   コネクタを初めてテストした後に、コネクタのプロパティをいくつか調整し、拡張機能を追加する必要がある場合があります。 For more information, see [Customizing and Extending a Domain-Specific Language](../modeling/customizing-and-extending-a-domain-specific-language.md).

## <a name="compartments"></a> Defining Shapes that Contain Lists: Compartment Shapes
 コンパートメント シェイプには、1 つ以上の項目リストが含まれています。 たとえば Music Library DSL では、コンパートメント シェイプを使用して Album (音楽) を表すことができます。 各 Album には Song のリストがあります。

 ![Compartment Shape](../modeling/media/compartmentshape.png "CompartmentShape")

 DSL 定義でこれを実現する最も簡単な方法は、コンテナーのドメイン クラスを １ つ定義し、各リストを表すドメイン クラスを 1 つずつ定義する方法です。 コンテナー クラスはコンパートメント シェイプにマップされます。

 ![Shape map](../modeling/media/music-mapcomp.png "Music_MapComp")

 For more information, see [Properties of Compartment Shapes](../modeling/properties-of-compartment-shapes.md).

#### <a name="to-define-a-compartment-shape"></a>コンパートメント シェイプを定義するには

1. **Create the container domain class**. Click the **Embedding Relationship** tool, click the root class of the model, and then click a blank part of the DSL definition diagram. これにより、例の図に示すように Album という名前のドメイン クラスが作成されます。

     あるいはルート クラスに埋め込む代わりに、スイムレーンにマップされるドメイン クラスにコンテナーを埋め込むことができます。

     Add a domain property such as Name to the class, and set its **Is Element Name** flag in the Properties window.

2. **Create the list item domain class**. Click the **Embedding Relationship** tool, click the container class (Album) and then click a blank part of the diagram. これにより、例の図に示すように Song という名前のドメイン クラスが作成されます。

     Add a domain property such as Title to the class, and set its **Is Element Name** flag.

     その他のドメイン プロパティを追加します。

     表示するリストごとに、別のリスト項目ドメイン クラスを追加します。

3. **To mix several types of item in the list**, create classes that inherit from the list class. Make the list class abstract by setting its **Inheritance Modifier**.

     たとえば、アーティストではなく作曲家に基づいてクラシック音楽をソートする場合は、Song のサブクラスとして ClassicalSong と NonClassicalSong という 2 つのサブクラスを作成します。

4. **Create the compartment shape**. Drag from the **Compartment Shape** tool onto the DSL definition diagram.

     テキスト デコレータを追加し、その名前を設定します。

     コンパートメントを追加し、その名前を設定します。

5. To let the user hide the list compartments, right-click the compartment shape class, point to **Add**, and then click **Expand/Collapse Decorator**. [プロパティ] ウィンドウで、デコレータの位置を設定します。

6. Click the **Diagram Element Map** tool, click the container domain class, and then click the compartment shape.

7. ドメイン クラスとシェイプの間の図要素マップ リンクを選択します。 In the **DSL Details** window:

    1. Click the **Decorators** tab. Click the name of the decorator and then select the appropriate item under **Display Property**. デコレータの名前の横にチェック マークが表示されていることを確認します。

    2. Click the **Compartment Maps** tab.

         コンパートメントの名前をクリックします。

         Under **Displayed elements collection path**, navigate to the list element class (Song). ナビゲーター ツールを使用するにはドロップダウン矢印をクリックします。

         Under **Display Property**, select the property that should be displayed in the list. この例では Title です。

> [!NOTE]
> [デコレータ マップ] フィールドと [コンパートメント マップ] フィールドの [パス] フィールドを使用して、ドメイン クラスとコンパートメント シェイプ間により複雑なリレーションシップを作成できます。

#### <a name="to-define-a-tool-for-creating-the-shape"></a>シェイプ作成ツールを定義するには

1. **Make a toolbox item for creating elements of the domain class.**

2. In **DSL Explorer**, expand the **Editor** node and all its sub-nodes.

3. Right-click the node under **Toolbox Tabs** that has the same name as your DSL, for example MusicLibrary. Click **Add Element Tool**.

    > [!NOTE]
    > If you right-click the **Tools** node, you will not see **Add Element Tool**. 代わりに、その上のノードをクリックします。

4. In the Properties window with the new element tool selected, set **Class** to the domain class that you have recently added.

5. Set **Caption** and **Tooltip**.

6. Set **Toolbox Icon** to an icon that will appear in the toolbox. 別のツールで既に使用されているアイコンまたは新しいアイコンに設定できます。

     To create a new icon, open Dsl\Resources in **Solution Explorer**. 既存の要素ツールの .BMP ファイルのいずれかをコピーして貼り付けます。 貼り付けたコピーの名前を変更して、ダブルクリックして編集します。

     Return to the DSL Definition diagram, select the tool, and in the Properties window click **[...]** in **Toolbox Icon**. In the **Select Bitmap** dialog box, select your BMP file from the drop-down menu.

#### <a name="to-test-a-compartment-shape"></a>コンパートメント シェイプをテストするには

1. **Click Transform All Templates** in the toolbar of Solution Explorer, to generate the DSL designer code.

2. **Build and run the DSL.** Press F5 or CTRL+F5 to run a new instance of [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] in experimental mode. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の実験用インスタンスで、DSL のファイル名拡張子が付いているファイルを開くかまたは作成します。

3. **Verify that the tool appears on the toolbox.**

4. ツールをモデル図にドラッグします。 シェイプが作成されます。

    要素の名前が表示され、既定の値に自動的に設定されることを確認します。

5. Right-click the header of the new shape, and then click Add *Your List Item.* この例では、このコマンドは [Song の追加] です。

    リストに項目が表示され、その項目に新しい名前が設定されていることを確認します。

6. リスト項目の 1 つをクリックし、[プロパティ] ウィンドウの内容を確認します。 リスト項目のプロパティが表示されます。

7. 言語エクスプローラーを開きます。 リスト項目ノードが含まれているコンテナー ノードが表示されることを確認します。

   ![Generated explorer of DSL](../modeling/media/music-explorer.png "Music_Explorer")

   コンパートメント シェイプを初めてテストした後に、シェイプのプロパティをいくつか調整し、拡張機能を追加したい場合があります。 For more information, see [Customizing and Extending a Domain-Specific Language](../modeling/customizing-and-extending-a-domain-specific-language.md).

### <a name="displaying-a-reference-link-in-a-compartment"></a>コンパートメント内の参照リンクの表示
 通常、コンパートメントに表示する要素は、コンパートメント シェイプで表される要素の子です。 ただし場合によっては、参照リレーションシップによってリンクされている要素を表示することがあります。

 たとえば、Album にリンクされている Artist のリストを表示する Album Shape に、 2 番目のコンパートメントを追加する場合などです。

 この場合は、コンパートメントに参照要素ではなくリンクを表示する必要があります。 これは、ユーザーがコンパートメント内の項目を選択して DELETE キーを押した場合、参照先要素ではなくリンクを削除するように設定したいからです。

 ただし、コンパートメントには参照要素の名前を表示できます。

 次の手順では、ドメイン クラス、参照リレーションシップ、コンパートメント シェイプ、および図要素マップが、このセクションの前述の説明に従って既に作成されていることを前提としています。

##### <a name="to-display-a-reference-link-in-a-compartment"></a>コンパートメント内に参照リンクを表示するには

1. **Add a compartment to the compartment shape**. On the DSL Definition diagram, right-click the compartment shape class, point to **Add**, and then click **Compartment**.

2. Set **Displayed elements collection path** to navigate to the link, instead of its target element. ドロップダウン メニューをクリックし、ツリー ビューでターゲットではなく参照リレーションシップを選択します。 In the example, the relationship is **ArtistAppearedOnAlbums**.

3. Set **Path to Display Property** to navigate from the link to the target element. In the example, this is **Artist**.

4. Set **Display Property** to the appropriate property of the target element, for example **Name**.

5. **Transform All Templates**, build and run the DSL, and open a test model.

6. モデル図で、シェイプの適切なクラスを作成し、その名前を設定し、クラス間のリンクを作成します。 コンパートメント シェイプに、リンク要素の名前が表示されます。

7. コンパートメント シェイプでリンクまたは項目のいずれかを選択します。 リンクも項目も非表示になります。

## <a name="ports"></a> Defining Ports on the Boundary of another Shape
 ポートは、別のシェイプの境界上に位置するシェイプです。

 ポートを使用して、別のシェイプへの固定接続ポイントを作成することもできます。ユーザーはこの接続ポイントへのコネクタを描画できます。 この場合、ポート シェイプを透明にできます。

 To see an example that uses ports, select the **Component Diagram** template when you create a new DSL solution. この例は、ポートを定義する際に検討する要点を示します。

- ポートのコンテナーを表すドメイン クラス (`Component`) があります。

- ポートを表すドメイン クラスがあります。 この例では `ComponentPort` です。

- コンテナー ドメイン クラスからポート ドメイン クラスへの埋め込みリレーションシップがあります。 For more information, see [Defining Domain Classes](#classes).

- 同一コンテナーに異なる種類のポートを混在させる場合は、ポート ドメイン クラスのサブクラスを作成できます。 この例では、`InPort` と `OutPort` は `ComponentPort` を継承します。

- コンテナー ドメイン クラスは任意の種類のシェイプにマップできます。 この例では `ComponentShape` が該当します。 For more information, see [Defining Shapes](#shapes).

- ポート ドメイン クラスはポート シェイプにマップされます。 派生クラスを個別のポート シェイプ クラスにマップするか、または基底クラスを 1 つのポート シェイプ クラスにマップできます。

  In other respects, port shapes behave as described in [Defining Shapes](#shapes).

  For more information, see [Properties of Port Shapes](../modeling/properties-of-port-shapes.md).

## <a name="swimlanes"></a> Defining a DSL that has Swimlanes
 スイムレーンとは、図の垂直方向または水平方向のパーティションです。 各スイムレーンはモデル要素に対応しています。 DSL 定義では、スイムレーン要素に対して 1つのドメイン クラスが必要です。

 スイムレーンを持つ DSL を作成する最適な方法は、新しい DSL ソリューションを作成し、タスク フローのソリューション テンプレートを選択する方法です。 DSL 定義では、Actor クラスはスイムレーンにマップされているドメイン クラスです。 プロジェクトに合わせて、このクラスと他のクラスの名前を変更します。

 スイムレーン内にシェイプとして表示するクラスを追加するには、スイムレーン クラスと新しいクラスの間に埋め込みリレーションシップを作成します。 ユーザーはスイムレーン間で要素をドラッグできますが、各要素は常に特定のスイムレーン内に位置しています。 タスク フローのソリューション テンプレートでは、FlowElement がスイムレーン クラスの子です。

 スイムレーンとは関係なくシェイプとして表示するクラスを追加するには、ルート クラスと新しいクラスの間に埋め込みリレーションシップを作成します。 ユーザーは図上の任意の位置 （スイムレーンの境界上、スイムレーン外部を含む） に、これらのシェイプを配置できます。 タスク フローのソリューション テンプレートでは、Comment がルート クラスの子です。

 For more information, see [Properties of Swimlanes](../modeling/properties-of-swimlanes.md).

## <a name="addTypes"></a> Adding Property Types

### <a name="domain-enumerations-and-literals"></a>ドメイン列挙型とリテラル
 ドメイン列挙型は、複数のリテラル値を使用する型です。

 To add a domain enumeration, right-click the root of the model in the **DSL Explorer** and then click **Add New Domain Enumeration**. The element will appear in the **DSL Explorer** under the **Domain Types** node. この要素は図には表示されません。

 To add enumeration literals to the domain enumeration, right-click the domain enumeration in the **DSL Explorer** and then click **Add New Enumeration Literal**.

 既定では、列挙型のプロパティには、列挙値を一度に 1 つだけ設定できます。 If you want users and programmers to be able to set any combination of values - a "bit field" - set the **IsFlags** property of the Enumeration.

### <a name="external-types"></a>外部型
 When you set the type of a domain property, if you do not find the type you want in the **Type** drop-down list, you can add an external type. For example, you could add the **System.Drawing.Color** type to the list.

 To add a type, right-click the root of the model in DSL Explorer, and then click **Add New External Type**. In the Properties window, set the name to **Color** and the namespace to **System.Drawing**. This type now appears in DSL Explorer under **Domain Types**. ドメイン プロパティの型を設定するときには常にこの型を選択できます。

## <a name="custom"></a> Customizing the DSL
 このトピックで説明する手法を使用すると、図の表記法、読み取り可能な XML フォーム、およびコードやその他の成果物の生成に必要な基本ツールを使用して、DSL を迅速に作成できます。

 DSL 定義は 2 とおりの方法で拡張できます。

1. DSL 定義のさまざまな機能を使用して DSL を細かく調整する。 たとえば、複数の種類のコネクタを作成できるコネクタ ツールを 1 つ作成し、1 つの要素を削除すると関連要素も削除されるという規則を制御できます。 ほとんどの場合この手法は、DSL 定義で値を設定することで実現しますが、場合によってはプログラム コードを数行記述する必要があります。

     For more information, see [Customizing and Extending a Domain-Specific Language](../modeling/customizing-and-extending-a-domain-specific-language.md).

2. より高度な効果を実現するプログラム コードを使用して、モデリング ツールを拡張する。 たとえば、モデルを変更できるメニュー コマンドを作成し、2 つ以上の DSL を統合するツールを作成することができます。 VMSDK は特に、DSL 定義から生成されるコードにより、拡張機能を容易に統合できるようにすることを目的としています。  For more information, see [Writing Code to Customise a Domain-Specific Language](../modeling/writing-code-to-customise-a-domain-specific-language.md).

### <a name="changing-the-dsl-definition"></a>DSL 定義の変更
 DSL 定義で項目を作成すると、多くの既定値が自動的に設定されます。 設定された既定値は変更できます。 これにより DSL の開発が簡素化され、かつ強力なカスタマイズが可能となります。

 たとえばシェイプを要素にマップすると、ドメイン クラスの埋め込みリレーションシップに基づいて、マッピングの親要素パスが自動的に設定されます。 ただし、埋め込みリレーションシップを後で変更しても、親要素のパスは自動的には変更されません。

 したがって、DSL 定義で一部のリレーションシップを変更するときには、定義の保存時またはすべてのテンプレートの変換時に、エラーが報告されることがよくある点に注意してください。 ほとんどのエラーは容易に修正できます。 エラーの発生場所を確認するには、エラー レポートをダブルクリックします。

 See also [How to: Change the Namespace of a Domain-Specific Language](../modeling/how-to-change-the-namespace-of-a-domain-specific-language.md).

## <a name="trouble"></a> Troubleshooting
 次の表に、DSL の設計時によく発生する問題を示し、併せて解決策を提示します。 More advice is available on the [Visualization Tools Extensibililty Forum](https://go.microsoft.com/fwlink/?LinkId=186074).

|問題|提案される解決策|
|-------------|----------------|
|DSL 定義ファイルで行った変更が反映されない。|Click **Transform All Templates** in the toolbar above Solution Explorer, and then rebuild the solution.|
|シェイプにプロパティ値ではなくデコレータ名が表示される。|デコレータ マッピングを設定します。 DSL 定義図で図要素マップをクリックします。図要素マップは、ドメイン クラスとシェイプ クラスの間に表示される灰色の線です。<br /><br /> Open the **DSL Details** window. If you cannot see it, on the View menu, point to **Other Windows**, and then click **DSL Details**.<br /><br /> Click the **Decorator Maps** tab. Select the name of the decorator. その横のボックスがオンになっていることを確認します。 Under **Display property**, select the name of a domain property.<br /><br /> For more information, see [Shapes on the Diagram](#shapes).|
|DSL Explorer (DSL エクスプローラー) でコレクションに追加できない。 たとえば、［ツール］ を右クリックしてもメニューに ［Add Tool］ (ツールの追加) コマンドが表示されない。<br /><br /> DSL のエクスプローラーで要素をリストに追加できない。|追加するノードの上にある項目を右クリックします。 リストに追加する場合、［追加］ コマンドはリスト ノードではなくその所有者に表示されます。|
|ドメイン クラスを作成したが、言語エクスプローラーでインスタンスを作成できない。|ルートを除くすべてのドメイン クラスは、埋め込みリレーションシップのターゲットである必要があります。|
|DSL のエクスプローラーで、要素がその型の名前でのみ表示される。|In the DSL Definition, select a domain property of the class and in the Properties window, set **Is Element Name** to true.|
|DSL が常に XML エディタで開かれる。|これは、ファイルの読み取り中に発生したエラーが原因で起こります。 ただし、そのエラーを修正した後でも、エディターを DSL デザイナーに明示的にリセットする必要があります。<br /><br /> Right-click the project item, click **Open With** and select _YourLanguage_**Designer (Default)** .|
|アセンブリ名を変更した後に、DSL のツールボックスが表示されない。|Inspect and update **DslPackage\GeneratedCode\Package.tt** For more information, see [How to: Change the Namespace of a Domain-Specific Language](../modeling/how-to-change-the-namespace-of-a-domain-specific-language.md).|
|アセンブリ名を変更していないのに、DSL のツールボックスが表示されない。<br /><br /> あるいは、拡張機能の読み込みに失敗したことを示すメッセージ ボックスが表示される。|実験用インスタンスをリセットして、ソリューションをリビルドします。<br /><br /> 1.  At the Windows Start menu, under **All Programs**, expand [!INCLUDE[vssdk_current_long](../includes/vssdk-current-long-md.md)], then **Tools**, and then click **Reset the Microsoft Visual Studio Experimental Instance**.<br />2.  On the [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]**Build** menu, click **Rebuild Solution**.|

## <a name="see-also"></a>参照
 [Getting Started with Domain-Specific Languages](../modeling/getting-started-with-domain-specific-languages.md) [Creating a Windows Forms-Based Domain-Specific Language](../modeling/creating-a-windows-forms-based-domain-specific-language.md) [Creating a WPF-Based Domain-Specific Language](../modeling/creating-a-wpf-based-domain-specific-language.md)
