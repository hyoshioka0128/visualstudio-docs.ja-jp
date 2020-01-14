---
title: 'シナリオ: 視覚化とモデリングを使用してデザインを変更するMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- code visualization [Visual Studio ALM]
- modeling software [Visual Studio ALM]
- software modeling [Visual Studio ALM]
- walkthroughs [Visual Studio ALM], visualizing code
- walkthrough [Visual Studio ALM], visualizing code
- walkthrough [Visual Studio ALM], modeling software
- walkthroughs [Visual Studio ALM], modeling software
ms.assetid: ccc80825-a4a0-44fa-a0bb-f95254785a3b
caps.latest.revision: 63
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 70cc3c81c426ec55d0afb36360155786ec97d937
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75918978"
---
# <a name="scenario-change-your-design-using-visualization-and-modeling"></a>シナリオ: 視覚化およびモデリングを使用したデザインの変更
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ソフトウェア システムがユーザーのニーズを確実に満たすようにするには、Visual Studio の視覚化およびモデリング ツールを使用します。 UML (Unified Modeling Language) 図、コード マップ、レイヤー図、およびクラス図などのツールを使用して、次のタスクを実行します。

 どのバージョンの Visual Studio が各ツールをサポートしているかについては、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

- ユーザーの要求およびビジネス プロセスを明らかにする。

- 既存のコードを視覚化して精査する。

- 既存のシステムに対する変更を記述する。

- システムが要求を満たしていることを確認する。

- コードと設計の一致を維持する。

  このチュートリアルでは、以下が扱われます。

- これらのツールをソフトウェア プロジェクトで使用する利点を説明します。

- 開発方法に関係なく、これらのツールを使用する方法をサンプル シナリオを使って示します。

  これらのツールの詳細およびサポートされるシナリオについては、以下のトピックを参照してください。

- [アーキテクチャの分析およびモデリング](../modeling/analyze-and-model-your-architecture.md)

- [コードの視覚化](../modeling/visualize-code.md)

- [アプリのモデルを生成する](../modeling/create-models-for-your-app.md)

## <a name="ScenarioOverview"></a> シナリオの概要
 このシナリオでは、Dinner Now と Lucerne Publishing という 2 つの架空の企業のソフトウェア開発ライフサイクルの事例について説明します。 Dinner Now は、シアトルで Web ベースの料理宅配サービスを提供しています。 顧客は、Dinner Now の Web サイトで料理を注文し、料金を支払うことができます。 注文は最寄りのレストランに送信され、そこから料理が配達されます。 ニューヨークを拠点とする Lucerne Publishing は、オフラインとオンラインでさまざまなビジネスを展開しています。 その 1 つに、顧客がレストランのレビューを投稿できる Web サイトがあります。

 先ごろ Dinner Now を買収した Lucerne は、現在次のような変更を計画しています。

- Dinner Now にレストランのレビューの機能を追加して両社の Web サイトを統合する。

- Dinner Now の支払いシステムを Lucerne のシステムに置き換える。

- Dinner Now のサービスを地域全体に拡大する。

  Dinner Now では、スクラムとエクストリーム プログラミングを使用しています。 テスト カバレッジは非常に高く、サポートされていないコードはほとんどありません。 また、小規模な作業バージョンのシステムを作成して徐々に機能を追加することにより、リスクを最小限に抑えています。 さらに、短い頻繁なイテレーションでコードを開発することにより、 システム変更時の信頼性の確保、コードの頻繁なリファクタリング、および "Big Design Up Front (最初に大規模な設計を行うこと)" の回避を実現しています。

  一方、Lucerne のシステムははるかに大規模で複雑です。中には 40 年以上前のシステムもあります。 Lucerne は、広範囲にわたる複雑なレガシ コードがあるために変更に対してはきわめて慎重で、 ソリューションの詳細な設計や開発中の設計および変更の記録を重視する、より厳格な開発プロセスに従っています。

  Dinner Now と Lucerne はどちらも、ユーザーのニーズを満たすシステムを開発するために Visual Studio のモデル図を使用しています。 また、作業の計画、整理、および管理のために、Team Foundation Server を他のツールと共に使用しています。

  Team Foundation Server の詳細については、次のトピックを参照してください。

