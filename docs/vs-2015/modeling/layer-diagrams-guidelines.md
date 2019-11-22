---
title: 'Layer Diagrams: Guidelines | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- architecture, layer diagrams
- layer diagrams
- diagrams - modeling, layer
- constraints, architectural
ms.assetid: 2903bec7-a93b-46a6-aac6-994ac4f3f1a7
caps.latest.revision: 57
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 51cb71d4bc2f66377b677d5be292c4eafa1dbd18
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299458"
---
# <a name="layer-diagrams-guidelines"></a>レイヤー図: ガイドライン
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Describe your app's architecture at a high level by creating *layer diagrams* in Visual Studio. コードをレイヤー図に照らして検証することで、作成したコードがこの図と一貫性があるかどうかを確認します。 レイヤーの検証をビルド プロセスに含めることもできます。 See [Channel 9 Video: Design and validate your architecture using layer diagrams](https://go.microsoft.com/fwlink/?LinkID=252073).

 この機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

## <a name="what-is-a-layer-diagram"></a>レイヤー図とは
 従来のアーキテクチャ図と同様に、レイヤー図にも、設計の主要なコンポーネントや機能ユニットのほか、それらの要素の依存関係が示されます。 Each node on the diagram, called a *layer*, represents a logical group of namespaces, projects, or other artifacts. 設計に必要な依存関係を描画できます。 従来のアーキテクチャ図とは異なり、ソース コード内の実際の依存関係が意図したとおりのものであることを検証できます。 [!INCLUDE[esprtfs](../includes/esprtfs-md.md)] で定期的なビルドの検証パーツを作成すると、今後変更が繰り返されても、プログラム コードがシステムのアーキテクチャに準拠している状態を維持できます。 See [Layer Diagrams: Reference](../modeling/layer-diagrams-reference.md).

## <a name="Update"></a> How to design or update your app with layer diagrams
 以下の手順では、開発プロセスにおけるレイヤー図の使用方法についての概要を示します。 このトピックの後半のセクションでは、各手順について詳細に説明します。 新しく設計を行う場合は、既存のコードを扱う手順は省略してください。

> [!NOTE]
> これらの手順は順序が決まっているわけではありません。 複数のタスクを並行して実行することも、状況に合わせてタスクの順序を変えることも、プロジェクト内で繰り返すたびに毎回同じ手順を実行することもできます。

