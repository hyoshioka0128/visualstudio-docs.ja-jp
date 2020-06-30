---
title: アーキテクチャの分析とモデル化 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio Ultimate, exploring code
- Visual Studio Ultimate, visualizing code
- diagrams - modeling
- Visual Studio ALM, modeling
- application, design
- architecture
- code visualization
- application design
- applications, architecture
- code exploration
- Visual Studio ALM, exploring code
- modeling
- application architecture
- application, modeling
- applications, modeling
- architecture [Visual Studio ALM], modeling
- application modeling
- Visual Studio Ultimate, modeling
- architecture [Visual Studio Ultimate], modeling
- application, architecture
- Visual Studio ALM, visualizing code
- applications, designing
ms.assetid: c9f04cfa-72bd-419d-a952-616eed01472e
caps.latest.revision: 129
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3e00735a180ec951a8afced0f5c74f7a9466e50b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534096"
---
# <a name="analyze-and-model-your-architecture"></a>アーキテクチャを分析およびモデルする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio アーキテクチャおよびモデリング ツールを使用してアプリを設計およびモデル化することによって、ユーザー要件を満たすアプリを作成できます。 Visual Studio を使用してコードの構造、動作、および関係を視覚化することによって、既存のプログラム コードを容易に理解できるようになります。

 開発プロセスの一部として、アプリケーション ライフサイクル全体においてさまざまな詳細レベルでモデルを作成できます。 Team Foundation Server の作業項目と自分の開発計画にモデル要素をリンクすることによって、モデルに関連付けられた要件、タスク、テスト ケース、バグ、およびその他の作業を追跡できます。 「[シナリオ: 視覚化とモデリングを使用してデザインを変更する](../modeling/scenario-change-your-design-using-visualization-and-modeling.md)」を参照してください。

 各機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

## <a name="to"></a>終了

