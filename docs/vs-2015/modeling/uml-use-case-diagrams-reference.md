---
title: 'UML ユースケース図: Reference |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
f1_keywords:
- vs.teamarch.usecasediagram.toolbox
- vs.teamarch.usecasediagram.diagram
- vs.teamarch.UMLModelExplorer.usecasediagram
helpviewer_keywords:
- diagrams - modeling, use case
- UML, use case diagrams
- diagrams - modeling, UML use case
- use case diagrams
- UML diagrams, use case
ms.assetid: aa15772b-eb67-4366-b145-b559112817df
caps.latest.revision: 35
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: cbea61c2a26b1dc81487365ef8fc3f320ac95943
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657306"
---
# <a name="uml-use-case-diagrams-reference"></a>UML ユース ケース図: リファレンス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio では、 *ユースケース図* は、アプリケーションまたはシステムを使用するユーザーと、アプリケーションまたはシステムを使用して実行できる操作をまとめたものです。 UML ユースケース図を作成するには、[ **アーキテクチャ** ] メニューの [ **新しい Uml またはレイヤー図**] をクリックします。

 ユース ケース図は、ユーザー要件の説明の焦点として機能します。 これは、要求、ユーザー、および主要なコンポーネントの間のリレーションシップについて説明します。 ただし、要求の詳細については説明しません。それらは個別の図または各ユース ケースにリンク可能なドキュメントで説明できます。 ユースケース図を使用してユーザーのニーズを理解し、話し、伝達する方法の詳細については、「 [ユーザー要件のモデル](../modeling/model-user-requirements.md)化」を参照してください。

 この機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

> [!NOTE]
> このトピックでは、ユース ケース図で使用可能な要素について説明します。 ユースケース図を描画する方法の詳細については、「 [UML ユースケース図: ガイドライン](../modeling/uml-use-case-diagrams-guidelines.md)」を参照してください。 モデリング図を作成して描画する方法の詳細については、「 [UML モデルとダイアグラムの編集](../modeling/edit-uml-models-and-diagrams.md)」を参照してください。

## <a name="reading-use-case-diagrams"></a>ユース ケース図の解説
 次のセクションの表では、ユース ケース図で使用できる要素と、それらの主要なプロパティについて説明します。 プロパティの完全な一覧については、「 [UML ユースケース図の要素のプロパティ](../modeling/properties-of-elements-on-uml-use-case-diagrams.md)」を参照してください。

### <a name="actors-use-cases-and-subsystems"></a>アクター、ユース ケース、およびサブシステム
 ![ユース ケース ダイアグラムの要素](../modeling/media/uml-ucovactor.png "UML_UCOvActor")

|**図形**|**Element**|**説明と主要なプロパティ**|
|---------------|-----------------|-----------------------------------------|
|1|**俳優**|ご使用のアプリケーションやシステムと対話するユーザー、組織、または外部システムを表します。 アクターは一種の型です。<br /><br /> -   **イメージパス** -既定のアクターアイコンの代わりに使用するイメージのファイルパス。 このアイコンは、Visual Studio プロジェクト内のリソース ファイルである必要があります。|
|2|**ユースケース**|特定の目的をめざして 1 つ以上のアクターによって実行されるアクションを表します。 ユース ケースは一種の型です。<br /><br /> -   [**サブジェクト**-ユースケースを表示するサブシステム。|
|3|**関連付け**|アクターがユース ケースに関与することを示します。|
|4|**サブシステムまたはコンポーネント**|作業しているシステムまたはアプリケーション、またはその一部。 大規模なネットワークからアプリケーション内の単一のクラスまで、あらゆるものが含まれます。<br /><br /> システムまたはコンポーネントがサポートするユース ケースは、長方形の中に表示されます。 一部のユース ケースを長方形の外側に表示して、システムの範囲を明確にすると役立つ場合があります。<br /><br /> ユース ケース図の中のサブシステムは、基本的にはコンポーネント図の中のコンポーネントと同じ型です。<br /><br /> -   **間接的にインスタンス化され** ます。 false の場合、実行中のシステムには、このサブシステムに直接対応する1つ以上のオブジェクトがあります。 True の場合は、サブシステムは、その構成パートのインスタンス化によってのみ実行中のシステムに表示される、設計内の構造体です。|

### <a name="structuring-use-cases"></a>ユース ケースの構成
 ![包含、拡張および汎化を含むユース ケース](../modeling/media/uml-ucovstructure.png "UML_UCOvStructure")

|図形|**Element**|説明|
|-----------|-----------------|-----------------|
|5|**用意**|包含する側のユース ケースは、包含される側のユースケースを呼び出します。 包含は、ユース ケースがさらに詳細な手順に分かれることを示すために使用します。 包含される側のユース ケースは、矢じり付きの端部にあります。<br /><br /> この図は手順の順序を示すものではないことに注意してください。 アクティビティ図、シーケンス図、またはその他のドキュメントを使用して、これらの詳細について記述することができます。|
|6|**延長**|拡張する側のユース ケースは、拡張される側のユース ケースに目標とステップを追加します。 拡張は、特定の条件下でのみ動作します。 拡張される側のユース ケースは、矢じり付きの端部にあります。<br /><br /> この図は拡張を適用する厳密な状況を示すわけではないことに注意してください。それらはコメントやその他のドキュメントに記録できます。|
|7|**継承**|特化された要素と汎化された要素を関連付けします。 汎用化された要素は、矢じり付きの端部にあります。<br /><br /> 特化されたユース ケースは、その汎化の目標とアクターを継承することが可能で、それらを実現するために、より具体的な目標と手順を追加することができます。<br /><br /> 特化されたアクターは、その汎化のユース ケース、属性、および関連付けを継承し、さらに追加できます。|
|8|**依存関係**|ソースの設計が、ターゲットの設計に依存していることを示します。|
|9|**解説**|図に一般的な注記を追加するために使用します。|
|10|**Artifact**|成果物は、別の図またはドキュメントへのリンクを提供します。 これは、ソリューション エクスプ ローラーからファイルをドラッグして作成することができます。 また、図上の他の要素への依存関係とリンクできます。 成果物は通常、ユース ケースを詳細に説明するシーケンス図、OneNote ページ、Word 文書や PowerPoint プレゼンテーションにユース ケースをリンクさせるために使用します。 ドキュメントは、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューション内の項目でも、SharePoint サイトなどの共有の場所にあるドキュメントでも可能です。<br /><br /> -   **Hyperlink**。 図またはドキュメントの URL またはファイルのパス。<br /><br /> 成果物をダブルクリックすると、リンク先のファイルまたは Web ページが開きます。|
|11 (非表示)|**パッケージ**|パッケージ内には、ユース ケース、アクター、およびサブシステムを格納できます。 パッケージ図形は図に表示されませんが、図の **linkedpackage** プロパティを設定できます。 図に後に作成する要素は、パッケージ内に配置されます。 詳細については、「 [Define packages and namespace](../modeling/define-packages-and-namespaces.md)」を参照してください。|

## <a name="see-also"></a>参照
 [Uml ユースケース図: ガイドライン](../modeling/uml-use-case-diagrams-guidelines.md)[編集 uml モデルと図](../modeling/edit-uml-models-and-diagrams.md) [uml シーケンス図: リファレンス](../modeling/uml-sequence-diagrams-reference.md)Uml[クラス図](../modeling/uml-class-diagrams-reference.md): リファレンス uml[コンポーネント図](../modeling/uml-component-diagrams-reference.md): リファレンス[uml コンポーネント図: リファレンス](../modeling/uml-component-diagrams-reference.md)
