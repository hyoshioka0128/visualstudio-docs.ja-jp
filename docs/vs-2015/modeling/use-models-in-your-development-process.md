---
title: Use models in your development process | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML, using models
ms.assetid: a33ac8fc-4ba0-4850-b71b-014dc8674e54
caps.latest.revision: 31
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5d5284bb163f474d67324c395a4342ccef6f8561
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298264"
---
# <a name="use-models-in-your-development-process"></a>開発プロセス内でのモデルの使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio では、システム、アプリケーション、またはコンポーネントについて理解し、変更するためのモデルを使用することができます。 モデルは、システムが動作する世界を視覚化できるようにして、ユーザーのニーズを明確化し、システムのアーキテクチャを定義し、コードを分析し、コードが要件を満たしていることを確認できるようにします。 See [Channel 9 Video: Improve architecture through modeling](https://go.microsoft.com/fwlink/?LinkID=252078).

 どのバージョンの Visual Studio が各モデルの種類をサポートしているかについては、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

## <a name="how-to-use-models"></a>モデルの使用方法
 モデルは、いくつかの方法で役立ちます。

- モデリング図を描画すると、要件、アーキテクチャ、および概要設計に関連する概念を明確にすることができます。 For more information, see [Model user requirements](../modeling/model-user-requirements.md).

- モデルの操作は、要件の不整合を明らかにするのに役立ちます。