|シナリオ|記事|
|-|-|
|**コードの視覚化**:<br /><br /> -コードマップを作成して、コードの編成と関係を確認します。 アセンブリ、名前空間、クラス、メソッドなどの間の依存関係を視覚化します。<br />-コードからクラスダイアグラムを作成して、特定のプロジェクトのクラス構造とメンバーを参照してください。<br />-コードを検証するためのレイヤー図を作成することにより、コードとそのデザインとの間の競合を検出します。<br /><br /> **注**: Visual Studio のこのリリースでは、 *依存関係グラフ* の代わりに、 *コード マップ*という用語を使用します。 一般的に、 *グラフ* という用語が単独で使用される場合は、有向グラフまたは DGML 図 (またはドキュメント) を表します。 コード マップは、DGML 図の特化された型です。|-   [コードを視覚化する](../modeling/visualize-code.md)<br />-   [クラスとその他の型の使用 (クラスデザイナー)](../ide/working-with-classes-and-other-types-class-designer.md)<br />-   [ビデオ: 視覚化によるコードの依存関係の理解 (Channel 9)](https://s.ch9.ms/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Understand-your-code-dependencies-through-visualization)<br />-   [ビデオ: 変更の影響の視覚化 (Channel 9)](https://s.ch9.ms/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Visualize-the-impact-of-a-change)|
|**ユーザーの要求を記述して伝達する**:<br /><br /> -ユーザーストーリー、ビジネスルール、およびその他の要件を明確にし、ユースケース図、アクティビティ図、クラス図などの UML 図を描画して一貫性を保つことができます。|-   [アプリのモデルを作成する](../modeling/create-models-for-your-app.md)<br />-   [ユーザー要件のモデル化](../modeling/model-user-requirements.md)<br />-   [ビデオ: モデリングによるアーキテクチャの改善 (Channel 9)](https://s.ch9.ms/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Improving-architecture-through-modeling)|
|**アーキテクチャを定義する**:<br /><br /> -UML コンポーネント、クラス、およびシーケンス図を描画して、ソフトウェアシステムの大規模な構造とデザインパターンをモデル化します。<br />-レイヤー図を作成することによって、コードのコンポーネント間の依存関係に対する制約を定義し、適用します。|-   [アプリのモデルを作成する](../modeling/create-models-for-your-app.md)<br />-   [アプリのアーキテクチャをモデル化する](../modeling/model-your-app-s-architecture.md)<br />-   [ビデオ: モデリングによるアーキテクチャの改善 (Channel 9)](https://s.ch9.ms/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Improving-architecture-through-modeling)<br />-   [ビデオ: レイヤー図を使用したアーキテクチャの設計と検証 (Channel 9)](https://s.ch9.ms/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Using-layer-diagrams-to-design-and-validate-your-architecture)|
|**要求と、必要とされる設計を照らし合わせてシステムを検証する:**<br /><br /> -要求モデルに基づいて、受け入れテストまたはシステムテストを定義します。 これにより、テストとユーザーの要求との間に強固な関係が生成され、要求が変更された場合にシステムをより簡単に更新できます。<br />-目的のアーキテクチャを記述するレイヤー図でコードの依存関係を検証し、設計と競合する可能性のある変更を防止します。|-   [開発時のシステムの検証](../modeling/validate-your-system-during-development.md)<br />-   [ビデオ: レイヤー図を使用したアーキテクチャの設計と検証 (Channel 9)](https://s.ch9.ms/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Using-layer-diagrams-to-design-and-validate-your-architecture)|
|**Team Foundation バージョン コントロールを使用してモデル、図、およびコード マップを共有する**:<br /><br /> -コードマップ、モデリングプロジェクト、UML 図、およびレイヤー図を Team Foundation バージョン管理下に配置して、共有できるようにします。|Team Foundation のバージョン コントロール下でこれらの項目を使用するユーザーが複数いる場合は、バージョン管理の問題を回避するために、次のガイドラインを使用します。<br /><br /> -   [バージョン管理の下でモデルと図を管理する](../modeling/manage-models-and-diagrams-under-version-control.md)|
|**UML 言語やドメイン固有の言語から、アプリケーションの各部分を生成または構成する**:<br /><br /> -要件の変更に対するデザインの応答性を高め、製品ラインを通じて簡単に変化させることができます。|-   [モデルからアプリを生成して構成する](../modeling/generate-and-configure-your-app-from-models.md)|
|**モデルと図をカスタマイズする**:<br /><br /> -UML 要素の追加プロパティを定義することによってモデルを使用する方法、モデルがビジネスルールに準拠していることを確認するための検証制約、および追加のメニューコマンドとツールボックス項目を定義することで、モデルを調整します。<br />-ドメイン固有の言語を独自に作成します。|-   [UML モデルと図の拡張](../modeling/extend-uml-models-and-diagrams.md)<br />-   [モデリング SDK for Visual Studio-ドメイン固有言語](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)|
|**T4 テンプレートを使用してテキストを生成する**:<br /><br /> -テンプレート内のテキストブロックとコントロールロジックを使用して、テキストベースのファイルを生成します。|-   [コード生成と T4 テキストテンプレート](../modeling/code-generation-and-t4-text-templates.md)|

## <a name="types-of-models-and-their-uses"></a>モデルの種類とその用途

|**モデルの種類と一般的な用途**|
|-------------------------------------|
|**コード マップ**<br /><br /> コード マップは、コードの編成や関係を理解するために役立ちます。<br /><br /> 一般的な用途:<br /><br /> -プログラムコードを調べて、その構造と依存関係の理解を深め、更新する方法、提案された変更のコストを見積もることができるようにします。<br /><br /> 参照トピック<br /><br /> -   [ソリューション間の依存関係のマッピング](../modeling/map-dependencies-across-your-solutions.md)<br />-   [コードマップを使用してアプリケーションをデバッグする](../modeling/use-code-maps-to-debug-your-applications.md)<br />-   [コードマップアナライザーを使用して潜在的な問題を検索する](../modeling/find-potential-problems-using-code-map-analyzers.md)|
|**レイヤー図**<br /><br /> レイヤー図を使用すると、アプリケーションの構造を一連のレイヤーまたは明示的な依存関係があるブロックとして定義できます。 検証を実行すると、コード内の依存関係と、レイヤー図で説明された依存関係の競合を検出できます。<br /><br /> 一般的な用途:<br /><br /> -アプリケーションの有効期間にわたるさまざまな変更を通じて、アプリケーションの構造を安定化します。<br />-コードへの変更をチェックインする前に、意図しない依存関係の競合を検出します。<br /><br /> 参照トピック<br /><br /> -   [コードからレイヤー図を作成する](../modeling/create-layer-diagrams-from-your-code.md)<br />-   [レイヤー図: リファレンス](../modeling/layer-diagrams-reference.md)<br />-   [レイヤー図を使用したコードの検証](../modeling/validate-code-with-layer-diagrams.md)|
|**UML モデル**<br /><br /> UML モデルには、クラス図、コンポーネント図、ユース ケース図、アクティビティ図、シーケンス図など、いくつかのビューが含まれます。 UML は、アプリケーション ドメインに合わせてカスタマイズできます。 たとえば、タグ、追加情報、および制約をモデル要素にアタッチできます。 モデルを操作するツールを定義することもできます。 「[アプリのモデルを作成する」を](../modeling/create-models-for-your-app.md)参照してください。<br /><br /> 一般的な用途:<br /><br /> -要件と設計について説明します。 UML は、あらゆるアプリケーションの開発にすばやく適用できます。 「[開発プロセスでのモデルの使用](../modeling/use-models-in-your-development-process.md)」を参照してください。<br />-アプリケーションのテストまたは部分を生成または構成します。 表記法のカスタマイズと生成テンプレートまたは構成可能アプリケーションの開発には、いくらかの作業が必要です。 「[モデルからのアプリの生成と構成](../modeling/generate-and-configure-your-app-from-models.md)」を参照してください。<br />-一般的な説明と、小さいプロジェクトでのコード生成または構成の場合。|
|**ドメイン固有言語 (DSL)**<br /><br /> DSL は、特定の目的のために設計する表記法です。 Visual Studio では、通常、グラフィックです。<br /><br /> 一般的な用途:<br /><br /> -アプリケーションの一部を生成または構成します。 表記法およびツールを開発するには、作業が必要です。 これを行うと、UML のカスタマイズよりもドメインに適合する結果となることがあります。<br />-大規模なプロジェクトまたは製品ラインで、DSL とそのツールの開発における投資が、複数のプロジェクトでの使用によって返されます。<br /><br /> 参照トピック<br /><br /> -   [モデリング SDK for Visual Studio-ドメイン固有言語](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)|

## <a name="where-can-i-get-more-information"></a>情報の入手方法

|リソース|リンク|
|-|-|
|**フォーラム**|-   [Visual Studio の視覚化ツールとモデリング ツール](https://social.msdn.microsoft.com/Forums/en-US/home?forum=vsarch)<br />-   [Visual Studio の視覚化およびモデリング SDK (DSL ツール)](https://social.msdn.microsoft.com/Forums/home?forum=dslvsarchx)|

## <a name="see-also"></a>関連項目

- [Visual Studio 2015 でのモデリングの新機能](../modeling/what-s-new-for-design-in-visual-studio.md)
- [DevOps とアプリケーション ライフサイクル管理](https://msdn.microsoft.com/library/74a1f71d-7f23-4c71-8fd7-89ede614fab6)