1. [Create a layer diagram](#Create) for the whole application, or for a layer within it.

2. [Define layers to represent primary functional areas or components](#CreateLayers) of your application. これらのレイヤーには、その機能に合わせて "プレゼンテーション" や "サービス" などの名前を付けます。 If you have a [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] solution, you can associate each layer with a collection of *artifacts*, such as projects, namespaces, files, and so on.

3. [Discover the existing dependencies](#Generate) between layers.

4. [Edit the layers and dependencies](#EditArchitecture) to show the updated design that you want the code to reflect.

5. [Design new areas of your application](#NewAreas) by creating layers to represent the principal architectural blocks or components and defining dependencies to show how each layer uses the others.

6. [Edit the layout and appearance of the diagram](#EditLayout) to help you discuss it with colleagues.

7. [Validate the code against the layer diagram](#Validate) to highlight the conflicts between the code and the architecture you require.

8. [Update the code to conform to your new architecture](#UpdateCode). 検証によって競合が報告されなくなるまで、コードの開発とリファクタリングを繰り返します。

9. [Include layer validation in the build process](#BuildValidation) to ensure that the code continues to adhere to your design.

## <a name="Create"></a> Create a layer diagram
 レイヤー図はモデリング プロジェクト内に生成する必要があります。 新しいレイヤー図を既存のモデリング プロジェクトに追加すること、レイヤー図の新しいモデリング プロジェクトを作成すること、または既存のレイヤー図を同じモデリング プロジェクト内でコピーすることができます。

> [!IMPORTANT]
> モデリング プロジェクトから別のモデリング プロジェクトまたはソリューション内の別の場所に、既存のレイヤー図を追加、ドラッグ、またはコピーしないでください。 この方法でコピーされたレイヤー図には、その図を変更しても、コピー元の図と同じ参照が含まれます。 これにより、レイヤー検証は正しく機能せず、要素が欠落したり、図を開こうとすると他のエラーが発生するなど、他の問題が生じる可能性があります。

 See [Create layer diagrams from your code](../modeling/create-layer-diagrams-from-your-code.md).

## <a name="CreateLayers"></a> Define layers to represent functional areas or components
 Layers represent logical groups of *artifacts*, such as projects, code files, namespaces, classes, and methods. Visual C# .NET プロジェクトおよび Visual Basic .NET プロジェクトの成果物からレイヤーを生成したり、Word ファイルや PowerPoint プレゼンテーションなどのドキュメントをリンクして仕様や計画をレイヤーに添付したりすることができます。 各レイヤーは、図では四角形として表示されます。また各レイヤーでは、レイヤーにリンクされている成果物の数が表示されます。 レイヤーには、より具体的なタスクを記述する入れ子になったレイヤーを含めることができます。

 一般的に、レイヤーには、その機能に合わせて "プレゼンテーション" や "サービス" などの名前を付けます。 密に相互依存している成果物は、同じレイヤーに配置します。 別々に更新できる成果物や別のアプリケーションで使用できる成果物は、異なるレイヤーに配置してください。 To learn about layering patterns, visit the Patterns & Practices site at [http://go.microsoft.com/fwlink/?LinkId=145794](https://go.microsoft.com/fwlink/?LinkId=145794).

> [!TIP]
> 一部のタイプの成果物は、レイヤーにリンクすることはできますが、レイヤー図と照らし合わせた検証はサポートしていません。 To see whether the artifact supports validation, open **Layer Explorer** to examine the **Supports Validation** property of the artifact link. See [Discover existing dependencies between layers](#Generate).

 よく知らないアプリケーションを更新する場合は、コード マップを作成することもできます。 これらの図を利用することで、コードを検証するときに、パターンと依存関係を見つけやすくなります。 ソリューション エクスプローラーを使って、名前空間やクラスを調べることができます。これらは、通常は既存のレイヤーに対応しています。 ソリューション エクスプローラーからこれらのコードの成果物をレイヤー図へドラッグして、レイヤーに割り当てます。 次に、レイヤー図を使用すると、コードの更新が簡単になり、デザインとの一貫性を維持することができます。

 参照トピック

- [コードからのレイヤー図の作成](../modeling/create-layer-diagrams-from-your-code.md)

- [コード マップを使用してアプリケーションをデバッグする](../modeling/use-code-maps-to-debug-your-applications.md)

- [ソリューション間の依存関係をマップする](../modeling/map-dependencies-across-your-solutions.md)

## <a name="Generate"></a> Discover existing dependencies between layers
 依存関係が存在するのは、あるレイヤーに関連付けられている成果物が、別のレイヤーに関連付けられている成果物を参照している場合です。 たとえば、あるレイヤー内のクラスが、別のレイヤー内のクラスを保持する変数を宣言する場合などです。 既存の依存関係を検出するには、リバース エンジニアリングします。

> [!NOTE]
> 成果物の種類によっては、依存関係をリバース エンジニアリングできないものもあります。 たとえば、テキスト ファイルにリンクされているレイヤーから、またはそのレイヤーに対して依存関係をリバース エンジニアリングすることはできません。 To see which artifacts have dependencies that you can reverse-engineer, right-click one or multiple layers, and then click **View Links**. In **Layer Explorer**, examine the **Supports Validation** column. Dependencies will not be reverse-engineered for artifacts for which this column shows **False**.

#### <a name="to-reverse-engineer-existing-dependencies-between-layers"></a>レイヤー間の既存の依存関係をリバース エンジニアリングするには

- Select one layer or multiple layers, right-click a selected layer, and then click **Generate Dependencies**.

  通常は、不要な依存関係がいくつか見つかります。 これらの依存関係を編集して、目的の設計に準拠するようアラインできます。

## <a name="EditArchitecture"></a> Edit layers and dependencies to show the intended design
 システムに追加予定の変更または目的のアーキテクチャを示すには、次の手順を実行してレイヤー図を編集します。 また、リファクタリングの変更を行い、コードを拡張する前に構造を改良することもできます。 See [Improving the structure of the code](#Improving).

|**目的**|**Perform these steps**|
|------------|-----------------------------|
|不要な依存関係を削除する|Click the dependency, and then press **DELETE**.|
|依存関係の方向を変更または制限する|Set its **Direction** property.|
|新しい依存関係を生成する|Use the **Dependency** and **Bidirectional Dependency** tools.<br /><br /> 複数の依存関係を描画するには、ツールをダブルクリックします。 When you are finished, click the **Pointer** tool or press the **ESC** key.|
|レイヤーに関連付けられている成果物が、指定した名前空間に依存できないように指定する|Type the namespaces in the layer's **Forbidden Namespace Dependencies** property. Use a semicolon ( **;** ) to separate the namespaces.|
|レイヤーに関連付けられている成果物を、指定した名前空間に所属させることができないように指定する|Type the namespaces in the layer's **Forbidden Namespaces** property. Use a semicolon ( **;** ) to separate the namespaces.|
|レイヤーに関連付けられている成果物を、指定した名前空間のいずれかに必ず所属させるように指定する|Type the namespace in the layer's **Required Namespaces** property. Use a semicolon ( **;** ) to separate the namespaces.|

### <a name="Improving"></a> Improving the structure of the code
 リファクタリングの変更を行ってもアプリケーションの振る舞いは変わりませんが、将来、コードの変更や拡張が容易になります。 適切に構成されたコードの設計は、レイヤー図に簡単に抽出できます。

 たとえば、各名前空間を表すレイヤーをコードで生成し、依存関係をリバース エンジニアリングした場合は、レイヤー間の一方向の依存関係が最小限であることを確認する必要があります。 クラスまたはメソッドをレイヤーとして使用して、より詳細に図を生成した場合は、完成した図も同じ特性を備えている必要があります。

 これを満たしていない場合、開発過程でコードの変更が難しくなるほか、レイヤー図を使用した検証に適さなくなります。

## <a name="NewAreas"></a> Design new areas of your application
 新規プロジェクトの開発を新たに開始する場合や、新規プロジェクトで新しい領域の設計を開始する場合、コードの開発前にレイヤーと依存関係を描画することで、主要なコンポーネントを把握できます。

- **Show identifiable architectural patterns** in your layer diagrams, if possible. たとえば、デスクトップ アプリケーションを示すレイヤー図には、プレゼンテーション、ドメイン ロジック、データ ストアなどのレイヤーを追加できます。 アプリケーションの単一の機能をカバーするレイヤー図には、モデル、ビュー、コントローラーなどのレイヤーを追加できます。 For more information about such patterns, see [Patterns & Practices: Application Architecture](https://go.microsoft.com/fwlink/?LinkId=145794).

     類似のパターンを生成することがよくある場合は、カスタム ツールを生成します。 See [Define a custom modeling toolbox item](../modeling/define-a-custom-modeling-toolbox-item.md).

- **Create a code artifact for each layer** such as a namespace, class, or component. これにより、コードの追跡やレイヤーへのコードのリンクが容易になります。 成果物を生成するごとに、すぐに適切なレイヤーにリンクさせてください。

- **You do not have to link most classes and other artifacts to layers** because they fall within larger artifacts such as namespaces that you have already linked to layers.

- **Create a new diagram for a new feature**. 一般には、アプリケーション全体を記述したレイヤー図を 1 つ以上生成します。 アプリケーション内の新機能を設計するときには、既存の図を流用しないでください。 代わりに、コードの新しい部分を反映した独自の図を生成します。 新しい図には、新機能のプレゼンテーション レイヤー、ドメイン ロジック レイヤー、データベース レイヤーなどを追加できます。

     アプリケーションをビルドするときに、全体を示す図とより詳細な機能の図の両方に対してコードが検証されます。

## <a name="EditLayout"></a> Edit the layout for presentation and discussion
 レイヤーおよび依存関係を識別しやすくするには、またはチーム メンバーとそれらについて話し合うことができるようにするには、次の方法で図の外観およびレイアウトを編集します。

- レイヤーのサイズ、形状、および位置

- レイヤーと依存関係の色

  - Select one or more layers or dependencies, right-click, and then click **Properties**. In the **Properties** window, edit the **Color** property.

## <a name="Validate"></a> Validate the code against the diagram
 図を編集した後は、コードに対して随時手動で検証を実行するか、またはローカル ビルドまたは [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] を実行するたびに自動的に検証を実行することができます。

 参照トピック

- [レイヤー図を使用したコードの検証](../modeling/validate-code-with-layer-diagrams.md)

- [Include Layer Validation in the Build Process](#BuildValidation)

## <a name="UpdateCode"></a> Update the code to conform to the new architecture
 通常、エラーは、更新されたレイヤー図に照らし合わせてコードを最初に検証したときに表示されます。 これらのエラーには、いくつかの原因が考えられます。

- 成果物が不適切なレイヤーに割り当てられている。 この場合、成果物を移動します。

- クラスなどの成果物が、アーキテクチャに違反する形で別のクラスを使用している。 この場合、コードをリファクタリングして依存関係を削除します。

  これらのエラーを解決するには、コードを更新して、検証時にエラーが表示されなくなるようにします。 通常、これは反復的な作業になります。 For more information about these errors, see [Validate code with layer diagrams](../modeling/validate-code-with-layer-diagrams.md).

> [!NOTE]
> コードを開発またはリファクタリングする際には、新しい成果物をレイヤー図にリンクしなければならないことがあります。 これは必ずしも必要な作業ではありません。たとえば、レイヤーが既存の名前空間を表しており、新しいコードでこれらの名前空間に要素を追加するだけの場合は不要です。

 開発プロセスの実行中は、検証時に報告される一部の競合を抑制できます。 たとえば、既に解決したエラーや特定のシナリオに関連しないエラーを抑制できます。 エラーを抑制した場合は、[!INCLUDE[esprfound](../includes/esprfound-md.md)] で作業項目をログに記録することをお勧めします。 To perform this task, see [Validate code with layer diagrams](../modeling/validate-code-with-layer-diagrams.md).

## <a name="BuildValidation"></a> Include layer validation in the build process
 今後、レイヤー図に従ってコードを変更できるように、ソリューションの標準のビルド処理にレイヤー検証を組み込むことができます。 他のチーム メンバーがソリューションをビルドした際には、コード内の依存関係とレイヤー図上の依存関係の相違がビルド エラーとして報告されます。 For more information about including layer validation in the build process, see [Validate code with layer diagrams](../modeling/validate-code-with-layer-diagrams.md).

## <a name="see-also"></a>参照
 [Layer Diagrams: Reference](../modeling/layer-diagrams-reference.md) [Create layer diagrams from your code](../modeling/create-layer-diagrams-from-your-code.md)