- モデルとの通信では、自然言語でのやり取りよりも曖昧さを残さずに、重要な概念をやり取りできます。 For more information, see [Model your app's architecture](../modeling/model-your-app-s-architecture.md).

- 場合によっては、モデルを使用して、コードまたはデータベース スキーマやドキュメントなどのその他の成果物を生成できます。 たとえば、[!INCLUDE[vsUltShort](../includes/vsultshort-md.md)] のモデリング コンポーネントはモデルから生成されます。  For more information, see [Generate and configure your app from models](../modeling/generate-and-configure-your-app-from-models.md).

  モデルは、手軽なアジャイルから高度なセレモニーまで、広範囲のプロセスで使用することができます。

### <a name="use-models-to-reduce-ambiguity"></a>モデルを使用したあいまいさの低減
 モデリング言語は、自然言語よりもあいまいさが少なく、一般的にソフトウェアの開発時に必要なアイデアを表すように設計されています。

 プロジェクトにアジャイル手法を適用する小規模なチームがある場合は、ユーザー ストーリーを明確にするためにモデルを使用できます。 顧客とのニーズについての話し合いにおいて、モデルを作成すると、スパイクやプロトタイプ コードを記述するよりもはるかに短時間かつ広い製品領域間で有益な質問を生み出すことができます。

 プロジェクトが大規模で、世界中の各地にチームがある場合は、モデルを使用すると、テキスト形式で行うよりはるかに効果的に要件およびアーキテクチャをやり取りできます。

 いずれのケースでも、モデルを作成すると、ほとんどすべての場合、不整合性やあいまいさが大幅に減少します。 さまざまな利害関係者が、システムが動作するビジネスの世界について異なる理解をすることはよくあります。また、さまざまな開発者が、システムの動作の仕方について異なる理解をすることもよくあります。 通常、ディスカッションを中心としたモデルを使用すると、これらの相違点が明らかになります。 For more information about how to use a model to reduce inconsistencies, see [Model user requirements](../modeling/model-user-requirements.md).

### <a name="use-models-with-other-artifacts"></a>その他の成果物によるモデルの使用
 モデルは、それ自体は要件仕様やアーキテクチャではありません。 モデルは、これらの一部の側面をより明確に表すツールですが、ソフトウェア設計時に必要な概念のすべてを表すことはできません。 そのため、モデルは、OneNote のページや段落、Microsoft Office ドキュメント、[!INCLUDE[esprfound](../includes/esprfound-md.md)] の作業項目、またはプロジェクト ルームの壁に貼られた付箋など、他のコミュニケーション手段とともに使用する必要があります。 最後の項目以外、すべてのオブジェクトの種類は、モデルの要素のパーツにリンクすることができます。

 通常、モデルと共に使用されるその他の仕様の側面は次のとおりです。 プロジェクトの規模とスタイルによって、これらの側面のいくつかを使用するか、まったく使用しない場合があります。

- ユーザー ストーリー。 ユーザー ストーリーは、いずれかのプロジェクトのイテレーションで提供される、システムの動作の側面についてユーザーと他の利害関係者が話し合う短い説明です。 一般的なユーザー ストーリーは、「顧客は･･･ができるようになります」で始まります。 ユーザー ストーリーでは、ユース ケースのグループが導入されることがあります。または、以前に開発されたユース ケースの拡張を定義することができます。 ユース ケースを定義または拡張すると、ユーザー ストーリーがより明確になります。

- 変更要求。 より正式なプロジェクトでは、変更要求は、アジャイル プロジェクトでのユーザー ストーリーによく似ています。 アジャイル手法では、すべての要件を、前のイテレーションで開発されたものの変更として取り扱います。

- ユース ケースの説明。 ユース ケースは、特定の目標を達成するために、ユーザーがシステムと対話する 1 つの方法を表します。 完全な説明には、目標、主要イベントと代替のイベントの順序、および例外的な結果などがあります。 ユース ケース図は、ユース ケースを要約し、ユース ケースの概要を説明するのに役立ちます。

- シナリオ。 シナリオとは、システム、ユーザー、およびその他のシステムが連携して利害関係者に価値を提供する方法を示す、イベントの順序に関する非常に詳しい説明です。 ユーザー インターフェイスのスライド ショーや、ユーザー インターフェイスのプロトタイプの形を取ることがあります。 1 つのユース ケースまたは一連のユース ケースとして説明できます。

- 用語集 プロジェクト要件の用語集は、顧客が自分の世界について説明する言葉について記載しています。 ユーザー インターフェイスおよび要件モデルも、これらの用語を使用する必要があります。 クラス ダイアグラムは、これらの用語のほとんどで、その関係を明確にするのに役立ちます。 ダイアグラムと用語集を作成すると、ユーザーと開発者の間の誤解が減るだけでなく、ほとんどすべての場合、異なるビジネスの利害関係者間の誤解が明らかになります。

- ビジネス ルール。 多くのビジネス ルールは、要件のクラス モデルにおける関連付けと属性の不変の制約、およびシーケンス図の制約として表すことができます。

- 概要設計。 主要なパーツと、それらを組み合わせる方法について説明します。 コンポーネント図、シーケンス図、およびインターフェイス図は、概要設計の主要なパーツです。

- デザイン パターン。 システムのさまざまな部分の間で共有されるデザインの規則について説明します。

- テスト仕様。 テスト スクリプトとテスト コードの設計では、アクティビティとシーケンス図を活用して、テスト手順の順序を記述できます。 システム テストは、要件が変更されたときに変更しやすいように、要件モデルの観点から表す必要があります。

- プロジェクト計画。 プロジェクト計画またはバックログでは、各機能がいつ提供されるかを定義します。 実装または拡張するユース ケースとビジネス ルールを記述することで、各機能を定義できます。 計画でユース ケースとビジネス ルールを直接参照するか、別のドキュメントで一連の機能を定義してから、計画内で機能のタイトルを使用することができます。

### <a name="use-models-in-iteration-planning"></a>イテレーション計画でのモデルの使用
 すべてのプロジェクトは規模と組織が異なりますが、一般的なプロジェクトは、2 ～ 6 週間の一連のイテレーションとして計画されます。 初期のイテレーションからのフィードバックを、後のイテレーションのスコープと計画の調整に使用できるように、十分なイテレーションを計画することが重要です。

 次の推奨事項は、反復的なプロジェクトでモデリングのメリットを実現するときに役立つ可能性があります。

#### <a name="sharpen-focus-as-each-iteration-approaches"></a>各イテレーションが近づくときに焦点をはっきりさせる
 各イテレーションが近づくときに、モデルを使用して、イテレーションの最後に提供される内容を定義します。

- 初期のイテレーションですべてを詳細にモデリングしないでください。 最初のイテレーションで、ユーザーの用語集で主なアイテムのクラス ダイアグラムを作成して、主要なユース ケースの図の描画と主要なコンポーネント図の描画を行います。 これらのいずれも細部まで記述しないでください。詳細はプロジェクトの後半で変化するからです。 機能の一覧または主要なユーザー ストーリーを作成するには、このモデルで定義されている用語を使用します。 プロジェクト全体で推定ワークロードの大まかなバランスをとるために、イテレーションに機能を割り当てます。 これらの割り当ては、プロジェクトの後半で変更されます。

- 初期のイテレーションで最も重要なすべてのユース ケースの簡略化バージョンを実装してみます。 これらのユース ケースは、後のイテレーションで拡張します。 この手法により、プロジェクトで要件やアーキテクチャの不具合の発見が遅すぎて手遅れになるリスクを低減できます。

- 各イテレーションの終盤で、要件ワーク ショップを開催して、要件や次のイテレーションで開発されるユーザー ストーリーを詳細に定義します。 優先度を決定できるユーザーとビジネスの利害関係者、および開発者とシステムのテスト担当者を招待します。 2 週間分のイテレーションの要件を定義するには 3 時間かかります。

- すべてのユーザーにとって、ワークショップの目的は、次のイテレーションが終了するまでに達成する事柄について同意することです。 要件を明確化するには、ツールの 1 つとしてモデルを使用します。 ワーク ショップのアウトプットは、イテレーションのバックログ、つまり、[!INCLUDE[esprfound](../includes/esprfound-md.md)] の開発タスクの一覧と [!INCLUDE[TCMext](../includes/tcmext-md.md)] のテスト スイートです。

- 要件のワーク ショップでは、開発タスクの見積もりを決定する必要がある限りは、設計のみについて話し合います。 それ以外の場合は、ユーザーが直接体験するシステムの動作について話し合いを続けます。 要件モデルとアーキテクチャのモデルは別にしておいてください。

- 通常、技術者以外の利害関係者は、いくらかのガイダンスがあれば、UML 図を理解するのに問題はありません。

#### <a name="link-model-to-work-items"></a>モデルから作業項目へのリンク
 要件のワーク ショップ後、要件モデルの詳細を推敲し、モデルを開発タスクとリンクさせます。 これを行うには、[!INCLUDE[esprfound](../includes/esprfound-md.md)] の作業項目をモデルの要素にリンクさせます。 To learn how to do this, see [Link model elements and work items](../modeling/link-model-elements-and-work-items.md).

 作業項目に任意の要素をリンクできますが、最も役立つ要素は次のとおりです。

- ユース ケース。 ユース ケースは、それを実装する開発タスクにリンクできます。

- ユース ケースの拡張。 ユース ケースの 1 つの側面のみをイテレーションに実装する場合は、基本のユース ケースと 1 つ以上の拡張に分割することができます。 拡張とは、«extend» リレーションシップによって基本ケースとリンクされたユース ケースです。 For more information about use case extension, see [UML Use Case Diagrams: Reference](../modeling/uml-use-case-diagrams-reference.md).

- ビジネス ルールやサービスの要件の品質について記載したコメントです。 For more information, see [Model user requirements](../modeling/model-user-requirements.md).

#### <a name="link-model-to-tests"></a>モデルとテストのリンク
 要件モデルを使用して、受け入れテストの設計をガイドします。 これらのテストは、開発作業と同時に作成します。

 To learn more about this technique, see [Develop tests from a model](../modeling/develop-tests-from-a-model.md).

#### <a name="estimate-remaining-work"></a>残存作業の見積もり
 要件モデルは、各イテレーションのサイズとの関係で、プロジェクトの合計サイズを見積もることができます。 ユース ケースとクラスの数と複雑さを評価することは、必要となる開発作業の見積もりに役立ちます。 最初のいくつかのイテレーションが完了したら、対象となる要件とまだ対象になっていない要件とを比較することで、プロジェクトの残りの費用とスコープの概算の測定値を得ることができます。

 各イテレーションの終盤で、今後のイテレーションに対する要件の割り当てを確認します。 これは、ユース ケース図中のサブシステムとして、各イテレーションの最後にソフトウェアの状態を表す際に役立ちます。 ディスカッションにおいて、ユース ケースとユース ケースの拡張を、これらのサブシステムから別のサブシステムに移動することができます。

## <a name="levels-of-abstraction"></a>抽象化レベル
 モデルには、ソフトウェアに関する抽象化の範囲があります。 ほとんどの具体的なモデルは直接プログラム コードを表し、ほとんどの抽象モデルはコードでは表現できない可能性があるビジネスの概念を表します。

 モデルは、数種類の図で表示できます。 For information about models and diagrams, see [Create models for your app](../modeling/create-models-for-your-app.md).

 さまざまな種類の図は、さまざまな抽象化レベルの設計を記述するのに役立ちます。 図の種類の多くは、複数のレベルで役立ちます。 次の表は、各種の図の使用方法を示しています。

|設計レベル|図の種類|
|------------------|-------------------|
|ビジネス プロセス<br /><br /> システムで使用するコンテキストを理解すると、ユーザーがコンテキストから必要としているものを理解することができます。|-   Activity diagrams describe the flow of work between people and systems to achieve business goals.<br />-   Conceptual class diagrams describe the business concepts used within the business process.|
|ユーザー要件<br /><br /> ユーザーがシステムから必要とするものの定義です。|-   Use case diagrams summarize the interactions that the users and other external systems have with the system that you are developing. 各ユース ケースに他のドキュメントを添付して、詳細に説明することができます。<br />-   UML class diagrams describe the types of information that the users and system communicate about.<br />-   Business rules and quality of service requirements can be described in separate documents.|
|概要設計<br /><br /> システムの全体的な構造、つまり主なコンポーネントとその組み合わせの仕方です。|-   Layer Diagrams describe how the system is structured into interdependent parts. プログラム コードをレイヤー図と照合すると、アーキテクチャを厳守していることを確認することができます。<br />-   Component diagrams show the interfaces of the parts, specifying the messages and services that are provided and required by each component.<br />-   Sequence diagrams show how the components communicate to implement each use case.<br />-   UML class diagrams describe the interfaces of the components and the types of data passed between the components.|
|デザイン パターン<br /><br /> 設計のすべての部分で使用される、設計の問題を解決する規約と方法です。|-   UML class diagrams describe the structures of a pattern<br />-   Sequence or activity diagrams show the interactions and algorithms|
|コード分析<br /><br /> コードから数種類の図を生成できます。|-   Sequence diagrams show the interaction between objects in the code.<br />-   Layer diagrams show the dependencies between classes. 更新されたコードは、レイヤー図と照合することができます。<br />-   Class diagrams show the classes in the code.|

## <a name="external-resources"></a>外部リソース

|**カテゴリ**|**Links**|
|------------------|---------------|
|**ビデオ**|![link to video](../data-tools/media/playvideo.gif "PlayVideo") [MSDN How Do I Videos: How to Create and Use UML Models and Diagrams (Visual Studio 2010 Ultimate)](https://go.microsoft.com/fwlink/?LinkId=214460)<br /><br /> ![link to video](../data-tools/media/playvideo.gif "PlayVideo") [Channel 9: UML with Visual Studio 2010](https://go.microsoft.com/fwlink/?LinkID=201106)<br /><br /> ![link to video](../data-tools/media/playvideo.gif "PlayVideo") [MSDN How Do I Series: UML Tools and Extensibility (Visual Studio 2010 Ultimate)](https://go.microsoft.com/fwlink/?LinkID=214467)|
|**フォーラム**|-   [Visual Studio の視覚化ツールとモデリング ツール](https://go.microsoft.com/fwlink/?LinkId=184720)<br />-   [Visual Studio の視覚化およびモデリング SDK (DSL ツール)](https://go.microsoft.com/fwlink/?LinkId=184721)|
|**ブログ**|[Visual Studio ALM + Team Foundation Server のブログ](https://go.microsoft.com/fwlink/?LinkID=201340)|
|**技術記事とジャーナル**|[MSDN アーキテクチャ センター](https://go.microsoft.com/fwlink/?LinkId=201343)<br /><br /> [Visual Studio アーキテクチャ ツーリング ガイダンス](../modeling/visual-studio-architecture-tooling-guidance.md)|

## <a name="see-also"></a>参照
 [Use models in Agile development](https://msdn.microsoft.com/592ac27c-3d3e-454a-9c38-b76658ed137f) [Create models for your app](../modeling/create-models-for-your-app.md) [Model user requirements](../modeling/model-user-requirements.md) [Model your app's architecture](../modeling/model-your-app-s-architecture.md) [Develop tests from a model](../modeling/develop-tests-from-a-model.md) [Structure your modeling solution](../modeling/structure-your-modeling-solution.md)