- [作業の計画および追跡](#PlanningTracking)

- [更新されたコードのテスト、検証、およびチェックイン](#TestValidateCheckInCode)

## <a name="ModelingDiagramsTools"></a> ソフトウェア開発におけるアーキテクチャ図とモデル図の役割
 ソフトウェア開発ライフサイクルのさまざまなステージにおけるこれらのツールの役割を次の表に示します。

||**ユーザー要求のモデリング**|**ビジネス プロセスのモデリング**|**システムのアーキテクチャと設計**|**コードの視覚化と精査**|**検証**|
|------|------------------------------------|-----------------------------------|--------------------------------------|------------------------------------------|----------------------|
|ユース ケース図 (UML)|√|√|||√|
|アクティビティ図 (UML)|√|√|√||√|
|クラス図 (UML)|√|√|√||√|
|コンポーネント図 (UML)|√|√|√||√|
|シーケンス図 (UML)|√|√|√||√|
|ドメイン固有言語 (DSL) 図|√|√|√|||
|レイヤー図、レイヤー検証|||√|√|√|
|コード マップ|||√|√|√|
|クラス デザイナー (コード ベース)||||√||

 UML 図とレイヤー図を描画するには、モデリング プロジェクトを作成する必要があります。既存のソリューションの一部として作成することも、そのために新しいソリューションを作成することもできます。 これらの図はモデリング プロジェクト内に生成する必要があります。 UML 図の項目は共通モデルの一部であり、UML 図は共通モデルのビューです。 レイヤー図の項目は、モデリング プロジェクトに配置されますが、共通モデルには格納されません。 コードから作成されたコード マップおよび .NET クラス図は、モデリング プロジェクトに含まれません。

 参照トピック

- [UML モデリング プロジェクトおよびダイアグラムを作成する](../modeling/create-uml-modeling-projects-and-diagrams.md)

- [コードからのレイヤー図の作成](../modeling/create-layer-diagrams-from-your-code.md)

- [ソリューション間の依存関係をマップする](../modeling/map-dependencies-across-your-solutions.md)

- [方法: プロジェクトにクラス ダイアグラムを追加する (クラス デザイナー)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md)

- [Modeling SDK for Visual Studio - ドメイン固有言語](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)

  アーキテクチャをさまざまな形で表示するために、同じモデルの要素を複数の異なる図で再利用できます。 たとえば、コンポーネントを別のコンポーネント図にドラッグしたり、シーケンス図にドラッグしてアクターとして使用したりすることができます。 「 [UML モデルとダイアグラムの編集」を](../modeling/edit-uml-models-and-diagrams.md)参照してください。

  Dinner Now と Lucerne Publishing は、開発中のコードで設計との一致を維持するためにレイヤー検証も使用しています。

  参照トピック

- [コードと設計の一致の維持](#ValidatingCode)

- [論理アーキテクチャの記述: レイヤー図](#DescribeLayers)

- [レイヤー図を使用したコードの検証](../modeling/validate-code-with-layer-diagrams.md)

  > [!NOTE]
  > Visual Studio のいくつかのバージョンでは、レイヤー検証と、視覚化およびモデリングのためのコード マップと UML 図の読み取り専用のバージョンがサポートされています。 この機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

## <a name="UnderstandingCommunicating"></a> システムに関する情報の把握と伝達
 Visual Studio のモデリング図は、使用する順番は特に決まっていません。したがって、それぞれのニーズや方法に合わせて使用できます。 モデルは通常、プロジェクト全体を通じて繰り返し頻繁に参照されます。 図にはそれぞれ長所があるため、さまざまな図を使用することにより、開発中のシステムのさまざまな側面を把握、記述、および伝達できます。

 Dinner Now と Lucerne は、プロジェクトに関するコミュニケーションのための共通の言語として図を使用しています。 たとえば、Dinner Now では次のような作業に図を使用しています。

- 既存のコードの視覚化。

- 新しいユーザー ストーリーや更新されたユーザー ストーリーの伝達。

- 新しいユーザー ストーリーや更新されたユーザー ストーリーをサポートするために必要な変更の特定。

  Lucerne では、次のような作業に図を使用しています。

- Dinner Now のビジネス プロセスの特定。

- システムの設計の把握。

- 新しいユーザー要求や更新されたユーザー要求の伝達。

- システムの更新の記録。

  これらの図は Team Foundation Server と統合されているため、Dinner Now と Lucerne にとっては作業の計画、管理、および追跡がより簡単になります。 たとえば、モデルを使用してテスト ケースと開発タスクを特定し、必要な作業を見積もることができます。 Lucerne では、進行状況を監視したり、システムがユーザーの要求を満たしていることを確認したりできるように、Team Foundation Server の作業項目をモデル要素にリンクしています。 たとえば、ユース ケースをテスト ケース作業項目にリンクして、すべてのテストに成功するとユース ケースが満たされたことがわかるようにしています。

  変更をチェックインする前には、レイヤー検証と自動テストを含むビルドを実行して、コードをテストと設計に照らし合わせて検証します。 これにより、更新されたコードが設計に矛盾していないこと、動作する既存の機能に悪影響を与えないことを確認できます。

  参照トピック

- [ビジネスプロセスにおけるシステムの役割について](#UnderstandingBPMandSystemDesign)

- [新規または更新されたユーザー要件の記述](#DescribingURM)

- [モデルからのテストの作成](#CreatingTests)

- [既存のシステムに対する変更の特定](#DeterminingChanges)

- [Keeping code consistent with the design](#ValidatingCode)

- [モデルの生成と使用に関する一般的なヒント](#GeneralTips)

- [作業の計画および追跡](#PlanningTracking)

- [更新されたコードのテスト、検証、およびチェックイン](#TestValidateCheckInCode)

### <a name="UnderstandingBPMandSystemDesign"></a>ビジネスプロセスにおけるシステムの役割について
 Lucerne は、Dinner Now のビジネス プロセスについてより深く知りたいと考えています。 そのため、Dinner Now に関する情報を整理するために以下の図を生成しました。

|**図**|**記述する内容**|
|-----------------|-------------------|
|*ユースケース図 (UML)*<br /><br /> 参照トピック<br /><br /> -   [UML ユースケース図: リファレンス](../modeling/uml-use-case-diagrams-reference.md)<br />[UML ユースケース図の -   : ガイドライン](../modeling/uml-use-case-diagrams-guidelines.md)|-現在のシステムでサポートされている活動<br />-アクティビティを実行するスタッフと外部システム<br />-各アクティビティをサポートするシステムの主要なコンポーネント<br />-現在のシステムの範囲外にあるビジネスプロセスの部分 (食品配送など)|
|*アクティビティ図 (UML)*<br /><br /> 参照トピック<br /><br /> -   [UML アクティビティ図: リファレンス](../modeling/uml-activity-diagrams-reference.md)<br />[UML アクティビティ図の -   : ガイドライン](../modeling/uml-activity-diagrams-guidelines.md)|顧客が注文を作成するときに実行されるステップのフロー|
|*クラスダイアグラム (UML)*<br /><br /> 参照トピック<br /><br /> -   [UML クラス図: リファレンス](../modeling/uml-class-diagrams-reference.md)<br />-   [UML クラス図: ガイドライン](../modeling/uml-class-diagrams-guidelines.md)|議論に使用されるビジネス エンティティと用語、およびそれらのエンティティの間の関係 (たとえば、このシナリオの用語には "注文" や "メニュー品目" などが含まれます)|

 たとえば、Dinner Now の Web サイトで実行されるタスクと、それらのタスクを実行する人を把握するために、次のようなユース ケース図を生成しました。

 ![UML ユース ケース図](../modeling/media/uml-usecase.png "UML_UseCase")

 **UML ユース ケース図**

 次のアクティビティ図は、Dinner Now の Web サイトで顧客が注文を作成するときに実行されるステップのフローを記述しています。 このリリースでは、ロールがコメント要素で示され、ステップをロール別に整理する *スイムレーン*が線で作成されます。

 ![UML アクティビティ図](../modeling/media/uml-dinnernowprocess.png "UML_DinnerNowProcess")

 **UML アクティビティ図**

 次のクラス図は、注文プロセスに参加するエンティティを記述しています。

 ![UML クラス図](../modeling/media/uml-dinnerorders.png "UML_DinnerOrders")

 **UML クラス図**

### <a name="DescribingURM"></a>新規または更新されたユーザー要件の記述
 Lucerne は、Dinner Now のシステムに機能を追加して、顧客がレストランのレビューを読んだり投稿したりできるようにしたいと考えています。 そのため、この新しい要求を記述し、それについて議論できるようにするために、以下の図を更新しました。

|**図**|**記述する内容**|
|-----------------|-------------------|
|*ユースケース図 (UML)*<br /><br /> 参照トピック<br /><br /> -   [UML ユースケース図: リファレンス](../modeling/uml-use-case-diagrams-reference.md)<br />[UML ユースケース図の -   : ガイドライン](../modeling/uml-use-case-diagrams-guidelines.md)|"レストランのレビューを書く" ための新しいユース ケース|
|*アクティビティ図 (UML)*<br /><br /> 参照トピック<br /><br /> -   [UML アクティビティ図: リファレンス](../modeling/uml-activity-diagrams-reference.md)<br />[UML アクティビティ図の -   : ガイドライン](../modeling/uml-activity-diagrams-guidelines.md)|顧客がレストランのレビューを書くときに実行されるステップ|
|*クラスダイアグラム (UML)*<br /><br /> 参照トピック<br /><br /> -   [UML クラス図: リファレンス](../modeling/uml-class-diagrams-reference.md)<br />-   [UML クラス図: ガイドライン](../modeling/uml-class-diagrams-guidelines.md)|レビューを格納するために必要なデータ|

 たとえば、次のユース ケース図には、この新しい要求を表す新しいユース ケース "Write Review" が含まれています。 すぐにわかるようにオレンジ色で強調表示されています。

 ![UML ユース ケース図](../modeling/media/uml-writerev.png "UML_WriteRev")

 **UML ユースケース図**

 次のアクティビティ図には、新しいユース ケースのステップのフローを記述するオレンジ色の新しい要素が含まれています。

 ![UML アクティビティ図](../modeling/media/uml-writereview.png "UML_WriteReview")

 **UML アクティビティ図**

 次のクラス図には、新しい Review クラスが含まれています。このクラスの他のクラスとの関係も示されています。これにより、このクラスの詳細について議論できます。 この図からは、Customer と Restaurant が複数の Review を持てることがわかります。

 ![UML クラス図](../modeling/media/uml-dinnerreviews.png "UML_DinnerReviews")

 **UML クラス図**

### <a name="CreatingTests"></a>モデルからのテストの作成
 Dinner Now と Lucerne は、システムに変更を加える前にシステムとそのコンポーネントの完全なテスト セットを用意する必要があるという点で合意しました。 Lucerne には、システム レベルとコンポーネント レベルのテストを担当する専任のチームが存在します。 このチームは、Dinner Now で生成されたテストを再利用し、UML 図を使用して次のように構成しました。

- 各ユース ケースを 1 つまたは複数のテストで表し、 ユース ケース図の要素を Team Foundation Server のテスト ケース作業項目にリンクします。

- アクティビティ図またはシステム レベルのシーケンス図の各フローを少なくとも 1 つのテストにリンクして、 アクティビティ図のすべてのパスを体系的にテストできるようにします。

- ユース ケース図、クラス図、およびアクティビティ図の定義に基づく用語を使用してテストを記述します。

  要求が変更され、その変更を反映して図が更新されたら、テストも更新します。 要求は、テストに成功した場合にのみ満たされたと見なされます。 可能であれば、実装を開始する前に UML 図に基づいてテストを定義します。

  参照トピック

- [モデルからテストを開発する](../modeling/develop-tests-from-a-model.md)

- [UML モデルの検証](../modeling/validate-your-uml-model.md)

### <a name="DeterminingChanges"></a> Identifying Changes to the Existing System
 Dinner Now では、新しい要求を満たすためのコストを見積もる必要があります。 これは、その変更がシステムの他の部分にどのくらい影響するかによって違ってきます。 そのため、Dinner Now の開発者の 1 人が、既存のコードから次のマップと図を作成しました。

|**マップまたは図**|**表示される内容**|
|------------------------|---------------|
|*コード マップ*<br /><br /> 参照トピック<br /><br /> [ソリューション間の依存関係をマップ -   に](../modeling/map-dependencies-across-your-solutions.md)は<br />[コードマップを参照および再配置](../modeling/browse-and-rearrange-code-maps.md)-   には<br />[DGML ファイルを編集してコードマップをカスタマイズ -   には](../modeling/customize-code-maps-by-editing-the-dgml-files.md)|コード内の依存関係とその他の関係。<br /><br /> たとえば、Dinner Now はまず、アセンブリのコード マップでアセンブリとその依存関係の概要を確認するとします。 そのとき、マップの詳細を表示してそれらのアセンブリの名前空間やクラスを調べることができます。<br /><br /> さらに、コードの特定の領域やその他の種類のリレーションシップを調べるためのマップを生成することもできます。 対象となる領域やリレーションシップを見つけて選択するにはソリューション エクスプローラーを使用します。|
|*コード ベースのクラス図*<br /><br /> 「 [How to: Add Class Diagrams to Projects (Class Designer)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md)」を参照してください。|コード内の既存のクラス。|

 たとえば、開発者はコード マップを作成します。 新しいシナリオの影響を受ける領域に合わせてスコープを調整します。 次のマップでは、それらの領域が選択されて強調表示されています。

 ![名前空間の依存関係グラフ](../modeling/media/namespace-reviewsystem.png "Namespace_ReviewSystem")

 **名前空間のコード マップ**

 選択した名前空間を展開すると、その名前空間のクラス、メソッド、および関係が表示されます。

 ![展開された名前空間の依存関係グラフ](../modeling/media/dep-reviewsystem.png "Dep_ReviewSystem")

 **展開された名前空間のコード マップ (グループ間リンクが表示されています)**

 こうしてコードを調べることにより、影響を受けるクラスとメソッドを見つけることができます。 それらに加えた変更による影響を確認するには、それぞれの変更後にコード マップを再生成します。 「[コードの視覚化](../modeling/visualize-code.md)」を参照してください。

 コンポーネントや相互作用など、システムの他の部分に対する変更を記述するには、それらの要素をホワイトボードに描くこともできますが、 Visual Studio で以下の図を描画すると、Dinner Now と Lucerne の双方で詳細を記録、管理、および把握できます。

|**図**|**記述する内容**|
|------------------|-------------------|
|*アクティビティ図 (UML)*<br /><br /> 参照トピック<br /><br /> -   [UML アクティビティ図: リファレンス](../modeling/uml-activity-diagrams-reference.md)<br />[UML アクティビティ図の -   : ガイドライン](../modeling/uml-activity-diagrams-guidelines.md)|顧客が以前に利用したことのあるレストランで注文を行った場合に、それを検出して顧客にレビューを求めるときに実行されるステップのフロー。|
|*クラスダイアグラム (UML)*<br /><br /> 参照トピック<br /><br /> -   [UML クラス図: リファレンス](../modeling/uml-class-diagrams-reference.md)<br />-   [UML クラス図: ガイドライン](../modeling/uml-class-diagrams-guidelines.md)|論理クラスとその関係。 たとえば、レビューを表す **Review** という新しいクラスを追加して、 **Restaurant**、 **Menu**、 **Customer**などの他のエンティティとの関係を記述します。<br /><br /> レビューを顧客に関連付けるには、システムで顧客の詳細を格納する必要があります。 UML クラス図を使用すると、それらの詳細がわかりやすくなります。|
|*コード ベースのクラス図*<br /><br /> 「 [How to: Add Class Diagrams to Projects (Class Designer)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md)」を参照してください。|コード内の既存のクラス。|
|*コンポーネント図 (UML)*<br /><br /> 参照トピック<br /><br /> -   [UML コンポーネント図: リファレンス](../modeling/uml-component-diagrams-reference.md)<br />-   [UML コンポーネント図: ガイドライン](../modeling/uml-component-diagrams-guidelines.md)|システムの高レベルのパート (Dinner Now Web サイトなど) とそのインターフェイス。 これらのインターフェイスは、コンポーネントがメソッドやサービスを提供および使用して相互作用する方法を定義します。|
|*シーケンス図 (UML)*<br /><br /> 参照トピック<br /><br /> -   [UML シーケンス図: リファレンス](../modeling/uml-sequence-diagrams-reference.md)<br />[UML シーケンス図の -   : ガイドライン](../modeling/uml-sequence-diagrams-guidelines.md)|インスタンス間の相互作用のシーケンス。|

 たとえば、次のコンポーネント図には、Dinner Now Web Site コンポーネントのパートである新しいコンポーネントが示されています。 オレンジ色で強調表示されているこの ReviewProcessing コンポーネントは、レビューを生成する機能を処理します。

 ![UML コンポーネント図](../modeling/media/uml-internal.png "UML_Internal")

 **UML コンポーネント図**

 次のシーケンス図は、顧客が以前に利用したことのあるレストランかどうかを Dinner Now Web Site がチェックするときに発生する相互作用のシーケンスを示しています。 利用したことのあるレストランだった場合はレビューの生成を求めます。生成されたレビューはそのレストランに送信され、Web サイトで公開されます。

 ![UML シーケンス図](../modeling/media/uml-revsystem.png "UML_RevSystem")

 **UML シーケンス図**

### <a name="ValidatingCode"></a> コードと設計の一致の維持
 Dinner Now では、更新されたコードが設計と一致していることを確認する必要があります。 そのため、システムの機能のレイヤーを記述するレイヤー図を生成し、レイヤー間で許容される依存関係を指定して、ソリューションの成果物をそれらのレイヤーに関連付けました。

|**図**|**記述する内容**|
|-----------------|-------------------|
|*レイヤー図*<br /><br /> 参照トピック<br /><br /> [コードからレイヤー図を作成 -   に](../modeling/create-layer-diagrams-from-your-code.md)は<br />-   [レイヤー図: リファレンス](../modeling/layer-diagrams-reference.md)<br />-   [レイヤー図: ガイドライン](../modeling/layer-diagrams-guidelines.md)<br />[レイヤー図を使用してコードを検証 -   に](../modeling/validate-code-with-layer-diagrams.md)は|コードの論理アーキテクチャ。<br /><br /> レイヤー図では、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューション内の成果物が整理されて、 *レイヤー*と呼ばれる抽象的なグループにマップされます。 これらのレイヤーは、それらの成果物がシステムで実行するロール、タスク、または機能を識別します。<br /><br /> レイヤー図は、必要とされるシステムの設計を記述し、コードの変更をその設計に照らし合わせて検証するのに便利です。<br /><br /> レイヤーを作成するには、ソリューション エクスプローラー、コード マップ、クラス ビュー、およびオブジェクト ブラウザーから項目をドラッグします。 新しいレイヤーを描画するには、ツールボックスを使用するか、図の画面を右クリックします。<br /><br /> 既存の依存関係を表示するには、レイヤー図の画面を右クリックし、 **[依存関係の生成]** をクリックします。 必要とされる依存関係を指定するには、新しい依存関係を描画します。|

 たとえば、次のレイヤー図は、レイヤー間の依存関係と、各レイヤーに関連付けられている成果物の数を記述しています。

 ![統合支払いシステムのレイヤー図](../modeling/media/layer-integrated-dnlucerne.png "Layer_Integrated_DNLucerne")

 **レイヤー図**

 Dinner Now と Lucerne は、コードの開発中に設計との競合が起こらないようにするために、Team Foundation ビルドで実行されるビルドでレイヤー検証を使用しています。 また、チェックイン操作でレイヤー検証を要求するカスタム MSBuild タスクを作成し、 ビルド レポートを使用して検証エラーを収集しています。

 参照トピック

- [ビルド プロセスの定義](https://msdn.microsoft.com/library/61593e10-d24b-492f-b19a-af4d85abea6b)

- [変更内容を検証するためのゲート チェックイン ビルド プロセスの定義](https://msdn.microsoft.com/library/9cfc8b9c-1023-40fd-8ab5-1b1bd9c172ec)

- [ビルド プロセス テンプレートのカスタマイズ](https://msdn.microsoft.com/library/b94c58f2-ae6f-4245-bedb-82cd114f6039)

### <a name="GeneralTips"></a> General Tips for Creating and Using Models

- ほとんどの図は、線で接続された一連のノードで構成されています。 図の種類ごとに異なるノードと線がツールボックスに表示されます。

   ツールボックスを開くには、 **[表示]** メニューの **[ツールボックス]** をクリックします。

- ノードを生成するには、ツールボックスから図にノードをドラッグします。 既存のノードにドラッグする必要がある種類のノードもあります。 たとえば、コンポーネント図では、新しいポートは既存のコンポーネントに追加する必要があります。

- 線 (接続) を生成するには、ツールボックスで適切なツールをクリックし、ソース ノードをクリックしてから、ターゲット ノードをクリックします。 特定の種類のノードの間にしか生成できない線もあります。 ソースまたはターゲットにするノードをポイントすると、接続を生成できるかどうかが示されます。

- UML 図で項目を生成すると、その項目が共通モデルにも追加されます。 モデリング プロジェクトの UML 図は、そのモデルのビューです。 レイヤー図の項目は、モデリング プロジェクトの一部ですが、共通モデルには格納されません。

   モデルを確認するには、 **[アーキテクチャ]** メニューの  **[ウィンドウ]** をポイントし、 **[UML モデル エクスプローラー]** をクリックします。

- **UML モデル エクスプローラー** から UML 図に項目をドラッグできる場合もあります。 アーキテクチャをさまざまな形で表示するために、同じモデルの要素を複数の異なる図で再利用できます。 たとえば、コンポーネントを別のコンポーネント図にドラッグしたり、シーケンス図にドラッグしてアクターとして使用したりすることができます。

- Visual Studio は UML 2.1.2 をサポートします。 この概要で説明するのはこのリリースの UML 図の主要な機能だけですが、UML およびその使用方法を詳しく説明している書籍は数多くあります。

  「[アプリのモデルを作成する」を](../modeling/create-models-for-your-app.md)参照してください。

### <a name="PlanningTracking"></a> Planning and Tracking Work
 Visual Studio のモデリング図は Team Foundation Server と統合されているため、Dinner Now と Lucerne にとって作業の計画、管理、および追跡がより簡単になります。 Dinner Now と Lucerne はどちらも、モデルを使用してテスト ケースと開発タスクを特定し、必要な作業を見積もることができます。 Lucerne では、Team Foundation Server の作業項目を作成し、ユース ケースやコンポーネントなどのモデル要素にリンクしています。 これにより、作業の進行状況を監視したり、関連するユーザーの要求を見直して、 変更後も引き続きそれらの要求が満たされていることを確認したりできます。

 Dinner Now と Lucerne は、作業の進行に伴って、タスクに費やされた時間を反映して作業項目を更新できます。 また、Team Foundation Server の以下の機能を使用して、作業の状況を監視および報告できます。

- 計画された作業を予定どおりに完了できるかどうかを示す日次 *バーンダウン レポート* 。 Team Foundation Server で他の同様のレポートを生成してバグの状況を追跡することもできます。

- Microsoft Excel を使用してチームのメンバーの作業負荷を監視および調整できる *イテレーション ワークシート* 。 このワークシートは Team Foundation Server にリンクされており、進行状況に関する定例会議で資料として使用できます。

- Office Project を使用してプロジェクトに関する重要な情報をチームに伝える *開発ダッシュボード* 。

  参照トピック

- [Visual Studio Team Services または Team Foundation Server を使用した作業の追跡](https://msdn.microsoft.com/library/52aa8bc9-fc7e-4fae-9946-2ab255ca7503)

- [モデル要素と作業項目とのリンク](../modeling/link-model-elements-and-work-items.md)

- [Visual Studio ALM のグラフ、ダッシュボード、およびレポート](https://msdn.microsoft.com/library/1f28ba6c-c5e5-46d3-9209-ede24ae78e48)

- [Project を使用したバックログとタスクの作成](https://msdn.microsoft.com/library/be5cef4f-755f-4ffe-8dd7-876d1e02c330)

### <a name="TestValidateCheckInCode"></a> コードのテスト、検証、およびチェックイン
 Dinner Now と Lucerne は、作業が完了するたびにコードを Team Foundation バージョン管理にチェックインします。その作業を忘れると、Team Foundation Server から通知されます。 Team Foundation Server でチェックインが受け入れられるためには、単体テストとレイヤー検証を実行して、コードをテスト ケースと設計に照らし合わせて検証する必要があります。 Dinner Now と Lucerne は、Team Foundation Server を使用して、ビルド、自動化された単体テスト、およびレイヤー検証を定期的に実行しています。 これにより、コードが以下の基準を満たしていることを確認できます。

- 正常に動作する。

- 既存の動作するコードを破損させない。

- 設計と一致している。

  Dinner Now には数多くの自動テストがあり、そのほとんどを引き続き適用できるため、Lucerne でそれらを再利用することができます。 新しい機能をカバーするために、それらのテストに変更を加えたり、新しいテストを追加したりすることもできます。 Dinner Now と Lucerne の両方で Visual Studio による手動テストも実行されます。

  また、コードが設計に準拠していることを確認するために、Team Foundation ビルドでレイヤー検証を含むビルドを構成しています。 競合が発生した場合は、詳細なレポートが生成されます。

  参照トピック

- [アプリケーションのテスト](https://msdn.microsoft.com/library/796b7d6d-ad45-4772-9719-55eaf5490dac)

- [開発時のシステムの検証](../modeling/validate-your-system-during-development.md)

- [バージョン管理の使用](/azure/devops/repos/tfvc/overview?view=azure-devops)

- [アプリケーションのビルド](/azure/devops/pipelines/index)

## <a name="UpdatingSystem"></a> Updating the System Using Visualization and Modeling
 Lucerne と Dinner Now は、支払いシステムを統合する必要があります。 以降では、この作業に役立つ Visual Studio のモデル図について説明します。

- [ユーザーの要件を理解する: ユースケース図](#UnderstandUseCases)

- [ビジネスプロセスを理解する: アクティビティ図](#UnderstandActivities)

- [システム構造の記述: コンポーネント図](#DescribeComponents)

- [相互作用の説明: シーケンス図](#DescribeSequence)

- [既存のコードの視覚化: コード マップ](#VisualizeCode)

- [型の用語集の定義: クラス図](#DefineClasses)

- [論理アーキテクチャの記述: レイヤー図](#DescribeLayers)

  参照トピック

- [アプリのモデルを生成する](../modeling/create-models-for-your-app.md)

- [コードの視覚化](../modeling/visualize-code.md)

- [開発プロセス内でのモデルの使用](../modeling/use-models-in-your-development-process.md)

- [ユーザー要件のモデリング](../modeling/model-user-requirements.md)

- [アプリのアーキテクチャをモデル化する](../modeling/model-your-app-s-architecture.md)

### <a name="UnderstandUseCases"></a>ユーザーの要件を理解する: ユースケース図
 ユース ケース図には、システムがサポートするアクティビティと、それらのアクティビティを実行する人の概要が示されます。 Lucerne では、ユース ケース図を使用することにより、Dinner Now のシステムについて以下の情報を得ることができます。

- 顧客が注文を作成する。

- レストランが注文を受け取る。

- Dinner Now Payment System が支払いの検証に使用する External Payment Processor Gateway は、Web サイトのスコープに含まれない。

  この図からは、いくつかの主要なユース ケースがより小さなユース ケースに分割されていることもわかります。 Lucerne は自社の支払いシステムを使用したいと考えているため、 Process Payment ユース ケースを別の色で強調表示して、変更が必要なことを示しています。

  ![ユースケース図でのプロセスの支払いの強調表示](../modeling/media/uml-processpay.png "UML_ProcessPay")

  **ユースケース図でのプロセスの支払いの強調表示**

  開発時間が短い場合は、顧客が直接レストランに料金を支払うようにすることを検討する可能性もあります。 そのことを示すには、Process Payment ユース ケースを Dinner Now のシステム境界の外側にあるユース ケースに置き換えて、 Customer を直接 Restaurant にリンクします。これにより、Dinner Now では注文の処理のみを行うことが示されます。

  ![ユースケース図でのレストランの従量課金](../modeling/media/uml-payrestaurant.png "UML_PayRestaurant")

  **ユースケース図でのレストランの従量課金**

  参照トピック

- [UML ユース ケース図: リファレンス](../modeling/uml-use-case-diagrams-reference.md)

- [UML ユース ケース図: ガイドライン](../modeling/uml-use-case-diagrams-guidelines.md)

#### <a name="drawing-a-use-case-diagram"></a>ユース ケース図の描画
 ユース ケース図の主な機能を以下に示します。

- *アクター* は、人、組織、マシン、またはソフトウェア システムのロールを表します。 たとえば、Customer、Restaurant、および Dinner Now Payment System はアクターです。

- *ユース ケース* は、アクターと開発中のシステムの間の相互作用を表します。  1 回のマウス クリックや 1 つのメッセージから何日にも及ぶトランザクションまで、あらゆる規模の相互作用を表すことができます。

- *関連* は、アクターをユース ケースにリンクします。

- 大きなユース ケースに小さなユース ケースを *包含* することができます。たとえば、Create Order は Select Restaurant を包含しています。 ユース ケースを *拡張* することもできます。拡張されたユース ケースにはゴールとステップが追加されます。これにより、そのユース ケースが特定の状況でのみ発生することが示されます。 ユース ケース間の継承もできます。

- *サブシステム* は、開発中のソフトウェア システムまたはそのコンポーネントを表します。 ユース ケースを囲む大きな枠がサブシステムです。 ユース ケース図では、要素がサブシステム境界の内側にあるか外側にあるかが明確に示されます。 ユーザーが特定のゴールを別の方法で達成しなければならないことを示すには、それらのユース ケースをサブシステム境界の外側に描画します。

- *成果物* は、図の要素を他の図またはドキュメントにリンクします。

  参照トピック

- [UML ユース ケース図: リファレンス](../modeling/uml-use-case-diagrams-reference.md)

- [UML ユース ケース図: ガイドライン](../modeling/uml-use-case-diagrams-guidelines.md)

#### <a name="summary-strengths-of-use-case-diagrams"></a>まとめ: ユース ケース図の長所
 ユース ケース図を使用すると、以下の要素を視覚化できます。

- システムがサポートするアクティビティまたはサポートしないアクティビティ

- それらのアクティビティを実行する人または外部システム

- 各アクティビティをサポートするシステムの主要コンポーネント (親システム内に入れ子にされたサブシステムとして表すことができます)

- ユース ケースがより小さなユース ケースやバリエーションに分割されるしくみ

#### <a name="relationship-to-other-diagrams"></a>他の図との関係

|**図**|**記述する内容**|
|-----------------|-------------------|
|アクティビティ図|ユース ケース内のステップのフローと、そのユース ケースでそれらのステップを実行する人。<br /><br /> ユース ケースの名前は、多くの場合、アクティビティ図のステップを反映しています。 アクティビティ図は、デシジョン、マージ、入力と出力、同時実行フローなどの要素をサポートしています。<br /><br /> 参照トピック<br /><br /> -   [UML アクティビティ図: リファレンス](../modeling/uml-activity-diagrams-reference.md)<br />[UML アクティビティ図の -   : ガイドライン](../modeling/uml-activity-diagrams-guidelines.md)|
|シーケンス図|ユース ケースの参加要素の間の相互作用のシーケンス。<br /><br /> 参照トピック<br /><br /> -   [UML シーケンス図: リファレンス](../modeling/uml-sequence-diagrams-reference.md)<br />[UML シーケンス図の -   : ガイドライン](../modeling/uml-sequence-diagrams-guidelines.md)|
|クラス図 (UML)|ユース ケースに参加するエンティティまたは型。<br /><br /> 参照トピック<br /><br /> -   [UML クラス図: リファレンス](../modeling/uml-class-diagrams-reference.md)<br />-   [UML クラス図: ガイドライン](../modeling/uml-class-diagrams-guidelines.md)|

### <a name="UnderstandActivities"></a>ビジネスプロセスを理解する: アクティビティ図
 アクティビティ図は、ビジネス プロセスのステップのフローを記述して、ワークフローを簡単に伝達できるようにします。 1 つの開発プロジェクトに複数のアクティビティ図を含めることができます。 通常は、1 つの外部アクション (料理の注文、メニューの更新、新しいレストランの追加など) に起因するすべてのアクションがアクティビティに含まれます。 複雑なアクションの詳細をアクティビティで記述する場合もあります。

 Lucerne は、Lucerne が支払いを処理してレストランへの支払いを行うことを示すために、アクティビティ図を次のように更新して、 Dinner Now Payment System を Lucerne Payment System に置き換えました (変更箇所が強調表示されています)。

 ![アクティビティ図の Lucerne 支払いシステム](../modeling/media/uml-lucerne.png "UML_Lucerne")

 **アクティビティ図の夕食の支払いシステムを置き換える**

 この更新された図を使用することで、Lucerne Payment System がビジネス プロセスのどこに組み込まれるのかを視覚化できます。 このリリースでは、ステップを実行するロールがコメントで示され、 ステップをロール別に整理する *スイムレーン*が線で作成されます。

 そのほかに、注文の料理が配達された後に顧客が直接レストランに料金を支払うという選択肢を検討する可能性もあります。 その場合は、ソフトウェア システムに対する要求が変わります。

 Dinner Now では、これらの図を以前はホワイトボードや PowerPoint で描いていましたが、 現在は Visual Studio も使用しています。これにより、Dinner Now と Lucerne の双方で詳細を記録、把握、および管理できます。

 参照トピック

- [UML アクティビティ図: リファレンス](../modeling/uml-activity-diagrams-reference.md)

- [UML アクティビティ図: ガイドライン](../modeling/uml-activity-diagrams-guidelines.md)

#### <a name="drawing-an-activity-diagram"></a>アクティビティ図の描画
 アクティビティ図の主な機能を以下に示します。

- アクティビティの最初のアクションを示す *開始ノード* 。

   アクティビティ図には常に開始ノードが 1 つ必要です。

- ユーザーまたはソフトウェアがタスクを実行するステップを記述する*アクション* 。

- アクション間のフローを示す*制御フロー* 。

- フローの条件分岐を表す*デシジョン ノード* 。

- 1 つのフローを複数の同時実行フローに分割する*フォーク ノード* 。

- アクティビティの終了を示す*アクティビティ終了ノード* 。

   これらのノードは必須ではありませんが、これらを図に含めると、アクティビティがどこで終了するのかわかるので便利です。

  参照トピック

- [UML アクティビティ図: リファレンス](../modeling/uml-activity-diagrams-reference.md)

- [UML アクティビティ図: ガイドライン](../modeling/uml-activity-diagrams-guidelines.md)

#### <a name="summary-strengths-of-activity-diagrams"></a>まとめ: アクティビティ図の長所
 アクティビティ図を使用すると、ビジネス、システム、またはプログラムのアクション間の制御フローと情報フローを視覚化および記述できます。 これにより、簡単にワークフローを記述して他の人々に伝達できます。

#### <a name="relationship-to-other-diagrams"></a>他の図との関係

|**図**|**説明**|
|-----------------|---------------------|
|ユース ケース図|各アクターが実行するアクティビティの概要を示します。<br /><br /> 参照トピック<br /><br /> -   [UML ユースケース図: リファレンス](../modeling/uml-use-case-diagrams-reference.md)<br />[UML ユースケース図の -   : ガイドライン](../modeling/uml-use-case-diagrams-guidelines.md)|
|コンポーネント図|明確に定義された一連のインターフェイスを通じて振る舞いを提供または使用する再利用可能なパートのコレクションとしてシステムを視覚化します。<br /><br /> 参照トピック<br /><br /> -   [UML コンポーネント図: リファレンス](../modeling/uml-component-diagrams-reference.md)<br />-   [UML コンポーネント図: ガイドライン](../modeling/uml-component-diagrams-guidelines.md)|

### <a name="DescribeComponents"></a>システム構造の記述: コンポーネント図
 コンポーネント図は、明確に定義された一連のインターフェイスを通じて振る舞いを提供または使用する分離可能なパートのコレクションとしてシステムを記述します。 パートは任意のスケールで記述でき、任意の方法で接続できます。

 Lucerne と Dinner Now は、システムのコンポーネントとそのインターフェイスを視覚化し、それらについて議論するために、次のようなコンポーネント図を生成しました。

 ![支払いシステムの外部コンポーネント](../modeling/media/uml-extdnpayment.png "UML_ExtDNPayment")

 **ディナー Now の支払いシステムのコンポーネント**

 この図には、さまざまな種類のコンポーネントと、それらの *依存関係*が示されています。 たとえば、Dinner Now Web Site と Lucerne Payment System は、支払いの検証のために External Payment Processor Gateway を必要とします。 コンポーネント間の矢印は依存関係を表します。依存関係は、コンポーネントが他のコンポーネントの機能を必要としていることを示します。

 Lucerne Payment System を使用するには、Lucerne Payment System の PaymentApproval インターフェイスと PayableInsertion インターフェイスを使用するように Dinner Now Web Site を更新する必要があります。

 次の図は、Dinner Now Web Site のコンポーネントの具体的な構成を示しています。 ここから、この Web サイトのインスタンスが次の 4 つの *パート*で構成されていることがわかります。

- CustomerProcessing

- OrderProcessing

- ReviewProcessing

- PaymentProcessing

  これらのパートは、指定されたコンポーネント型のインスタンスであり、次のように接続されています。

  ![ディナー Web サイト内のコンポーネント](../modeling/media/uml-dinnernow.png "UML_DinnerNow")

  **ディナー Now Web サイト内のコンポーネント**

  Dinner Now Web Site の振る舞いは、これらのパートに委譲されています。したがって、これらのパートがこの Web サイトの機能を処理します。 *委譲* は、親がインターフェイスで送受信するメッセージをどのパートが処理するかを示し、親コンポーネントとそのメンバー コンポーネントの間の矢印によって表されます。

  この構成では、顧客の支払いは PaymentProcessing コンポーネントによって処理されます。 したがって、Lucerne の支払いシステムと統合するためには、このコンポーネントを更新する必要があります。 場合によっては、コンポーネント型の複数のインスタンスが同じ親コンポーネントに存在することもあります。

  参照トピック

- [UML コンポーネント図: リファレンス](../modeling/uml-component-diagrams-reference.md)

- [UML コンポーネント図: ガイドライン](../modeling/uml-component-diagrams-guidelines.md)

#### <a name="drawing-a-component-diagram"></a>コンポーネント図の描画
 コンポーネント図の主な機能を以下に示します。

- 分離可能なシステム機能を表す*コンポーネント* 。

- コンポーネントによって実装され、他のコンポーネントまたは外部システムによって使用されるメッセージまたは呼び出しのグループを表す*提供インターフェイス ポート* 。

- コンポーネントが他のコンポーネントまたは外部システムに送信するメッセージまたは呼び出しのグループを表す*要求インターフェイス ポート* 。 この種類のポートは、コンポーネントが他のコンポーネントまたは外部システムに対して少なくとも要求する操作を記述します。

- コンポーネントのメンバーで、通常は他のコンポーネントのインスタンスである*パート* 。 パートは、親コンポーネントの内部設計の一部です。

- コンポーネントが他のコンポーネントの機能を必要としていることを示す*依存関係* 。

- 親コンポーネントによって送受信されるメッセージをそのコンポーネントのパートが処理することを示す*委譲* 。

  参照トピック

- [UML コンポーネント図: リファレンス](../modeling/uml-component-diagrams-reference.md)

- [UML コンポーネント図: ガイドライン](../modeling/uml-component-diagrams-guidelines.md)

#### <a name="summary-strengths-of-component-diagrams"></a>まとめ: コンポーネント図の長所
 コンポーネント図の長所を以下に示します。

- 実装の言語やスタイルに関係なく、システムを分離可能なパートのコレクションとして視覚化できます。

- 明確に定義されたインターフェイスを持つコンポーネントを視覚化できます。これにより、設計がわかりやすくなり、要求が変更された場合の更新も容易になります。

#### <a name="relationship-to-other-diagrams"></a>他の図との関係

|**図**|**説明**|
|-----------------|---------------------|
|コード マップ|既存のコード内の編成や関係を視覚化します。<br /><br /> コンポーネントの候補を特定するには、コード マップを生成し、項目をシステム内の機能別にグループ化します。<br /><br /> 参照トピック<br /><br /> [ソリューション間の依存関係をマップ -   に](../modeling/map-dependencies-across-your-solutions.md)は|
|シーケンス図|コンポーネント間またはコンポーネント内のパート間の相互作用のシーケンスを視覚化します。<br /><br /> コンポーネントからシーケンス図の生存線を生成するには、コンポーネントを右クリックし、 **[生存線の生成]** をクリックします。<br /><br /> 参照トピック<br /><br /> -   [UML シーケンス図: リファレンス](../modeling/uml-sequence-diagrams-reference.md)<br />[UML シーケンス図の -   : ガイドライン](../modeling/uml-sequence-diagrams-guidelines.md)|
|クラス図 (UML)|提供ポートまたは要求ポートのインターフェイスと、コンポーネントの機能を実装するクラスを定義します。<br /><br /> 参照トピック<br /><br /> -   [UML クラス図: リファレンス](../modeling/uml-class-diagrams-reference.md)<br />-   [UML クラス図: ガイドライン](../modeling/uml-class-diagrams-guidelines.md)|
|レイヤー図|コンポーネントに関連するシステムの論理アーキテクチャを記述します。 レイヤー検証を使用して、コードが設計と常に一致することを確認します。<br /><br /> 参照トピック<br /><br /> [コードからレイヤー図を作成 -   に](../modeling/create-layer-diagrams-from-your-code.md)は<br />-   [レイヤー図: リファレンス](../modeling/layer-diagrams-reference.md)<br />-   [レイヤー図: ガイドライン](../modeling/layer-diagrams-guidelines.md)<br />[レイヤー図を使用してコードを検証 -   に](../modeling/validate-code-with-layer-diagrams.md)は|
|アクティビティ図|受信メッセージに対する応答としてコンポーネントによって実行される内部処理を視覚化します。<br /><br /> 参照トピック<br /><br /> -   [UML アクティビティ図: リファレンス](../modeling/uml-activity-diagrams-reference.md)<br />[UML アクティビティ図の -   : ガイドライン](../modeling/uml-activity-diagrams-guidelines.md)|

### <a name="VisualizeCode"></a> 既存のコードの視覚化: コード マップ
 コード マップは、コード内の現在の編成やリレーションシップを示します。 マップの *ノード* によって項目が表され、 *リンク*によってリレーションシップが表されます。 コード マップは次のような作業に役立ちます。

- よく知らないコードを調べる。

- 提案された変更が既存のコードのどこにどのような影響を与えるのかを把握する。

- 複雑な領域、自然レイヤー、パターンなど、改良の余地がある領域を見つける。

  たとえば、Dinner Now では PaymentProcessing コンポーネントの更新のコストを見積もる必要があります。 これは、その変更がシステムの他の部分にどのくらい影響するかによって違ってきます。 そのため、Dinner Now の開発者の 1 人がコードからコード マップを生成し、変更の影響を受ける領域に合わせてスコープを調整しました。

  次のマップは、PaymentProcessing クラスと Dinner Now システムの他の部分との依存関係を示しています。該当する箇所が選択されています。

  ![ディナー Now の支払いシステムの依存関係グラフ](../modeling/media/dep-dnpayment.png "Dep_DNPayment")

  **Dinner Now の支払いシステムのコード マップ**

  開発者はこのマップを調べるために、PaymentProcessing クラスを展開してそのメンバーを選択します。これにより、影響を受ける可能性がある領域が表示されます。

  ![PaymentProcessing 内のメソッドと依存関係](../modeling/media/depgraph-expandeddn.png "DepGraph_ExpandedDN")

  **PaymentProcessing クラス内のメソッドとその依存関係**

  さらに、Lucerne Payment System のクラス、メソッド、および依存関係を調べるために次のマップを生成しました。 これにより、Dinner Now のその他のパートと相互作用するためには Lucerne のシステムにも手を加える必要があることがわかりました。

  ![Lucerne の支払いシステムの依存関係グラフ](../modeling/media/depgraph-lucernepay.png "DepGraph_LucernePay")

  **Lucerne の支払いシステムのコード マップ**

  Dinner Now と Lucerne は協力して、2 つのシステムを統合するのに必要な変更を特定しました。 その結果、一部のコードを更新しやすくするためにリファクタリングすることになりました。 まず、PaymentApprover クラスを DinnerNow.Business 名前空間に移動します。新しいメソッドをいくつか追加する必要もあります。 また、トランザクションを処理する Dinner Now のクラスに固有の名前空間を割り当てます。 さらに、作業の計画、整理、および追跡のための作業項目を作成し、 それらの作業項目を必要に応じてモデル要素にリンクします。

  コードの再構成が完了したら、2 つのチームは新しいコード マップを生成して、更新された構造とリレーションシップを確認します.

  ![再構成されるコードを含む依存関係グラフ](../modeling/media/depgraph-integrated.png "DepGraph_Integrated")

  **再構成されたコードを含むコード マップ**

  このマップから、PaymentApprover クラスが DinnerNow.Business 名前空間に移動され、新しいメソッドがいくつか追加されたことがわかります。 また、Dinner Now のトランザクション関連のクラスに、PaymentSystem という固有の名前空間が新たに割り当てられています。これにより、これらのコードが扱いやすくなります。

#### <a name="creating-a-code-map"></a>コード マップの作成

- ソース コードの概要をすばやく確認するには、次の手順に従ってコード マップを生成します。

     **[アーキテクチャ]** メニューで、 **[ソリューションのコード マップを生成]** をクリックします。

     コンパイル済みコードの概要をすばやく確認するには、空のコード マップを生成し、アセンブリ ファイルまたはバイナリ ファイルをそのマップにドラッグします。

- 特定のコードまたはソリューション項目について調べるには、ソリューション エクスプローラーを使用して、視覚化する項目およびリレーションシップを選択し、 新しいマップを生成するか、選択した項目を既存のマップに追加します。 「 [Map dependencies across your solutions](../modeling/map-dependencies-across-your-solutions.md)」を参照してください。

- マップを調べる際には、実行する作業に合わせてレイアウトを再配置することができます。

     たとえば、コードのレイヤーを視覚化するにはツリー レイアウトを選択します。 「[コードマップの参照および再配置」を](../modeling/browse-and-rearrange-code-maps.md)参照してください。

#### <a name="summary-strengths-of-code-maps"></a>まとめ: コード マップの長所
 コード マップは次のような作業に役立ちます。

- 既存のコード内の編成や関係を把握する。

- 提案された変更によって影響を受ける可能性がある領域を特定する。

- 複雑な領域、パターン、レイヤーなど、コードの保守、変更、および再利用を容易にするために改良できる領域を見つける。

#### <a name="relationship-to-other-diagrams"></a>他の図との関係

|**図**|**記述する内容**|
|-----------------|-------------------|
|レイヤー図|システムの論理アーキテクチャ。 レイヤー検証を使用して、コードが設計と常に一致することを確認します。<br /><br /> 既存のレイヤーまたは必要なレイヤーを特定するには、コード マップを生成し、関連する項目をグループ化します。 レイヤー図を作成する場合は、次のトピックを参照してください。<br /><br /> [コードからレイヤー図を作成 -   に](../modeling/create-layer-diagrams-from-your-code.md)は<br />-   [レイヤー図: ガイドライン](../modeling/layer-diagrams-guidelines.md)|
|コンポーネント図|コンポーネントとそのインターフェイスおよび関係。<br /><br /> コンポーネントを特定するには、コード マップを生成し、項目をシステム内の機能別にグループ化します。<br /><br /> 参照トピック<br /><br /> -   [UML コンポーネント図: リファレンス](../modeling/uml-component-diagrams-reference.md)<br />-   [UML コンポーネント図: ガイドライン](../modeling/uml-component-diagrams-guidelines.md)|
|クラス図 (UML)|クラスとその属性、操作、および関係。<br /><br /> これらの要素を特定するには、それらの要素を示す UML クラス図を作成します。<br /><br /> 参照トピック<br /><br /> -   [UML クラス図: リファレンス](../modeling/uml-class-diagrams-reference.md)<br />-   [UML クラス図: ガイドライン](../modeling/uml-class-diagrams-guidelines.md)|
|クラス図 (コード ベース)|特定のプロジェクトに対するコード内の既存のクラス。<br /><br /> コード内の既存のクラスを視覚化して変更するには、クラス デザイナーを使用します。<br /><br /> 「 [How to: Add Class Diagrams to Projects (Class Designer)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md)」を参照してください。|

### <a name="DescribeSequence"></a>相互作用の説明: シーケンス図
 シーケンス図は、システムのパート間の一連の相互作用を記述します。 パートの規模に制限はなく、 たとえば、プログラムの個々のオブジェクトから大規模なサブシステムや外部アクターまでが対象に含まれます。 相互作用の規模と種類にも制限はなく、 たとえば、個々のメッセージから長時間にわたるトランザクションまでが対象に含まれます。関数呼び出しや Web サービス メッセージも相互作用として記述できます。

 Lucerne と Dinner Now は、Process Payment ユース ケースのステップを記述し、それについて議論するために、コンポーネント図から次のようなシーケンス図を生成しました。 図の生存線には、Dinner Now Web Site コンポーネントとそのパートが反映されています。 生存線の間のメッセージは、コンポーネント図の接続に従っています。

 ![プロセス支払いユースケースのシーケンス図](../modeling/media/umlsequence-processpayment.png "UMLSequence_ProcessPayment")

 **プロセス支払いユースケースのシーケンス図**

 このシーケンス図から、顧客が注文を作成すると Dinner Now Web Site が OrderProcessing インスタンスの ProcessOrder を呼び出すことがわかります。 その後、OrderProcessing が PaymentProcessing の ProcessPayment を呼び出し、 同じように呼び出しが続けられた後、最終的に External Payment Processor Gateway によって支払いが検証されます。 Dinner Now Web Site に制御が戻るのはそれからです。

 Lucerne では、Dinner Now システムとの統合のために自社の支払いシステムを更新するのにかかるコストを見積もる必要があります。 これを調べるため、このチームはコード マップを作成して影響を受けるコードを視覚化することができます。

 参照トピック

- [UML シーケンス図: リファレンス](../modeling/uml-sequence-diagrams-reference.md)

- [UML シーケンス図: ガイドライン](../modeling/uml-sequence-diagrams-guidelines.md)

- [ソリューション間の依存関係をマップする](../modeling/map-dependencies-across-your-solutions.md)

#### <a name="drawing-a-sequence-diagram"></a>シーケンス図の描画
 シーケンス図の主な機能を以下に示します。

- 縦方向の *生存線* は、アクターまたはソフトウェア オブジェクトのインスタンスを表します。

   参加要素が開発中のシステムの外部にあることを示すアクター シンボルを追加するには、生存線をクリックし、 **[プロパティ]** ウィンドウで **Actor** を **True**に設定します。 **[プロパティ]** ウィンドウが表示されていない場合は **F4**キーを押します。

- 横方向の *メッセージ* は、メソッド呼び出しや Web サービス メッセージなどの通信を表します。 生存線上の網掛けされた縦長の四角形として示される*実行発生* は、受信側のオブジェクトが呼び出しを処理する期間を表します。

- *同期*メッセージの実行中、sender オブジェクトは、コントロールが < になるまで待機し\<通常の関数呼び出しと同様に > > を返します。 *非同期* メッセージでは、送信側がすぐに続行できます。

- <\<使用して > > メッセージを作成し、他のオブジェクトによるオブジェクトの構築を示すことができます。 このメッセージは、そのオブジェクトに送信される最初のメッセージである必要があります。

  参照トピック

- [UML シーケンス図: リファレンス](../modeling/uml-sequence-diagrams-reference.md)

- [UML シーケンス図: ガイドライン](../modeling/uml-sequence-diagrams-guidelines.md)

#### <a name="summary-strengths-of-sequence-diagrams"></a>まとめ: シーケンス図の長所
 シーケンス図を使用すると、以下の内容を視覚化できます。

- ユース ケースの実行中にアクターまたはオブジェクトの間を移動する制御のフロー。

- メソッド呼び出しやメッセージの実装。

#### <a name="relationship-to-other-diagrams"></a>他の図との関係

|**図**|**説明**|
|-----------------|---------------------|
|クラス図 (UML)|生存線によって表されるクラスと、生存線間で送信されるメッセージで使用されるパラメーターと戻り値を定義します。<br /><br /> 生存線からクラスを生成するには、生存線を右クリックし、 **[クラスの生成]** または **[インターフェイスの生成]** をクリックします。 クラス図の型から生存線を生成するには、型を右クリックし、 **[生存線の生成]** をクリックします。<br /><br /> 参照トピック<br /><br /> -   [UML クラス図: リファレンス](../modeling/uml-class-diagrams-reference.md)<br />-   [UML クラス図: ガイドライン](../modeling/uml-class-diagrams-guidelines.md)|
|コンポーネント図|生存線によって表されるコンポーネントと、メッセージによって表される振る舞いを提供および使用するインターフェイスを記述します。<br /><br /> コンポーネント図から生存線を生成するには、コンポーネントを右クリックし、 **[生存線の生成]** をクリックします。<br /><br /> 参照トピック<br /><br /> -   [UML コンポーネント図: リファレンス](../modeling/uml-component-diagrams-reference.md)<br />-   [UML コンポーネント図: ガイドライン](../modeling/uml-component-diagrams-guidelines.md)|
|ユース ケース図|シーケンス図に示されるユーザーとコンポーネントの間の相互作用を、ユーザーのゴールを表すユース ケースとしてまとめます。<br /><br /> 参照トピック<br /><br /> -   [UML ユースケース図: リファレンス](../modeling/uml-use-case-diagrams-reference.md)<br />[UML ユースケース図の -   : ガイドライン](../modeling/uml-use-case-diagrams-guidelines.md)|

### <a name="DefineClasses"></a> 型の用語集の定義: クラス図
 クラス図は、システムに参加するエンティティ、用語、または概念と、それらの関係を定義します。 たとえば、開発中にこれらの図を使用すると、各クラスの属性と操作を、実装の言語やスタイルに関係なく記述できます。

 Lucerne は、Process Payment ユース ケースに参加するエンティティを記述し、それについて議論するために、次のようなクラス図を描画しました。

 ![クラスダイアグラムでの支払いエンティティの処理](../modeling/media/uml-payentities.png "UML_PayEntities")

 **クラス図の Process Payment のエンティティ**

 この図から、Customer が複数の注文と支払い方法を持てること、 BankAccount と CreditCard が Payment を継承していることがわかります。

 開発中に次のようなクラス図を使用することにより、各クラスの詳細を記述し、それについて議論することができます。

 ![クラスダイアグラムでの支払いエンティティの詳細の処理](../modeling/media/uml-payment.png "UML_Payment")

 **クラス図の Process Payment の詳細**

 参照トピック

- [UML クラス図: リファレンス](../modeling/uml-class-diagrams-reference.md)

- [UML クラス図: ガイドライン](../modeling/uml-class-diagrams-guidelines.md)

#### <a name="drawing-a-class-diagram"></a>クラス図の描画
 クラス図の主な機能を以下に示します。

- クラス、インターフェイス、列挙などの型:

  - *クラス* とは、特定の構造上または振る舞い上の特性を共有するオブジェクトの定義です。

  - *インターフェイス* は、外部から見えるオブジェクトの振る舞いの一部を定義します。

  - *列挙* とは、リテラル値のリストを含む分類子です。

- *属性* とは、 *分類子*の各インスタンスを記述する特定の型の値です。 分類子とは、型、コンポーネント、ユース ケース、およびアクターの総称です。

- *操作* とは、分類子のインスタンスが実行できるメソッドまたは関数です。

- *関連* は、2 つの分類子の間の何らかの関係を表します。

  - *集約* とは、分類子間の共有所有権を表す関連です。

  - *コンポジション* とは、分類子間の全体 - 部分の関係を表す関連です。

    集約やコンポジションを示すには、関連の **Aggregation** プロパティを設定します。 **Shared** は集約を示し、 **Composite** はコンポジションを示します。

- *依存関係* は、ある分類子の定義を変更すると別の分類子の定義が変更される可能性があることを表します。

- *汎化* は、特定の分類子の定義の一部が一般的な分類子から継承されていることを表します。 *実現* は、インターフェイスによって提供された操作および属性をクラスで実装することを表します。

   これらの関係を生成するには、継承 ツールを使用します。 実現は、 *ロリポップ*として表すこともできます。

- *パッケージ* とは、分類子、関連、生存線、コンポーネント、および他のパッケージのグループです。 *インポート* の関係は、あるパッケージが別のパッケージのすべての定義を含むことを表します。

  クラス デザイナーを使用すると、既存のクラスについての調査や議論の開始点としてコードからクラス図を生成できます。

  参照トピック

- [UML クラス図: リファレンス](../modeling/uml-class-diagrams-reference.md)

- [UML クラス図: ガイドライン](../modeling/uml-class-diagrams-guidelines.md)

- [方法: プロジェクトにクラス ダイアグラムを追加する (クラス デザイナー)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md)

#### <a name="summary-strengths-of-class-diagrams"></a>まとめ: クラス図の長所
 クラス図を使用すると、以下の要素を定義できます。

- ユーザーのニーズやシステムに参加するエンティティについて議論する際に使用する用語の共通用語集。 「[モデルユーザーの要件](../modeling/model-user-requirements.md)」を参照してください。

- システムのパート (コンポーネントなど) によって使用される型。実装に関係なく定義できます。 「[アプリのアーキテクチャのモデル](../modeling/model-your-app-s-architecture.md)化」を参照してください。

- 型の間の関係 (依存関係など)。 たとえば、ある型を別の型の複数のインスタンスに関連付けられることを示すことができます。

#### <a name="relationship-to-other-diagrams"></a>他の図との関係

|**図**|**説明**|
|-----------------|---------------------|
|ユース ケース図|ユース ケースのゴールとステップを記述するために使用される型を定義します。<br /><br /> 参照トピック<br /><br /> -   [UML ユースケース図: リファレンス](../modeling/uml-use-case-diagrams-reference.md)<br />[UML ユースケース図の -   : ガイドライン](../modeling/uml-use-case-diagrams-guidelines.md)|
|アクティビティ図|オブジェクト ノード、入力ピン、出力ピン、およびアクティビティ パラメーター ノードによって受け渡されるデータの型を定義します。<br /><br /> 参照トピック<br /><br /> -   [UML アクティビティ図: リファレンス](../modeling/uml-activity-diagrams-reference.md)<br />[UML アクティビティ図の -   : ガイドライン](../modeling/uml-activity-diagrams-guidelines.md)|
|コンポーネント図|コンポーネントとそのインターフェイスおよび関係を記述します。 クラスが完全なコンポーネントを記述する場合もあります。<br /><br /> 参照トピック<br /><br /> -   [UML コンポーネント図: リファレンス](../modeling/uml-component-diagrams-reference.md)<br />-   [UML コンポーネント図: ガイドライン](../modeling/uml-component-diagrams-guidelines.md)|
|レイヤー図|クラスに関連するシステムの論理アーキテクチャを定義します。<br /><br /> レイヤー検証を使用して、コードが設計と常に一致することを確認します。<br /><br /> 参照トピック<br /><br /> [コードからレイヤー図を作成 -   に](../modeling/create-layer-diagrams-from-your-code.md)は<br />-   [レイヤー図: リファレンス](../modeling/layer-diagrams-reference.md)<br />-   [レイヤー図: ガイドライン](../modeling/layer-diagrams-guidelines.md)<br />[レイヤー図を使用してコードを検証 -   に](../modeling/validate-code-with-layer-diagrams.md)は|
|シーケンス図|生存線の型と、生存線が受信するすべてのメッセージの操作、パラメーター、および戻り値を定義します。<br /><br /> クラス図の型から生存線を生成するには、型を右クリックし、 **[生存線の生成]** をクリックします。<br /><br /> 参照トピック<br /><br /> -   [UML シーケンス図: リファレンス](../modeling/uml-sequence-diagrams-reference.md)<br />[UML シーケンス図の -   : ガイドライン](../modeling/uml-sequence-diagrams-guidelines.md)|
|コード マップ|既存のコード内の編成や関係を視覚化します。<br /><br /> クラスとその関係およびメソッドを特定するには、それらの要素を示すコード マップを生成します。<br /><br /> 参照トピック<br /><br /> [ソリューション間の依存関係をマップ -   に](../modeling/map-dependencies-across-your-solutions.md)は|

### <a name="DescribeLayers"></a>論理アーキテクチャの記述: レイヤー図
 レイヤー図は、ソリューションの成果物を抽象的なグループ ( *レイヤー*) に整理することによってシステムの論理アーキテクチャを記述します。 成果物には、名前空間、プロジェクト、クラス、メソッドなど、さまざまなものがあります。 レイヤーは、それらの成果物がシステムで実行するロールやタスクを表します。 コードが設計と一致していることを確認するために、ビルドやチェックイン操作にレイヤー検証を組み込むこともできます。

 Dinner Now と Lucerne は、コードと設計の一致を維持するために、次のようなレイヤー図を使用してコードの変更を検証します。

 ![統合支払いシステムのレイヤー図](../modeling/media/layer-integrated-dnlucerne.png "Layer_Integrated_DNLucerne")

 **Lucerne と統合されたディナーのレイヤー図**

 この図のレイヤーは、Dinner Now と Lucerne の対応するソリューション成果物にリンクされています。 たとえば、Business レイヤーは DinnerNow.Business 名前空間とそのメンバー (新しい PaymentApprover クラスも含まれています) にリンクされており、 Resource Access レイヤーは DinnerNow.Data 名前空間にリンクされています。 図の矢印 ( *依存関係*) は、Resource Access レイヤーの機能を使用できるのは Business レイヤーだけであることを示しています。 コードを更新する過程で定期的にレイヤー検証を実行することにより、発生した競合をその場で検出して速やかに解決できます。

 互いに協力して 2 つのシステムの統合とテストを徐々に進めることにした Lucerne と Dinner Now は、 PaymentProcessing の作業に入る前に、PaymentApprover と Dinner Now のその他の部分とのやり取りが正常に動作するかどうかを確認しました。

 次のコード マップは、Dinner Now と PaymentApprover の間の新しい呼び出しを示しています。

 ![統合システムを使用した依存関係グラフの更新](../modeling/media/depgraph-intsystem.png "DepGraph_IntSystem")

 **更新されたメソッド呼び出しを含んだコード マップ**

 システムが正常に動作することを確認した後、Dinner Now の PaymentProcessing のコードをコメント アウトしました。 その結果、レイヤー検証でエラーは報告されず、コード マップに PaymentProcessing の依存関係が存在しなくなりました。

 ![PaymentProcessing のない依存関係グラフ](../modeling/media/depgraph-nomore.png "DepGraph_NoMore")

 **PyamentProcessing を含まないコード マップ**

#### <a name="drawing-a-layer-diagram"></a>レイヤー図の描画
 レイヤー図の主な機能を以下に示します。

- *レイヤー* は、成果物の論理グループを記述します。

- *リンク* とは、レイヤーと成果物の間の関連です。

   成果物からレイヤーを作成するには、ソリューション エクスプローラー、コード マップ、クラス ビュー、またはオブジェクト ブラウザーから項目をドラッグします。 新しいレイヤーを描画して成果物にリンクするには、ツールボックスを使用するか図の画面を右クリックしてレイヤーを生成し、そこに項目をドラッグします。

   レイヤーの数字は、レイヤーにリンクされている成果物の数を示します。 このような成果物には、名前空間、プロジェクト、クラス、メソッドなどがあります。 レイヤーの成果物の数を解釈するときには、次の点に注意してください。

  - 1 つのレイヤーが他の成果物を含む 1 つの成果物にリンクされているが、他の成果物に直接リンクされていない場合、その数字にはリンクされた成果物のみが含まれます。 ただし、レイヤー検証時の分析にはそれらの他の成果物も含まれます。

     たとえば、1 つのレイヤーが 1 つの名前空間にリンクされている場合、その名前空間に複数のクラスが含まれていても、リンクされた成果物の数は 1 です。 レイヤーに名前空間の各クラスへのリンクもある場合、その数字にはリンクされたクラスが含まれます。

  - 1 つのレイヤーに成果物にリンクされた他のレイヤーが含まれている場合は、そのコンテナー レイヤーの数字にそれらの成果物が含まれていなくても、コンテナー レイヤーはそれらの成果物にリンクされます。

    レイヤーにリンクされた成果物を表示するには、レイヤーを右クリックし、 **[リンクの表示]** をクリックして **レイヤー エクスプローラー**を開きます。

- *依存関係* は、あるレイヤーが別のレイヤーの機能を使用することはできても、その逆はできないことを示します。 *双方向の依存関係* は、あるレイヤーが別のレイヤーの機能を使用でき、その逆もできることを示します。

   レイヤー図に既存の依存関係を表示するには、図の画面を右クリックし、 **[依存関係の生成]** をクリックします。 必要とされる依存関係を記述するには、新しい依存関係を描画します。

  参照トピック

- [コードからのレイヤー図の作成](../modeling/create-layer-diagrams-from-your-code.md)

- [レイヤー図: リファレンス](../modeling/layer-diagrams-reference.md)

- [レイヤー図: ガイドライン](../modeling/layer-diagrams-guidelines.md)

- [レイヤー図を使用したコードの検証](../modeling/validate-code-with-layer-diagrams.md)

#### <a name="summary-strengths-of-layer-diagrams"></a>まとめ: レイヤー図の長所
 レイヤー図は次のような作業に役立ちます。

- 成果物の機能に従ってシステムの論理アーキテクチャを記述する。

- 開発中のコードが指定された設計に準拠していることを確認する。

#### <a name="relationship-to-other-diagrams"></a>他の図との関係

|**図**|**説明**|
|-----------------|---------------------|
|コード マップ|既存のコード内の編成や関係を視覚化します。<br /><br /> レイヤーを作成するには、コード マップを生成し、レイヤーにするマップ項目をグループ化して、 そのグループをマップからレイヤー図にドラッグします。<br /><br /> 参照トピック<br /><br /> [ソリューション間の依存関係をマップ -   に](../modeling/map-dependencies-across-your-solutions.md)は<br />[コードマップを参照および再配置](../modeling/browse-and-rearrange-code-maps.md)-   には|
|コンポーネント図|コンポーネントとそのインターフェイスおよび関係を記述します。<br /><br /> レイヤーを視覚化するには、システムのさまざまなコンポーネントの機能を記述するコンポーネント図を生成します。<br /><br /> 参照トピック<br /><br /> -   [UML コンポーネント図: リファレンス](../modeling/uml-component-diagrams-reference.md)<br />-   [UML コンポーネント図: ガイドライン](../modeling/uml-component-diagrams-guidelines.md)|

## <a name="external-resources"></a>外部資料

|**カテゴリ**|**Links**|
|------------------|---------------|
|**フォーラム**|-   [Visual Studio の視覚化ツールとモデリング ツール](https://social.msdn.microsoft.com/Forums/en-US/home?forum=vsarch)<br />-   [Visual Studio の視覚化およびモデリング SDK (DSL ツール)](https://social.msdn.microsoft.com/Forums/home?forum=dslvsarchx)|

## <a name="see-also"></a>参照
 [コードを視覚化](../modeling/visualize-code.md)する[アプリの](../modeling/create-models-for-your-app.md)モデルを作成[する開発プロセスで](../modeling/use-models-in-your-development-process.md)のモデルの使用[アジャイル開発でのモデルの使用](https://msdn.microsoft.com/592ac27c-3d3e-454a-9c38-b76658ed137f)[開発時のシステムの検証](../modeling/validate-your-system-during-development.md) [UML モデルと図の拡張](../modeling/extend-uml-models-and-diagrams.md)
